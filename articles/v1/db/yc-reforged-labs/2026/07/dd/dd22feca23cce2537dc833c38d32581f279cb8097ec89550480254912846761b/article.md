---
schema_version: "1.0.0"
document_id: "dd22feca23cce2537dc833c38d32581f279cb8097ec89550480254912846761b"
company_key: "yc-reforged-labs"
company: "Reforged Labs"
source_id: "yc-reforged-labs-news-import-c817b6f59bac"
canonical_url: "https://reforgedlabs.com/blog/boa-benchmark-video-understanding-creative-strategy"
published_at: null
first_seen_at: "2026-07-22T11:15:42.017495+00:00"
fetched_at: "2026-07-28T21:20:12.930591+00:00"
content_hash: "sha256:4893fee1fd725ca18a853f29813993362e75b778e7f28ea0ed43cc22a628d347"
---

# Video Understanding for Creative Strategy: Boa vs. Leading Multimodal Models

Benchmark Report


Evaluating how well AI systems understand video game advertisements — from hook identification to creative strategy extraction — across 65 human-graded criteria.


April 2026 · 13 evaluation tasks · 5 systems compared · 65 binary criteria


## Executive summary


We evaluated five AI systems on their ability to understand video game ad creatives — the kind of analysis that creative strategists perform daily when optimizing ad performance. The benchmark covers video description, multi-ad comparison, creative strategy extraction, cultural reference identification, and player motivation analysis.


To simulate what an in-house team would build, we gave the leading foundation models from Google, OpenAI, and Anthropic the best possible setup: AI-generated structured labels extracted from each video, paired with the same evaluation questions. This is the approach most teams attempt when they try to build video understanding themselves.


Boa achieved a **98.5% overall accuracy** , outperforming every competitor by a significant margin. The next-best result, Claude Opus 4.6 with AI-generated labels, scored 76.9% — a 22-point gap. Gemini 3.1 Pro and GPT-5.4 tied at 72.3%, and Gemini 3.1 Pro processing raw video directly scored just 46.2%.


## Overall scores


Boa


98.5%


64 / 65


Opus 4.6


76.9%


50 / 65


Gemini 3.1 Pro


72.3%


47 / 65


GPT-5.4


72.3%


47 / 65


Gemini 3.1 Multi.


46.2%


30 / 65


**Key finding:** Boa missed only 1 criterion out of 65 — referencing supporting scenes in emotional analysis. Every competing system missed at least 15 criteria, with the largest gaps appearing in video description accuracy and strategic understanding tasks.


## Performance by category


Criteria are grouped into five capability domains. Scores shown as percentage of criteria passed within each category.


Boa


Opus 4.6


Gemini 3.1 Pro


GPT-5.4


Gemini 3.1 Multimodal


### Video description accuracy (20 criteria)


Boa


100%


Opus 4.6


55%


Gemini 3.1 Pro


55%


GPT-5.4


55%


Gemini 3.1 Multi.


45%


### Multi-ad analysis (15 criteria)


Boa


93%


Opus 4.6


87%


Gemini 3.1 Pro


87%


GPT-5.4


87%


Gemini 3.1 Multi.


67%


### Comparative analysis (10 criteria)


Boa


100%


Opus 4.6


90%


Gemini 3.1 Pro


90%


GPT-5.4


80%


Gemini 3.1 Multi.


60%


### Strategic understanding (10 criteria)


Boa


100%


Opus 4.6


70%


Gemini 3.1 Pro


60%


GPT-5.4


60%


Gemini 3.1 Multi.


40%


### Cultural & motivational insight (10 criteria)


Boa


100%


Opus 4.6


100%


GPT-5.4


90%


Gemini 3.1 Pro


80%


Gemini 3.1 Multi.


10%


---


## Full results by evaluation task


Each task was scored on 5 binary criteria (pass/fail). Cells show the number of criteria passed out of 5, with the percentage equivalent.


Evaluation task Boa Gemini 3.1 Multi. Gemini 3.1 Pro GPT-5.4 Opus 4.6


Q1.1 – Describe video (ad 1) 5/5 100% 2/5 40% 3/5 60% 3/5 60% 3/5 60%


Q1.2 – Describe video (ad 2) 5/5 100% 1/5 20% 2/5 40% 2/5 40% 2/5 40%


Q1.3 – Describe video (ad 3) 5/5 100% 5/5 100% 5/5 100% 5/5 100% 5/5 100%


Q1.4 – Describe video (ad 4) 5/5 100% 1/5 20% 1/5 20% 1/5 20% 1/5 20%


Q2 – Best gameplay moment in hooks 5/5 100% 2/5 40% 4/5 80% 5/5 100% 5/5 100%


Q3 – Duration patterns in gameplay 5/5 100% 4/5 80% 5/5 100% 4/5 80% 4/5 80%


Q4 – Common emotions targeted 4/5 80% 4/5 80% 4/5 80% 4/5 80% 4/5 80%


Q5 – Compare key differences 5/5 100% 4/5 80% 5/5 100% 5/5 100% 5/5 100%


Q6 – Compare ad variances 5/5 100% 2/5 40% 4/5 80% 3/5 60% 4/5 80%


Q7 – Creative strategy 5/5 100% 2/5 40% 3/5 60% 3/5 60% 3/5 60%


Q8 – Shared concepts across videos 5/5 100% 2/5 40% 3/5 60% 3/5 60% 4/5 80%


Q9 – Pop culture references 5/5 100% 1/5 20% 4/5 80% 4/5 80% 5/5 100%


