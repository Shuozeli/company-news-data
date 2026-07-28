---
schema_version: "1.0.0"
document_id: "65db2c80ca8690b5bed002ccb920fff1bca9a427078e05f95788df9b2e541b93"
company_key: "yc-andi"
company: "Andi"
source_id: "yc-andi-news-import-887dceecc721"
canonical_url: "https://andiai.com/blogs/announcement-yc-application-advisor-writing-reads-like-20260324-1519"
published_at: "2026-03-24T00:00:00+00:00"
first_seen_at: "2026-07-21T06:48:18.083780+00:00"
fetched_at: "2026-07-28T21:26:23.229623+00:00"
content_hash: "sha256:12843a25e921d0eb55c5b1b21b6f9bb1ae419d6991ad29f31606beabe3d83b95"
---

# YC Application Advisor: Writing That Reads Like a Person

Feedback you ignore is feedback that doesn’t work.


The[YC Application Advisor](https://yc-advisor.andiai.com/) gives AI-powered feedback on Y Combinator application drafts: per-question scoring and suggestions, plus rewritten answers grounded in real YC partner guidance. It’s free, built by Andi AI (YC W22), and YC Summer 2026 applications are open now.


Most AI feedback tools have the same problem, though: if the writing sounds like AI wrote it, people stop reading. Vague claims and generically encouraging paragraphs. The advice might be correct, but the delivery makes it easy to dismiss. Version 0.3.3 ships two changes that fix this.


## Writing quality pipeline


We built andi-write, the same writing standards we use across Andi products, into the advisor’s system prompt. These rules define what good feedback looks like: specific and direct, grounded in what the founder actually wrote rather than reaching for generic encouragement.


A review-then-edit pipeline now runs after every review. The first pass checks feedback text for AI writing patterns: vague claims, generic praise, the kind of language that makes advice feel templated. The second pass rewrites anything it finds. Both steps run automatically; if either fails, the review still completes normally.


A typical AI review might read:


> Your response demonstrates a solid understanding of the market. Consider elaborating on your competitive advantages to strengthen this section.


After the advisor’s polish pipeline:


> You mention three competitors but don’t say why customers switch to you. What’s the specific reason your last five customers chose you over the alternative they were using?


The first version could apply to any application; the second names what’s missing and tells the founder what to fix.


## Styled email cards


We redesigned the emails for review requests and application sharing. Each question now gets its own styled card showing the score, specific suggestions, rewritten answer, and a star rating, all inline.


Previously, recipients had to click through to the app to see detailed feedback. Now the actionable information arrives in the email itself: what to change and how the advisor would rewrite it. Gradient headers and proper formatting for each card make the emails useful on their own.


## Pairs with gstack evaluation


These writing improvements build on the gstack-based evaluation upgrade from last week, which added harder questions and anti-sycophancy patterns to the review process. The advisor pushes founders to be specific about their market, users, and traction (gstack), then delivers that feedback in clear, direct writing (andi-write).


Harder questions produce more useful feedback, and better writing makes it worth reading.


## Try it


YC Summer 2026 applications close May 4. The YC Application Advisor is free at[yc-advisor.andiai.com](https://yc-advisor.andiai.com/) . Paste a draft or fill out the form from scratch, and you’ll get a full review back in about 60–90 seconds.
