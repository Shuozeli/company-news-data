---
schema_version: "1.0.0"
document_id: "214dd78f24ab4a9abe23fed841e6a3222b364f20ac57afc14c887e1b5c895857"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/how-to-integrate-prometheus-with-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:79dc360a2acc40495ba82f8349143ab464509c90293af06b69cc1d9cf7ed3e72"
---

# How to Integrate Prometheus with Argo Workflows

Kubernetes is well-known for being complex, but fortunately, tools like[Argo Workflows](https://argoproj.github.io/argo-workflows/) can help you orchestrate parallel jobs on the platform. It’s a free, open-source workflow manager that defines workflows in a container-native way, models complex workflows as a simple list of tasks, performs compute-intensive jobs for ML or[Big Data](https://pipekit.io/blog/dask-argo-workflows-big-data) , and seamlessly integrates with modern CI/CD tools.


Sounds awesome, right? But defining and deploying workflows is only part of the process. You have to monitor your clusters rigorously to ensure service uptime and application health.


Here comes[Prometheus](https://prometheus.io/) . A reliable tool for gathering Kubernetes metrics and setting up automated alerts, Prometheus is lightweight, blazing fast, and highly scalable. It’s one of the most popular monitoring tools for engineers for good reason.


In this article, you'll learn how to integrate Prometheus with your[Argo Workflows instance](https://pipekit.io/blog/top-10-argo-workflows-examples) and capture metrics related to workflows and templates.


## Implementing Prometheus with Argo Workflows


First, you'll need to set up and configure Argo Workflows, CLI, and Prometheus.


However, since Argo Workflows is a workflow manager for Kubernetes, you also need a Kubernetes cluster and access to the {% c-line %}kubectl{% c-line-end %} command. Using a local Kubernetes cluster is fine for the purposes of this article. You may choose one of the following to set up your own local cluster:


- [minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kind](https://kind.sigs.k8s.io/)
- [k3s](https://k3s.io/) or[k3d](https://k3d.io/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)


This tutorial uses kind for this demonstration. But you can use any cluster of your choice.


{% cta-1 %}


### Install and Configure kind


[kind](https://kind.sigs.k8s.io/) is a local cluster for running and testing Kubernetes. You can use it to implement your Argo Workflows and integrate Prometheus metrics. If you're on Linux, use the following commands to install kind:


```text


```


You can install kind on Windows and macOS following their[quick start guide](https://kind.sigs.k8s.io/docs/user/quick-start/) .


After installation, verify it using the {% c-line %}kind version{% c-line-end %} command. Then go ahead and create your first Kubernetes cluster. However, since kind utilizes Docker, make sure it's running. Then you can create your cluster by running the kind create command.


```text


```


This creates a Kubernetes cluster in your local machine where you can install Argo Workflows and Prometheus. After that, install the {% c-line %}kubectl{% c-line-end %} CLI to access and manage your cluster resources.


```text


```


These commands install {% c-line %}kubectl{% c-line-end %} on Linux. Follow the Kubernetes doc to[install kubectl on other operating systems](https://kubernetes.io/docs/tasks/tools/) .


You will also[need to install helm](https://helm.sh/docs/intro/install/) .


### Install and Deploy Argo Workflows


You can install Argo Workflows in multiple namespaces, either in a cluster or in a scoped namespace. This tutorial installs Argo Workflows in a namespace-scoped configuration.


First, create the argo namespace using the following {% c-line %}kubectl{% c-line-end %} command.


```text


```


Then use the {% c-line%}namespace-install.yaml{% c-line-end %} manifest to install Argo Workflows inside the argo namespace.


```text


```


Now, you can wait for the Argo Workflow Controller to deploy; it's the component that interacts with your clusters. You can configure it to observe a single namespace or all cluster namespaces.


```text


```


### Install the Argo CLI


The Argo CLI exposes many useful commands for submitting, viewing, running, and deleting workflows. You can also use {% c-line %}kubectl{% c-line-end %} for those. But the CLI requires less typing and offers syntax checking, among other features.


```text


```


This command downloads the Linux CLI binary from the[GitHub releases](https://github.com/argoproj/argo-workflows/releases) page. The following commands unpack the file, set up execute permission, and move the file.


```text


```


The same releases page describes the mac installation instructions.


### Create a Sample Workflow


Now that you've got a running cluster alongside Argo Workflows and the CLI, it's time to run some workflows. This step will also generate the data needed for Prometheus metrics.


Let’s use a basic workflow to keep this guide short. Create a file in your current directory called {% c-line %}hello-world.yaml{% c-line-end %} and populate it with the following snippet.


```text


```


Save this file and run the following command to submit it as an argo workflow:


```text


```


### Set Up Prometheus


Now, you can finally integrate Prometheus with your[Argo Workflows instance](https://pipekit.io/blog/top-10-argo-workflows-examples) . There are several ways to deploy Prometheus in a Kubernetes cluster. This tutorial uses the[kube-prometheus-stack](https://github.com/prometheus-operator/kube-prometheus) Helm Chart, as it'll make the deployment quick and simple.


Run the following {% c-line %}kubectl{% c-line-end %} and {% c-line %}Helm{% c-line-end %} commands to complete the setup process.


```text


```


{% c-line %}--set prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues=false{% c-line-end %} simply tells Prometheus to look across all namespaces to gather metrics. By default, it wouldn’t look at the {% c-line %}argo{% c-line-end %} namespace.


### Find and Integrate Metrics from Argo Workflows


You're now ready to collect metrics from your Argo Workflows using Prometheus. Argo supports the primary Prometheus metric types, such as:


- **Counter.** Informs the number of times an event took place
- **Gauge.** Informs of things like workflow duration
- **Average.** Informs internal metrics, like error rate


Argo exposes several metrics that inform the controller's state at any time. You can also define custom metrics based on your requirements.


The default controller metrics include the four golden signals of monitoring: latency, traffic, errors, and saturation. You can learn more about different[Argo Workflows metric types in the documentation](https://argoproj.github.io/argo-workflows/metrics/) .


Since you're responsible for defining custom metrics, emitting them is also your responsibility. Moreover, remember that these data are temporary when emitting metrics from your Argo Workflows for Prometheus.


You should not emit historical data to Prometheus — only data that inform the current state. oing this will allow you to build effective time-series monitoring data for Prometheus. You can later use this with Grafana for building powerful visualization dashboards.


We must deploy a service that points to the monitoring port of the workflow controller (9090). We can then use a ServiceMonitor to get Prometheus to use that service as a metrics target.


Create a file called {% c-line %}workflow-controller-metrics-servicemonitor.yaml{% c-line-end %} and copy the following snippet to it:


```text


```


Save this file and run the following command to create {% c-line %}ServiceMonitor{% c-line-end %}:


```text


```


You may need to wait a few minutes before Kubernetes and Prometheus detect the changes.


{% related-articles %}


### Visualize Argo Metrics in Prometheus


You can visualize the metrics exposed by {% c-line %}workflow-controller-metrics{% c-line-end %} via the Prometheus dashboard. But first, you need to expose the Prometheus dashboard to a local port so that you can view it.


```text


```


Open a web browser and go to {% c-line %}http://localhost:9090{% c-line-end %}. Click on the **Status** dropdown menu and then **Service Discovery** , and you should see an {% c-line %}argo/workflow-controller-metrics/0{% c-line-end %} entry.


prometheus-service-discovery


Navigate to **Status** and then to **Targets** to verify that the {% c-line %}workflow-controller-metrics{% c-line-end %} is up and running.


prometheus-target-section


The **Graph** page provides robust graphs to help better visualize the metrics. You can enter various expressions such as {% c-line %}argo_workflows_count{}{% c-line-end %} and {% c-line %}argo_workflows_queue_depth_count{}{% c-line-end %} to evaluate the health of your service.


prometheus-graph


## Conclusion


[Argo Workflows](https://argoproj.github.io/argo-workflows/) is a workflow engine for orchestrating parallel jobs in a Kubernetes cluster. Prometheus is a monitoring tool that effectively collects metrics from Kubernetes. These two tools are widely used together, with Prometheus monitoring Argo Workflows.


However, with new tech comes new responsibilities. If you have a small team or developers already working on multiple tasks, you may not want them to take time away from their core focus in order to learn new tools.


Instead, consider using a dedicated solution like[Pipekit](https://pipekit.io/) . An open-source workflow engine, Pipekit takes care of the details for you and gives you production-ready Argo Workflows pipelines in minutes. Manage and visualize your pipelines with its simple-to-use control plane, enjoy access to enterprise-grade support, and keep your data safe.