Q10 – Player motivation 5/5 100% 0/5 0% 4/5 80% 5/5 100% 5/5 100%


Total 64/65 98.5% 30/65 46.2% 47/65 72.3% 47/65 72.3% 50/65 76.9%


---


## Key insights


### Boa dominates video description tasks


The largest performance gap appeared in video description (Questions 1.1–1.4), where Boa scored 100% while all competitors averaged around 50–55%. This category tests whether a system can correctly identify hooks, gameplay mechanics, event sequences, creative elements, and specific moments within an ad. Competing systems consistently failed to capture the correct sequence of events and to reference specific moments — the two criteria most important for actionable creative analysis.


### Strategic understanding is Boa’s sharpest edge


In strategic understanding tasks (Questions 7–8), Boa scored a perfect 100% while the next-best competitor, Opus 4.6, reached only 70%. These tasks required systems to identify hook strategies, emotional angles, narrative structure, and shared concepts across multiple videos — precisely the skills a creative strategist needs. Competing systems frequently failed to ground their claims in actual scenes or to cover the full duration of an ad’s strategy.


### All competitors struggled with the same hard ad


Question 1.4 was the hardest single task: every system except Boa scored just 1/5 (20%). This ad contained visual complexity and unconventional structure that tripped up general-purpose models, which defaulted to describing only surface-level creative elements. Boa’s purpose-built video understanding correctly parsed the full ad.


### Raw multimodal is the weakest approach


The simplest build-it-yourself approach — feeding raw video directly into Gemini 3.1 Pro — scored the lowest at 46.2%. Its weakest areas were player motivation (0%), pop culture references (20%), and several video description tasks (20%). Even adding AI-generated labels as an intermediate step (the approach used by the other three competitors) only brought scores up to the 72–77% range. Neither approach comes close to Boa’s 98.5%.


### Competitors close the gap on simpler tasks


On tasks with clearer structure — such as comparing two videos (Q5), identifying emotion patterns (Q4), or analyzing gameplay duration (Q3) — the gap between Boa and competitors narrowed significantly, with several systems matching Boa’s performance. General-purpose models handle well-structured analytical tasks competently, but falter when tasks require deep, scene-level video understanding — exactly the tasks that drive real creative decisions.


---


## Methodology


### Systems evaluated


We tested the most common way teams try to build video understanding in-house: feeding video content into a leading foundation model and prompting it to analyze the creative. To give these models every advantage, we used **Gemini 3.1 Pro** to first generate structured labels from each video — extracting hooks, scenes, gameplay, emotions, and more — then fed those labels into each model as context alongside the evaluation question.


This produced four competitor configurations, plus Boa:


- **Gemini 3.1 Pro Multimodal** — raw video fed directly into Gemini, the best-case scenario for a pure multimodal approach
- **Gemini 3.1 Pro** — Gemini-generated labels fed back into Gemini as text
- **GPT-5.4** — Gemini-generated labels fed into OpenAI’s latest model
- **Claude Opus 4.6** — Gemini-generated labels fed into Anthropic’s latest model
- **Boa** — Reforged’s purpose-built video understanding system for ad creatives


All five systems received the same evaluation questions and were scored against identical criteria. The competitor setup mirrors what an internal team would realistically build: use the best available model to extract video information, then use the best available model to reason over it.


### Evaluation structure


The benchmark comprises 13 evaluation tasks spanning 10 distinct question types. Four of the tasks (Q1.1–1.4) test the same prompt across different video ads to measure consistency. Each task is scored against 5 binary criteria (pass = 1, fail = 0), producing 65 total criteria across all tasks.


### Evaluation criteria


Criteria were designed to capture the skills a creative strategist uses when analyzing video game ads:


- **Accuracy** — correctly identifying hooks, gameplay mechanics, event sequences, and creative elements
- **Completeness** — covering all ads, all major elements, and the full duration of each video
- **Evidence grounding** — referencing specific scenes, moments, or timestamps to support claims
- **Strategic depth** — identifying emotional strategies, narrative structures, player motivations, and cultural references
- **Comparative reasoning** — analyzing similarities and differences across multiple ad creatives


### Scoring process


Each criterion was evaluated as a binary pass/fail by a human evaluator using a standardized evaluator question (e.g., "Did the system correctly describe what happens in the first 1–3 seconds?"). Scores were recorded independently for each system, with no knowledge of other systems’ responses during evaluation.


### Open source


The evaluation framework, prompts, and scoring criteria used in this benchmark are open source. You can inspect the methodology, reproduce the results, or adapt the framework for your own evaluations at[github.com/Reforged-Labs/mg-vau](https://github.com/Reforged-Labs/mg-vau) .


---


## Conclusion


This benchmark demonstrates that Boa delivers near-perfect accuracy (98.5%) on video understanding tasks designed for creative strategy in video game advertising. The best DIY approach — using a leading foundation model with AI-generated video labels — tops out at 76.9%, leaving a 22-point accuracy gap that no amount of prompt engineering can close.


Boa’s advantage is most pronounced in the areas that matter most for production creative workflows: accurately describing what actually happens in an ad, identifying the strategic choices behind creative decisions, and grounding analysis in specific video evidence rather than surface-level generalizations.


**Bottom line:** Building video understanding in-house with general-purpose models means accepting 23–54% error rates on the tasks that drive creative decisions. Boa delivers 98.5% accuracy out of the box — purpose-built for the work your creative strategists do every day.
