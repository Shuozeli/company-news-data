---
schema_version: "1.0.0"
document_id: "0289247c15a95e169db62ca10f944d79723a4d9a80fe357058a88cb8885ed425"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/exit-handlers-argo-workflows-trigger-notifications-part-1"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:18.654833+00:00"
content_hash: "sha256:c37fdad668b547f0924070e4756e83864291d487b88b2c82c0053a907f7161ec"
---

# How to Use Exit Handlers with Argo Workflows to Trigger Notifications Part 1

Argo Workflows is a Kubernetes resource that’s used to orchestrate jobs or tasks in a Kubernetes cluster. A workflow consists of templates that define the jobs that will be run. Jobs are run in pods and the defined tasks range from downloading data from a storage bucket to running data analytics workloads.


Pipelines that run in Argo Workflows may be long-running or business-critical. You want to be able to inform site reliability engineers and other product owners of the status of a workflow when it completes its run. Fortunately, Argo Workflows can inform you when a workflow succeeds, fails, or throws an error. This functionality is provided by the **exit-handler API** .


In this article, you’ll learn about exit handling on Argo Workflows and its application in artifact cleanups, webhook notifications, and workflow chaining.


## What Are Exit Handlers?


Exit handlers are tasks that run when a workflow reaches an end state. There are three possible end states: success, failure, or error. Exit handlers can be defined at the workflow level using spec.onExit, or at the template level using template.onExit.


Difference between template and workflow level exit handling


You will typically use a workflow-level exit handler when you want to start another workflow after the current one completes its tasks. You can also use it to save the progress of a task to avoid starting from scratch if the workflow abruptly exits.


{% cta-1 %}


### Exit Handlers vs. Airflow Operators


Tools like[Prefect](https://www.prefect.io/) and[Apache Airflow](https://airflow.apache.org/) can be used to define workflows that run on Kubernetes. Apache Airflow can run as a standalone application on Linux, Windows, and macOS, or as a pod on Kubernetes.


Airflow operators that serve as exit handlers are designed to only do one thing. Argo Workflows exit handlers, on the other hand, allow you to run any task that can be packaged as a container image. This provides greater flexibility in what you can use exit handlers to achieve.


Airflow provides operators such as SimpleHttpOperator, EmailOperator, and SlackOperator for sending webhook requests, email, and Slack notifications respectively. These operators can be used upon the exit of a task within Airflow.


## Argo Workflows Exit Handler Use Cases


Exit handlers are for tasks such as:


- Deleting artifacts and resources that were created as part of the workflow run.
- Posting a pass, fail, or error status to a webhook endpoint.
- Chaining workflows by submitting a workflow when the current one completes its run.
- Saving the progress of a task to storage to prevent double work or starting from scratch.


The following sections present an overview of various use cases, including code examples.


### Cleaning Up After a Workflow Runs


Provisioned Kubernetes resources need to be unallocated or deleted after a workflow runs. Exit handlers can be used to achieve this within workflows. For example, consider a config map that was created as part of a workflow run. You’ll want to remove the resource at the end of the workflow run to free up memory for other workflows and jobs. The snippet below shows a Kubernetes manifest that creates a config map and deletes it in the exit-handler step of the workflows:


```text


```


### Posting the Pass/Fail Status to Webhook Results


Your operations team may need to perform an action after a workflow completes, so you’ll want to notify them on your organization’s communication tool, like Slack. However, they might not have access to the Kubernetes cluster where Argo is deployed and running the workflows. Using exit handlers, you can send webhooks from your Argo Workflows to tools like Slack, Discord, Twilio, PagerDuty, or email for notification and reporting.


You can use either a cURL command provided by a cURL container or simply use the HTTP workflow template type:


```text


```


### Submitting or Resubmitting Another Workflow


Workflow tasks may fail unexpectedly due to network errors or glitches. In such cases, you’ll want to resubmit the workflow so that failed tasks can be run again. Fortunately, Argo Workflows[memoizes](https://stackedit.io/%5Bhttps://argoproj.github.io/argo-workflows/memoization/%5D(https://argoproj.github.io/argo-workflows/memoization/)) workflows so that successful tasks can be omitted when resubmitting the workflow. The following is an example scenario that combines a DAG and a step template together with an exit handler that resubmits the workflow on failure.


```text


```


### Saving the Progress of an Argo Workflow to Storage to Prevent Double Work


Exit handlers can be used to store the progress of an Argo Workflow to persistent storage when the workflow or task exits and before the processing task completes. In this way, you can restart the workflow and skip completed tasks. This reduces the processing time and costs for long-running tasks that can be broken down into sub tasks.


The following is a snippet of a workflow that saves completed tasks as files in[MinIO](https://min.io/) and loads the MinIO directory when the workflow is resubmitted. In this way, the workflow can skip tasks that have already been completed, as identified by the marker (file) name:


```text


```


## Global Exit Handlers vs. Hooks for Step/Template Exit Handling


A global exit handler is an exit handler set on the workflow level.


- Use a global exit handler when you want to do some task after all other tasks within the workflow have run.
- A global exit handler is specified just once within a workflow.


Global exit handlers can be used to send a notification or perform a cleanup after all tasks within a workflow have run.


### Examples of Global Exit Handlers


There are two ways of defining a global exit handler:


1. Using the onExit key on a workflow’s spec object:


```text


```


1. Defining an exit key within a hooks object on a workflow’s spec object:


```text


```


{% related-articles %}


### Where Do Lifecycle Hooks Come into Play?


[A lifecycle hook](https://argoproj.github.io/argo-workflows/lifecyclehook/) is a part of a workflow that’s triggered at different points of the lifecycle of a template. It provides an abstraction to let you work with the error, success, running, and exit states of a workflow without the need for checking these states yourself. (Lifecycle hooks are available starting in Argo Workflows v3.3)


The snippet below is a step template with two steps that shows how you can use the success, exit, and running lifecycle hooks. The exit hook within the first step contains an arguments key where an array with a single object is passed. This array can be accessed by the handle-exit template within the workflow. The handle-exit template can then log the arguments, make an API call with them, or create a file, message.txt, on the chosen storage bucket containing the logs of the first step, if any:


```text


```


## Conclusion


In this article, you learned about exit handlers in Argo Workflows. You also learned how to set up exit handlers in Argo Workflows using YAML. You saw the differences between exit handlers and Airflow operators. Finally, you learned about lifecycle hooks in Argo Workflows and how they can serve as exit handlers.


The workflow in this article is a good example where a fully-managed solution might be a more practical option. Fully managed solutions, like[Pipekit](https://pipekit.io/) , can help relieve the pressure of managing clusters for long-running workflows, allowing you to focus on your workflows rather than the architecture. Pipekit is a control plane for Argo Workflows that enables massive data pipelines in minutes, leading to significant savings in engineering time and cloud spend.


## **Go to Part 2**


Ready to take it further?[Visit Part 2 of our Exit Handlers series](https://pipekit.io/blog/exit-handlers-argo-workflows-trigger-notifications-part-2) for in-depth tips.
