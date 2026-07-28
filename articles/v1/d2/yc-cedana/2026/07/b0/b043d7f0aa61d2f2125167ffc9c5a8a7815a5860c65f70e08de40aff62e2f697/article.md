---
schema_version: "1.0.0"
document_id: "b043d7f0aa61d2f2125167ffc9c5a8a7815a5860c65f70e08de40aff62e2f697"
company_key: "yc-cedana"
company: "Cedana"
source_id: "yc-cedana-news-import-d2b6a3d3a0df"
canonical_url: "https://cedana.com/post/the-era-of-stateful-inference/"
published_at: "2026-07-14T00:00:00+00:00"
first_seen_at: "2026-07-24T23:42:29.819860+00:00"
fetched_at: "2026-07-28T21:22:05.726331+00:00"
content_hash: "sha256:973bc710777d3ddf044db989d870201b21d7bedcaa121758f44c8381eb412e19"
---

# The Era of Stateful Inference: how to improve cost per token.

cedana / blog


# The Era of Stateful Inference: how to improve cost per token.


We are entering the stateful inference era, driven by frontier models with longer context windows, longer in-flight sessions, and single instances spanning 8, 16, or more GPUs.


[All posts](https://cedana.com/blog/)[Schedule a demo](https://cedana.com/connect/)[Read the docs](https://docs.cedana.ai/)


Published 2026-07-14 by Cedana


A coding agent is thirty turns into a session, reasoning across a repository. Every turn has added to the context the model holds in GPU memory: on GLM-5.2 at FP8, a 100K-token context computes to roughly 4.5 GB of KV cache (GLM-5.2 config.json). Then the GPU fails. Everything above the GPU survives: the transcript, the workspace, the sandbox snapshot are all durable. What is lost is the expensive part: the GPU-resident KV cache and the in-flight computation. A KV offload tier, if deployed, can reload the prefixes it already wrote out; the in-flight computation has no copy anywhere. The retry re-runs rather than resumes. It lands on a warm replica, capacity held idle for failover, or it waits for a replacement worker to reload weights. The context is re-prefilled from scratch, or reloaded where an offload tier holds it. The interrupted turn’s reasoning is regenerated, and the regeneration may diverge from the lost computation. On a cache miss, recovery recomputes all thirty turns.


> This is what stateful means at the GPU level. Inference now accumulates session-scoped state that lives only in VRAM, can be reconstructed only by redoing the work, and is destroyed by any interruption. We are entering the stateful inference era, driven by frontier models with longer context windows, longer in-flight sessions, and single instances spanning 8, 16, or more GPUs.


Cost per token and revenue per megawatt are the same equation read from opposite sides: if you run a serving stack, you read it as cost per GPU-hour over delivered tokens per GPU-hour (NVIDIA Rethinking AI TCO 2026); if you run the fleet, you read it as delivered tokens per megawatt. Both move on delivered token output. This article explains why stateful inference changes that arithmetic, and why checkpoint/restore plus migration is becoming a first-class control-plane primitive for raising it.


### 1. Longer horizons.


Agentic workloads hold more state, longer, than any prior inference traffic. Agentic traces run a median of 33 turns per session across 610 Codex/SWE-bench Pro traces (vLLM/Mooncake, May 2026). Across agent benchmarks, 84.6 to 99.5% of input tokens are reused across turns, so the cache is the session’s accumulated work rather than per-request scratch, and its replacement cost grows with every turn (Agentic workload characterization, 2026). Agent trajectories run to dozens or hundreds of steps with a KV footprint that expands monotonically for the session’s lifetime (CONCUR, 2026).


Long horizons compound the exposure: over hours, failure becomes expected, and the state at risk peaks when the session is oldest. And without request boundaries, the fleet never gets a free moment to rebalance or drain.


An entire industry layer has made the record of the session durable, from transcripts and workspace checkpoints to sandbox snapshots of full process memory (Daytona, E2B, Google’s Agent Sandbox). The computation itself remains the one uninsured asset in the stack, destroyed with the silicon and repaid at full price, at a size that grows with every turn. The harness vendors have optimized the cost of paying the tax. Nobody above the GPU can remove it.


### 2. Longer context windows.


Context windows are growing as users want models to reason over entire codebases, massive document sets, and hours of video, and newer attention designs cut the memory cost per token far enough to make serving them feasible. Each running request holds a KV cache that grows with context length, large enough at long context to rival the model’s own weights in VRAM (AnTKV, 2025). The frontier has moved to million-token windows. DeepSeek-V4 ships a 1M-token context, and even with its compressed attention design, Together AI’s early bring-up put a full HGX B200 node’s usable KV capacity at roughly 1.2M to 3.7M tokens depending on cache policy (Together AI DeepSeek-V4 bring-up, May 2026). One long-context request can consume most of an eight-GPU node’s state budget after every compression trick in the modern stack, which is why Together frames million-token context as an inference-systems problem rather than a model problem.


### 3. Larger models.


More parameters mean more VRAM and more GPUs per instance, making workers slower to load and harder to place and pack. The open-weight frontier makes the arithmetic concrete: Kimi K2.6 is a trillion-parameter mixture-of-experts model whose weights run roughly 600 GB even in natively quantized INT4, with 8xH200 as the officially verified serving configuration; at full precision the same weights would run near 2 TB, roughly double that node’s VRAM (Kimi-K2.6 model card and deployment guide, 2026). DeepSeek-V4 Pro runs 1.6 trillion total parameters. A frontier worker is no longer a process on a GPU; it is half a terabyte or more of weights sharded across an entire node before the first byte of session state arrives, and every gigabyte of session state multiplies those costs.


> Compounding inference state makes workers slower to start, costlier to lose, and harder to move: cold starts, failures, and immobility.


Delivered token output leaks three ways. The mechanisms differ; the result is the same: paid-for GPU-hours delivering fewer tokens than the hardware can, and often none.


### 1. Long cold starts.


Cold starts are not just a latency problem for frontier models; they are a fleet-utilization, power-efficiency, and revenue-per-megawatt problem. Loading and initializing a frontier model is not a typical container cold start: it takes 10 minutes and sometimes up to an hour. It is a distributed GPU start-up sequence involving multi-GPU or multi-node placement, runtime startup, weight fetch, HBM materialization, NCCL/distributed initialization, KV cache profiling, CUDA graph capture, and only then prefill.


The denominator impact is severe: because users cannot tolerate minutes of time-to-first-token, operators keep spare replicas and GPU pools warm, converting an elasticity problem into an overprovisioning problem. A single slow shard, network fetch, graph-capture step, or distributed initialization barrier can hold an entire 8-GPU, 16-GPU, 72-GPU, or multi-node placement idle.


This problem is severe enough that even limited mitigations show large economic value: Microsoft’s SageServe (SageServe, SIGMETRICS 2025) uses scheduling techniques such as prediction, pooling, routing, and workload shaping to achieve up to 25% GPU-hour savings and an 80% reduction in inefficient-autoscaling waste while maintaining tail latency and SLAs. They projected to save $2.5M a month. However this works around the cold-start problem instead of solving it, leaving more savings on the table.


Cold starts and slow reprovisioning are an overprovisioning tax, lowering delivered tokens per GPU-hour and with them cost per token and revenue per megawatt.


### 2. Failures.


Failures tax the denominator three ways, and every one grows with scale.


**Increasing frequency of catastrophic failures.** As deployments scale, failures grow due to hardware degradation, thermal instability, and unpredictable preemptions: production clusters report one failure per 7.9 hours per 1024 GPUs, with 2 to 5% of nodes failing each month (ReviveMoE, 2026; He et al. Unicron, 2023; Hu et al., 2024; Meta reliability study, HPCA 2025; Jiang et al., 2024; Epoch AI).


**Increasing blast radius.** Frontier models increase blast radius due to multi-GPU and multi-node deployments. For example, NVIDIA’s NVLink72 binds 72 GPUs into one NVLink domain, increasing the blast radius of a single GPU failure to impact 71 other GPUs (FailSafe, 2025; NVIDIA GB200 NVL72 documentation). To recover from the failure, the KV cache for all inflight requests is irrecoverably lost, requiring expensive and time-consuming recomputation before inference can continue. In addition, the surviving 71 GPUs must reshard and rebalance model weights resulting in substantial data movement and traffic over PCIe (FailSafe, 2025). This means that for the duration of recovery, waiting on the node is a 72x multiplier on GPU-hours delivering zero tokens.


**Increasing recovery duration.** The third factor scales with model and context size, not cluster size. Recovery today means restarting the instance: reload weights, rebuild KV state from scratch. Alibaba Cloud’s own docs warn that loading full DeepSeek-R1 takes 20 to 30 minutes (Alibaba PAI, 2026). One rank failure in a 32-GPU expert-parallel instance means 348 seconds of unavailability under standard full-restart recovery (EEP, 2026). Rebuilding one million-token request’s KV cache on a 405B model: ~20 minutes on 8×H100 (GhostServe, 2026). Both inputs keep growing, weights with every model generation, KV with every context window. For a service on a single deployment, a 99.9% SLO allows 43 minutes of violation per month, and one frontier cold restart burns half to two-thirds of it.


### 3. Immobility (placement).


Cold starts and failures are about workers that are down. This tax is about workers that are up, fully powered, and simply in the wrong place. A scheduler can place a worker and it can kill a worker, but it generally cannot move the full initialized worker (weights, runtime state, CUDA graphs, and in-flight KV) without losing or rebuilding state. That makes placement a one-way decision even as traffic, hardware availability, and failure risk change. As traffic and conditions shift, capacity strands in stale positions, drawing full power while producing fewer tokens per hour than the same GPUs could produce elsewhere.


Immobility exacts its price three ways:


**Fragmentation.** Free GPUs scatter as jobs come and go, and a frontier replica needs a contiguous multi-GPU or multi-node resource that isn’t available across fragmented capacity. On one production cluster of 6,200 GPUs, about 500 sat unusable once the fleet was roughly 90% packed (Weng et al., ATC 2023; NVIDIA Volcano scheduler blog).


**Load imbalance.** Output lengths vary by an order of magnitude, so decode instances that started balanced diverge: some saturate while others sit idle, and neither scaling out nor rerouting new requests fixes an instance already holding state. Only moving live work rebalances it. STAR migrates a single request’s KV cache to a lighter instance and yields up to 2.63x higher goodput with P99 time-per-output-token cut by 75% (STAR, 2025). Matching the prefill/decode split to live traffic recovers up to 1.5x goodput over vLLM and DistServe baselines, with P90 time-to-first-token cut by roughly two-thirds (DOPD, 2025). Moving the smallest movable unit of state, one request’s cache, between identical warm instances is worth multiples of throughput. However, this requires a warm replica: weights loaded, graphs captured, silicon fixed at deploy time. The requests move because the workers cannot.


**Hardware mismatch.** Even a well-loaded worker can be running on the wrong silicon for what it is starved for: decode on compute-rich, bandwidth-poor GPUs while bandwidth-rich silicon runs prefill. The two phases are bound by different resources. Prefill runs every prompt token in one parallel pass and is bound by compute; decode emits tokens one at a time, each streaming the full weights and a growing KV cache out of memory, and is bound by bandwidth and capacity. The H100 and H200 price that split exactly: identical compute die, 43% more bandwidth and 76% more memory on the H200. Prefill gains nothing from the upgrade, time to first token is roughly equal on both parts (Baseten H100/H200 benchmark, 2024), so the cheaper H100 is the right prefill part; decode-dominated throughput rises 37% to 42% on MLPerf Llama 2 70B from the memory subsystem alone, so the H200 is the right decode part (MLPerf Inference v4.0, 2024). Invert the assignment and the premium is paid twice: H200 bandwidth idles under prefill while H100 decode runs slow.


Matching phase to hardware is worth real money at every layer of the stack. Clusters that split prompt computation onto compute-heavy GPUs and token generation onto cheaper or power-capped ones deliver up to 1.4x higher throughput at 20% lower cost, or 2.35x more throughput within the same power and cost budgets (Splitwise, ISCA 2024). On mixed fleets of H100s, A100s, L40s, and A6000s, optimizing the prefill/decode placement yields up to 2.0x higher throughput at the same price, or equal performance at 30% lower (HexGen-2, ICLR 2025). The mismatch is large enough to design out of the chip entirely: a prefill part that swaps HBM for cheaper memory beats a modeled H100 by 8% at 52% lower hardware cost, a decode part with pared-back compute holds 97% of performance at 28% lower TDP, and clusters of both cut hardware cost 19% to 41% at equal performance (SPAD, 2025).


Both architectures pay this tax. Colocated serving runs both phases on a single GPU, so one phase is always starved: chunked prefill interleaves the phases in time but cannot change what the silicon is, and the mismatch survives any schedule. Disaggregated serving fixes the alignment at deploy time, but becomes suboptimal as fleet and traffic evolve. TetriInfer flips a prefill instance to decode in 5 to 7 milliseconds, but only after draining in-flight work and only on the same silicon: a flipped H100 is still an H100 (TetriInfer, 2024). NVIDIA Dynamo reassigns GPU roles at runtime, but each switch kills in-flight decodes and forces a full model reload and warmup, roughly 40 seconds of degraded capacity on Qwen3-32B across 8xH100, growing with model size (DuetServe, 2025). That 40 seconds is a cold start paid to correct immobility: two taxes in one transaction. As with load imbalance, everything moves except the worker: requests migrate, roles flip, and the worker stays fixed to the GPU.


> The danger of immobility waste is that it never trips an alarm. It shows up only as delivered tokens per hour sitting below what the hardware could produce.


Three taxes with a single root cause. A cold start is state that cannot be pre-built. A failure is state that cannot be saved. A stranded placement is state that cannot follow the hardware it needs. The fleet can start workers and it can kill them, but it has limited ability to preserve and move them, and every one of these taxes is the price of that missing primitive.


> The missing primitive is migration. The control plane scales it across the fleet.


State portability turns a running inference worker into a schedulable object: initialized weights, CUDA graphs, runtime state, and in-flight KV can be captured and resumed on compatible hardware. The control plane makes it useful by deciding when to move workers, where to place them, and how to enforce operator policy across failures, maintenance, fragmentation, and hardware mismatch. Each tax is transformed: cold starts become restores, failures become resumes, and stranded placement becomes a scheduling decision instead of a sunk cost.


### 1. Cold starts become fast restores.


Each model’s cold start runs once. Checkpoint a worker after full initialization, weights in HBM, NCCL initialized, CUDA graphs captured, and every later start restores that state instead of rebuilding it. A ten-minute initialization becomes a state copy.


Point solutions have proven the concept. ServerlessLLM loads models from loading-optimized checkpoints for fast startup (ServerlessLLM, OSDI 2024); Foundry snapshots CUDA graph state to cut cold starts (Foundry, 2026). But both are engine-specific and application-visible: Foundry needs per-engine Python integration, a pinned KV cache configuration, and discards in-flight request state. Adopting one means integration work per engine and per version, redone whenever the parallelism configuration changes.


The results validate restoring pre-built state; the integration cost is the argument for doing it below the engine. Cedana takes the lower-level route: it productizes checkpoint/restore below the serving engine, so the same mechanism can apply across engines such as vLLM, SGLang, and Triton with minimal or no application changes. That lowers the integration burden versus engine-specific cold-start and recovery paths, while still leaving engine schedulers free to optimize request-level behavior.


Measured on 8xB200: frontier models (Llama-405B, Mistral-Large, Mixtral-8x22B, Qwen-235B) with checkpoints sizes ranging from 234 to 501 GiB **restore in less than a minute** , against cold starts of 10-15 minutes on the same nodes. The fleet effect is the larger number: operators hold warm pools because starts are slow, and SageServe showed that merely scheduling around this is worth up to $2.5M a month (SageServe, SIGMETRICS 2025). Restores at this speed shrink the warm pool itself, reducing the tax instead of working around it.


### 2. Failures become resumes.


With continuous, incremental checkpointing, a worker’s full state, in-flight KV included, survives the hardware that failed. Resume it on any healthy GPU or node: no full reload, no KV recompute. A failure costs the resume time, not the state.


Existing failure recovery is built one architecture at a time. Tarragon cuts failure stalls from ~64 s to 0.3-0.4 s, but only for its MoE attention/expert split architecture (Tarragon, 2026). FailSafe recovers 183x faster with proactive KV backup, but only for tensor-parallel groups (FailSafe, 2025). ReviveMoE avoids instance restarts, but is built into Huawei’s xDeepServe on Ascend (ReviveMoE, 2026). The results validate stateful recovery. The limits point towards a lower-level portability layer that can complement architecture-specific recovery systems rather than requiring every serving stack to implement its own full recovery path.


Each failure tax maps to a property of resume.


**Frequency:** At one failure per 7.9 hours per 1024 GPUs (Meta reliability study, HPCA 2025), recovery cannot depend on an operator; the control plane detects failures and resumes workers on its own, so failure handling scales with the fleet rather than the on-call rotation.


**Blast radius:** Checkpoint and restore operate at multi-GPU and multi-node scope, so a 72-GPU domain resumes as one unit and the 72x zero-token window shrinks to restore time.


**Duration:** The instance resumes from its checkpoint in restore time. The 20-to-30-minute cold start becomes less than a minute, and because the control plane detects the failure and triggers the resume automatically, that minute starts at detection, not when an operator picks up the page. With resume, the same event costs about a minute, 2% of the budget, leaving room for forty more failures a month before the SLO is at risk.


### 3. Stranded placement becomes a scheduling decision.


Each immobility tax resolves into a move.


**Fragmentation.** Migrate scattered workers to pack them onto fewer nodes. The 500 GPUs stranded on a 6,200-GPU cluster (Weng et al., ATC 2023) stop being a packing loss and become schedulable capacity.


**Load imbalance:** Workers migrate off saturated nodes as demand shifts, under operator policy. Because it runs below the engine, it needs no per-engine scheduler and can shift capacity between pools, not just load within one: a light decode worker’s hardware can re-enter service as prefill when the traffic mix moves. Request-level rescheduling like STAR remains complementary.


**Hardware mismatch:** When the right GPU for a worker changes, migrate the worker and resume it there, mid-request. The common case: a decode worker lands on H100s because that was the free capacity at rollout, and now H200s are available. Today that mismatch is permanent for the worker’s lifetime. With migration, the worker checkpoints and resumes on the H200s, decode throughput up roughly 40% from bandwidth alone (MLPerf Inference v4.0, 2024), no dropped requests, no re-prefill; prefill consolidates the other way, onto the cheaper compute-equal H100s. The Splitwise and HexGen-2 gains, 1.4x at 20% lower cost, 2x on mixed fleets, stop being deploy-time-only and become collectable whenever the fleet or traffic shifts. Today’s alternative is teardown: kill the in-flight decodes, then reload and re-warm, a cost that grows with model size. Migration moves the worker without destroying it.


Cedana’s product provides state-preserving migration below the serving engine with a fleet control plane. Operators define policies once: where to resume failed workers, how to drain nodes before maintenance, when to consolidate fragmented capacity, and how to vacate spot instances inside reclaim windows, and Cedana executes those policies by moving state instead of destroying it.


### 1. Detection is extensive, ubiquitous, and still improving.


Operators already see their fleets in detail. DCGM exports ECC counts, thermals, power draw, and row-remap counters. The driver logs Xid and SXID errors. Cloud providers publish maintenance events, and Kubernetes probes every node. NVIDIA’s inference reference architecture now treats serving signals such as queue depth and phase saturation as first-class telemetry (NVIDIA Inference RA, 2026).


Detection research is moving faster than the rest of the loop. ECC error trends predict GPU failures a day or more before they happen (ByteDance, SYSTOR 2023). Meta identifies failure-prone nodes from historic health signals with 85% accuracy, cutting large-job failures from 14% to 4% (Meta reliability study, HPCA 2025). Thermal drift shows up before a GPU falls off the bus (GWDG early-warning study, 2026). At three-million-GPU scale a cluster sees a hard failure every 30 minutes and a link flap every 48 seconds, and catching the flaps is an open research problem (Ghost in the Datacenter, 2026). The fleet increasingly knows what is about to go wrong.


### 2. The response loop is built, and it ships disabled.


The automation to act on these signals exists too. NVSentinel runs a full pipeline from detection through remediation on more than 40,000 GPUs inside NVIDIA (NVIDIA NVSentinel blog, March 2026). Crusoe replaces a failed node in about five minutes (Crusoe AutoClusters, 2026). Nscale runs its own closed loop (Nscale Fleet Operations, 2025). Look at the actions these systems can take. They cordon, drain, reset, and replace. Every one destroys the state of whatever was running. That is why NVSentinel ships with its remediation modules disabled by default and tells operators to enable them as they build confidence. It is why Crusoe keeps the customer’s own approval logic between detection and replacement. Automating a destructive action across a fleet is a liability, so the last step stays gated on a human.


### 3. Prediction goes unused because acting costs too much.


Acting on a day-ahead warning means evicting a healthy worker for a failure that may never come. The eviction pays the failure’s full cost including the lost sessions, the long cold starts, and the wasted GPU-hours. Prediction turns a possible failure into a certain one, paid earlier. So precursor signals pile up in dashboards instead of triggering anything, and money spent on better detection buys better-documented losses. A destructive response needs a near-certain signal before it is worth firing, and that certainty bar is what keeps the loop open.


### 4. A state-preserving move resets the math.


With safe preemption and resume, the worst case of acting on a false alarm is a short migration instead of a lost session and a ten-minute restart. When acting costs seconds, the optionality for improving reliability and throughput expands. Signals become worth firing on, prediction becomes prevention, and the modules that ship disabled become safe to turn on. The loop closes not because detection got better but because the action stopped being destructive.


### 5. Every signal becomes a policy.


Each signal the operator already exports maps to a policy the control plane runs, enforced when the expected benefit exceeds the cost of moving state.


- An ECC or Xid trend triggers migration ahead of the failure.
- A thermal throttle moves the worker off the hot rack.
- A spot reclaim or maintenance notice vacates the node with state intact.
- A fragmentation threshold triggers consolidation.
- A maintenance window drains without dropping a session.


All of this consumes the telemetry operators already trust, DCGM and Prometheus and the health events NVSentinel already emits, with no parallel monitoring stack. And it compounds forward. Every detector the industry builds next ends in an action instead of a page.


### 6. The ledger becomes a control loop.


Monitoring detects the problem but does not fix it, and the gap between detection and remediation is where GPU-hours are wasted and operators get paged (NVSentinel docs, Overview). Today’s observability stack can account for the three taxes but has limited ability to remedy them in time. Migration is the control-plane primitive that lets observability become action: the fleet uses the signals it already trusts to preserve, move, and resume inference state before GPU-hours are lost. With it, the ledger becomes a control loop.


The hardware curve keeps going up. A GB200 NVL72 rack runs $2.8 to $3.4M and roughly $3.9M all-in, with per-GPU capital cost at 1.6 to 1.7x the H100, and per-GPU power climbing from 700W toward 1.8kW on the Rubin roadmap. Rubin-generation NVL72 VR200 systems are quoted at $5M to $7M. (Tom’s Hardware, March 2026; SemiAnalysis, 2025). Capability now arrives in bigger, more expensive, and rigid blocks.


The unit of loss grows with the unit of purchase. Meta expects GB200 to move the unit of repair from the server to the rack, and projects job MTTF falling from 7.9 hours at 1,024 GPUs to under 15 minutes at 131,072 (Meta reliability study, HPCA 2025).


Larger workloads are harder to pack and mixed GPU generations make placement matter more. Left alone, the gap between what a fleet could deliver and what it does deliver widens by default.


> Cedana closes this gap by making GPU-resident inference state portable. It productizes checkpoint/restore and migration below the serving engine, then connects that primitive to fleet policy so operators can preserve state through failures, maintenance, fragmentation, spot reclaim, and hardware mismatch. The result is a practical path to improving token TCO and increasing delivered tokens per megawatt.


Thanks to[Abhishek Singh](https://www.linkedin.com/in/tremblerz/) and[Mihir Patel](https://x.com/mvpatel2000) for feedback.
