---
schema_version: "1.0.0"
document_id: "26ae3d7805715082591b75972c98979d72a94ed6e3f461886909775f5a7ee3a0"
company_key: "yc-unsloth-ai"
company: "Unsloth AI"
source_id: "yc-unsloth-ai-news-import-bb4a9dd43ab2"
canonical_url: "https://unsloth.ai/blog/nvidia-collab"
published_at: "2026-05-06T00:00:00+00:00"
first_seen_at: "2026-07-24T05:34:23.482806+00:00"
fetched_at: "2026-07-28T21:25:33.541420+00:00"
content_hash: "sha256:88dca4d6463dcf86fa30b11cc27f7aabc6e7577939ab6ec6eb60d0f1213c7b28"
---

# How to Make LLM Training Faster with Unsloth and NVIDIA

# How to Make LLM Training Faster with Unsloth and NVIDIA


## May 6, 2026


## May 6, 2026


**Authors:** Daniel, Michael, Mathew and Datta, with help from NVIDIA


We collabed with NVIDIA to make LLM training ~25% faster and in this blog/guide we'll breakdown exactly how we did it. These optimizations have no loss in accuracy and are an extra addition on top of Unsloth’s already 2-5x faster speedup! The new algorithms are auto enabled on RTX laptops, data center GPUs and DGX Spark machines, so just update Unsloth to get the latest improvements. By working with NVIDIA, we show how:


1. Caching packed sequence metadata makes training 14.3% faster.
2. Using double buffered async gradient checkpointing gives a 8% speedup.
3. gpt-oss training is 15% faster by using argsort and bincount during MoE routing.


## 1. Caching Packed-Sequence Metadata


Suppose we have several short examples:


Instead of padding all of them to the same length and wasting compute on padding tokens, we concatenate them into one longer packed sequence:


The model still needs to know where each original sequence starts and ends. So, alongside the packed tokens, we carry sequence metadata such as:


- sequence lengths
- cumulative sequence offsets (` cu_seqlens` )
- the maximum sequence length
- attention structure derived from the three items above


This is the key point: for a fixed packed batch, that metadata is the same for every layer.


If we write the boundary information for a packed batch as:


*B* = { lengths, cu_seqlens, max_seqlen, mask structure }


then every transformer layer in that forward pass consumes the same *B* .


If the model has *L* layers, rebuilding or re-synchronizing on *B* once per layer is not new work. It is the same information being reconstructed again and again.


In other words, the useful work is:


build *B* once, use it *L* times.


The wasteful version is:


build *B* + build *B* + ⋯ + build *B* ( *L* times)


The overhead here is not primarily extra FLOPs. Some of these paths can force device-to-host synchronization, effectively creating a GPU-CPU sync point. Once that happens inside a per-layer path, the overhead recurs at every layer.


That is what the packed-sequence caching change reduces. Instead of repeatedly reconstructing packed sequence info, SDPA packed masks, and xFormers block masks, it caches the reusable metadata and the attention-side structures derived from it, per device, for the current packed batch. Those cached structures are then reused across layers.


### Why this helps


Packed training already improves utilization by eliminating padding waste. But if the metadata path keeps forcing synchronization, some of that gain is lost to overhead that has nothing to do with the model's actual learning.


Caching helps because it removes repeated coordination work from the hot path. The forward pass benefits the most because that is where the same packed metadata is consumed repeatedly across many layers.


### Benchmarks


On` Qwen3-14B QLoRA SFT` :


- forward:` +43.3%`
- backward:` +5.8%`
- per batch:` +14.3%`


The forward pass sees the biggest benefit because repeated metadata and mask preparation show up most directly there. Backward also improves, but the effect is smaller. The time saved is similar, but the backward pass, especially with gradient checkpointing, takes longer, so the relative gains appear smaller.


Now that we know the measured gain, we can ask a simpler question: does that scale make sense?


### A quick sanity check


If we assume each layer is roughly similar, we can model the packed-attention path as:


*T_uncached* ≈ *L* · ( *A* + *s* )


where:


- *L* is the number of layers,
- *A* is the useful attention-side work per layer,
- *s* is the repeated metadata and mask-preparation overhead per layer.


With caching, that repeated overhead is paid once for the batch instead of once per layer:


*T_cached* ≈ *L* · *A* + *s*


So the saved time is approximately:


*T_saved* ≈ ( *L* − 1) · *s*


For the packed` SDPA` path, our microbenchmark on NVIDIA Blackwell GPUs showed that the low-level, host-visible metadata calls were real but small, at about` 0.2 ms` each. The dominant repeated cost was the packed` SDPA` mask-construction path itself, which measured about` 13.7 ms` for a synthetic packed batch with` 2048` total packed tokens.


For the` SDPA` backend, a better mental model is:


*small stream fence* + *mask rebuild* ≈ *mask rebuild*


That lets us do a cleaner consistency check. If one packed-mask rebuild costs` m` milliseconds, then under a uniform-layer model:


*T_saved* ≈ ( *L* − 1) · *m*


