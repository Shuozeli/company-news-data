---
schema_version: "1.0.0"
document_id: "234bb9a6adbab7e9bf283c86cb3884031c1961615ffe3a7ca8458e6df085392d"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/dask-argo-workflows-big-data"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:2928ff28a89b9b7b9466b7d9d96da0456322648549a90ea2564f9eb9d553cfe8"
---

# How to Orchestrate Dask with Argo Workflows for Big Data Workloads

## Introduction


This article details how to orchestrate Dask with[Argo Workflows](https://pipekit.io/blog/what-is-argo-workflows) based on[a talk Pipekit and ACCURE Battery Intelligence gave at ArgoCon 2021](https://www.youtube.com/watch?v=f5lPS9WKy_8&list=PLGHfqDpnXFXKwNGO_8usFuTO-rIHNyefC&index=14) . You’ll learn how to combine Kubernetes-native scheduling and automation available from Argo Workflows with the low-latency scalability of Dask to distribute your Python jobs.


To do so, we’ll discuss how Pipekit provisioned Argo Workflows for[ACCURE Battery Intelligence](https://accure.net/) and show how ACCURE uses Dask orchestrated by Argo Workflows to process petabytes of data with super low-latency for their customers.


Let’s get started with the basics.


### Who is ACCURE Battery Intelligence?


ACCURE makes batteries smarter by creating computational algorithms that compute useful metrics for batteries. This can include computing the state of health of batteries, devising safety alerts, and drawing up operational optimizations.


## ACCURE’s data processing requirements


### Data engineering requirements


ACCURE’s team intended to stay in Python and avoid a situation where they constantly needed to switch between Python and other environments.


They also wanted to have capabilities beyond map-reduce functions. The battery industry has multiple heuristic algorithms that need to be implemented, and ACCURE wouldn’t be able to do that if they were limited to simple functions.


Another necessity was to have the same development experience in testing and production environments. They want to write code once and have it work — whether they’re invoking it in a situation using one computer where everything is running sequentially, or have a distributed cluster of computers that are working together on the same pipeline.


ACCURE also needed to conduct both batch processing and shared parallel-processing.They have many independent, batched workloads that run parallel to one another, while also have workloads where they have one big task that many workers help solve simultaneously leveraging parallel processing.


Lastly, ACCURE wanted to promote self-service for data engineers, data scientists, and customer support managers to streamline processes within their organization whenever possible.


{% cta-1 %}


### Infrastructure and Security Requirements


ACCURE needed ultra-low latency parallelization to help them run massively parallel jobs in order to complete jobs in a timely manner for their customers.


They also needed a multi-tenant environment: different customer workflows on the same Kubernetes cluster with each customer having a dedicated namespace. However, ACCURE needed to have good separation among the different workflows so that one workflow can only access resources that belong to one customer and not the others.


Of course, everything needed to run smoothly on production with no downtime and monitoring in place to quickly diagnose and pinpoint issues that might arise.


For example, logging should be easily accessible in ACCURE’s ELK stack and scheduling should be dependable. Workflow runs also need to be archived so that if there’s any that need troubleshooting then ACCURE can access them immediately.


## Provisioning Argo Workflows and the need for Kubernetes resources


ACCURE uses infrastructure as code (IaC). They use GitLab to store their workflow configuration, Kubernetes configuration, and the Pipekit daemon which manages Argo workflows. They’re using[Pulumi](https://www.pulumi.com/) for actual spinning up/down of resources. For instances like these, it’s also possible to use Terraform or Cloud formation infrastructures, but they chose Pulumi because it’s Python-native which the team was most comfortable with.


They’re also doing a cluster-wide installation of Argo Workflows, meaning they install the workflow controller and the Argo server in a cluster scope. They’re also provisioning a namespace for each customer that ACCURE is serving. Operators then have access to creating, updating, deleting Argo Workflows and Workflowtemplates in each namespace.


Individual workflows can’t access other resources within the Kubernetes cluster, which means that there are customer-specific namespaces. Workflowtemplates are differentiated by namespace and configured for specific customer contexts.


ACCURE is using[Cron workflows](https://argoproj.github.io/argo-workflows/cron-workflows/) to trigger workflow templates. Each of those Cron workflows is sitting in each customer’s namespace and is highly customizable regarding the schedules you want them to run on.


Lastly, Pipekit set up the connection to ACCURE’s ELK stack, using[Fluentbit](https://fluentbit.io/) to send logs to ACCURE’s Elasticsearch instance and[Metricbeat](https://www.elastic.co/beats/metricbeat) for sending Prometheus metrics.


Diagram of the ACCURE Kubernetes cluster


## Dask Overview


ACCURE chose to use[Dask](https://dask.org/) because it allows for high-throughput data pipelines completely done in Python.


Dask is also equipped with:


- Multi-domain execution. Even going from sequential execution on a single machine up to distributed execution across many machines, and more or less every imaginable cluster.
- Dask[DataFrames](https://docs.dask.org/en/stable/dataframe.html) &[futures interface](https://docs.dask.org/en/stable/futures.html) that allows for batch processing.


Dask also has helpful support resources, with Dask development support from a sizeable community, as well as the option to get helpdesk support as a service. Some services can even provision clusters for you on your behalf.


However, Dask doesn’t have everything, and ACCURE had to implement a few extras:


- Work-avoidance: Instead of recalculating a task that has been done before, they implemented a fix that refers to previous results to save time and resources.
- Artifact storage:They connected Dask to their task artifacting system that is set up on S3.
- Logging: As mentioned above, an ELK stack with Fluentbit, Elasticsearch, Prometheus, and Metricbeat.


### **Demo**


The following demonstration will look at time series data in Spain for 5 cities to answer the question of which of these cities is the windiest.


There is a pipeline that will take a look at all timestamps and datasets, it will then send each timestamp one by one to Dask where a generic Python function will be executed.


Check out a demo of this in[the ArgoCon 2021 talk here](https://youtu.be/f5lPS9WKy_8?t=1264) on YouTube (starts at minute 21:04).


{% related-articles %}


## Conclusion: Should you use Dask and Argo Workflows?


Do you need to schedule automated workflows? Do you need a way to execute several large jobs quickly and in parallel? Do you want a way to start taking advantage of the latest parallelization frameworks for big data?


Answering “yes” to any of these questions means Argo Workflows and Dask are a great choice.


Dask-as-a-service also has its benefits, but comes at an increased cost. It allows for faster development iteration and empowers self-service for data engineers.


### Dask is not a silver bullet


Dask does show some instabilities for long-running tasks. Pipekit and ACCURE found that tasks that run for a few hours are manageable, whereas tasks that run for days are not.


It’s important to note that Dask can do batch processing, but that’s not its main focus. It excels in the shared parallel processing scenario, especially with the Dask DataFrame and futures interface.


If you’re only doing batch processing, consider using something else, like Apache Spark or Ray, as it probably would provide better stability.


Learn more about Argo Workflows and more best practices for data processing by requesting your personalised demo.
