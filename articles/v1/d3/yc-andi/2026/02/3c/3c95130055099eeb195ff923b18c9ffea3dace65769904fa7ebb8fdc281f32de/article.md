---
schema_version: "1.0.0"
document_id: "3c95130055099eeb195ff923b18c9ffea3dace65769904fa7ebb8fdc281f32de"
company_key: "yc-andi"
company: "Andi"
source_id: "yc-andi-news-import-887dceecc721"
canonical_url: "https://andiai.com/blogs/announcement-andi-search-we-shipped-february-2026-20260218-1243"
published_at: "2026-02-18T00:00:00+00:00"
first_seen_at: "2026-07-21T06:48:18.083780+00:00"
fetched_at: "2026-07-28T22:19:43.789522+00:00"
content_hash: "sha256:fd392f2cca99b2fad69a6d12be6a2fe8675b814423b9e8f3693218be21b2b426"
---

# Andi Search: What We Shipped in February 2026

Most search engines get slower as they add features. We went the other way.


Over the past two weeks, we’ve been heads down on the kind of work that doesn’t make for a splashy launch but matters to anyone who uses Andi daily. Faster searches, better answers, fewer things that shouldn’t be there.


## Speed


Average search times are now regularly under 500ms, roughly 2x faster than where we were. For most queries, Andi responds before you’ve finished reading what you typed.


Getting a search engine this fast with two people is more a focus problem than a resource problem. Large companies add layers of abstraction, tracking, and ad-serving between the query and the answer. We don’t have any of that, so we can optimize the path that actually matters.


## Understanding questions better


We rebuilt how Andi figures out what you’re asking. Intent detection is sharper, topic classification catches more edge cases, and query rewriting does a better job with complex or ambiguous searches. This means fewer “I didn’t mean that” moments, and more depth when you ask something hard.


## Instant math


Math answers are instant now. Ask Andi “what’s 15% of 847” and the answer appears in milliseconds. We replaced the previous approach with a built-in calculator that handles the common cases without any round-trip delay.


## Smarter safe search


Safe search filtering got better at telling the difference between queries that are genuinely looking for adult content and queries that happen to contain a word with multiple meanings. So you see less over-filtering, while retaining protection where it’s needed.


## A leaner app


We removed informational pages from the search app that were less relevant to the search app itself: this includes old content pages, archived help docs, and others things that accumulated over time. The app loads faster and does one thing now.


## New website


We moved a lot of resources to this new[AndiAI.com](https://andiai.com/) website, including the waitlist for early access to our developer API, information about our open source projects, and a community page. The search app at andisearch.com stays focused on search. The marketing and developer story lives on its own domain. If you build with AI,[join the API waitlist](https://andiai.com/api) .


## Two people


All of this shipped in the same two-week stretch, built by two founders. We don’t have a growth team, a platform team, or a lot of resources. We have a codebase, a clear idea of what needs to be better, and the ability to ship without asking permission.


PCMag named Andi the top free AI search engine in January. We scored 87% accuracy on independent benchmarks where Google scored 71% and Perplexity scored 59%. None of that happened because we had more resources than those companies. It happened because we’re laser focused on building better search.


Try it at[andisearch.com](https://andisearch.com/) .
