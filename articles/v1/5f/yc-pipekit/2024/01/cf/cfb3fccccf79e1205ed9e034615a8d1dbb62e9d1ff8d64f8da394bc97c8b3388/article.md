---
schema_version: "1.0.0"
document_id: "cfb3fccccf79e1205ed9e034615a8d1dbb62e9d1ff8d64f8da394bc97c8b3388"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/using-helm-charts-to-deploy-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:35287859b26c15a3993574933aab0b156e3f26de78b6a8f4bf1a8f5b3bad7a39"
---

# Using Helm Charts to Deploy Argo Workflows on Kubernetes

# Using Helm Charts to Deploy Argo Workflows on Kubernetes


This article explains how to deploy Argo Workflows on Kubernetes using Helm charts.[Helm](https://helm.sh/) , a package manager for Kubernetes, simplifies the process of installing and managing complex applications on a cluster. It does so by providing[Helm charts](https://helm.sh/docs/topics/charts/) , which are preconfigured templates or Kubernetes manifests for deploying applications.


[Argo Workflows](https://argoproj.github.io/argo-workflows/) is a Kubernetes-native workflow engine that enables the creation, management, and tracking of complex workflows. These workflows can encompass a wide range of tasks, such as running machine learning models, managing CI/CD pipelines, and processing data. As a part of the[Argo Project](https://argoproj.github.io/) , it is designed specifically for Kubernetes, supporting both DAG and step-based workflows.


This article will guide you through[installing Argo Workflows](https://pipekit.io/blog/production-install-of-argo-workflows) on Kubernetes using Helm charts, discuss the challenges and considerations that come with this installation method, and provide examples to illustrate key concepts. By the end of this article, you'll have a comprehensive understanding of how to use Helm charts to deploy Argo Workflows on Kubernetes.


## What is Argo Workflows?


[Argo Workflows](https://pipekit.io/blog/what-is-argo-workflows) provides a simple and powerful way to define and execute a series of steps in a structured, repeatable, and scalable manner. Argo Workflows is built on top of Kubernetes and leverages its native features — such as pods, services, and ConfigMaps — to manage and execute workflows. It's designed to be flexible and extensible, allowing you to create custom workflows tailored to your specific use case. It supports a wide range of inputs and outputs, including files, environment variables, and Kubernetes resources. It also allows you to create, manage, and track complex workflows with multiple parallel and sequential steps, loops, and conditions.


Argo Workflows can be used in a[variety of scenarios](https://pipekit.io/blog/top-10-argo-workflows-examples) , including[CI/CD](https://pipekit.io/blog/why-teams-are-implementing-ci-cd-for-data-pipelines-using-argo-workflows) ,[building ETL pipelines](https://pipekit.io/blog/argo-workflows-etl-examples) , and[running cloud-native Spark jobs](https://pipekit.io/blog/why-teams-use-argo-workflows-to-run-cloud-native-spark-jobs) , to name but a few examples.


{% cta-1 %}


## Deploying Argo Workflows on Kubernetes Using Helm Charts


When deploying Argo Workflows on Kubernetes, Helm can be used to automate installing and configuring the necessary resources. Using Helm charts, users can define the desired state of their Argo Workflows deployment, including things like the number of replicas, resource limits, and configuration settings. This can make the deployment process more efficient and less error-prone, as users do not need to manually create and manage the necessary resources.


Helm allows for easy upgrades and rollbacks of Argo Workflows deployments. It also makes the deployment of Argo Workflows on Kubernetes more manageable and streamlined, allowing users to focus on the actual workflows and not the underlying infrastructure.


### Challenges with Helm


Using Helm to[install Argo Workflows on Kubernetes](https://pipekit.io/blog/install-argo-workflows-on-aws-gcp-azure) can make the deployment process a bit more complex than the official Argo Workflows YAML manifests, so it might be harder to manage and troubleshoot issues. Additionally, Helm has some limitations in terms of customization options and version compatibility with Argo Workflows. Namely, it’s critical to be aware that the Argoproj Helm charts are community supported so may lag behind the official releases of Argo Workflows. However, the Argo Helm community is very active and you can find help on GitHub and in the CNCF Slack channel,[#argo-helm-charts](https://argoproj.github.io/community/join-slack) . It's important that you weigh the benefits of using Helm against the potential limitations and challenges before deciding to use it.


### Prerequisites for Installation


In order to begin, it's necessary to have a Kubernetes cluster and kubectl installed and configured for access to the cluster. A local cluster is sufficient for initial setup and testing; possible local Kubernetes cluster options include minikube, kind, k3s or k3d, and Docker Desktop. You also need Helm and the Helm CLI.


#### Installing minikube


This example uses minikube, and its latest version at the time of writing is v1.28.0. You can download and install minikube by following the instructions[here](https://minikube.sigs.k8s.io/docs/start/) .


Once minikube is installed, start the cluster and check its status:


```text


```


#### Installing kubectl


kubectl, the Kubernetes command line tool, is required to interact with the cluster. At the time of writing, the latest version of kubectl is v1.26.0. You can download and install kubectl by following the instructions[here](https://kubernetes.io/docs/tasks/tools/#kubectl) .


#### Installing Helm and the Helm CLI


Now, install Helm and the Helm CLI. At the time of writing, the latest version of Helm and the Helm CLI is v3.11.0. You can download and install Helm by following the instructions[here](https://helm.sh/docs/intro/install/) .


Verify that Helm and kubectl are working by running the following command:


```text


```


### Installing Argo Workflows without Helm


Before continuing to learn how Argo Workflows is installed with Helm, it's worth looking at how the installation would work without Helm charts.


The following command will create a namespace and will install Argo Workflows version 3.4.4 using the installer manifests:


```text


```


Use the following code to patch the Argo server authentication and get it started (you can find more on this[here](https://argoproj.github.io/argo-workflows/quick-start/) ):


```text


```


Run the {% c-line %}port-forward{% c-line-end %} command on local to access the UI:


```text


```


This will serve the UI at[https://localhost:2746](https://localhost:2746/) , as shown in the following image:


Argo Workflows running


**Note:** Ignore the SSL error on localhost and proceed securely in your web browser.


### Installing Argo Workflows with Helm


Now that you've seen how the installation normally works, this section demonstrates how Helm charts simplify the process.


Argo Helm charts are available from two sources:[Bitnami](https://bitnami.com/stack/argo-workflows/helm) and the[Argo Project GitHub page](https://github.com/argoproj/argo-helm) .


The instructions for installation using the Bitnami chart are as follows:


```text


```


The instructions for installation using the community-managed[Argo Helm chart](https://github.com/argoproj/argo-helm) are as follows:


```text


```


In order to disable the authentication of Argo server for purposes such as running in local dev-mode, you can add values in the helm installation.


```text


```


You can also download and edit the Argo Workflow default[values.yaml](https://github.com/argoproj/argo-helm/blob/main/charts/argo-workflows/values.yaml) and use it with Helm install.


```text


```


## Argo Workflows Data Processing Example


After completing the installation steps for Argo Workflows, you can dive into a practical example workflow to better understand its functionality. This example will take you through a data processing use case, where the workflow will process a file containing IP addresses. Each task in the workflow, including generating the IP file, processing the IP file, counting the IP addresses, and deleting the files, performs a specific action. By the end of this example, you'll have a better grasp of how Argo Workflows can automate complex tasks and orchestrate multiple steps in a workflow.


The Argo workflow is defined in a YAML file {% c-line %}dataprocessing-workflow.yaml{% c-line-end %} , which outlines multiple steps or tasks executed by containers running in Kubernetes pods:


```text


```


The workflow above has three steps with dependencies:


- {% c-line %}generate-ips{% c-line-end %} generates 200 random IP addresses and writes them to a file named {% c-line %}ips.txt{% c-line-end %}
- {% c-line %}process-ips{% c-line-end %} processes the generated IP addresses from {% c-line %}ips.txt{% c-line-end %} and creates the counter.
- {% c-line %}delete-ips{% c-line-end %} deletes the generated {% c-line %}ips.txt{% c-line-end %} file.


The tasks are connected in a[directed acyclic graph](https://argoproj.github.io/argo-workflows/walk-through/dag/) (DAG), with dependencies between the tasks specified in the YAML file. This structure simplifies the maintenance of complex workflows and maximizes parallelism when executing tasks.


As an example, in the workflow, the {% c-line %}generate-ips{% c-line-end %} step runs first, as it has no dependencies. Upon completion of {% c-line %}generate-ips{% c-line-end %}, the {% c-line %}process-ips{% c-line-end %} step runs, which is dependent on the completion of {% c-line %}generate-ips{% c-line-end %}. Finally, {% c-line %}delete-ips{% c-line-end %} can run once both {% c-line %}generate-ips{% c-line-end %} and {% c-line %}process-ips{% c-line-end %} have finished.


### Argo Workflow Architecture


The following image illustrates the architecture behind the execution of an Argo workflow, including the real-world example in the previous section:


Argo workflow architecture


The Argo workflow architecture has three main components:


1. A Kubernetes cluster running Argo Workflows, which acts as the orchestration platform for the workflow.
2. A set of Kubernetes pods, each running a container that performs a specific task in the workflow, such as generating the IP file, processing the IP file, or counting the IP addresses.
3. A set of Kubernetes services, used to expose the pods to each other and to the outside world so that they can communicate and exchange data.


### Submitting Workflow to Argo


You can submit your {% c-line %}dataprocessing-workflow.yaml{% c-line-end %} workflow either via the GUI accessible at[https://localhost:2746/workflows](https://localhost:2746/workflows) or by using the Argo CLI client.


To use the Argo CLI, download the latest version of it from the[releases page](https://github.com/argoproj/argo-workflows/releases) , then submit your workflow using the following command:


```text


```


Once the workflow is submitted, it will start processing the steps or DAGs accordingly.


This is how the completed workflow looks in the GUI:


Argo workflow completed


{% related-articles %}


## Conclusion


The article provided step-by-step instructions for installing Argo Workflows using Helm charts. Overall, Argo Workflows is a valuable tool for managing and automating tasks in Kubernetes that can be easily installed and managed using Helm charts.


Additionally, if you'd like to save time writing and maintaining Helm charts for Argo Workflows, consider[Pipekit](https://pipekit.io/) . It's a powerful tool that makes it easier to use Argo by managing your Argo Workflows deployment for you. With Pipekit, you can focus on the important tasks of designing and implementing your pipeline without worrying about the details of Helm chart creation and maintenance.
