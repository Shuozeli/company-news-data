---
schema_version: "1.0.0"
document_id: "8d52ae95e957caba08c9021af2db93c39fd53401dbee9cbae50157381cb44c99"
company_key: "galaxy-digital-inc-class-a-common-stock"
company: "Galaxy Digital Inc. Class A Common Stock"
source_id: "galaxy-digital-inc-class-a-common-stock-news-import-fbc635ef0517"
canonical_url: "https://www.galaxy.com/insights/research/inference-capital-markets-ai-compute-gpu-futures-onchain-crypto"
published_at: null
first_seen_at: "2026-07-25T06:07:02.932709+00:00"
fetched_at: "2026-07-28T21:35:55.789196+00:00"
content_hash: "sha256:8566db60c72088e366273b700010503e515b482805b26bfca64c0a07e89d6bc5"
---

# Inference Capital Markets

## Introduction


The term *onchain inference capital markets* describes the set of networks, protocols, supporting infrastructure, and applications coordinating AI model[inference](https://hai.stanford.edu/ai-definitions/what-is-inference) outside the centralized API surface controlled by[frontier labs](https://www.longtermwiki.com/wiki/E820) and[hyperscalers](https://www.redhat.com/en/topics/cloud-computing/what-is-a-hyperscaler) , together with the financial layer now forming on top of that activity. Rather than routing every API call through[frontier model](https://www.nvidia.com/en-us/glossary/frontier-models/) providers like OpenAI, Anthropic, or the underlying cloud providers that service them, users can send prompts to networks of GPU operators coordinated by crypto token incentives and onchain settlement, and in some configurations receive cryptographic or economic guarantees about output correctness and privacy. The category has drawn growing attention in 2026 as inference – the act of running a trained AI model on new data to produce an output – has overtaken training as the dominant share of global GPU demand. Meanwhile,[autonomous agents](https://www.nvidia.com/en-us/glossary/ai-agents/) have emerged as a new class of inference consumer, software that pays programmatically and operates without a human in the loop.


In recent years,[decentralized GPU marketplaces](https://www.galaxy.com/insights/research/decentralized-ai-training) , inference protocols, payment rails, tokenization, capital formation vehicles, and onchain liquidity each had its moment. What is new is that these primitives are converging into a single integrated system, an *inference capital market* , which is projected to find growing demand as inference is increasingly used for all work. Ongoing onchain experimentation is organized around genuinely productive and economically significant activity and around demand that originates not only from crypto.


A few forces are driving this convergence. GPU usage is shifting decisively from[training](https://www.nvidia.com/en-us/glossary/ai-training/) toward inference, and[open-weight models](https://hai.stanford.edu/ai-definitions/what-is-an-open-weight-model) are closing the gap with frontier models for the tier of work where "good enough" suffices. This makes it economical to route otherwise costly tasks to whatever serves them cheapest, on crypto rails or off. Growing demand for inference is also pushing users to source compute creatively. Citadel recently[published a note](https://x.com/Moshaikh/status/2064754006208008218) showing a decline in token expenditures as measured by the Silicon Data LLM Index, reflecting a shift to cheaper model usage. ([AI tokens](https://blogs.nvidia.com/blog/ai-tokens-explained/) , the units in which AI companies price their services, should not be confused with *crypto* tokens, assets created on blockchain networks.)


Companies[including](https://x.com/yuhasbeentaken/status/2071464716786950223?s=46) Coinbase, Microsoft, AirBnB, and many others have also recently shifted toward using open models, predominately Chinese ones. OpenRouter's[recent raise](https://openrouter.ai/announcements/series-b) is also a testament to growing demand for access to a diversified set of models that can make inference more economical. This is partly a[result of supply constraints](https://newsletter.semianalysis.com/p/the-great-ai-silicon-shortage) that make the marginal cost of provisioning inference more expensive.


The second force is financialization. The prevalence of AI and the use of its intelligence as an input in nearly every task is creating demand for its commodification and financialization. Increasingly, teams are thinking about ways to make AI compute a tradable asset that fits into a broader financial layer. ** The early scaffoldings of inference capital markets are emerging, financializing AI hardware and capacity, and aiming to assemble those into a comprehensive market.


## GPU Indices and Futures Markets


Before diving into the onchain manifestations of inference capital markets, it’s important to first acknowledge the much larger offchain markets already in development, most notably GPU futures.


Estimates for the scale of the AI build-out vary widely.[Morgan Stanley](https://www.morganstanley.com/content/dam/msdotcom/en/assets/pdfs/Research_Bridging-Data-Center-Gap.pdf?utm_source=chatgpt.com) forecasts roughly $2.9 trillion of global data-center capex through 2028, excluding power investments, with about $2.5 trillion tied specifically to AI-related workloads.[McKinsey](https://www.mckinsey.com/industries/technology-media-and-telecommunications/our-insights/the-cost-of-compute-a-7-trillion-dollar-race-to-scale-data-centers?utm_source=chatgpt.com) estimates that data centers will require $6.7 trillion of global capex by 2030, including $5.2 trillion for AI-processing facilities and $1.5 trillion for traditional IT workloads; its AI-specific scenarios range from $3.7 trillion in a constrained-demand case to $7.9 trillion in an accelerated-demand case.[Goldman Sachs](https://www.goldmansachs.com/insights/articles/tracking-trillions-the-assumptions-shaping-scale-of-the-ai-build-out?utm_source=chatgpt.com) estimates approximately $7.6 trillion of AI infrastructure capex between 2026 and 2031 across compute, data centers, and power. Whatever the exact figure, these projections consistently show that compute/hardware is the largest category of spend, ranging from roughly 55% to 67% across the Morgan Stanley, McKinsey, and Goldman Sachs estimates.


Such projections are difficult to make due to unknown supply and demand factors. One factor is demand elasticity. If cheaper compute gets reinvested into larger models and broader deployment rather than pocketed as savings, then efficiency gains will expand usage instead of shrinking the bill. Another factor is the useful life of the chips. This remains an open question, with depreciation estimates ranging anywhere from three to seven years. While increasingly performant chips are released every year, which one would expect to push older chips toward obsolescence, those relics have continued to hold value. Severe supply constraints render the use of older hardware necessary to keep up with demand and they can also be used to serve lower-tier models. The result is an enormous and sustained amount of capital flowing into a volatile asset, exactly the conditions under which markets to price, hedge, and finance that asset start to form.


> ***The job of sourcing compute has been likened to a drug market, where you have a "guy" you call for supply.***


In one sense these markets already exist, just not in standardized form. Large buyers already lock in future compute privately, from on-demand hourly rentals to multi-year reserved contracts (the GPU equivalent of[offtake agreements](https://www.investopedia.com/terms/o/offtake-agreement.asp) ) to bilateral deals between providers and their biggest customers, often priced in opaque, relationship-driven negotiations. Frontier labs like OpenAI[sell tokens in bulk](https://openai.com/api-scale-tier/) , hyperscalers reserve capacity from each other, and[neoclouds](https://www.cio.com/article/4143053/what-you-need-to-know-about-the-coming-of-age-of-neoclouds.html) buy forward from clouds and brokers because there is not enough to go around. One of the world's largest inference operators, Baseten,[likened sourcing](https://www.youtube.com/watch?v=Qh7Oxvo5sJI) compute today to a drug market, where you have a "guy" you call for supply. The firms that profit from that opacity, the brokers and large holders trading on relationships and information, have little reason to abandon it for a transparent screen and a few basis points of efficiency.[Incumbent resistance of the same kind](https://x.com/jvb_xyz/status/2071961528585093414) , from the likes of Vitol, BP, and Shell, helped kill a decade of attempts to build an exchange for liquefied natural gas. GPU futures are emerging on top of this fragmented base as a standardized layer for transferring price risk, not yet a replacement for how capacity is provisioned.


For a futures market to function, it needs an accurate index for contracts to reference. This is harder for compute than for more standardized commodities. A[GPU-hour](https://www.computetape.com/learn/what-is-a-gpu-hour/) means little without specifying the chip, its memory and networking, the region, and whether the capacity is on-demand or reserved. Similar discrepancies in the underlying commodity existed for electricity, bandwidth, and LNG before each became a liquid market. It was resolved the same way each time, by defining grades and reference prices rather than insisting every unit be identical. Crude oil is priced off benchmark grades like the New York Mercantile Exchange’s WTI contract and[Brent](https://www.ice.com/brent-crude) . Natural gas is priced off hubs like[Henry Hub](https://www.eia.gov/dnav/ng/hist/rngwhhdm.htm) .


GPUs are converging on a similar structure. Ornn (a Galaxy portfolio company) publishes a Compute Price Index built from live transaction data. Silicon Data publishes H100, A100, and B200 Rental Indexes daily on Bloomberg terminals, normalizing pricing data across configurations, providers, and regions into a single benchmark. Compute Desk is building in the same direction. As Ornn frames it, these indexes operate more like the Secured Overnight Financing Rate ([SOFR](https://www.newyorkfed.org/markets/reference-rates/sofr) ) than its[benighted predecessor](https://www.newyorkfed.org/medialibrary/media/research/staff_reports/sr667.pdf) ,[LIBOR](https://www.bbc.com/news/business-21358362) . Each is built from a broad pool of observed transactions across the market rather than a panel's estimates, tracking no single GPU but the going rate for an aggregated set of defined compute. That real-world grounding is what makes heterogeneity manageable. The index does not need any two GPU-hours to be identical, only enough real transactions to compute a representative price. It still faces a problem crude does not have. WTI has anchored oil for decades because a standard barrel does not change, while a GPU benchmark decays as the fleet rolls from H100 to H200, B200, GB200, and Rubin, forcing the reference to be rewritten each generation. Fragmentation compounds the problem, as AMD, Google TPUs, Amazon Trainium, hyperscaler ASICs, and sovereign chips split demand across incompatible silicon. A durable benchmark gets harder to hold, not easier.


The second point of contention is settlement. A lab hedging its compute budget or a trading desk taking a view may be satisfied with pure price exposure, not hardware, and for them a contract that pays the difference against an index is the entire point. A neocloud that needs real chips to serve customers, however, needs the capacity itself. The futures now being launched are cash-settled because price-hedging demand is the easiest to standardize, the same reason most commodity futures settle financially even when the buyer could take delivery. Physical delivery is possible, but much trickier to provide because it requires even further standardization and specificity. Given the pace of development of cash-settled futures, and emerging demand, it would be no surprise if physically delivered contracts emerge in the coming year. There is a case the order is backwards. Cash settlement against a thin index invites manipulation when a few sellers control supply, and commodities usually need physical delivery, or a working exchange-for-physical mechanism, to force prices to converge on reality first.


A market also needs participants on both sides with genuine reasons to trade, not just speculators taking a view. The natural buyers are the firms whose costs are tied to compute and who want to lock them in. This includes AI labs, application companies, and neoclouds that have promised capacity downstream and need to secure the input. The natural sellers are the firms sitting on GPU inventory with uncertain future use, hyperscalers, large GPU owners, and brokers. Lenders financing GPU purchases need the same reference price, because debt backed by depreciating hardware has to be marked against something. Speculators and proprietary trading firms, present in every market where there is an opportunity to make money, sit on top and add liquidity. For now, the main structural tension in the market is that most sellers want to sell long-dated contracts and buyers want to buy short-dated ones, because sellers want to lock in revenue and buyers want flexibility.


Despite these challenges, the early signs of a more mature GPU market are beginning to emerge. Prediction market platforms including Kalshi have launched[markets](https://kalshi.com/markets/kxrtx5090mon/rtx-5059-monthly-price/kxrtx5090mon-26mar31) for the prices of specific GPUs. And New York Stock Exchange parent ICE (in partnership with Ornn) and the[CME](https://www.cmegroup.com/media-room/press-releases/2026/5/12/cme_group_and_silicondatapartnertolaunchfirstcomputefutures.html) (in partnership with Silicon Data) have announced plans to list GPU futures in the coming year. "[Compute as a Commodity](https://variant.fund/articles/compute-as-commodity-framework-gpu-futures-markets-emerge/) " could soon be a reality.


## Onchain Inference Capital Markets


Model and inference providers are essentially token factories. They take the crude input, GPUs, and refine it into outputs in the form of tokens. Whereas a GPU-hour is increasingly standardizing through GPU indices, the token layer above it is far less developed, complicated by the fact that a token from one model is not priced like a token from another. That layer is starting to take shape regardless.[China's three state telecom operators have begun retailing inference as a metered utility](https://www.digitimes.com/news/a20260522PD204/telecom-china-telecom-2025-china-mobile-china-unicom.html) , selling standardized monthly token packages much like mobile data plans. Amazon[reportedly](https://cryptobriefing.com/amazon-anthropic-token-payments-shift/) will begin paying Anthropic by tokens consumed rather than by the compute hours it committed to before. And the[Shanghai Futures Exchange](https://www.reuters.com/world/china/china-works-ai-token-futures-market-sources-say-race-with-us-2026-05-28/) is said to be in early-stage design of futures tied to AI tokens, a counterpart to the GPU contracts CME and ICE are building on the input side.


Crypto is building its own version of this. These onchain inference capital markets build on[established crypto-AI primitives](https://www.galaxy.com/insights/research/understanding-intersection-crypto-ai) such as GPU providers and decentralized model developers, while incorporating newly emerging verticals such as[agentic payment standards](https://www.galaxy.com/insights/research/x402-ai-agents-crypto-payments) and tokenized inference marketplaces. The ecosystem already spans many chains and execution environments, but development is especially concentrated around Base and Solana thanks to their established developer and user bases.


At the core are inference providers and networks, the projects that turn prompts into outputs. Around them sit the layers that make inference useful, available, and financializable: model developers, GPU and compute providers, routers and marketplaces, agents and applications, payment rails, and capital formation infrastructure. Those surrounding layers matter because they either create demand for inference, supply inputs for it, or transform its usage into something that can be paid for, financed, routed, or owned.


Many of these offerings are not unique to crypto and have close offchain equivalents. At the top of the stack,[agent harnesses](https://medium.com/@d3xvn/what-is-an-ai-agent-harness-20a573f24e01) like Hermes and Ironclaw serve inference interchangeably from frontier labs or onchain providers like Venice. Models from decentralized developers like Nous Research are accessible on OpenRouter, a one-stop shop for LLMs. GPU providers are the permissionless, open-source counterparts to hyperscalers and data centers, often at much smaller scale. And agentic payment protocols like x402 and MPP can pay for an OpenAI or Anthropic subscription as easily as a Venice one. Programmatic settlement is fast becoming standard rather than a crypto-specific edge, with OpenAI and Visa recently announcing agentic payment infrastructure of their own.


The unique components emerge on the financialization side, where crypto changes how inference is owned, priced, and financed. We have written extensively on how crypto rails accelerate capital formation (read our reports “[The Agentic Flywheel”](https://www.galaxy.com/insights/research/zero-human-companies-ai-agents-defi-crypto) and “[Raising for Robots”](https://www.galaxy.com/insights/research/agentic-capital-markets-ai-agents-crypto-ralph-wiggum-truth-terminal-gas-town) ), and many of those same primitives apply directly to inference.


Financializing inference has attracted a range of onchain projects that use blockchain payment rails and tokenization to turn inference activity into tradable assets. This takes three forms.


-


*Inference service providers* like Venice and Morpheus tokenize inference access, turning a claim on future inference into something that can be held, priced, and resold.


-


*Proof of useful work* projects like Pearl and Ambient tokenize inference production, paying out a token for the work of serving it.


-


*Credit providers* like USD.AI do something different. Rather than tokenizing inference , they finance the hardware it runs on, using stablecoin deposits to fund the GPUs and data centers underneath.


Collectively, these components come together to form onchain inference capital markets.


## Inference Providers


The inference provider layer is the heart of the stack. This is where decentralized inference most directly resembles the traditional AI API market. A user or developer selects a model; sends a prompt; pays per token, per request, or through a subscription; and receives an output. In the simplest version, this looks like using OpenRouter, Together AI, Fireworks, or a frontier-lab API. The difference is that crypto-native providers may source capacity from decentralized GPU networks, accept stablecoins or tokens as payment, provide access to open or uncensored models, include privacy guarantees, or attach tokenized access rights to usage.


OpenRouter is one of the most favorable venues onchain inference will find. Demand there is priced by the token, and users are free to switch providers on any request, the exact setting where a cheaper or faster provider should take share. Onchain providers have serviced anywhere from 0.5%-1% of daily tokens processed by OpenRouter over the past three months, a stretch when total tokens served on OpenRouter continued to explode. While this demonstrates some initial traction outside of the crypto-native community, it is still a small portion of total usage and demonstrates these providers cannot yet compete with established centralized offerings, whether due to lack of distribution, relative cost, or other factors.


But OpenRouter represents only a portion of the total token usage. Venice, for example,[reported](https://x.com/ErikVoorhees/status/2070188683416715519) processing 100 billion tokens across all its access points on June 23, 10 times the amount it processed on OpenRouter. Looking just at OpenRouter usage does not account for total traction at the individual project level, where onchain inference providers are attempting to establish a consistent customer base with a variety of methods. Some of these are specific features. Venice aggressively markets privacy as a distinguishing feature, enabling users to access inference with less worry about their providers retaining, inspecting, leaking, censoring, or being compelled to disclose sensitive information. Chutes and AkashML enable anyone to plug a GPU into their network and monetize latent compute to attempt to bring down costs. While these features may win a provider some share, they are largely replicable by centralized providers and may not be enough to gain meaningful market share.


Where onchain offerings can carve out real differentiation is with mechanisms that financialize inference, turning access into an asset a buyer can own, hold, and resell rather than a subscription it can only consume.


### Venice: Tokenizing Inference Ownership


Venice, founded by crypto OG and serial entrepreneur Erik Voorhees, is the furthest along in turning inference access into an ownable asset. It runs a two-token system, VVV and DIEM, that wraps a claim on future inference into something a holder can mint, own, and resell.


VVV serves as the project's "capital asset." It does not confer ownership of the Venice platform, which has its own separate equity (in June, Venice[raised](https://techcrunch.com/2026/07/01/venice-ai-becomes-a-unicorn-with-65m-series-a-as-its-privacy-first-ai-platform-takes-off/) a $65 million Series A round), but holders can in theory benefit from the project's success. Most directly, a portion of Venice's revenue buys and burns VVV. The buy-and-burn runs two ways: discretionary burns funded from general revenue, and a programmatic burn that routes a fixed portion of every new subscription into buying and burning the token. To date, 42% of VVV has been burned.


VVV also carries utility functions. Any amount can be staked to earn annual VVV emissions, or 100 VVV can be staked to unlock a pro subscription. Its most interesting use, however, is its relationship with DIEM, Venice's "compute asset." Holders lock staked VVV to mint DIEM, and each DIEM grants access to $1 of Venice inference credits in perpetuity. A holder of 100 DIEM has $100 of API credits, good across every model on Venice's platform, forever (or at least as long as Venice is in business).


The staked VVV required per DIEM follows a curve Venice set, rising exponentially as DIEM supply approaches a target that Venice controls, because each DIEM is a perpetual dollar-a-day liability on its books. Supply now sits near that target, so the rate has climbed from roughly 90 VVV per DIEM at launch to several hundred today. That brakes issuance and means early minters acquired their DIEM far cheaper, in VVV terms, than anyone can now. While VVV is locked to back a DIEM, the staker keeps only 80% of regular VVV staking yield, with the other 20% routed to Venice. And the lock releases only by burning the DIEM, so a minter who has sold must re-acquire DIEM on the market to reclaim their VVV, at a loss if the price has risen. The exact mint formula is[here](https://venice.ai/blog/7-days-to-diem) .


The two tokens reinforce each other. DIEM can only be minted by locking staked VVV, so rising DIEM demand pulls VVV out of liquid supply and gives it a use beyond speculation. DIEM, in turn, benefits from Venice's growth. The more useful and widely used the platform becomes, the more valuable a transferable claim on daily access to it. A DIEM holder does not just own resaleable inference, they hold a position tied to Venice's success.


The broader product feeds the token economy even when users never touch crypto. Venice's team[says](https://www.youtube.com/watch?v=7ttIdA-wNa0) most users are not crypto-native and many do not care about the token. But when they subscribe, buy credits, or use the platform, that activity still drives VVV buy-and-burn and demand for Venice inference. The token economy sits downstream of the product rather than replacing it. Venice is not a crypto token searching for an AI use case, but an AI product routing some of its usage and access rights into a tokenized inference market.


> ***What makes Venice's DIEM distinct is ownership. It lets users own the inference they consume rather than rent it.***


DIEM is an experiment in how to tokenize and deliver inference access. What makes it distinct is ownership. It lets users own the inference they consume rather than rent it. A buyer paying per request gets nothing back once the inference is spent, while a holder of tokenized access owns an asset they can keep, transfer, or sell. That opens several use cases:


-


Because the claim is tradeable, a holder with uneven demand can keep baseline access and sell or lease the days they do not need, recovering cost that pay-per-request simply forfeits. An agent can hold DIEM directly, giving it a permissionless, ownable balance of inference to draw on. This runs through a venue like Aerodrome for outright sales or a marketplace like Surplus, UsePod, AntSeed, or CarpeDiem for fixed-duration leases.


-


Another case the Venice team often cites is a user buys DIEM, uses it for inference for a day, and sells it back the next. If the price holds steady, the inference was effectively free. If it rises, the user comes out ahead. The reverse also holds. If the price drops, the holder can lose far more than buying the inference outright would ever have cost. For some users, this means they can both speculate on the price of inference while also consuming it.


-


DIEM can also provide cost certainty. A business or agent with steady, predictable demand can use DIEM to fix its compute cost in compute terms, the same logic as a multi-year cloud reservation. It cannot know what a dollar of inference will buy in two years, but it can lock that in now, and if it uses the access and resells near cost later, the inference comes cheap. At $1,270 (DIEM’s price as of July 7, 2026), a DIEM is roughly four years of credits at a dollar a day, so the buyer is prepaying about three and a half years of a perpetual stream. The catch is that buying this certainty means holding a volatile, perpetual, dollar-denominated asset, which works against the certainty the buyer wanted. Priced against a perpetual promise, DIEM implies a double-digit discount rate on Venice's ability to keep serving, and the claim is worth something only for as long as Venice keeps serving it.


The mechanism is early and comes with real drawbacks:


-


Tokenizing inference is most useful to issuers that need to pull demand forward and raise capital. The labs with the best models and real pricing power have little incentive to tokenize because it sacrifices price discrimination between customers, breakage revenue (unredeemed credits), and repricing flexibility.


-


DIEM has no maturity that makes the holder whole and no collateral or reserve behind it, unlike the GPU-backed lending discussed below. It is an open-ended bet that Venice is still serving the dollar years out, with no covenant or recourse if it is not.


-


A DIEM is a claim on what Venice decides a dollar of inference buys, not on a fixed quantity of inference. Venice sets the token price per model, which can fluctuate depending on demand and availability. The risk is not just which way market prices move; it is the discretion between Venice and the holder. Cheaper models should mean a dollar buys more, but the holder sees that savings only if Venice passes it through.


Erik Voorhees' Venice is the project furthest along in turning inference access into an ownable asset. (YouTube/ReasonTV, CC BY 3.0)


The deeper question is whether DIEM's perpetual, dollar-denominated form is the exposure inference buyers want, or whether they would prefer a claim that is term-dated, denominated in compute or tokens, or both.


Today, DIEM is mostly held as a speculative asset rather than used as inference access, with less than 50% of the inference provided used on a weekly basis. Venice's own[materials](https://venice.ai/blog/7-days-to-diem) call DIEM a "range-bound perpetuity" and sort its buyers into API users, VVV holders extracting value without selling, and speculators arbitraging the spread. The latter two account for the largest share of holders. The closest centralized analogue is OpenAI’s Scale Tier: a prepaid commitment to model throughput, denominated in tokens per minute and purchased over a fixed term. But Scale Tier is not ownable inference. It is account-bound, non-transferable capacity inside OpenAI’s platform. DIEM’s advantage is the opposite: it can be held, resold, and composed across the rest of the crypto inference stack. The better instrument may pair Scale Tier’s tenor and compute-denominated capacity with DIEM’s ownership and transferability.


> ***For Venice, every DIEM outstanding is a dollar of compute it must serve and can never sell to anyone else, a liability. This is why it buys the token back out of revenue, not as a favor to holders.***


Ultimately, VVV and DIEM are not meant to resemble equity instruments for Venice. They initially served as a bootstrapping mechanism to build the platform's user base. Today, their value comes from the compute claim they provide access to. A holder of VVV, through the DIEM they can mint, owns a perpetual claim on Venice inference that is worth more as Venice grows and its compute becomes more valuable. For Venice, every DIEM outstanding is a dollar of compute it must serve and can never sell to anyone else, a liability, which is why it buys the token back out of revenue rather than as a favor to holders. One side owns the claim and wants it to appreciate; the other owes it and wants to manage it down. That shared position in Venice's compute, not any equity interest, is the aligning force, and it is what makes VVV an interesting attempt at introducing a utility token mechanism to build an inference business.


## Tokenizing Inference Production


Where Venice tokenizes *access* to inference, useful proof-of-work networks tokenize its *production* , using emissions to subsidize the cost of serving it. Proof of work bootstraps a network by paying a token reward to whoever solves an arbitrary puzzle, which is what secures Bitcoin and also what makes it burn energy on nothing else. *Useful* proof of work swaps that puzzle for real inference, so the same compute that secures the chain also produces something a customer will pay for. Pearl and Ambient are the two live attempts at it, built on opposite designs.


### Pearl


The Pearl Network is a Layer-1 blockchain forked from Bitcoin's codebase that keeps the latter’s[UTXO](https://strike.me/en/learn/what-is-a-utxo/) model and[difficulty adjustment](https://www.lightspark.com/glossary/difficulty-adjustment) but replaces the SHA-256 hashing algorithm with[matrix multiplication](https://medium.com/@danailkhan1999/why-matrix-multiplication-matters-in-deep-learning-bb4ac0d9f356) , the core operation in AI inference and training. Pearl’s claim is that the same matrix multiplication that serves a customer's inference can double as a mining attempt.


When an AI model answers a prompt, under the hood it multiplies two big grids of numbers together; that’s matrix multiplication. Pearl has the miner take those exact grids, scramble them slightly by adding a layer of random numbers, and multiply the scrambled versions instead. Multiplying the scrambled grids is the heavy computation, and it is this computation that gets entered into the mining competition. As it runs, the intermediate results are continuously checked against a difficulty target. If one falls below it, that miner wins the block, the same rule Bitcoin uses, except the work being tested is the real computation of serving a model rather than the throwaway hashing of standard mining. Once the multiplication is done, a quick final step subtracts the random layer back out, leaving the exact inference request the customer wanted. So the single act of multiplication produces two things at once. The real AI output, and a chance at the block reward.


Two design choices make this twofer practical. Pearl ships as a plugin for vLLM, a popular piece of software that AI companies already use to run their models, so a provider can switch it on without rebuilding its setup. And because a winning entry must be published for the network to verify it, Pearl wraps it in a[zero-knowledge proof](https://ethereum.org/zero-knowledge-proofs/) so the customer's prompt and the provider's proprietary model weights stay hidden. The cost of adding all this is small. Pearl reports that running a model its way adds somewhere between 0.5% and 10% of extra work, and in its launch tests on Llama-3.3-70B, a widely used open model, the Pearl version ran as fast or faster than the normal one, because the team's reengineered version of the core computation happened to be more efficient than the standard one in some configurations.


As one of the first networks to combine proof of work and inference, Pearl saw strong early interest from miners after launch, with hashrate climbing quickly. But the protocol cannot distinguish a useful calculation (one servicing a real inference request) from a useless one, because a computation is valid whether or not a customer wanted the result. Pearl's white paper assumes as much, building into its assumptions a population of miners running throwaway calculations purely to earn the block reward. Pearl's launch showed it. The early mining rush drove a rapid climb in compute, with little sign any of it was serving real inference.


There are, however, growing signs of real-world traction. Most notably, in May Pearl[announced a partnership](https://www.together.ai/blog/together-ai-partners-with-pearl-research-labs) with Together.ai, one of the leading inference and compute providers, launching an inference endpoint priced more than 25% below Together's standard rate, with the discount funded by the Pearl token rewards earned on the same compute. Ultimately, Pearl's dual-use design only delivers useful work to the extent that real, paying inference demand drives the compute. Absent that demand, the block reward alone will only attract speculative miners, and the result is just a different Bitcoin-style proof of work with no productive output.


### Ambient


Ambient takes the opposite design choice from Pearl. Rather than letting miners run any model, it standardizes the entire network on one large open-weight model and builds its consensus around verifying that model's output.


Where Pearl has miners compete by brute force, all racing to solve the same puzzle, Ambient has them compete through an auction. A user or agent posts an inference job with a deadline and a price, in effect "serve this within X minutes and I will pay Y," and miners bid to take it. The winning miner runs the query on the network model, posting a deposit it forfeits if it fails to deliver on time, which holds it to quality and speed commitments. A randomly chosen set of validators, their priority weighted by each one's track record of useful work rather than by staked capital, then checks the result. Because miners serve many different jobs at once rather than all racing a single block, the network avoids the bottleneck that makes traditional proof of work slow, and the whole system, a Solana fork that swaps staking for useful work, is meant to run at Solana-like speed.


[Ambient is the second cheapest provider for input and output tokens on OpenRouter’s Kimi K2.7 Model](https://openrouter.ai/moonshotai/kimi-k2.7-code?tableSort=price:text-input:/M+tokens&tableSortDir=desc#pricing)


The auction is also the mechanism that can make Ambient’s inference pricing competitive. A normal API provider has to recover the full cost of serving a request from the user’s payment. An Ambient miner can be paid twice for the same unit of work: once by the user or agent whose query it wins, and again through protocol rewards for validated useful work. Because miners compete for jobs with a stated price and latency target, they should bid toward their net cost after expected token rewards, not their gross cost before rewards. In effect, token emissions subsidize the supply side, and the auction forces much of that subsidy through to the demand side as cheaper inference. The important difference from a generic mining subsidy is that the reward is attached to a job someone posted and paid for. If the mechanism works, emissions do not merely buy hashrate; they buy lower-priced, verified inference, which attracts more usage, gives miners more work, and strengthens the case for demand for the network’s token.


This auction is also what lets Ambient claim it has solved a problem Pearl has not. In Pearl, a miner earns block rewards by running matrix multiplications whether or not a customer wanted the output, which is why the network attracts compute serving no real demand. In Ambient, a miner only earns Ambient’s token (not yet released) by winning a job that someone posted and paid for, so mining and serving real inference are the same act by design.


Ambient also takes a unique approach to inference output verification. If a miner claims it ran your query on the agreed model, how do you know it did not quietly swap in a cheaper, lower-quality one to save money? This is a real concern even with today's centralized providers, which[have been accused of](https://hdsr.mitpress.mit.edu/pub/y95zitmz/release/2) quietly degrading model quality to cut costs. Ambient's answer uses a property of how language models work. As a model generates text, each step produces logits, the raw numerical scores it assigns to every possible next word before picking one. That stream of scores is effectively a fingerprint of which exact model did the thinking, and it can be hashed down to a short number and checked.


To check a miner that generated thousands of tokens of output, a validator does not rerun the whole job. It picks a random point in the text, asks the miner for its fingerprint at that point, and then runs the model for just one token at that spot to see whether its own fingerprint matches. One token of work confirms thousands. This is similar to Bitcoin, where producing the work is expensive but checking it is cheap. Ambient claims this keeps verification cost overhead near 0.1%, compared with the rough 10x to 1,000x overhead of the zero-knowledge proof methods other projects have tried.


### How Useful Is Useful Proof of Work?


What separates these projects from the rest of decentralized compute is that the work securing the chain is the work a customer wanted. When it works, a unit of energy buys both security and a saleable product. The mining is a second revenue stream on hardware a provider was already running, and the output is verifiable enough that an agent can buy inference without having to trust the provider to not degrade the model or cut off access.


> ***Absent sufficient genuine demand, the block reward alone attracts miners, and the PoW network fills with compute serving no customer, useful work in form but not in substance.***


Beyond the technical challenges, two other problems stand between that promise and its realization. The first is demand. A decentralized inference network competes against centralized providers and plain GPU rental, both cheaper and faster with no crypto token attached. To win, there must be buyers that want inference in a trust-minimized form, verifiable, censorship-resistant, neutral, with no provider that can rug them. The slice of demand willing to pay for that today is still small but could quickly expand as these projects prove their ability to provide consistent and stable inference at a cheaper cost, or as trust in centralized AI erodes. Pearl's launch is the cautionary illustration. Absent sufficient genuine demand, the block reward alone attracts miners, and the network fills with compute serving no customer, useful work in form but not in substance.


The second is token value accrual. Each project promises a flywheel where real usage drives demand for their crypto token, which funds the mining rewards that secure the network, which supports more usage. None has closed it. Mining mints the token and miners sell it to cover costs, but nothing on the demand side forces buyers to acquire it, because consuming the actual product, inference or proofs, mostly does not require the crypto token at scale. Pearl's inference can be paid for in dollars, and its proposed future marketplace where tokens would buy compute is a tacit acknowledgement that the loop does not yet exist. Ambient has deferred releasing its tokenomics and not said whether inference will be priced in the token. So each token is earned and sold rather than used.


Most likely, these networks will make their tokens the native payment rails for inference, the obvious way to close the loop. Paired with the emissions subsidy that lets them undercut market pricing, that strategy could be compelling. Cheaper inference draws real usage, and if it must be paid for in the token, usage becomes token demand. The flywheel only turns the right way, however, if that adoption sticks, with organic token demand eventually outweighing emission sell-pressure as the subsidy tapers.


## Financing AI Inference Hardware


While Venice tokenizes inference access and Pearl and Ambient tokenize inference production, a layer below them, a different onchain market is emerging to finance the GPUs that inference runs on. It is the cleanest case in this report of crypto doing what it is good at, and it works precisely because it does not mint a token or attempt to bootstrap demand for one. It raises ordinary capital against the hardware, channeling stablecoin deposits into loans for the operators buying GPUs and repaying depositors out of rental cashflow.


The largest operators already raise against their fleets through bank facilities, asset-backed securitizations, and private credit. CoreWeave's multibillion-dollar GPU-backed debt is[the canonical example](https://investors.coreweave.com/news/news-details/2026/CoreWeave-Closes-3-1-Billion-Loan-Facility-Expanding-Access-to-Public-Markets-for-GPU-Backed-Financing/default.aspx) . Smaller neoclouds have a harder time. They own the hardware and hold the contracted cashflows to support a loan, but lack the balance sheet, treasury function, and lender relationships to get one quickly. USD.AI lends to them. Depositors fund the loans, rental income repays them, and the interest returns to depositors as yield. Three things here are hard for a bank to match. The lender side is open to anyone holding stablecoins rather than a closed set of credit funds. Each loan becomes a composable onchain instrument that can be staked, traded, or pledged as collateral elsewhere. And the collateral claim is represented onchain while still relying on traditional legal enforcement underneath.


USD.AI runs on two tokens. Depositors mint USDai, a synthetic dollar[backed by PayPal's PYUSD](https://docs.usd.ai/usdai/how-it-works) (which in turn is backed by U.S. Treasury bills and cash). USDai pays no yield and is built to stay liquid and composable. To earn, a depositor stakes it into sUSDai, whose value accrues as the position earns rewards. That yield comes from two places: interest paid by GPU borrowers on active loans, and T-bill yield on reserves sitting idle between deployments. Staking yield has run[around 8%](https://coingape.com/usdai-crosses-20m-in-yield-paid-as-gpu-backed-loans-grow/) with the loan book at roughly half of reserves, and the protocol targets 10% to 15% yields as more capital gets deployed.


The hard part of lending against physical GPUs is enforcing the claim when the borrower defaults. USD.AI used to document each financed GPU as an[ERC-721](https://ethereum.org/developers/docs/standards/tokens/erc-721/)[NFT](https://ethereum.org/nft/) , which it described as a legal document of title under Uniform Commercial Code[Article 7](https://www.law.cornell.edu/ucc/7) , with the borrower keeping the machine under a[bailment](https://www.law.cornell.edu/wex/bailment) arrangement while the NFT stood as collateral. It called that framework CALIBER. The protocol has since retired it, finding it created too much commercial friction. Today the NFT represents a record of the loan. It carries the terms of service and routes repayments onchain, and it does not by itself move the legal claim to the collateral. Enforcement runs through conventional offchain loan documentation, and physical recovery still depends on the operational stack any hardware lender relies on: site inspection, proof of installation, collateral monitoring, lien filings, and data center or custodian cooperation. Neither that enforcement path nor the protocol's broader model has been tested through a full distressed recovery.


A liquid token backed by loans that amortize over three years is an asset-liability mismatch. Most RWA credit protocols paper over it by promising instant redemption, then break under stress, as the[USD0++](https://pharos.watch/learn/case-studies/usd0pp-usual-2025/?utm_source=chatgpt.com) depeg showed. USD.AI does not promise instant exit. Redemptions clear on a 30-day epoch against whatever principal has amortized in, first-in-first-out, and the protocol will not liquidate a performing loan to fund a withdrawal. A priced queue borrowed from Flashbots'[MEV-Boost](https://www.alchemy.com/overviews/mev-boost) design sits on top, letting redeemers who want to jump the line bid for priority, with those fees routed to the holders who wait. The loan terms are[CMBS-like](https://www.philadelphiafed.org/-/media/frbp/assets/working-papers/2023/wp23-27.pdf) : 70% to 80% loan-to-value, a borrower reserve covering roughly three months of debt service, liquidation after two missed payments, and hardware that is insured, monitored, and repossessable through dedicated partners.


USD.AI belongs in this report because it connects the credit layer to the pricing layer. A lender financing GPUs has to mark its collateral against something: how fast the hardware depreciates, what it would fetch in a forced sale, what advance rate is safe, and how to hedge the residual. Compute indices and the futures now forming give lenders that reference, and the lenders in turn supply the real credit exposure that gives those prices a use beyond speculation. What a GPU lender needs to know is less the spot rental rate on a given day than what the machine would resell for if a loan goes bad, and a liquid index and futures curve are what can eventually pin that down.


USD.AI says roughly 95% of its loan book is secured by long-term offtake contracts rather than spot rentals, so a borrower's ability to service debt turns less on the daily rental rate than on the counterparty that pre-committed to the capacity. Two things now sit between that risk and the depositor. The protocol derisks each loan quickly. A 70% to 80% loan-to-value ratio plus a three-month debt-service reserve funded upfront brings effective LTV into the 60s at origination, and USD.AI says roughly a quarter to a third of a loan is paid down over the first year, so it recovers a large share of its exposure before hardware value has fallen far. Fast depreciation, usually the thing to fear here, works in the lender's favor as long as amortization outruns it. Second, every new loan now carries value-loss coverage from[Barkr](https://barkr.ai/) , whose AI-driven collateral valuations are warrantied and reinsured by Munich Re, an[A+/AA-rated](https://www.munichre.com/en/company/investors/ratings-and-solvency.html) reinsurer. If a loan defaults and the collateral sells below Barkr's assessed value, the shortfall is paid to the protocol, which USD.AI presents as full coverage of the outstanding debt given the 80% LTV cap.


Insurance changes the risk without erasing it. It hands residual-value risk to a strong counterparty, but it also concentrates a new dependency on Barkr's valuation model and on the reinsurance staying in force, and neither the coverage nor USD.AI's offchain enforcement has run through a real wave of defaults. A loan still amortizes over three years against a claimed seven-year useful life, and a faster hardware cycle would narrow that gap. The difference from a few months ago is that a bad liquidation now lands on an insurer before it lands on a depositor.


## Conclusion


For now, inference capital markets, both onchain and off, are tiny relative to the growth of the AI industry. For onchain offerings to scale, they have to prove that the advantages they introduce are sustainable and durable.


Those advantages are clear. Tokenized access (Venice) turns a claim on inference into a bearer asset a holder can keep, resell, lease, or hand to an agent, rather than a subscription tied to one account a provider can revoke. Useful proof of work (Pearl and Ambient) uses token emissions to subsidize inference below market cost and makes the output verifiable so a buyer can pay without trusting the provider not to swap in a cheaper model. Financing (USD.AI) turns illiquid GPU credit into a composable instrument anyone holding stablecoins can fund and exit, faster than the incumbent credit industry moves. Underneath all three, the stack is permissionless and programmatic, the form most naturally suited to the class of agents likely to drive most of the demand for onchain capital market inference. Crypto is being used where ownership, neutrality, composability, and capital access matter.


The headwinds to adoption are not minor. No one has connected real demand for the compute to real demand for the crypto token. Production networks mint a token and sell it, funding below-market inference with emissions that get sold as fast as they are earned. Tokenized access trades more on speculation about the issuer than on use, with DIEM held largely by speculators and priced as a bet on Venice rather than as inference. Financing is the exception, the one form with real customers, neoclouds that need capital and have the cashflows to repay it, so its yield comes from serviced demand rather than a token minted to bootstrap interest. So far, the financial layer has been better at attracting speculative capital than at producing self-sustaining, usage-driven demand.


The onchain inference capital market's real edge in the ongoing AI build-out is not competing with incumbents at what they do best, serving inference cheaply at scale. It is in forming the capital and reaching markets traditional finance is too slow, too small, or not equipped to serve. This is the pattern crypto keeps rediscovering. It rarely wins the product, the exchange, the model, the application, but it is repeatedly the fastest way to build the financial layer around one, whether that be pricing an asset, fractionalizing it, financing it, or settling it.


Inference is the newest and largest instance. A multi-trillion-dollar asset class is being assembled in real time, and the market structure for compute as a financial asset – indices, futures, credit, tokenized capacity – barely exists yet. That absence is the opportunity. The financing layer works today because it is the first piece of that structure to find real demand, and the rest of the stack is a bet that the same edge will extend upward as compute itself financializes.


The inference market may take years to mature, but the financial layer being built around it is forming now.


*UPDATE (July 15): The section on USD.AI was updated to reflect changes in how the protocol enforces claims on defaulted loans.*


Legal Disclosure


This document, and the information contained herein, has been provided to you by Galaxy Digital Holdings LP and its affiliates (“Galaxy Digital”) solely for informational purposes. This document may not be reproduced or redistributed in whole or in part, in any format, without the express written approval of Galaxy Digital. Neither the information, nor any opinion contained in this document, constitutes an offer to buy or sell, or a solicitation of an offer to buy or sell, any advisory services, securities, futures, options or other financial instruments or to participate in any advisory services or trading strategy. Nothing contained in this document constitutes investment, legal or tax advice or is an endorsement of any of the assets mentioned herein. You should make your own investigations and evaluations of the information herein. Any decisions based on information contained in this document are the sole responsibility of the reader. Readers should consult with their own advisors and rely on their independent judgement when making financial or investment decisions.


Participants, along with Galaxy Digital, may hold financial interests in Diem (DIEM) and Venice (VVV). Galaxy Digital regularly engages in buying and selling DIEM and VVV, including through hedging transactions, for its own proprietary accounts and on behalf of its counterparties. Galaxy Digital also provides services to vehicles that invest in DIEM and VVV. If the value of such assets increases, those vehicles may benefit, and Galaxy Digital’s service fees may increase accordingly. The information and analysis in this communication are based on technical, fundamental, and market considerations and do not represent a formal valuation. For more information, please refer to Galaxy’s public filings and statements. Certain asset classes discussed, including digital assets, may be volatile and involve risk, and actual market outcomes may differ materially from perspectives expressed here.


For additional risks related to digital assets, please refer to the risk factors contained in filings Galaxy Digital Inc. makes with the Securities and Exchange Commission (the “SEC”) from time to time, including its Quarterly Report on Form 10-Q, available at www.sec.gov.


Certain statements in this document reflect Galaxy Digital’s views, estimates, opinions or predictions (which may be based on proprietary models and assumptions, including, in particular, Galaxy Digital’s views on the current and future market for certain digital assets), and there is no guarantee that these views, estimates, opinions or predictions are currently accurate or that they will be ultimately realized. To the extent these assumptions or models are not correct or circumstances change, the actual performance may vary substantially from, and be less than, the estimates included herein. None of Galaxy Digital nor any of its affiliates, shareholders, partners, members, directors, officers, management, employees or representatives makes any representation or warranty, express or implied, as to the accuracy or completeness of any of the information or any other information (whether communicated in written or oral form) transmitted or made available to you. Each of the aforementioned parties expressly disclaims any and all liability relating to or resulting from the use of this information. Certain information contained herein (including financial information) has been obtained from published and non-published sources. Such information has not been independently verified by Galaxy Digital and, Galaxy Digital, does not assume responsibility for the accuracy of such information. Certain information contained herein constitutes forward-looking statements, which can be identified by the use of terms such as “may”, “will”, “should”, “expect”, “anticipate”, “project”, “estimate”, “intend”, “continue” or “believe” (or the negatives thereof) or other variations thereof. Due to various risks and uncertainties, including those discussed above, actual events or results may differ materially from those reflected or contemplated in such forward-looking statements. As a result, you should not rely on such forward-looking statements in making any investment decisions. Affiliates of Galaxy Digital may have owned, hedged and sold or may own, hedge and sell investments in some of the digital assets, protocols, equities, or other financial instruments discussed in this document. Affiliates of Galaxy Digital may also lend to some of the protocols discussed in this document, the underlying collateral of which could be the native token subject to liquidation in the event of a margin call or closeout. The economic result of closing out the protocol loan could directly conflict with other Galaxy affiliates that hold investments in, and support, such token. Except where otherwise indicated, the information in this document is based on matters as they exist as of the date of preparation and not as of any future date, and will not be updated or otherwise revised to reflect information that subsequently becomes available, or circumstances existing or changes occurring after the date hereof. This document provides links to other Websites that we think might be of interest to you. Please note that when you click on one of these links, you may be moving to a provider’s website that is not associated with Galaxy Digital. These linked sites and their providers are not controlled by us, and we are not responsible for the contents or the proper operation of any linked site. The inclusion of any link does not imply our endorsement or our adoption of the statements therein. We encourage you to read the terms of use and privacy statements of these linked sites as their policies may differ from ours. The foregoing does not constitute a “research report” as defined by FINRA Rule 2241 or a “debt research report” as defined by FINRA Rule 2242 and was not prepared by Galaxy Digital Partners LLC. Similarly, the foregoing does not constitute a “research report” as defined by CFTC Regulation 23.605(a)(9) and was not prepared by Galaxy Derivatives LLC.


For all inquiries, please email[\[email protected\]](https://www.galaxy.com/cdn-cgi/l/email-protection) .


©Galaxy Holdings LP. 2026. All rights reserved.