With *m* ≈ 13.7 ms, that predicts:


- ` 16` layers:` (16 - 1) x 13.7 ≈ 206 ms`
- ` 28` layers:` (28 - 1) x 13.7 ≈ 370 ms`


Smaller packed-sequence runs showed the same pattern:


- ` Llama-3.2-1B` ,` 16` layers: about` 199 ms` saved per step, which is about` 11.5%` lower end-to-end step time
- ` Qwen3-0.6B` ,` 28` layers: about` 319 ms` saved per step, which is about` 14.8%` lower end-to-end step time


Those percentages are relative to full training step time, so they still include work outside the packed-attention path, such as embeddings, the MLP, the LM head, the loss, and framework overhead. This estimate is intentionally only about the packed-attention side of the block, not the whole transformer layer. It is there only to check that the measured gains are in the right range for the packed` SDPA` path.


## 2. Hiding Latency With Double-Buffered Checkpoint Reloads


Activation checkpointing is a standard technique for training large models. The idea is to save memory by not keeping every intermediate activation alive through the backward pass. In exchange, we pay for some extra work during backward.


That trade-off is usually worth it, especially for larger models.


But it raises another systems question: if an activation has been offloaded, how does it get back to the GPU for backward?


In Unsloth's smart checkpointing path, activations can be staged in pinned CPU memory and copied back when needed. That saves VRAM, but it can introduce a bottleneck:


1. Copy the activation from CPU to GPU.
2. Wait for the copy to complete.
3. Run backward compute on that activation.
4. Start the next copy.


That is a serialization pattern. If one buffer is reused for both copy and compute, the copy stream and the compute stream keep taking turns.


Let *T_copy* be the activation reload time and *T_compute* be the backward compute time for the current layer.


With a single buffer, this part of the step is roughly limited by:


*T_single* ≈ *T_copy* + *T_compute*


That is the serialized case. We pay for both almost entirely, one after the other.


A cleaner way to handle this is to use two buffers.


While the backward pass is running on buffer *A* , the copy stream can preload the next activation into buffer *B* . Then the roles swap. That creates pipeline overlap, though not perfect overlap.


Double buffering does not reduce the amount of math. It hides copy latency behind useful compute.


### Why this helps


This kind of optimization tends to get stronger once the model is large enough that backward compute is substantial, but not so dominant that all copy overhead disappears into noise. For larger models, higher hidden dimensions mean more data movement, so hiding that movement has a larger impact. Larger models also tend to have more layers, which creates more opportunities to hide copies behind computation.


That is why larger dense models are a good fit for this improvement. The GPU has enough real work going on that the copy can overlap with it, and the extra VRAM needed for the second buffer stays modest.


The implementation also keeps practical guardrails in place:


- use extra buffers only when enough VRAM is available
- fall back cleanly when the memory budget is tight
- keep correctness unchanged


### Benchmarks


On the larger dense-model runs, benchmarked with NVIDIA B200 Blackwell GPUs:


- ` 8B` :` 0.3739 -> 0.4053 steps/s` ,` +8.40%`
- ` 14B` :` 0.2245 -> 0.2395 steps/s` ,` +6.70%`
- ` 32B` :` 0.1979 -> 0.2070 steps/s` ,` +4.61%`


Memory overhead stayed modest:


- ` +0.37 GB` at` 8B`
- ` +0.47 GB` at` 14B`
- ` +0.23 GB` at` 32B`


In these runs, final losses were effectively unchanged.


The speedup is consistent across larger dense models, and the extra VRAM cost stays relatively small.


Once we know the measured gain, the natural follow-up is: does the scale make sense?


### A quick sanity check


If we assume there are *L* checkpointed layers and each layer is roughly similar:


- each reload takes time *c*
- each backward compute chunk takes time *g*


This also scales with batch size, sequence length, and other factors that affect data movement and computation. We omit those terms for brevity.


With one buffer:


*T_single* ≈ *L* · ( *c* + *g* )


With two buffers, the first layer still has to wait for its activation to arrive, and the last layer still has to finish computing. So a better approximation is:


*T_double* ≈ *c* + ( *L* − 1) · *max* ( *c* , *g* ) + *g*


So the saved time is approximately:


*T_saved* ≈ ( *L* − 1) · *min* ( *c* , *g* )


This is the useful reading of the result:


- the first copy is still exposed
- the last compute is still exposed
- but for the middle of the pipeline, copy and compute can overlap


If the overlap is good, the *per-layer* cost in the middle gets much closer to:


*T_middle* ≈ *max* ( *T_copy* , *T_compute* )


From the measured larger-model results, the saved time per training step is roughly:


- ` 8B` : about` 207 ms`
- ` 14B` : about` 279 ms`
- ` 32B` : about` 222 ms`


These host buffers are pinned allocations, so the relevant bandwidth is measured pinned-memory host-to-device bandwidth, not pageable-memory bandwidth. On our NVIDIA B200 Blackwell-based system, that bandwidth was about` 55.7 GB/s` , with` 64 GB/s` as a useful PCIe ceiling for comparison.


