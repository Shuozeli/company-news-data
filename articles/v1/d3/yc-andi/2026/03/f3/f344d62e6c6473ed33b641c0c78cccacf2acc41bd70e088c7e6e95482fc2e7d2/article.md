---
schema_version: "1.0.0"
document_id: "f344d62e6c6473ed33b641c0c78cccacf2acc41bd70e088c7e6e95482fc2e7d2"
company_key: "yc-andi"
company: "Andi"
source_id: "yc-andi-news-import-887dceecc721"
canonical_url: "https://andiai.com/blogs/essay-yc-application-advice-office-hours-actually-20260319-1131"
published_at: "2026-03-19T00:00:00+00:00"
first_seen_at: "2026-07-21T06:48:18.083780+00:00"
fetched_at: "2026-07-28T21:26:23.229623+00:00"
content_hash: "sha256:0292f11ab7ba51f5d6d42eb5f2f209303d84f9df0cb0ce6828d59c16d3194d98"
---

# YC Application Advice: What Office Hours Actually Test

Most advice about YC applications focuses on the writing: be concise, tell a compelling story, show your traction. That advice addresses the surface. The applications that get interviews answer harder questions.


I’ve been through the Y Combinator application process four times, and the thing that took me longest to understand is that partners aren’t reading for polish. They’re reading for evidence that you’ve done the work of understanding your users. The difference between a weak application and a strong one usually comes down to specificity.


## The questions behind the questions


YC’s application form asks straightforward things: What does your company do? Who are the founders? How far along are you? But behind those written prompts, partners are running a second evaluation. They’re pressure-testing your thinking the way they would in office hours.


The pattern became clearer to me recently when Garry Tan open-sourced gstack, a set of AI skills that encode how YC partners think. The /office-hours skill, specifically, lays out the questions partners actually push on when they’re sitting across from a founder:


Do you have real demand, or just interest? Can you name a specific person who needs this? What are people doing today without your product? What’s the narrowest version someone would pay for right now?


These questions share a trait: they punish abstraction and reward specificity.


## Specificity as a proxy for understanding


A founder who writes “small businesses need better invoicing” is making a category claim. A founder who writes “my friend Sarah runs a bakery and spent four hours last week reconciling Stripe payments with her spreadsheet” is describing something she observed. Both might be building the same product. The second founder has talked to a user.


This pattern, specificity as evidence of understanding, runs through every strong YC application I’ve read. The gap between a middling score and a strong one is rarely the idea itself. It’s whether the founder can point to a real person with a real problem and describe what that person is currently doing about it.


The “what are they doing today” question is particularly revealing. If the answer is “nothing,” the problem often isn’t painful enough for someone to pay you to solve it. If the answer is “they duct-taped together three different tools and a spreadsheet,” you’ve probably found a gap worth filling. The existence of a bad workaround is stronger evidence of demand than any amount of survey data, because someone cared enough to build one.


The “narrowest paid version” question forces a different kind of honesty. Most first-time founders describe products that are too broad: the full platform, the long-term vision. The question isn’t what your product could become in three years. It’s what’s the smallest thing you could charge for next month. That answer tells a partner whether you understand what actually matters to your users versus what you’ve imagined matters.


## When methodology gets open-sourced


Garry described gstack as “only a 10% strength version of what a real YC partner can do for you.” That framing is worth taking literally. No tool replaces a real conversation with someone who’s seen thousands of startups. But 10% of that thinking, applied systematically before you submit, catches the most common failure modes: vague demand claims, unnamed users, missing competitive context, overly broad product descriptions.


When you open-source a methodology, people can build on it. When the office hours approach is published as a skill that any tool can integrate, the thinking becomes infrastructure rather than a one-time conversation. You can see the source on[Garry’s gstack repo](https://github.com/garrytan/gstack) .


We did that with the[YC Application Advisor](https://yc-advisor.andiai.com/) . The tool already scored YC applications with per-question ratings, specific improvement suggestions, and rewritten answers. With v0.3.1, we wired the office hours methodology into the review chain. The advisor now pushes on the same things partners push on — demand validation, user specificity, competitive positioning. It asks the questions that separate applications that get interviews from those that don’t.


## Before you write a single answer


The office hours questions work as a startup evaluation tool whether or not you’re applying to YC. Before you fill out the form, try answering these:


- Who specifically has this problem? Name them.
- What are they doing about it today?
- Have they told you they want a solution, or have they paid for one?
- What’s the smallest version of this product someone would pay for?


If you struggle with any of these, the application isn’t the problem. Your understanding of the market is. Go talk to more users. The application will write itself when you come back with real answers.


Y Combinator Summer 2026 applications are open, with a deadline of May 4. The[YC Application Advisor](https://yc-advisor.andiai.com/) is free — built by Andi AI (YC W22), with the office hours methodology applied to every review.
