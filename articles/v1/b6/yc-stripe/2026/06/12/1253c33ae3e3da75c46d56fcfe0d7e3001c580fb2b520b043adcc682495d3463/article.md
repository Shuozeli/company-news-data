---
schema_version: "1.0.0"
document_id: "1253c33ae3e3da75c46d56fcfe0d7e3001c580fb2b520b043adcc682495d3463"
company_key: "yc-stripe"
company: "Stripe"
source_id: "yc-stripe-dev-blog-rss"
canonical_url: "https://stripe.dev/blog/microservice-testing-with-apache-spark-part-2"
published_at: "2026-06-08T00:00:00+00:00"
first_seen_at: "2026-07-19T22:29:11.601208+00:00"
fetched_at: "2026-07-28T04:01:00.398137+00:00"
content_hash: "sha256:b008d2c6944627896edc4cbcb3552f4aca710db59bea024793bc2229e0cd5328"
---

# Scaling up your microservice testing with Apache Spark—Part 2

Some microservices are difficult to test because their behavior depends on a long tail of inputs that are hard to model by hand. This post focuses on how to build a repeatable Apache Spark replay harness for testing without creating a second implementation of the service.
