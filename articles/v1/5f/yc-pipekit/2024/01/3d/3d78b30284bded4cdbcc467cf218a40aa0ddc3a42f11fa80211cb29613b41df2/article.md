---
schema_version: "1.0.0"
document_id: "3d78b30284bded4cdbcc467cf218a40aa0ddc3a42f11fa80211cb29613b41df2"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/artifacts-management-at-scale-for-ci-and-data-processing-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:cb2b1ae8dde505931e59cd3b0538ff6406209e55ce581a3d0b594cc004109adf"
---

# Artifacts Management at Scale for CI and Data Processing Workflows

A team’s ability to process, analyze, and make sense of large amounts of data is a must. These tasks can be and often are challenging because of the increasing complexity of data pipelines. Processing that data accurately and efficiently is very much a daunting task, one that was top of mind as I prepared for my talk at ArgoCon EU.


While there, Julie Vogelman, Staff Software Engineer at Intuit, and I delivered the talk “Managing Artifacts at Scale for CI and Data Processing.” We shared the best practices we learned from using Argo Workflows at Intuit and Pipekit that helped our teams address some of the most common challenges that come with artifact management.


This post will highlight those challenges, but not before providing a summary of which types of artifacts and data you’re most likely to use with Argo Workflows and why it’s important to manage your artifacts effectively.


## Types of artifacts used in data processing


Artifacts are one kind of byproduct created during software development. Some[artifacts](https://en.wikipedia.org/wiki/Artifact_(software_development)) help to describe the function, architecture, and design of software while others detail the development process itself. The function that artifacts serve has a lot to do with their use case.


In data processing, artifacts take on a few different forms, including tabular data, image and video files, geospatial data, and vector data. We often see tabular data used in data processing and analysis, whereas image and video files tend to be used for object detection, facial recognition, and image processing tasks. When working with geospatial data and vector data, they are typically most prevalent in mapping and geographic information systems (GIS) applications.


Artifacts used in CI (continuous integration) look very different. Here, we’re looking at dockerfiles, git repositories, built binaries, binary caches, and other software components. For example, dockerfiles specify the environment in which software is run while git repos will store the source code, ultimately allowing developers to track changes as they collaborate. Built binaries and binary caches provide us with the final executable code that gets deployed during production, making them essential in CI.


With machine learning, we’re working with artifacts such as training datasets, trained ML models, and feature stores. Used to train ML models and extract relevant features used as input to a given model, training datasets are a key artifact in machine learning. Training datasets might include tabular data, image and video files, and text or audio data, among other things. Trained ML models learn and make predictions or classifications based on ML algorithms applied to data. Once created, these models get saved as artifacts to be used later in the data processing pipeline. Feature stores are artifacts extracted from raw data, added to a collection, and used as inputs for ML models. They provide us with a reliable way to share feature data and ensure reproducibility and consistency throughout the ML workflow.


{% cta-1 %}


## The persistence of data in Argo workflows


While you might already be familiar, one thing to be aware of working with these artifacts is that there are several different data types. During my talk, I chose to zoom in on how persistent the data Julie and I discussed is because of how significantly it impacts the management of that data throughout the Argo workflow.


Here are those different types of data:


- **Transient data** — Passed between workflow steps; data not needed beyond life of the workflow
- **Semi-persistent data** — Relevant across multiple runs of workflows; yet, easy to reinstate if lost, like module/binary/dockerfile caches
- **Persistent data** — Data we want to keep, often the final output from a running workflow


Transient data is data that we don’t really care about beyond the step during which it’s used in the workflow. Rarely do we need transient data beyond the life of the workflow. As we get more persistent, we grow more concerned with how to archive data and find it. With semi-persistent data, there tends to be less concern with lost data because it can pretty easily be reinstated.


## How to choose the right storage type for your artifacts


Storage types have to be considered when building an Argo workflow, and there are three main types to explore including blob, block, and network file system. When selecting a storage type for your workflow, it's important to weigh the pros and cons of each option and choose the best fit for your specific use case.


‍[Blob storage](https://www.cloudflare.com/learning/cloud/what-is-blob-storage/) is the most popular storage option, the one that most of us are familiar with. Examples include S3, GCS, and MinIO. Blob storage is easy to set up, easily queryable, offers useful data archiving settings, and makes artifacts visible in the Argo Workflows UI, making it a convenient option. However, it does have some downsides, such as being slower because of the data tarring between workflow steps and its lack of Read-Write-Many compatibility.


‍[Block storage](https://www.ibm.com/topics/block-storage) is an alternative to blob storage that is less commonly used but offers slight performance advantages over blob storage. Like blob storage, block storage is easy to set up, however, it has lower latency and offers easy data backup and restoration. This option is, intended for per-instance storage use cases and also doesn't have Read-Write-Many compatibility.


‍[Network file systems](https://en.wikipedia.org/wiki/Network_File_System) actually offer Read-Write-Many compatibility and auto-scale well for high throughput needs. There’s no tarring required here, which means faster transfers between steps. Some of the drawbacks of NFS to consider include usability only for cloud setups, it can’t be dynamically provisioned with a PVC, and it is slow with parallel read/writes at scale.


{% related-articles %}


## How to choose the right storage type for your artifacts


The core problem at hand with artifact management is finding a way to pass data between workflow steps. But before starting to pass artifacts between steps, you’ll need to configure your artifact management properly. That will involve:


- Centralizing the artifact repository configuration for scale and security
- Implementing smart artifact naming patterns
- Managing small versus large artifacts
- Utilizing artifact garbage collection


Once that has been managed, you will be ready to address the core problem. To do this you can use parameters, blob storage, or network file systems.


- ‍ **Parameters** — Parameters are the most basic way to pass information, including strings and commands, between steps in a workflow. They also allow for passing small script outputs and small, stringified .json and .txt files. With parameters, the biggest challenge is that there is a memory limit per workflow.
- **Blob storage** — Blob provides more persistent artifacts, such as data tables and trained models. When seeking to pass data between workflow steps, it’s necessary to package up outputs between steps.
- **Network file system — NFS doesn't require you package up your outputs between steps, and it will save runtime. If you want Read-Write-Many functionality, you’ll need to use NFS. Finally, for some use cases, NFS can be higher cost as a tradeoff for faster runtime.**


## Watch the full talk


Effective artifact management is critical to workflow management in Argo Workflows. By centralizing the storage of artifacts, implementing smart artifact naming patterns, managing small and large artifacts, and using garbage collection, you can ensure scalable, secure, and efficient artifact management.


Watch our complete talk from ArgoCon EU, including a few demos,[here](https://youtu.be/ucnOQuNkIbE) . And if you are interested in reviewing the slides alongside the talk,[visit our repo](https://github.com/pipekit/talk-demos/tree/main/argocon-demos/2023-artifact-management-at-scale) . Finally, for insight on another approach to managing your artifacts, watch this talk —[Configuring Volumes for Parallel Workflow Reads and Writes](https://youtu.be/QZI-LXJGWYI) — from our team member Tim Collins and Lukonde Mwila from AWS.
