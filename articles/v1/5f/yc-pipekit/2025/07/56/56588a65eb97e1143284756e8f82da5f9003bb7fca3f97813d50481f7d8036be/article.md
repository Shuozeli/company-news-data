---
schema_version: "1.0.0"
document_id: "56588a65eb97e1143284756e8f82da5f9003bb7fca3f97813d50481f7d8036be"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/hacking-on-the-argo-workflow-of-workflows-pattern"
published_at: "2025-07-16T19:48:26+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:56:43.889340+00:00"
content_hash: "sha256:62e58454756b4b2da6377867ba1e35f3b4830a9740ffa72386da49e44431ee9d"
---

# Hacking on the Argo Workflow-of-Workflows Pattern

This post demonstrates some new ways of working with the[workflow-of-workflows](https://argo-workflows.readthedocs.io/en/stable/workflow-of-workflows/) pattern using Argo Workflows, where a parent workflow creates multiple child workflows. If you're already using workflow-of-workflows, or thinking of using them to split up your work, these techniques might help with managing them, as the Argo UI doesn't provide much assistance navigating amongst your group of workflows.


In this sample we have two parameters:


- ‍ *runID* : a unique identifier for the run, which could be anything you like, it's just to help you identify the run *‍*
- *locations* : a list of locations to process, in this case we have a list of cities. It's not actually used in the child workflow, but it's a good way to demonstrate how to use a list of parameters and visualize them in the UI.


The parent workflow creates one child workflow per location. The child workflow is just a diamond pattern workflow that does nothing useful.


This isn't a substitute for a proper UI for workflow-of-workflows, but it's better than nothing.


## Parent Workflow


The parent workflow takes a *runID* and a list of *locations* , then creates one child workflow per location:


**parent-workflows.yaml:**


```text


```


## Child WorkflowTemplate


The child workflow uses a diamond pattern and includes dynamic metadata:


**dag-diamond.yaml:**


```text


```


## Key Features Used


### Labels


Labels are kubernetes indexes for filtering objects, and we're using them to filter workflows by the *runID* label.


We use this to create a UI link to all of the workflows for a given *runID* .


```text


```


### **Markdown Support (Argo Workflows v3.6+)**


The parent workflow uses markdown in the title annotation to create a clickable link that filters workflows by the *runID* label, thus listing all workflows for this runID:


Filtering to the 'morning-run'


The child workflow additionally uses markdown to provide a link to the parent workflow:


```text


```


Jump straight to the parent from the child


### Template Display Names (Argo Workflows v3.7+)


The *submit-diamond* template uses the display-name annotation to show the location field in the UI:


```text


```


This changes how the parent fan out looks in the UI:


Traditional withParams presentation


Using display-name to make this easier to read


## Usage


Submit the parent workflow with custom parameters:


```text


```


This creates one diamond workflow per location, each with the same *runID* for tracking and the parent workflow name for lineage.


## Conclusion


Here I've demonstrated some ways in which the new features of markdown titles and descriptions, and renaming of nodes can help with understanding and navigating your workflows.


The Workflow of Workflows pattern is a powerful way of breaking up your work to make it more manageable, but at the moment the UI doesn't make navigating it easy. With these techniques some of that pain is alleviated.
