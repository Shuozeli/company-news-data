---
schema_version: "1.0.0"
document_id: "0f7eadea5b0b35a009436b5cebb100d9fbb01e7e62df4e38acb3d212867d3c3c"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/upgrade-to-kubernetes-127-take-advantage-of-performance-improvements"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:535d8f8ca80c44d55bb1c5febc7e2e768e5327169323d234962ff983ed464333"
---

# Upgrade to K8s 1.27+ to Take Advantage of Argo Workflows Performance Improvements

# Upgrade to Kubernetes 1.27 or later to take advantage of key performance improvements


When using Argo Workflows at scale, you may encounter issues with performance. A large number of workflows and workflow tasks can cause the Kubernetes API requests to be rate limited. Whilst there are[a number of configuration changes](https://argoproj.github.io/argo-workflows/running-at-massive-scale/) you can make to Argo Workflows to improve performance, you are still ultimately at the mercy of the Kubernetes API server.


In this post, I’ll briefly highlight some of the key performance improvements in[Kubernetes 1.27](https://kubernetes.io/releases/download/) that allowed us to run Argo Workflows at scale, as well as walk you through the outcomes of the performance tests we ran.


{% cta-1 %}


# Testing Argo Workflows at Scale


We ran a test to evaluate the performance of Argo Workflows on Kubernetes 1.27. We created a simple workflow that created 50 pods in parallel, each of which slept for a random amount of time between 120 and 150 seconds. We then invoked this workflow 150 times in parallel.


```text


```


```text


```


This will result in 7,500 pods being requested as quickly as possible. We strongly recommend that you do not run these scripts in a cluster used for any production workloads.


Our testing was admittedly unscientific but is indicative of what you should expect in your own cluster.


We ran the bash script against an EKS 1.26 cluster using Argo Workflows v3.4.8.


Argo Workflows had no performance tuning whatsoever. We used the Cluster Autoscaler to provision additional nodes as they were required.


When we ran this test on an EKS 1.26 cluster, we observed that after approximately 2,500 pods were scheduled, the Kubernetes API became unresponsive to basic queries. The Workflow Controller logs indicated that it was unable to query the Kubernetes API, and the Kubernetes API server logs indicated that it was rate limiting requests. Ultimately, we temporarily lost administrative access to the cluster while the workflows eventually ran and cleaned themselves up.


When we repeated the test on an EKS 1.27 cluster, all 7,500 pods were scheduled without any issues. The Kubernetes API server logs indicated that it was not rate limiting requests and we could continue performing other administrative tasks on the cluster.


# Conclusion


The performance improvements introduced in Kubernetes 1.27 can help you run Argo Workflows at scale without impacting the performance of your cluster. If you are using Argo Workflows to run complex workflows, we recommend[upgrading to Kubernetes 1.27](https://kubernetes.io/releases/download/) or later.
