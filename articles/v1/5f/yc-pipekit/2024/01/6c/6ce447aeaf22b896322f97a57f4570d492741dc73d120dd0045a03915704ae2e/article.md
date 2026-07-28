---
schema_version: "1.0.0"
document_id: "6ce447aeaf22b896322f97a57f4570d492741dc73d120dd0045a03915704ae2e"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/set-up-logging-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:18.654833+00:00"
content_hash: "sha256:89e038db189ffa432edd398bd362746822f35e927b3669a702583c33accee2f3"
---

# How to Set up Logging for Argo Workflows

Argo Workflows, which is among the most used open source tools in Kubernetes, orchestrates workflows in parallel. Since these tasks are often intensive and complex, setting up logging in[Argo Workflows can help you](https://pipekit.io/blog/top-10-argo-workflows-examples) keep track of executed jobs, collect metrics for later analysis, and troubleshoot any problems.


Because logs are such a crucial part of using Argo Workflows, you should be sure to store them properly so you can easily access them. This tutorial will show you how to set up logging in Argo Workflows using two techniques: artifact repositories and log exporters.


## Options for Logging in Argo Workflows


There are two main ways you can use to extract and store logs in Argo Workflows.


1. Use an object storage solution, like MinIO, AWS S3, or GCP GCS
2. Use a log exporter solution, like Fluentd or LogDNA


### Store Logs Using Object Storage


The first option is to use object storage to make a global[artifact repository](https://pipekit.io/blog/configure-artifact-repo-argo-workflows) . Argo supports multiple out-of-the-box S3-compatible object storage services, including AWS, GCS, and MinIO. This gives your workflows several advantages, including the following:


- You can pass data between pods at will, because nodes in a Kubernetes cluster can simultaneously access S3-compatible repositories.
- Since major cloud providers offer S3-compliant object storage, this method gives you great flexibility in multi-cloud and hybrid cloud deployments.
- Thanks to the shared storage provided by artifact repositories, you can run parallel container steps in your Argo Workflows.


While using an artifact repository to store logs is a sound solution, it also has some limitations. T, the biggest challenge with this option is its dependency on cloud object storage providers, which might introduce an additional layer of complexity depending on your use case. That said, MinIO is an option for scenarios in which you require on-premise installs that don’t depend on a public cloud provider.


{% cta-1 %}


### Store Logs Using a Log Exporter and ELK Stack


You’re not required to use an artifact repository to store logs, though, because Argo is flexible enough to give you other options. You could also use tools like Fluentd or LogDNA to export your logs to an ELK stack. That path provides the following benefits:


- It decouples data sources from backend systems by providing a unified logging layer in the middle.
- It uses the same data collector for app logs, alerting logs, access logs, and databaseDB logs, among others.
- Data consumption and analysis are easier, because a unified platform is used for all its systems.


There are many advantages to using a log exporter, but it might not be the most viable solution in some cases. Limitations of this approach include:


- You must install an agent on each node, which might hurt performance. When using artifact repositories, you only need one node to orchestrate object storage sharing.
- Because agents are required in each node, that greater complexity can make it more difficult to scale the infrastructure on demand. This is not an issue when using artifact repositories.


### Setting up Logging in Argo Workflows


To illustrate both of the above log generation methods, you’re going to set up a basic Argo Workflow.


### Prerequisites


You’ll need the following for this tutorial:


1. A functional Kubernetes cluster. For this, you can use[Docker Desktop](http://pipekit.io/blog/argo-workflows-with-docker-desktop) ,[K3s](http://pipekit.io/blog/how-to-run-argo-workflows-in-k3s) ,[minikube](https://minikube.sigs.k8s.io/docs/start/) , or any other Kubernetes distribution of your choice.


1. The[Kubectl command-line tool](https://kubernetes.io/docs/reference/kubectl/) properly configured on your local machine to access the Kubernetes installation. Follow[these instructions](https://kubernetes.io/docs/tasks/tools/) to install kubectl on your workstation.
2. The most recent release of the Argo CLI installed on your local machine.[Check the instructions](https://github.com/argoproj/argo-workflows/releases) to install the Argo CLI on Windows, macOS, or Linux.


### Setting up Argo Workflows


Create a new namespace. Although this step is not necessary, it does keep the elements in this example separate from other workloads you may have in Kubernetes.


This example uses argo, but you can use any name you like:


```text


```


Next, deploy a basic Argo Workflow. The easiest way to do this locally is to use the[Quick Start](https://argoproj.github.io/argo-workflows/quick-start/) manifest, which will install Argo Workflows along with some components. Assuming your namespace is called argo, run the following command:


```text


```


Depending on the speed of your internet connection, the installation may take a few minutes. To check the status, run the following command:


```text


```


You will know the installation is complete when all pods are running.


```text


```


As you can see, the Quick Start manifest creates four pods: the Argo server, the Workflow controller, MinIO, and PostgreSQL. This manifest includes the benefit of configuring Argo Workflows to use the MinIO distributed object storage server. That makes this deployment convenient for learning how Argo Workflows uses artifact repositories to store logs.


### Storing Logs Using an Artifact Repository


Now that Argo Workflows is installed, it’s time to explore the logging methods using a sample workflow. Create a hello.yaml file using your favorite text editor and paste the following content:


```text


```


This deployment introduces the definitions *Workflow* and *templates* , which are used by Argo to automate and execute tasks within Kubernetes. In this example, the popular whalesay container is used to showcase a simple task. You can find more information about Argo’s Workflow Templates[in the documentation](https://argoproj.github.io/argo-workflows/workflow-templates/) .


Save the file, then use the following command to submit the task:


```text


```


Note that the optional --watch flag is used to watch the workflow as it runs, which will display messages showing the progress of the task. For more information about the argo command-line interface and the available options, you can[read the documentation](https://argoproj.github.io/argo-workflows/cli/argo/) .


Once the task is complete, you’ll see an output similar to the following:


Argo Workflow sample running


You can check the status of the task using the following command:


```text


```


This command should show on the console that the workflow was completed successfully:


```text


```


If you prefer, you can also check the pods in the argo namespace:


```text


```


The output should be similar to the one shown below:


```text


```


Since the workflow was successfully completed, it’s time to view the logs. Argo makes this easy using the command:


```text


```


The above command displays the latest logs collected in the artifact repository. The output should be similar to this:


Whalesay sample workflow


You have learned how to set up a simple workflow and how to view the logs stored in the artifact repository. For this example, all the components were pre-configured by the Quick Start manifest.


To learn more about how to configure artifact repositories, read the post[How to Configure an Artifact Repo for Argo Workflows](http://homepage.pipekit.io/blog/configure-artifact-repo-argo-workflows) as well as the[Argo documentation](https://argoproj.github.io/argo-workflows/configure-archive-logs/) .


{% related-articles %}


### Storing Logs Using a Log Exporter


As noted earlier, using a log exporter allows you to collect logs from components other than Argo Workflows. However, depending on your use case, the added complexity can be challenging.


To take advantage of Fluentd, for instance, you need to first set up a logging stack like EFK (Elasticsearch, Fluentd, and Kibana); otherwise, you won’t be able to collect the logs. This implementation can become complex, considering that you must install a Fluentd agent on each node. If you are interested in setting up an EFK logging stack, check[this tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes) for details.


If you prefer a cloud-based solution, LogDNA might be a better alternative. After registering your account and obtaining your ingestion key, you can install a LogDNA agent using the commands:


```text


```


Once the agent is installed, you can configure it by modifying the /etc/logdna/config.yaml file so that it collects the Kubernetes events you want, including Argo Workflows. To learn about the available options, read[LogDNA’s documentation](https://github.com/logdna/logdna-agent-v2/blob/3.2/docs/README.md#configuration) .


Regardless of which log exporter you prefer, keep in mind that the configuration process will be more complex than using an S3-compatible artifact repository to store your logs.


## Conclusion


Using logs in Argo Workflows can help you optimize your work on your Kubernetes projects. As you learned, there are two ways to set up logs—storing logs in artifact repositories and using log exporters. Each option offers advantages and disadvantages, depending on your use case.


Along with properly storing your Argo Workflows logs and metrics, you should also optimize the way you trigger workflows across multiple clusters.[Pipekit](https://pipekit.io/) , a single-plane workflow management tool for Argo Workflows, can help you more easily orchestrate multi-cluster workloads and quickly create and scale large data pipelines.
