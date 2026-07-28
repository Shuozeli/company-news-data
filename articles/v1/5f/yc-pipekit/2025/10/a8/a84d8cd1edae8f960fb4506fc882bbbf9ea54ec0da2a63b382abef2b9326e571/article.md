---
schema_version: "1.0.0"
document_id: "a84d8cd1edae8f960fb4506fc882bbbf9ea54ec0da2a63b382abef2b9326e571"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/the-importance-of-setting-resource-requests-on-all-argo-workflows-containers"
published_at: "2025-10-14T20:55:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:55:41.466450+00:00"
content_hash: "sha256:fb62bae1150a33b3f4e916ce30923f0f6335badac8d648029843a98fec773237"
---

# The Importance of Setting Resource Requests on All Argo Workflows Containers

When developing and operating Argo Workflows at scale, it is important to remember to configure resource requests for all containers within workflow pods. This guide explains why setting resource requests on the init, wait, and main containers is crucial for reliable workflow execution and provides practical guidance for implementation.


Each workflow step runs as a Kubernetes pod containing multiple containers that work together to execute your workload. Without proper resource requests, Kubernetes will not understand how to efficiently bin-pack your pod into a node or any of these containers can fail, causing entire workflows to become unreliable or randomly fail completely.


## **Understanding Argo Workflows Container Architecture**


Argo Workflows implements a multi-container pod architecture where each container serves a specific purpose in workflow execution. The init container runs first to fetch artifacts and parameters, making them available to the main container. Once dependencies are satisfied, the main container executes the desired actions for the workflow step. The wait sidecar container monitors the main container and communicates with the Argo Workflow controller about step or task progress.


This architecture means that resource starvation in any container can cascade into workflow failure. If the init container lacks sufficient memory to download large artifacts, the entire workflow step can fail before the main workload even begins. Similarly, if the wait container experiences node memory pressure, the pod will be evicted.


## **How Kubernetes uses Resource Requests**


Without resource requests, Kubernetes treats pods as having no minimum resource requirements, leading to unpredictable scheduling behaviour. The scheduler may place pods on heavily loaded nodes, causing performance degradation and potential failures. This becomes particularly problematic in multi-tenant clusters where resource contention is common.


The knock-on effect of not setting resource requests will be a lack of repeatability in your workflows. You may find that a given workflow runs flawlessly one day, and then runs slowly or keeps crashing/failing the next day.


## **Pod Scheduling and Resource Allocation**


Kubernetes scheduling behaviour fundamentally changes when resource requests are present versus absent. With properly configured requests, the scheduler ensures that nodes have sufficient resources before placing pods, preventing resource starvation scenarios. The scheduler calculates the total requests for all containers in a pod and only places the pod on nodes that can satisfy those requirements.


When resource requests are missing, pods may be scheduled successfully but later fail due to resource contention. This creates a false sense of reliability where workflows appear to start correctly but fail unpredictably during execution. In high-throughput scenarios, this can manifest as intermittent failures that are difficult to diagnose and reproduce.


## **Impact on Different Container Types**


### **Init and Wait Containers**


The init and wait containers, controlled by executor resource configuration, have specific resource patterns that differ from main containers. Init containers typically require burst memory allocation for artifact downloads, while wait containers need a small amount of CPU and memory until the end of the step when it needs enough to compress and upload the artifacts (if there is one).


### **Main Containers**


Main containers execute the primary workflow logic and typically have the most variable resource requirements. Container templates, script templates, and containerSet templates all benefit from explicit resource requests that match their workload characteristics.


## **Practical Configuration Strategies**


Resource requests can be managed at the global, workflow-controller level, an individual workflow level, or within specific templates. There is an inherited hierarchy here with global being overwritten by workflow, which is overwritten by template. The goal is to ensure that every container in the pod has appropriate resource requests set.


### **Controller-Level Configuration**


Workflow controller configuration allows setting organisation-wide defaults for executor resources and template defaults. This approach ensures consistent baseline resource allocation while reducing the configuration burden on workflow authors:


```text


```


### ` ‍
` **Workflow-Level Configuration**


Setting executor resources at the workflow level provides consistent resource allocation for init and wait containers across all steps. This approach ensures baseline reliability while allowing individual templates to specify additional resources for main containers:


```text


```


### **Template-Level Configuration**


Individual templates should specify resource requests based on their specific workload requirements. CPU-intensive tasks require higher CPU requests, while memory-intensive operations need substantial memory allocations. The key is balancing resource requests with actual usage patterns to avoid both under-allocation and waste. Note that using podSpecPatch here allows you to assign difference resource requests for the init container and the wait container.


```text