If we use the extra buffer size as a rough proxy for one activation reload, then each reload is naturally on the order of only a few milliseconds:


- ` 8B` ,` 0.37 GB` : about` 6.6 ms` at` 55.7 GB/s` , or` 5.8 ms` at the` 64 GB/s` ceiling
- ` 14B` ,` 0.47 GB` : about` 8.4 ms` at` 55.7 GB/s` , or` 7.3 ms` at the` 64 GB/s` ceiling
- ` 32B` ,` 0.23 GB` : about` 4.1 ms` at` 55.7 GB/s` , or` 3.6 ms` at the` 64 GB/s` ceiling


To explain the observed saved time per step, we would need to hide roughly a few dozen such reloads:


- ` 8B` : about` 31` reloads at` 55.7 GB/s` , or` 36` at` 64 GB/s`
- ` 14B` : about` 33` reloads at` 55.7 GB/s` , or` 38` at` 64 GB/s`
- ` 32B` : about` 54` reloads at` 55.7 GB/s` , or` 62` at` 64 GB/s`


Hiding one such reload across a few dozen checkpointed layers lands in the few-hundred-millisecond range of saved step time, which is exactly the scale we observed.


Again, that saved time is part of the full end-to-end training step. It is not supposed to explain embeddings, the LM head, the loss, optimizer work, or every other non-checkpointed part of the step. The point is only that the communication we can hide is large enough to plausibly account for the measured step-time gains.


## 3. A Smaller but Useful MoE Optimization


The third change is more specialized, but it shows the same pattern in MoE routing.


In the PyTorch-based GPT-OSS MoE path we examined, one expensive part of routing is figuring out which tokens go to which expert. A naive implementation can do something like:


```text
for expert_idx in range(num_experts):
token_idx, _ = torch.where(router_indices == expert_idx)


```


At first glance, this looks harmless. But` torch.where` is data-dependent here: the number of tokens routed to each expert changes from batch to batch. This can introduce CPU-GPU synchronization or related runtime overhead because output sizes depend on the routing pattern. If this happens once per expert, the number of dynamic queries scales with` num_experts` .


The better approach is to group everything once:


1. Flatten all expert assignments.
2. Stable-sort by expert ID.
3. Use` bincount` once to get tokens per expert.
4. Build offsets from those counts.
5. Slice the grouped token list per expert.


Mathematically, the gain is not that we changed the routing logic. We changed how often we asked the runtime to answer a dynamic indexing question.


Instead of roughly:


*dynamic-query overhead* ∝ *num_experts*


because we do one dynamic query per expert, we move much closer to:


*dynamic-query overhead* ∝ 1


plus cheap bookkeeping after that.


This is the same theme in a more specialized setting: group once, then reuse offsets instead of repeatedly asking for dynamic token lists.


### Benchmarks


Note that these optimizations apply to any MoE using the` native_torch` backend.


For this GPT-OSS-specific routing improvement:


- team validation showed roughly` 10-15%` speedups on GPT-OSS configurations
- in the targeted routing path, we saw` +23%` forward and` +13%` backward


## What These Changes Have in Common


Even though these three optimizations live in different parts of the stack, they are solving the same problem.


The key optimization opportunities were in the glue code around the main kernels:


- rebuilding metadata that already exists
- synchronizing on information we could have cached
- letting copies and compute serialize instead of overlap


This is also why the improvements compose conceptually. As the main kernels get faster, overhead that used to be invisible starts becoming a meaningful fraction of the total step time.


There is a useful engineering lesson here. Once the math kernels are optimized, "faster" often means one of two things:


1. do less unnecessary work
2. make the unavoidable work happen in parallel


That is exactly what happened here.


## TL;DR


Optimization Main bottleneck removed Measured gain


Packed-sequence metadata caching *[(PR link)](https://github.com/unslothai/unsloth/pull/4243)* Repeated metadata reconstruction and synchronization across layers Qwen3-14B QLoRA SFT: +43.3% forward, +5.8% backward, +14.3% per batch


Double-buffered checkpoint reload *[(PR link)](https://github.com/unslothai/unsloth-zoo/pull/534)* Copy and backward compute serialized on one buffer +8.4% on 8B, +6.7% on 14B, +4.6% on 32B


GPT-OSS MoE routing with` bincount` *[(PR link)](https://github.com/unslothai/unsloth-zoo/pull/535)* Repeated synchronization from per-expert dynamic indexing ~10-15% in team validation, targeted-path +23% forward and +13% backward


💕 Thank you!


A huge thank you to NVIDIA for assisting us with open-source efforts to help the community and for helping us with this article. Also thank you for reading and using Unsloth - we appreciate it. 🙏


As always, be sure to join our[Reddit page](https://www.reddit.com/r/unsloth/) and[Discord](https://discord.gg/unsloth) server for help or just to show your support! You can also follow us on[Twitter](https://twitter.com/unslothai) and our newsletter on:[Substack](https://unslothai.substack.com/) .


Thank you for reading!


Daniel & Michael Han


🦥
May 6, 2026
