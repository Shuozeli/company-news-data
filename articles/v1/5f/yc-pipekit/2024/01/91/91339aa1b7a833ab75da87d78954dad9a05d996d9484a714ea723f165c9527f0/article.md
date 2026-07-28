---
schema_version: "1.0.0"
document_id: "91339aa1b7a833ab75da87d78954dad9a05d996d9484a714ea723f165c9527f0"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/why-teams-use-argo-workflows-to-run-cloud-native-spark-jobs"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:2c8c217a72adccad3f437ae52894ff9a409de34ed7ae2459af4e3bec2dc14c8f"
---

# Why teams use Argo Workflows to run cloud-native Spark jobs

During Open Source Summit, I delivered a talk on the advantages of using Argo Workflows to run cloud-native Spark jobs alongside my teammate Darko Janjic. In this talk —[Automating Cloud-native Spark Jobs with Argo Workflows](https://youtu.be/QV3YKUOiKo0) — we discuss:


- Scaling and stability advantages of running Spark jobs on Kubernetes
- Using Argo Workflows to deploy and automate multiple Spark jobs on Kubernetes successively or in parallel
- Realizing the possibilities once you’re running Spark on Kubernetes


Let’s take a look at some of the key advantages we discussed during the talk and what running Spark jobs with Kubernetes and Argo Workflows can do for your team.


## Why teams use Spark, Kubernetes, and Argo Workflows


### Why Spark?


[Apache Spark](https://github.com/apache/spark) is the most popular big data compute framework. It’s super performant for batch data jobs and is highly versatile. More and more, teams are moving away from Yarn to run their Spark jobs and turning to Kubernetes. There are a few key disadvantages or limitations of Yarn that have led to this, including that it:


- Requires global installs
- Doesn’t support Docker natively
- Consumes more resources
- Doesn’t offer auto-scaling


### Why Kubernetes?


[Kubernetes](https://github.com/kubernetes/kubernetes) is great for data science for a number of reasons. First, when containers are the building blocks teams get reproducibility — users can share parts or the full data pipeline with different people on their team — and reliability. Second, Kubernetes takes a declarative approach to data pipelines. This is much more advantageous because it allows teams to define what outputs they want and you can let Kubernetes handle auto-scaling for you. Third, vertical auto-scaling helps teams handle spikey data jobs. Kubernetes is a great complement to the horizontal scaling that a framework like Spark offers as it introduces the ability to vertically scale depending on a team’s desired compute. And finally, using Kubernetes for data sciences allows you to tap into the cloud-native ecosystem for additional tooling (e.g., CI/CD, observability, etc.).


### Why Argo Workflows?


[Argo Workflows](https://argoproj.github.io/argo-workflows/) is the[best way to run workloads](https://pipekit.io/blog/argo-workflows-the-best-way-to-run-kubernetes-workflows) on Kubernetes. Here’s why:


- **Generalizable** — Can be used to automate anything, including ETL, ELT, batch data processing, ML training, serving, and CI/CD workloads
- **Lightweight to deploy** — Can be used as a workflow engine and orchestrator to automate many Spark jobs rather than having to run them manually
- **YAML or Python** — Define workflows using YAML or Python SDK
- **CNCF open source project**


At Pipekit we use Argo Workflows to scale data pipelines for enterprises. We offer a SaaS control plane that sets up Argo Workflows and gets them running on production using Kubernetes to build faster and more reliable data pipelines without having to know everything about Argo.


{% cta-1 %}


## So, why should you run cloud-native Spark jobs with Argo Workflows?


You’re probably familiar with some of the challenges that come with running a traditional Spark deployment on YARN. Global installs make it risky to share libraries between Spark jobs on a single cluster. While you might want to use a different Spark version for the different applications you’re building so you don’t have to go back and refactor jobs as versions are upgraded, this isn’t really possible with YARN. Applications also have to be containerized if ever you intend to take advantage of the faster dev experience and improved dependency management offered by Docker. Finally, with running Spark jobs on YARN, you can expect greater resource consumption and no auto-scaling.


For those reasons, more and more teams are moving away from YARN and choosing Kubernetes and Argo Workflows. Deploying Spark with Kubernetes and Argo Workflows solves a number of the issues that occur when running a traditional Spark deployment with YARN. This setup is:


- Container-native
- Has lower resource requirements for running jobs
- Auto-scales compute vertically (e.g., scale up to GPU, add more CPU)


Beyond that, adopting Kubernetes and Argo Workflows opens up bonus benefits. Using these tools together introduces:


- Duplicability — Use similar architecture for other frameworks
- Extendability — Bring other data processing and ML tooling into same cluster
- Scalability — Enable CI/CD, GitOps for your data platform
- Cloud-native ecosystem — Add logging, metrics, and more
- Flexibility — Avoid cloud vendor lock-in by remaining platform agnostic


Here’s a little more on each of those benefits.


### Duplicability


This is relevant if you have a team that wants to move beyond Spark to start adopting other parallel computing libraries, like Dask or Ray. When deploying on Kubernetes, you don’t have to set up a completely new cluster for a new version of Spark or a new library, like Dask or Ray. You can spin up similar architecture on the same cluster in a new namespace, and run some jobs with Spark, some with Dask or Ray, and use Argo Workflows to orchestrate them all.


### Extendability


Bring in new tooling, such as data processing or machine learning solutions, to the same cluster. You can also extend your CI/CD pipelines so that you can bring everything into Argo and Kubernetes to cover the entire process, everything from the moment you build images and submit chains to git to the moment you run tests and run the actual workload.


### Scalability


Kubernetes and Spark are great compliments, as Kubernetes offers vertical scaling while Spark enables horizontal scaling. Together, the two allow your teams to handle spikey data jobs and, when necessary, add additional nodes or machines to cope with increased demands.


### Cloud-native ecosystem benefits


Add logging, metrics, and more tooling to your compute platform by taking advantage of the many cloud-native solutions available.


### Flexibility


Part of being cloud-native and using Kubernetes means you’re vendor-agnostic. You’re not locked into using a specific vendor as your compute platform and instead have the flexibility to make changes as your team’s needs change.


## Example architecture of Spark on Kubernetes with Argo Workflows


### Beyond the basics: Here’s what comes next


- Use CRON workflows: run your workloads daily — or on whatever basis you prefer — with CRON Argo Workflows.
- Define different node pools in order to use different instance types for machine learning, like GPU nodes, and more.
- Autoscaling: run your Spark jobs and, based on the needs, Kubernetes will spin up more worker nodes, execute the job, and then downscale to 1 or 0. This ultimately allows you to lower your costs, extend your entire pipeline, have everything in git, and to trigger your workflow by creating events. Use the[NodeSelector feature in Argo Workflows](https://github.com/argoproj/argo-workflows/blob/master/examples/node-selector.yaml) to autoscale your workloads to the appropriate node size.


{% related-articles %}


## Watch the full talk and demo


Before wrapping, we walk through a couple of demos. The first shows how to run two Spark jobs in parallel on Kubernetes with Argo and the second shows how to parameterize that workflow file so more people on a team can run workflows on their own just by passing in arguments.


‍[Visit our repo](https://github.com/pipekit/talk-demos/tree/main/oss-2022) to run the demo yourself, and watch the demo and full talk[here](https://youtu.be/QV3YKUOiKo0) . If you’re interested in reviewing the slides alongside the talk, you can access them[here](https://github.com/pipekit/talk-demos/blob/main/argocon-demos/2022-ci-cd-for-data/ArgoCon-2022-CI-CD_for_Data_Pipelines-JP-Zivalich_Pipekit.pdf) .
