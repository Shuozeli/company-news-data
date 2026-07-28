---
schema_version: "1.0.0"
document_id: "c1553c68ca69b8ea27709b024c823adb58fab49ac0d21c0c594582b9ed81b0d3"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/backfill-data-argo-workflows"
published_at: "2024-08-07T12:06:59+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:59:29.484597+00:00"
content_hash: "sha256:a04cdf12027be45f680ee68acb74c5766b8c42ef6d883d667845e8e4a250419c"
---

# How to Backfill Data with Argo Workflows

Let's talk about a common challenge we face —[data backfilling](https://medium.com/riskified-technology/k8s-workflow-management-for-software-developers-using-argo-workflows-1e5247d2c4a6) . It's that pesky problem when you have a new dataset or an updated process that needs to be applied retroactively to historical data. The task can be a nightmare. But don't worry. Argo Workflows can help.


In this post, we’ll walk through setting up Argo Workflows in order to help you simplify and automate the process of data backfilling. And if you want to see Argo Workflows in action,[book some time with us](https://pipekit.io/demo-sign-up) so we can show you more.


## **What Are Argo and Argo Workflows?**


[Argo](https://argoproj.github.io/) is an open-source project that provides a set of Kubernetes-native tools for running and managing jobs and applications on[Kubernetes](https://kubernetes.io/) . It's designed to leverage the power of Kubernetes to run complex, large-scale tasks without you having to worry about the underlying infrastructure.


Argo Workflows we’ve discussed previously.[It's a workflow engine](https://pipekit.io/blog/top-10-argo-workflows-examples) for Kubernetes. It allows you to define complex data transformations, ML pipelines, or even simple CI/CD pipelines as a sequence of tasks (a "workflow"). Each task runs in its own container in an isolated environment. You define your workflows using YAML, which gives you a lot of flexibility.


### **How Does Argo Workflows Work?**


So, how does Argo Workflows work? Well, under the hood, it communicates with the Kubernetes API server, just like kubectl, the Kubernetes CLI. It creates, updates, and monitors Kubernetes resources (like Pods, CronJobs, etc.) according to your defined workflows, events, or deployments. This allows it to use all Kubernetes' features, like scaling, failover handling, and service discovery.


In essence, Argo Workflows empowers you to create complex, cloud-native applications, automating a lot of the hard work that goes into managing them. It's like having a personal assistant for your Kubernetes tasks.


Now, let’s create a workflow to backfill our data. Remember to have your Kubernetes cluster and Argo Workflows installed and running.


## ‍ **Step 1: Define Your Workflow**


First, we'll create a YAML definition file for our workflow. It's basically a roadmap that Argo Workflows follows to carry out tasks. Let's call this file **backfill-workflow.yaml** .


Here's a basic template you can start with:


```text


```


### **Breaking It Down**


Let's break down the workflow configuration in the **backfill-workflow.yaml** file.


Here, we've defined a workflow as a directed acyclic graph (DAG) of tasks. In Argo Workflows, a workflow is a series of tasks executed sequentially or in parallel, making it ideal for data processing.


Our workflow starts at the entry point, which we've named backfill-sales-data. We also have two workflow parameters, **startDate** , and **endDate** , which we will use to specify the data range to backfill.


```text


```


Next, we've defined a DAG for our backfilling task. Each task in an Argo Workflow is a template describing the steps the task should take.


```text


```


Here, the DAG consists of the fetch-data task, and the store-data task, running the fetch-sales-data and store-sales-data templates respectively. The store-data task depends on fetch-data completing successfully.


The two templates might look something like following:


```text


```


In this part of the workflow, we specify the Docker image ( **sales-data-processor:1.0** ), which contains the scripts for our data processing job. The commands given by each container’s **command** field are executed inside the Docker container with the **args** (if present); this is where you might do processing such as fetching from a database and storing on S3 storage.


## **Step 2: Create and Run the Workflow**


Next, we'll use the[argo submit](https://argoproj.github.io/argo-workflows/cli/argo_submit/) command to create and run our workflow, passing the start and end dates as arguments. This looks something like this:


```text


```


Submitting the workflow using argo submit sends our workflow to the Argo Workflow engine. By specifying the **startDate** and **endDate** parameters, we can control which data is processed in this run.


After hitting **Enter** , Argo will take the wheel and start processing your data — it does all of the heavy lifting.


When submitted, the Argo Workflow engine manages the lifecycle of the tasks. It starts them, monitors their progress, and handles any failures according to the policies defined in the workflow.


## **Step 3: Monitor Your Workflow**


You can keep an eye on your workflow's progress with the[argo get](https://argoproj.github.io/argo-workflows/cli/argo_get/) command:


argo get @latest


The Argo Workflows UI or the **argo get** command allows you to monitor the progress of your workflows and view the logs for each task.


## **Step 4: Automate the Process**


If you have to backfill data for different periods often, doing it manually every time can be quite a chore. But don't worry. There's a solution for this, too — automation! We can automate our backfilling process with Argo Workflow's cron workflows feature. CronWorkflows look very similar to a regular Workflow, but you give a **name** (rather than **generateName** ) and also define a **schedule** . The Workflow that you want to create goes under the **workflowSpec** . Argo will create a new workflow based on this **workflowSpec** at every scheduled interval.


Here's an example of what a **cron-workflow.yaml** file would look like:


```text


```


This configuration will run the backfill workflow every day at midnight. Modify the schedule field as needed to suit your needs.


To create and run the[cron](https://argoproj.github.io/argo-workflows/cli/argo_cron_create/) workflow, use the following command:


argo cron create cron-workflow.yaml


Argo will now automatically run your backfilling workflow as per the schedule.


## **Conclusion**


And there you have it! We've gone through the entire process of creating, running, and automating a data backfilling workflow using Argo Workflows. So next time you're faced with backfilling data, remember that Argo has got you covered.


‍ *This post was written by Juan Reyes. As an entrepreneur, skilled engineer, and mental health champion, Juan pursues sustainable self-growth, embodying leadership, wit, and passion. With over 15 years of experience in the tech industry, Juan has had the opportunity to work with some of the most prominent players in mobile development, web development, and e-commerce in Japan and the US.*
