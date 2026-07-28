---
schema_version: "1.0.0"
document_id: "5889b3264e5b08415effb7478324d7974b98bdc34da95cb8ea2ea1c82170fe7a"
company_key: "yc-andi"
company: "Andi"
source_id: "yc-andi-news-import-887dceecc721"
canonical_url: "https://andiai.com/blogs/announcement-yc-application-advisor-v2-wholeapplication-feedback-20260504-1129"
published_at: "2026-05-04T00:00:00+00:00"
first_seen_at: "2026-07-21T06:48:18.083780+00:00"
fetched_at: "2026-07-28T21:25:33.541420+00:00"
content_hash: "sha256:b6b9f2ea6dbc6d818d1c89e6c2500ebf79b6379229a61ed194304d321b6a3460"
---

# YC Application Advisor V2: Whole-Application Feedback for S26

In the past two weeks, 353 S26 applications have been through our little side project, the YC Application Advisor. Thirty-four founders scored high enough to earn an in-person review from a YC alum.


V2 is now live and available.


It features smarter advice and a much friendlier UX that better shows you progress and streams in suggestions progressively as they’re available.


## Why did Andi build this?


We try to pay it forward by helping as many founders as we can with reviews every cycle, but it’s hard to get to everyone in person, especially on deadline day!


We built this to help!


As AI side projects go, the new V2 of the Advisor is pretty cool, and I’ve learnt a lot about how to improve the UX of AI-driven systems that aren’t chat based by building it. I’ve been working on the new version over the last few weeks, and we shipped in time YC S26 Application deadline day.


It’s also a good showcase of our new AI Search API’s capabilities for grounding interactive AU applications, and a fun way to give back to the YC community.


The model sees all seven sections of a YC application at once. When it reviews your Progress answer, it already knows your Founders bio, your traction numbers, your idea description. The analysis goes through a drafting => review => rewrite => finalize pipeline. It can take 6-8 minutes or more. So figuring out how to make the UX feel responsive and engaging was a fun challenge.


YC applications tell a story across sections. A strong fact buried in your background notes belongs is often better in an answer where a partner will actually look for it. The advisor now catches that and moves it. It can even generate a draft set of answers just from rough notes.


We calibrated scoring to reflect the strength of the business case, not just how well the answer reads. Polished prose alone doesn’t earn a high score (although “easy-to-understand” is a key factor). And it’s even harder on fact-checking and pushing for specifics on metrics, names and quotes.


In the two weeks since V2 capabilities started rolling out, 353 S26 applications have been through the advisor. 34 founders scored high enough to earn an in-person review from a YC alum.


## What the alum-review unlock looks like


Founders who score above a threshold can request an in-person review from a YC alum. A real person reads your application and gives you direct feedback.


Thirty-four founders have scored high enough for that in the last 2 weeks. The invitation is based on the strength of the application, not the quality of the writing.


## Try it


The advisor is free, private and needs no account: paste your application or fill it out from scratch.


[yc-advisor.andiai.com](https://yc-advisor.andiai.com/)
