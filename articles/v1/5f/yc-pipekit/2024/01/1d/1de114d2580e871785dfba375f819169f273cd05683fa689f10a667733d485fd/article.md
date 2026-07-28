---
schema_version: "1.0.0"
document_id: "1de114d2580e871785dfba375f819169f273cd05683fa689f10a667733d485fd"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/pass-key-values-between-argo-workflows-part-2"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:18.654833+00:00"
content_hash: "sha256:4543e7673a41c56bfbebab1939e21858d8a845b44bc6c62f32f0303fb19f6dc6"
---

# How to Pass Key-Values between Argo Workflows Part 2

The[first part](https://pipekit.io/blog/pass-key-values-between-argo-workflows-part-1) of this series introduced Argo Workflows, explained how to set up an Argo workflow in your Kubernetes cluster, and discussed different methods of passing key-values between Argo workflow steps, which included using {% c-line %}scripts and results{% c-line-end %} and {% c-line %}output parameters{% c-line-end %}.


In this second part of the series, you’ll learn how to pass key-values between Argo workflows, which include using {% c-line %}ConfigMap{% c-line-end %}, {% c-line %}Secrets{% c-line-end %}, and {% c-line %}Artifacts{% c-line-end %}.


## Why Do You Need to Pass Key-Values between Workflows?


As your project gets bigger, it becomes harder to fit all your jobs in a single workflow containing multiple steps. Instead, you start to namespace similar jobs together in multiple workflows for easier management and to keep related jobs together.


However, there are instances where you need to share configuration data across multiple workflows. Fortunately, Argo’s {% c-line %}ConfigMap{% c-line-end %} and {% c-line %}Secrets{% c-line-end %} allow you to share configuration data across multiple workflows, removing the overhead of scoping each configuration data to every workflow.


Furthermore, there are instances where you want to use the output result of a workflow in multiple other workflows. This can be accomplished using an[artifact repository](https://pipekit.io/blog/configure-artifact-repo-argo-workflows) , which you can configure in Argo Workflows. The following sections will discuss how to use {% c-line %}ConfigMap{% c-line-end %}, {% c-line %}Secrets{% c-line-end %}, and {% c-line %}Artifacts{% c-line-end %} to share data.


## Passing Key-Values Between Workflows Using ConfigMap


Argo Workflows provides three methods of using {% c-line %}ConfigMap{% c-line-end %} key-values in your workflows:


- Using {% c-line %}arguments{% c-line-end %} parameters from {% c-line %}ConfigMap{% c-line-end %}
- Using {% c-line %}global parameters{% c-line-end %} referenced from {% c-line %}ConfigMap{% c-line-end %} as a local variable
- Using {% c-line %}global parameters{% c-line-end %} referenced from {% c-line %}ConfigMap{% c-line-end %}


In order to use any of these methods, the {% c-line %}ConfigMap{% c-line-end %} you want to use should already exist in your cluster.


Create a file named {% c-line %}simple-configmap.yaml{% c-line-end %} and paste the following:


```text


```


In your terminal, run the command below to apply the {% c-line %}ConfigMap{% c-line-end %} in your cluster:


```text


```


The {% c-line %}ConfigMap{% c-line-end %} you just created will be used to explain the different methods of using {% c-line %}ConfigMap{% c-line-end %} key-values in your Argo workflows.


{% cta-1 %}


## Using Arguments Parameters from ConfigMap


In part one of this series, you learned how to use {% c-line %}parameters{% c-line-end %} to pass key-values to Argo workflows. The {% c-line %}parameters{% c-line-end %} contained custom values that you manually included in the workflow template via {% c-line %}arguments{% c-line-end %} or {% c-line %}inputs{% c-line-end %}. In scenarios where these custom values are required in multiple workflow files, it becomes cumbersome to manually edit these files, and this is where {% c-line %}ConfigMap{% c-line-end %} becomes useful, as mentioned earlier.


Using {% c-line %}ConfigMap{% c-line-end %}, you can pass values into your workflow {% c-line %}parameters{% c-line-end %}. In the workflow below, the {% c-line %}whalesay{% c-line-end %} template has {% c-line %}config{% c-line-end %}, a parameter whose value is extracted from the {% c-line %}simple-configmap{% c-line-end %} you created earlier:


```text


```


## Using Global Parameters Referenced from ConfigMap as a Local Variable


ConfigMaps are not only restricted to steps in a {% c-line %}WorkflowTemplate{% c-line-end %}. When the {% c-line %}ConfigMap{% c-line-end %} value is to be used in multiple steps, instead of referencing the {% c-line %}ConfigMap{% c-line-end %} locally as {% c-line %}input{% c-line-end %} in each {% c-line %}WorkflowTemplate{% c-line-end %}, you can reference the {% c-line %}ConfigMap{% c-line-end %} in {% c-line %}arguments{% c-line-end %} at the {% c-line %}spec{% c-line-end %} level; this change will allow each step in the workflow to use the {% c-line %}ConfigMap{% c-line-end %} value that’s set in the {% c-line %}arguments.parameters{% c-line-end %}:


```text


```


## Using Global Parameters Referenced from ConfigMap


You can also reference your workflow {% c-line %}arguments.parameters{% c-line-end %} directly in your template steps, without having to create an {% c-line %}inputs.parameters{% c-line-end %} reference in the {% c-line %}WorkflowTemplate{% c-line-end %} as seen below:


```text


```


## Passing Key-Values between Workflows Using Secrets


Similar to using {% c-line %}ConfigMap{% c-line-end %} to pass key-values, you can also use {% c-line %}Secrets{% c-line-end %}. You can first start by creating a sample secret to use. In your terminal, run the following command to create {% c-line %}new-secret{% c-line-end %}:


```text


```


Next, you can create a workflow using the secret you just created. To access the secret as a file, you add a volume entry in {% c-line %}specs.volumes{% c-line-end %} and also add a mount using {% c-line %}volumeMounts{% c-line-end %} in the container template spec:


```text


```


You can now use the {% c-line %}Secret{% c-line-end %} directly in your workflow step as seen above in the {% c-line %}whalesay template{% c-line-end %}.


{% related-articles %}


## Passing Key-Values between Workflows Using the Artifact Repository


Artifacts are output files generated by Argo Workflow steps. There are instances in your Argo workflows where a particular workflow requires the output of another workflow. For instance, continuous integration/continuous development (CI/CD) is an important process in the development and release of an application. You can have a workflow that ensures your application passes all the tests and then creates a build artifact that can be deployed by another workflow to your staging environment.


The example below demonstrates this process as a workflow that generates a text in a file, which is then used by another workflow. The other workflow retrieves the text in the file and displays it.


However, you should note that you need an artifacts repository to use artifacts. Argo supports S3-compatible artifact repositories such as AWS, GCS, MinIO, and so on. You can check out the[Argo Workflow Repository](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) and follow the guide to install the repository storage of your choice.


The workflow below generates a text file containing “hello world” and saves it in the location configured in the artifact repository:


```text


```


Other workflows will be able to use the artifact generated by the first workflow when they’re submitted using the sample code below. The workflow template links to the location in the artifact repository where the required data is stored. It then retrieves the data and performs the necessary action, which is to output the data:


```text


```


## Conclusion


This article concludes this series about passing key-values between Argo workflows. In this two-part series, you were introduced to Argo Workflows, a Kubernetes tool for running multiple[Kubernetes jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/) in series or in parallel. You also learned about the structure of an Argo {% c-line %}Workflow template{% c-line-end %} and how to pass key-values between workflows using {% c-line %}scripts and results{% c-line-end %}, {% c-line %}output parameters{% c-line-end %}, {% c-line %}ConfigMap{% c-line-end %}, {% c-line %}Secrets{% c-line-end %}, and {% c-line %}Artifacts{% c-line-end %}.


If your team has been looking to get started with Argo Workflows,[Pipekit](https://pipekit.io/) provides production-ready workflows in minutes by configuring Argo Workflows on your infrastructure. It’s easy to set up and provides a built-in logging system. You can even run Argo Workflows on Pipekit Cloud without running Kubernetes.
