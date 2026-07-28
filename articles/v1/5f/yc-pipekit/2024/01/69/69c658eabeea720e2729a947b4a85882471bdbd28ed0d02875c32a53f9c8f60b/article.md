---
schema_version: "1.0.0"
document_id: "69c658eabeea720e2729a947b4a85882471bdbd28ed0d02875c32a53f9c8f60b"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/why-teams-are-implementing-ci-cd-for-data-pipelines-using-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:2f657c3c35451eefbe83e7f64289bc72c43634858403df7bfde9c38909da8658"
---

# Why teams are implementing CI/CD for data pipelines using Argo Workflows

While at ArgoCon 2022, I delivered a talk on an emerging trend in data engineering that’s helping teams ensure their data pipelines don’t break in production. During the talk, *CI/CD for Data Pipelines with Argo Workflows* , I introduce this paradigm shift and highlight five major learnings:


- Using Argo Workflows to implement CI/CD for data pipelines
- Storing Workflows and WorkflowTemplates in git
- Validating WorkflowTemplates on pull requests
- Syncing WorkflowTemplates to clusters
- Testing WorkflowTemplates (demo)


In this post we’ll take a look at some of the key lessons and takeaways from the event.


## Why you should use CI/CD for data pipelines


When we consider how many teams use data pipelines — and how often they use them — it's surprising how many are pushing to staging and production and simply hoping for the best. Instead, what we want to do is validate our data pipelines and data transforms when making pull requests or pushing changes, so that we prevent issues later on in the development lifecycle.


Why does this matter? Rollbacks for one. When a bug gets introduced, it’s hard to go from a current version of staging or production to a previous version. This task grows even more challenging for larger teams where many people might be pushing changes all at once. What we’ve observed is most data teams do not have a concept of versioning for their pipeline components.


This is one of the reasons teams are beginning to apply CI/CD concepts and processes seen in traditional software engineering to data pipelines. Forward thinkers are:


- Factoring out transforms and other critical pieces into components
- Running tests on these components during pull requests and other change events
- Versioning these components using semantic versioning


This new way of approaching data pipelines solves two big problems:


1. **Wasted cloud spend (money)** — Data pipelines can significantly increase already high budgets for AWS, GCP, Azure, etc. Having to re-run data-intensive pipelines is a waste of compute resources, so ensuring pipelines pass tests before being run can save teams thousands of dollars per month.
2. **Data engineering time (time)** — Re-running a broken data pipelines often means a data engineer or data scientist needs to spend time debugging the pipeline and manually re-running it. Smart teams want to learn earlier in the dev cycle if bugs are being introduced, ideally before actually pushing changes to staging or production. This means they’ll save cycle time on debugging broken data pipelines by using CI/CD to catch common pitfalls earlier in the dev lifecycle.


{% cta-1 %}


## What is Argo Workflows?


Argo Workflows is an open source[workflow engine](https://en.wikipedia.org/wiki/Workflow_engine) that allows teams to orchestrate jobs on Kubernetes. It is implemented as a custom resource definition (CRD), so it's container native, and you can run it on[EKS](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) ,[GKE](https://cloud.google.com/kubernetes-engine/) , or any other K8s implementation.


With Argo Workflows, you can define workloads (workflows) such that each of its steps runs in a container. Depending on how you define the steps and their dependencies, you can run workflows sequentially or in parallel. An Argo Workflows spec that follows a YAML format is used to define your workflows and dependencies.


One of the primary reasons teams are flocking to Argo Workflows is because it allows them to run and scale pipelines for nearly any purpose. Companies commonly use it for machine learning, data processing, continuous integration/continuous deployment (CI/CD), and infrastructure automation.


## Understanding, testing, and versioning WorkflowTemplates


### What are Argo WorkflowTemplates?


[WorkflowTemplates](https://argoproj.github.io/argo-workflows/workflow-templates/) and[ClusterWorkflowTemplates](https://argoproj.github.io/argo-workflows/cluster-workflow-templates/) are native reusable components of Argo Workflows. Say you have part of a workflow and you want to refactor it into a piece that you can reuse over and over again. Saving time by not repeating tasks is one use case for WorkflowTemplates.


Good candidates to make components in workflows include:


- Doing data transforms
- Setting up/tearing down Kubernetes resources like[Dask](https://pipekit.io/blog/dask-argo-workflows-big-data) or[Spark deployments](https://www.youtube.com/watch?v=QV3YKUOiKo0)
- Running utilities like cloning git repositories


### How to test Argo WorkflowTemplates


WorkflowTemplates are just functions. Each one can take inputs and generate outputs, which we want to use if we’re looking to test. When testing, we want to make sure that the WorkflowTemplates of these components are pure functions (i.e., for a given set of inputs there’s the same set of outputs). Anything random or non-deterministic will cause problems.


### Versioning Argo WorkflowTemplates


Semantic versioning allows for structured promotion of components and easy rollbacks. While great to have, it is not currently available in vanilla Argo.


There are two ways of implementing semantic versioning for WorkflowTemplates in Argo Workflows that we’ve seen:


- Appending the version to the name with dashes; i.e., template-12-3-9
- Adding a label or annotation denoting the version


{% related-articles %}


## Watch the full talk and demo


Before wrapping up my talk, I shared a brief demo. In it I create an Argo Event source and sensor that reads GitHub pull requests and runs Argo Workflows. After that, I test changes made to a WorkflowTemplate in that same pull request.


[Visit our repo](https://github.com/pipekit/talk-demos/tree/main/argocon-demos/2022-ci-cd-for-data) to run the demo yourself, and watch my full talk from ArgoCon[here](https://www.youtube.com/watch?v=729GwVMgeXw&list=PPSV) . If you’re interested in reviewing the slides alongside the talk, you can access them[here](https://github.com/pipekit/talk-demos/blob/main/argocon-demos/2022-ci-cd-for-data/ArgoCon-2022-CI-CD_for_Data_Pipelines-JP-Zivalich_Pipekit.pdf) .


Want to use Argo Workflows with your team? Consider Pipekit. It’s a control plane for Argo Workflows that enables you to develop and run large, complex workflows. With Pipekit, you’ll be able to trigger workflows, collect logs, and manage secrets. It allows you to maintain pipelines across multiple environments and multiple clusters.
