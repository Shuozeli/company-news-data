---
schema_version: "1.0.0"
document_id: "9c55ba09b6181a423b72cf6a3b18f1e47fab10600caa48bf1a524ff18af8bb6b"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/what-is-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:93a78ba1740e6736874e4da4f00ae3a9e7e432498d2d21a6aca0d7912faf6b1d"
---

# Everything You Need to Know About Argo Workflows

Your business thrives on data and your ability to process it quickly, efficiently, and effectively. And like everyone else, you need to process larger and larger volumes of data with each passing week, if not each day. Processing data sets in small batches—or worse, by hand—doesn't work anymore. You need the ability to process large quantities of data in parallel. You need tools like Kubernetes and Argo Workflows.


In this post, we'll look at Argo Workflows and how it can help you. If you want to see Argo Workflows in action,[book your personalized demo with us.](https://homepage.pipekit.io/demo-sign-up)


## ‍ **What Is Argo Workflows?**


Argo Workflows is a[workflow engine](https://en.wikipedia.org/wiki/Workflow_engine) for Kubernetes (K8s) clusters. It runs as a[custom resource definition](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) , so it's container native, and you can run it on[EKS](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) ,[GKE](https://cloud.google.com/kubernetes-engine/) , or any other K8s implementation. Argo Workflows is a[CNCF incubating](https://www.cncf.io/projects/argo/)[open-source](https://github.com/argoproj/argo-workflows) project maintained by Intuit.


With Argo, each step in your workflow runs in a container. So, depending on how you describe the steps and their dependencies, it's easy to run them sequentially or in parallel. You define your workflow and those dependencies using Argo's Workflow spec, a YAML format that's easy to follow.


With Argo Workflows, you can run and scale pipelines for nearly any purpose. For example, many companies use it for machine learning, data processing, continuous integration/continuous deployment (CI/CD), and infrastructure automation.


Let's look at a few examples and how easy they are to create and run.


{% cta-1 %}


## ‍ **Argo Workflows Examples**


#### ‍ **Getting Set up**


For many, the best way to learn how things work is to roll up their sleeves and get their hands dirty. All of the[example workflows](https://pipekit.io/blog/top-10-argo-workflows-examples) we'll cover here work, so you can follow along.


What you'll need is a K8s cluster. If you're not familiar with setting up K8s,[Docker Desktop](https://www.docker.com/products/docker-desktop) comes with a convenient Kubernetes cluster built-in. If you have another Kubernetes cluster already available, feel free to use that too.


Once you have a pod up and running, follow the[Argo Quick Start guide](https://argoproj.github.io/argo-workflows/quick-start/) , and you're ready to go.


Let's run some workflows!


#### ‍ **Hello, World!**


In accordance with prevailing custom, let's say hello to the world.


Here's the first example workflow from the[Argo Core Concepts guide](https://argoproj.github.io/argo-workflows/workflow-concepts/) . This is a simple one-step workflow:


```text


```


Let's run this before examining it line by line.


First, save the YAML to a file named {% c-line %}hello.yaml{% c-line-end %}. Then, use the Argo CLI to pass it to your Kubernetes pod. Assuming you named your pod {% c-line %}argo{% c-line-end %}, here's the command:


```text


```


(Screen refreshes several times)


```text


```


###### Your terminal will refresh a few times before the workflow completes. Where's the message? We need to check the logs.


{% c-line %}argo logs -n <pod name> @latest{% c-line-end %} **** retrieves the latest logs from your pod.


```text


```


The Docker whale says hello!


```text


```


What happened in this workflow? Let's break it down.


The first few lines identify the kind of document this file contains. An Argo workflow is a special type of K8s resource, so we need a document header to identify it.


The only user-serviceable part here is the workflow name defined by {% c-line %}generateName: hello-world-{% c-line-end %}.


```text


```


The next block, the **spec** , defines the workflow.


The first field is the {% c-line %}entrypoint{% c-line-end %}. This is the first step in the workflow. In this example, it's the one and only step.


```text


```


So, logically, the definition of {% c-line %}whalesay{% c-line-end %} follows.


**Templates** are the basic building block of Argo Workflows. In this case, we have one:


```text


```


All templates use a container. This one uses[docker/whalesay](https://hub.docker.com/r/docker/whalesay/) . When K8s starts the container, it executes the {% c-line %}cowsay{% c-line-end %} command and passes in the listed {% c-line %}args{% c-line-end %} So we get our "Hello, world!" message in the Docker logs.


That's a simple one-step job. What does running more than one job look like?


#### ‍ **Managing Multiple Steps With a DAG**


Running a single step was a great intro, but the real power in Argo Workflows comes from managing multiple steps with multiple dependencies.


This workflow uses a[directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (DAG) to establish dependencies between steps. While the name can be a little intimidating, DAGs are straightforward tools for establishing dependencies between steps in a workflow.


```text


```


Let's run this workflow.


Here are the output and the logs on my system:


The output from the running workflow shows the four steps, and the logs reflect that Argo executed each step. The logs show that they ran in numerical order this time. As we'll see below, this won't always be the case.


This workflow has two templates. The first is an {% c-line %}alpine{% c-line-end %} container that executes the {% c-line %}echo{% c-line-end %} shell command with a string passed in as an argument. So, each time this template is called, it will echo the text to the standard output, which will end up in the Docker logs.


```text


```


The next template is the DAG.


It defines four {% c-line %}tasks{% c-line-end %}. **** Each **task** uses the {% c-line %}echo{% c-line-end %} template to send its name to the Docker log. Below, you can see one template can refer to another via the {% c-line %}dependencies{% c-line-end %} field. You can also see where templates get their names. They're robust tools for implementing[DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) in your workflows. If you have some code that you need to use more than once, put it in a template.


```text


```


The working part of the DAG is in {% c-line %}tasks Second{% c-line-end %}, {% c-line %}Third{% c-line-end %}, and {% c-line %}Fourth{% c-line-end %}. Each has a {% c-line %}dependencies{% c-line-end %} field that tells Argo which {% c-line %}tasks{% c-line-end %} need to complete before it can run. Let's look at this graph as, well, a graph. We can do this in the Argo UI.


First, tell {% c-line %}kubectl{% c-line-end %} to forward the TCP port for the UI to the host operating system.


```text


```


Then, point your browser at port 2746 on the Kubernetes host. For me, that’s[http://genosha:2746](http://genosha:2746/) . You may have to tell your browser to ignore that the site isn’t secure, since it’s not running HTTPS.


Click the workflows icon.


Find the {% c-line %}dag-hello-XXXX{% c-line-end %} workflow, click on it, and then click the graph button.


You’ll see a graphic representation of your workflow.


The lines represent how Argo executes the workflow. {% c-line %}First{% c-line-end %} must be completed successfully before {% c-line %}Second{% c-line-end %} and {% c-line %}Third{% c-line-end %} can run. Only after that will {% c-line %}Fourth{% c-line-end %} commence.


{% related-articles %}


#### **Adding a Template**


If you'll pardon the pun, let's take this template one step further.


Let's add the {% c-line %}whalesay{% c-line-end %} template from the "Hello, world!" example and call it from {% c-line %}tasks Second{% c-line-end %} and {% c-line %}Fourth{% c-line-end %}.


```text


```


The output is what we expect. Although, it's worth noting that this time {% c-line %}Third{% c-line-end %} finished executing before {% c-line %}Second{% c-line-end %}. Since there are no dependencies between them, there's no guarantee that Second will run first. The order in the workflow definition is not important—only the dependencies count.


## **Argo Workflows for Your Pipelines**


In this post, we covered Argo Workflows basics. You saw how to create a basic workflow with a single step. Then we covered how to use DAGs to define more complicated workflows with multiple steps that depend on being executed in the correct order. While we walked through the examples, you learned how Argo templates are defined and reused to make up workflows.


Argo Workflows makes it easy to build complex workflows for processing large amounts of data quickly and efficiently. Put them to work on your data today!
