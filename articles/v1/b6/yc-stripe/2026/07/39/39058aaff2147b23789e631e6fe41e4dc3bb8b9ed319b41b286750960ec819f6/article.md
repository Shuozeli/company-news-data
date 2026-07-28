---
schema_version: "1.0.0"
document_id: "39058aaff2147b23789e631e6fe41e4dc3bb8b9ed319b41b286750960ec819f6"
company_key: "yc-stripe"
company: "Stripe"
source_id: "yc-stripe-dev-blog-rss"
canonical_url: "https://stripe.dev/blog/how-stripe-uses-graph-search-and-state-machines-to-auto-remediate-a-global-database-fleet"
published_at: "2026-07-16T00:00:00+00:00"
first_seen_at: "2026-07-19T22:29:11.601208+00:00"
fetched_at: "2026-07-28T04:01:00.398137+00:00"
content_hash: "sha256:69809d9d572e75f3ca1d23d360a536ba5eb02c10ff7923912e815e45fd181b60"
---

# How Stripe uses graph search and state machines to auto-remediate a global database fleet

Discover how we modeled our MongoDB infrastructure as a traversable graph and then use pathfinding algorithms to dynamically compute and execute recovery plans. This automated approach reduced pager volume by 30% (~200 pages/year), eliminated 12 days of unhealthy shard states annually, and supports new shard layouts with zero manual effort.
