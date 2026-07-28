---
schema_version: "1.0.0"
document_id: "11bf34669ef551e2e30b9e270a6350e6829af11cec083ed0e384d8a0f25b8251"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/pass-key-values-between-argo-workflows-part-1"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:472e3f0b72b8dc7b4986f06ff1974986189e8a1564c4a8115bd7c4d31acc68a5"
---

# How to Pass Key-Values between Argo Workflows Part 1

Kubernetes provides a native way to run container[pods to completion](https://pipekit.io/blog/clean-up-pods-save-logs-argo-workflows) using[Kubernetes Jobs](https://stackedit.io/%5Bhttps://kubernetes.io/docs/concepts/workloads/controllers/job/%5D(https://kubernetes.io/docs/concepts/workloads/controllers/job/)) . The process can become complex when you need to run jobs that are dependent on each other and this is where Argo Workflows comes in.


[Argo Workflows](https://argoproj.github.io/argo-workflows/) is an open source container-native workflow engine for orchestrating parallel jobs on Kubernetes. Argo Workflows is implemented as a Kubernetes CRD (Custom Resource Definition). Using Argo Workflows, you can easily automate, schedule, and manage complicated workflows and compute-intensive jobs on Kubernetes in a fraction of the time it would normally take. Such intensive jobs and complicated workflows include data processes, machine learning, data analytics, and so on.


With Argo Workflows, you can define each step in the workflow as a container, create multiple-step workflows as a sequence of tasks and run them in parallel, and even run CI/CD pipelines on your Kubernetes cluster natively without integrating complex CI/CD software tools in your infrastructure.


If you create multiple steps in Argo Workflows, values will inevitably have to be passed between these steps at some point. Fortunately, Argo Workflows provides different methods of passing values between these steps, which you’ll learn more about in this article. Specifically, we’ll be looking at how to pass key-values between your Argo Workflows.


## Argo Workflows Quick Installation


Ensure you have your Kubernetes cluster up and running. You can use any of the managed Kubernetes services offered by various cloud providers, such as AWS Elastic Kubernetes Service (EKS), Google Cloud GKE, Azure Kubernetes Service, and so on. Or you can create a cluster locally on your computer using any of the following:


- MiniKube
- [K3s](http://pipekit.io/blog/how-to-run-argo-workflows-in-k3s) ‍
- [Docker Desktop](http://pipekit.io/blog/argo-workflows-with-docker-desktop)


Then, in your terminal create a dedicated namespace for Argo and apply the quick installation guide as seen below:


```text


```


Once it’s installed, you can access your Argo UI on[https://localhost:2746](https://localhost:2746/) by running the following command:


```text


```


You can also install the[Argo CLI](https://github.com/argoproj/argo-workflows/releases/tag/v3.3.5) on your local machine, which you can use to run your workflows, and introduce more benefits to kubectl, including syntax checking, better output, fewer keystrokes on your terminal, and so on.


The following are some useful Argo CLI commands:


```text


```


{% cta-1 %}


## Structure of an Argo Workflow


As mentioned, Argo Workflows is implemented as a[Kubernetes CRD](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) ; therefore, you can manage your workflows using kubectl. Argo also natively integrates with other Kubernetes services such as volumes, secrets, and so on. The following is a brief example of an Argo workflow:


```text


```


## Why Pass Key-Values between Steps of a Workflow


There are certain scenarios where a step is dependent on the output of a previous step. A hypothetical example of such a scenario might occur during data processing. There are three steps in this example data processing workflow, namely, Step A, Step B, and Step C. Step A is responsible for loading data from different sources; Step B then acts on the output result of Step A by transforming its result to the desired format; finally, the output is used by Step C, which saves the data in the database.


Another reason for passing key-values between steps is passing configuration data. You can set environment variables for the containers that run in each step with the help of parameters. This allows you to execute the same container in multiple steps with different parameters.


## How to Pass Key-Values between Steps of a Workflow


Now that you understand why you might need to pass key-values between steps in a workflow, this section will explore three different ways to achieve this:


1. Using parameters.
2. Using scripts and results
3. Using output.parameters


### Using Parameters


Using[parameters](https://argoproj.github.io/argo-workflows/walk-through/parameters/) is the simplest way of passing key-values between workflows. You define the parameters you want to use in spec.arguments.parameters, and then you can use them in any of your templates by declaring them with inputs.parameters.\[Name_of_the_Parameter\], as you can see in the example below:


```text


```


### Using Scripts and Results


The[script](https://argoproj.github.io/argo-workflows/walk-through/scripts-and-results/) keyword in Argo Workflows allows you to run scripts in a container, whose output can be used in other steps of a workflow:


```text


```


In the example above, there are five different templates, the first template is specified as the entry point of the workflow, which contains two steps. The first step points to generate-random-int-in-bash, which is a script that generates a random number between one and 200 in the bash environment. The output is then saved in the result variable, which can be accessed via steps.\[Name of the calling step\].outputs.result, and in this case, the name of the step generated. Therefore, other steps can access the result from steps.generate.outputs.result, such as the print step, which immediately runs after the generate step.


{% related-articles %}


### Using outputs.parameters


[outputs.parameters](https://argoproj.github.io/argo-workflows/walk-through/output-parameters/) is slightly different from scripts and results. Rather than using a script to generate output that will be used by other steps, the container saves its output result in a location, which is then referenced in an outputs.parameters argument. This argument can then be used by any step in the workflow as seen below:


```text


```


In the example above, the output-parameter, which is the entry point, generates a “hello world” text and saves it in a temporary location. The outputs.parameters are then used to reference the location where the “hello world” output is saved and then assigned its hello-param parameter.


Similar to what was done in scripts and results, other steps can use this parameter to read the message using **steps.\[Name of the step generating an output\].outputs.parameters.\[Name of the parameter assigned to the output\]** , which is steps.generate-parameter.outputs.parameters.hello-param in the above example.


## Conclusion


In this article, you learned how to pass key-values between these steps and the importance of doing so. Furthermore, you learned the different ways of passing key-values between workflows, which include scripts and results, output parameter, and parameters.


[Pipekit](https://pipekit.io/) provides production-ready workflows in minutes by configuring Argo Workflows on your infrastructure. It’s easy to set up and provides a built-in logging system. Furthermore, you can run Argo Workflows on Pipekit without running Kubernetes.


## **Go to Part 2**


Ready to take it further?[Explore Part 2 of our series for in-depth tips on Passing Key-Values between Argo Workflows.](https://pipekit.io/blog/pass-key-values-between-argo-workflows-part-2)
