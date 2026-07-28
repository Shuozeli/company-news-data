---
schema_version: "1.0.0"
document_id: "86deb28649430043138fe747091b41d91f14cd4069581967ea89d971efc1a08a"
company_key: "yc-zepto"
company: "Zepto"
source_id: "yc-zepto-rss-8182f1493a2f"
canonical_url: "https://blog.zepto.com/building-a-lightning-fast-search-relevance-ranker-9319943a3880"
published_at: "2026-05-21T07:39:12+00:00"
first_seen_at: "2026-07-20T23:24:50.197566+00:00"
fetched_at: "2026-07-28T20:50:36.289404+00:00"
content_hash: "sha256:070430e0ce6a3d64705b5cef29fde196ad770e30e89eebd35c5ff31a645c6ce3"
---

# Building a Lightning-Fast Search Relevance Ranker

# Building a Lightning-Fast Search Relevance Ranker


[Zepto Tech](https://medium.com/@tech.culture?source=post_page---byline--9319943a3880---------------------------------------)


8 min read


·


May 21, 2026


--


Press enter or click to view image in full size


## Teaching a Tiny Model to Think Like a Giant


When someone types *“low fat milk”* into Zepto, a race begins.


Within milliseconds, our retrieval system pulls back around a hundred products that *might* match the query. Some are exactly right: “skimmed milk”, “2% fat milk”. Some are loosely related: “organic milk”, “toned milk”. And a few are simply enthusiastic guesses: “low-fat yogurt”, “protein shakes”.


At this point, we already know something important:


Search is not about finding products.
Search is about ordering them.


Because on a mobile screen, ordering is destiny.


If the right milk is at position #1, the user taps and checks out.
If it’s at position #14, they may never see it.


And if the first result is wrong twice in a row, they might not come back.


This is where the relevance ranker lives; in that thin, invisible layer between “results found” and “results trusted.”


## The Ten-Second Rule


Imagine you walk into a grocery store and ask an employee for low-fat milk.


They first hand you yogurt.
Then point to protein shakes.
Then finally, after some rummaging, show you the right carton.


You’re not impressed. You’re impatient.


Digital search is harsher. Even when results load instantly, users decide within a few seconds whether the page feels useful.


In quick commerce, the “top fold” is everything. The first two or three results carry disproportionate weight. If those are correct, search feels magical. If they aren’t, the entire experience feels broken.


So the challenge wasn’t just to build a relevance model.


It was to build one that was:


- Extremely accurate
- Extremely fast
- Efficiently scalable
- And robust enough to handle millions of distinct queries


All at once.


## Where the Relevance Ranker Sits in the Search Stack


Modern search systems are pipelines, not single models.


**Stage 1 is recall.** We use lexical search, embeddings, rules, and hybrid methods to fetch a few hundred potentially relevant products. This stage optimizes for coverage and speed. We covered one major part of this layer in[How We Built High-Precision, Low-Latency Semantic Search in Production ,](https://blog.zeptonow.com/how-we-built-high-precision-low-latency-semantic-search-in-production-75a6c61dee25) where we wrote about using semantic retrieval to move beyond exact keyword matching.


**Stage 2 is relevance scoring** . This is where we take the shortlisted candidates and score them precisely based on semantic alignment with the query.


Stage 3 is final ranking. Here we blend in behavioral signals like clicks, ATCs, price, availability, personalization, diversity.


This blog focuses entirely on Stage 2.


This is the stage where mistakes are most visible. If the relevance model fails, downstream ranking cannot fix a fundamentally wrong ordering. Getting the top position right is disproportionately valuable compared to small improvements deeper in the list.


So the challenge was clear. Build a ranker that is extremely accurate, extremely fast, and production ready at Zepto scale.


## Bi-Encoders vs Cross-Encoders, Choosing the Right Tool


Before building anything, we needed to choose the architecture.


In semantic search, two families dominate, bi-encoders and cross-encoders.


A bi-encoder processes the query and the document independently. It encodes the query into a vector, encodes the document into another vector, and computes cosine similarity. This allows us to precompute document embeddings and scale to millions of products.


Bi-encoders are excellent for retrieval. They are fast and scalable. But they miss fine-grained interactions between query tokens and document tokens because those tokens never interact inside the model.


A cross-encoder works differently. It concatenates the query and document into a single input sequence:


> \[CLS\] Query \[SEP\] Document


The transformer processes both simultaneously. Self-attention computes relationships between every token in the query and every token in the document. Concretely, each token generates Query, Key, and Value vectors. The attention score between two tokens is the dot product of their Query and Key representations, normalized via Softmax. This produces an attention map that determines how much context from each document token influences each query token.


This mechanism allows the model to capture subtle semantic dependencies. “Low fat milk” can downweight “chocolate milk” despite lexical overlap. “Diet protein shake” can be recognized as related but not equivalent.


The tradeoff is computational cost. We cannot precompute document vectors. Each query-document pair must be processed jointly.


The strategy we adopted was deliberate. Use bi-encoders for recall. Use cross-encoders for reranking. Let recall maximize coverage. Let cross-encoders maximize precision.


## The Labeling Problem at Scale


Architecture is only half the problem. Labels are the other half.


Relevance labeling is inherently subjective. Even with detailed guidelines, annotators disagree. Domain expertise introduces bias. Personal interpretation introduces noise. The “ground truth” shifts depending on who is labeling.


At Zepto scale, manual annotation is not just expensive. It is inconsistent.


So we took a different route.


We used a powerful self-hosted LLM as a teacher model.


For each query-product pair, the teacher outputs a relevance score between 0 and 1. Not binary. Continuous. Fine-grained.


> For example:
>
>
> Query: low fat milk
> Document: Amul Skimmed Milk 1L
> Teacher score: 0.94
>
>
> Query: low fat milk
> Document: Chocolate Milk 1L
> Teacher score: 0.41


This scalar score represents the degree to which the product satisfies the intent behind the query.


Each search query was paired with roughly 100 retrieved products. Across millions of search queries, this resulted in approximately 40 million query-product pairs.


This is dense supervision. Far richer than clicks alone. Far more scalable than human labels.


## Teacher–Student Distillation


The teacher model is powerful but expensive. Running it online for every search would be infeasible.


So we trained student models to mimic the teacher.


This process is known as knowledge distillation. The student does not just learn binary relevance. It learns to approximate the teacher’s score distribution. The final layer of the student cross-encoder applies a sigmoid activation to produce a score between 0 and 1, aligned with the teacher’s output.


## Get Zepto Tech’s stories in your inbox


Join Medium for free to get updates from this writer.


Remember me for faster sign in


The goal was not to replicate the teacher perfectly. It was to preserve ranking quality while dramatically reducing latency and cost.


## Hard Negatives, Learning the Subtle Distinctions


Not all irrelevant examples are equally useful.


A toaster for a milk query teaches the model nothing. It is trivially irrelevant.


But “chocolate milk” for “low fat milk” is interesting. It is semantically close. It is lexically overlapping. It is incorrect.


These are hard negatives.


We generated them in two ways.


First, teacher score thresholding. We extracted query-product pairs whose teacher scores were just below the relevance cutoff. These borderline examples are precisely the ones that can confuse a model.


Second, semantic similarity filtering. We used a lightweight embedding model to identify products with high cosine similarity to the query but low teacher relevance scores. These are semantic decoys. They look similar at the surface level but are not aligned with intent.


By including roughly 20 hard negatives per search term, we forced the student model to learn fine-grained distinctions instead of relying on obvious mismatches.


In practice, this significantly reduced false positives in production.


## Model Architecture Experiments


We evaluated four student architectures, each representing a different point on the accuracy-speed curve.


ModernBERT-base, 100M parameters, roughly 600MB.
RexBERT-base, 100M parameters, domain-tuned for e-commerce.
MiniLM-L6-v2, around 22M parameters, roughly 90MB.
TinyBERT-L2-v2, 4M parameters, roughly 17MB.


All models were implemented using the SentenceTransformers CrossEncoder class. Tokenization, attention masks, and output formatting were handled consistently across experiments. The final output was a sigmoid score between 0 and 1.


Training was conducted on a single GPU. We used AdamW to decouple weight decay from gradient updates. The learning rate followed a cosine decay schedule with warmup. Specifically, 20 percent of the training steps were allocated to warmup, gradually ramping up to a maximum learning rate of 2e-5. After reaching the peak, the learning rate decayed following a cosine curve down to 1e-6. We used two hard restart cycles, allowing the optimizer to explore the loss landscape more effectively than monotonic decay.


## Loss Functions, Theory vs Practice


We experimented with three loss formulations.


Pointwise Binary Cross-Entropy treats each query-product pair independently. The model predicts a score, and BCE pulls the prediction toward the target label. This optimizes calibration. A score of 0.8 should correspond to roughly 80 percent relevance likelihood.


Pairwise loss focuses on relative ordering. If document A is more relevant than document B for a given query, the model is penalized when score(A) is less than or equal to score(B). We used MarginMSE for this formulation.


Listwise loss considers the entire candidate set for a query. We used ListNetLoss, which minimizes the cross-entropy between predicted ranking distribution and ground truth ranking distribution.


Theoretically, pairwise and listwise losses are more aligned with ranking objectives.


In practice, pointwise Binary Cross-Entropy performed best.


Why?


Because with 40 million labeled examples, pointwise training leveraged data scale more effectively. Each pair contributed independently to gradient updates. The simplicity of the objective allowed the model to converge more stably at scale.


This is a recurring lesson in production ML. Elegant theory does not always win. Data scale often does.


Press enter or click to view image in full size


Model architecture at a glance


## Evaluation, Correlation vs Ranking Quality


We evaluated models using Pearson and Spearman correlation against teacher scores.


ModernBERT achieved the highest correlations. TinyBERT had noticeably lower correlation values.


But correlation measures distribution similarity, not ranking correctness.


What matters in production is whether the top-ranked products are correct.


In offline simulations, TinyBERT matched the ranking quality of larger models in the positions that mattered most.


It delivered:


5x faster inference.
25x fewer parameters.
Comparable top-k ranking behavior.


When scoring hundreds of thousands of queries across hundreds of thousands of products, that speed difference is not cosmetic. It is infrastructure cost. It’s a latency budget. It’s user experience.


TinyBERT was not the best at mimicking the teacher’s exact score distribution.


It was the best at solving business problems.


Press enter or click to view image in full size


## Our Learnings


- Cross-encoders provide unmatched precision for reranking.
- Knowledge distillation allows us to compress large models effectively.
- Hard negatives teach nuance.
- Pointwise training scales surprisingly well.
- Correlation metrics must be validated against real ranking behavior.
- Smaller models can outperform larger ones when evaluated on the right objective.


Today, when someone searches for “low fat milk” on Zepto, they see the right product first. They do not scroll. They do not second-guess. They tap.


Behind that tap lies:


- 40 million labeled pairs
- Teacher-student distillation
- Hard negative mining
- Careful optimizer scheduling
- A 4M parameter model making decisions in under 100 milliseconds


Invisible systems often have the most leverage.


## What’s Loading Next


The relevance scores from this system did not remain isolated.


They became foundational signals for a broader ranking layer that went beyond pure semantic relevance. By combining semantic relevance with user, query, product, and cohort-level features, we were able to personalize search results for different users and shopping contexts.


That evolution is covered in detail in[Personalized Search Ranking: The Zepto Way .](https://blog.zeptonow.com/personalized-search-ranking-the-zepto-way-496d0d405b71)


But personalization is not a universal answer.


In many search systems, performance is strongest where data is abundant. Popular queries have rich click histories, strong cohort signals, and dense personalization features. But tail queries are different. They are infrequent, sparse, and often lack reliable behavioral feedback. Even cohort-level personalization signals can be weak or noisy in these regions.


This next system is designed precisely for those gaps.


It is a unified ranker that leverages strong semantic relevance as its backbone, and optimizes across multiple objectives simultaneously, relevance, engagement, and business outcomes, especially in scenarios where historical interaction signals are limited.


In other words, when personalization is weak and behavior is sparse, semantic understanding becomes the anchor. That system deserves its own deep dive. Coming soon.
