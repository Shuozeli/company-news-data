---
company_key: "yc-stripe"
company: "Stripe"
source_id: "yc-stripe-dev-blog-rss"
url: "https://stripe.dev/blog/extending-stripes-network-with-stablecoins"
canonical_url: "https://stripe.dev/blog/extending-stripes-network-with-stablecoins"
published_at: "2026-06-22T00:00:00+00:00"
fetched_at: "2026-07-21T09:58:36.382580+00:00"
content_hash: "sha256:1762b244c0bb8e8d60804b475e53f0a548cff52118e6db51792937f5f0ede4b8"
---

# Extending Stripe’s network with stablecoins

Most of the world's money still moves in batches. A wire submitted at 2pm might settle by end of day, if you made the cutoff. ACH takes one to three business days. Cross-border payments touch correspondent banks, each adding lag and a fee. Stripe has spent over a decade building the Global Payments and Treasury Network (GPTN), a programmable infrastructure for global money movement that batches transfers to reduce cost, nets opposing flows to minimize actual cash moved, and routes through the optimal path between accounts. Under the hood, it's a graph with accounts as nodes, and payment rails as edges.
