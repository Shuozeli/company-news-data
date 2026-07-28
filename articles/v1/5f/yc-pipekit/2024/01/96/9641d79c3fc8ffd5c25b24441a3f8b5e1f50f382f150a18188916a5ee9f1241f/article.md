---
schema_version: "1.0.0"
document_id: "9641d79c3fc8ffd5c25b24441a3f8b5e1f50f382f150a18188916a5ee9f1241f"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/canva-decides-argo-workflows-airflow-kubernetes-native"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:5f078b38e385f2da41593f30dfa07178a95114ed6ad3f4fbb479447bcd2414ff"
---

# Canva Decides: Argo Workflows vs. Airflow for Kubernetes-native Workflows

# Canva Decides: Argo Workflows vs. Airflow for Kubernetes-native Workflows


Canva gave a talk at Data Council explaining why they chose Argo Workflows instead of Airflow for orchestrating their Spark data jobs.


Canva is a Sydney-based startup on a mission to empower the world to design. Their application allows users to use templates, images and videos to create designs.


When the data team ran into various limitations and issues with their existing workflow system, they searched for a new, effective workflow system. Because of time constrictions, they only conducted a comprehensive proof of concept between Argo and Airflow to see which one would work for them.


Below we summarize the talk delivered by Greg Roodt from Canva where he shared the evaluation process and his experience with using Argo so far. You can view[Greg’s talk here on YouTube](https://www.youtube.com/watch?v=oXPgX7G_eow) .


## Context and Problem


Canva uses workflows (orchestrated and repeatable patterns of activity) to:


- Improve the search relevance in their media library
- Generate recommendations for their user templates


## Problem


Initially, when Canva had a very small data team, they used AWS data pipelines that worked well for them. Even though it was a complicated tool, it solved a complicated problem reliably for them.


As the team grew in scale (and ambition) they started running into limitations with AWS data pipelines.


Some issues they had were:


- They had limitations in the types of EC2 instances they could run in the IWC data pipeline.
- Installing custom software was slow and awkward.
- They had to develop custom workarounds for their scheduling system.
- The tool was not well known and had little community support or knowledge around it.


These issues were the reason why they explored alternative workflow tools.


{% cta-1 %}


## Selecting Argo Workflows vs. Airflow


The Canva data team had limited time to evaluate the tools in the market and decided to conduct a comprehensive proof of concept between Argo Workflows and Airflow to see which one would work for them.


For their proof of concept, they set up both Airflow and Argo Workflows and implemented an existing, simple, realistic data pipeline. They did the setup themselves on AWS to get a better understanding of the various components and dependencies of both projects.


### **The evaluation criteria**


**As part of the evaluation criteria, they needed it to:**


- Support existing data workloads at Canva (mostly[Apache Spark](https://pipekit.io/blog/argo-workflows-spark) ).
- Be easy to set up and operate.
- Have a good workflow deployment story.
- Have live logging and live UI updates.
- Have timeouts and retries.
- Have reproducibility (be deterministic).


**What they did not want:**


- Locked into only using Python for their data pipelines
- GUI for creating and editing DAGs
- Overly complex or dynamic DAGs - basic conditional logic and loops were enough.
- To update a DAG at runtime.


### **The evaluation results**


**The main issues they found with Airflow:**


- Deploying DAGs wasn’t robust.
- There wasn’t an API to deploy DAGs. This meant that the DAG that was deployed was not necessarily the DAG that ran.
- The installation was complicated with a lot of dependencies and moving parts. They found that they almost certainly needed to run the database and the scheduler on separate machines, and had to monitor the Web UI, the scheduler and the executors (using the celery executer added to the complexity).
- They realized there was a lot of excitement around the Kubernetes executor for Airflow, but wondered why they would not simply use Kubernetes directly instead.


**The main issues they found with Argo Workflows:**


- The amount of YAML required could make the management and templating messy very quickly.
- Argo Workflows also required Kubernetes which increased the complexity somewhat, but if Kubernetes was the answer, Argo Workflows was a lighter weight orchestrator to implement.
- The UI had less mature features.


{% related-articles %}


## Why Canva chose Argo Workflows over Airflow


Canva found Airflow and Argo Workflows to be capable tools because they could both support their workflows, do live UI and logging updates, and timeouts and retries.


But they did not like Airflow's deployment, so chose Argo Workflows over Airflow.


Argo Workflows had a better deployment story for their DAGs via an API and command-line tool, and the DAGs were more declarative.


The added benefit with Argo Workflows was that the tasks were defined as containers, so if Canva needed to move to another tool in the future (and the tool ran containers), it would be a relatively straightforward migration path.