```


` ‍
`


You can use podSpecPatch to set resource request values using workflow parameters. For example:


```text


```


` ‍
`


### **Dynamic resource request increases**


It is possible to have your workflow step increase its resource requests when the step retries.This example will start the hello-world task with a 10Mi memory request. If that step is retried, it’ll increase the request to 20Mi, and then 30Mi.


```text


```


` ‍
`


## **Common Resource-Related Problems and Solutions**


### **Pending Pod Issues**


Pods stuck in pending state can indicate insufficient cluster resources to satisfy resource requests. The solution involves either reducing resource requests, adding cluster capacity, or optimising resource utilisation across workflows. Analysing pod events using` kubectl describe pod` reveals specific resource constraints causing scheduling failures.


In Argo Workflows 3.6+, you can look at the emitted` pod_pending_count` metric to understand how many pods are pending and what the reason is for their pending state.


### **OOMKilled Errors**


Out-of-memory kills occur when containers exceed memory limits, but they can also result from insufficient resource requests causing poor scheduling decisions. Setting appropriate memory requests ensures pods are scheduled on nodes with sufficient memory, while limits prevent individual containers from consuming excessive resources.


It is highly recommended that you have alerting in place so that you are aware of when an OOM occurs in your cluster. OOMs are hard to diagnose after the event because the evidence of the failure disappears quickly.


## **Resource Quota Violations**


Namespace resource quotas can prevent workflow pods from starting when aggregate resource requests exceed quota limits. Designing workflows within quota constraints requires balancing parallelism, resource requests, and workflow complexity to stay within allocated budgets.


## **Monitoring and Optimisation**


### **Resource Duration Tracking**


Argo Workflows provides resource duration metrics that indicate the cost of workflow execution based on resource requests and runtime. These metrics help identify optimisation opportunities and validate that resource requests align with actual usage patterns.


### **Performance Metrics**


Monitoring CPU and memory utilisation alongside resource requests reveals optimisation opportunities. Consistently low utilisation suggests over-allocation, while resource contention indicates under-allocation. Tools such as Prometheus and Grafana provide detailed insights into workflow resource usage patterns.


If you are new to the world of Workflow observability, you can use our[free Pipekit Metrics tool](https://pipekit.io/metrics-signup) to view and understand the impact your workflows are having on your cluster.


### **Cost Optimisation**


Resource requests directly impact infrastructure costs by influencing node utilisation and scaling behaviour. Optimising requests based on actual usage patterns reduces costs while maintaining reliability. Regular analysis of resource duration metrics guides optimisation efforts.


## **Best Practices and Recommendations**


### **Establishing Baselines**


Start with conservative resource requests based on container image requirements and gradually adjust based on observed usage patterns. Monitor workflow execution to identify resource bottlenecks and optimisation opportunities. Establishing organisation-wide defaults reduces configuration burden while ensuring baseline reliability.


### **Quality of Service Classes**


Understanding Kubernetes QoS classes helps optimise resource allocation for different workflow priorities. Guaranteed QoS (where resource requests equal limits) provides maximum reliability for critical workloads, while Burstable QoS (where resource limits are greater than the resource requests) allows resource sharing for batch processing workloads.


### **Testing and Validation**


Thoroughly test workflows under realistic load conditions to validate resource configurations. Use tools like` kubectl top` and resource monitors to verify that resource requests align with actual usage. Regular load testing reveals resource bottlenecks before they impact production workflows.


## **Conclusion**


Setting resource requests on all Argo Workflows containers - init, wait, and main - is fundamental to reliable workflow execution at scale. This practice ensures predictable scheduling behaviour, prevents resource contention, and enables effective cost optimisation. The multi-container architecture of Argo Workflows means that resource starvation in any container can cause workflow failure, making comprehensive resource configuration essential.


Organisations adopting Argo Workflows should establish resource request standards, implement monitoring for resource usage optimisation, and regularly review resource configurations based on actual usage patterns. The investment in proper resource configuration pays dividends through improved reliability, reduced operational overhead, and optimised infrastructure costs.


By treating resource requests as a first-class configuration concern rather than an optional optimisation, teams can build robust workflow systems that scale effectively and operate reliably in production environments. The techniques and examples provided in this guide offer a foundation for implementing resource-aware Argo Workflows that deliver consistent performance and reliability.
