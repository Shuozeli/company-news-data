---
schema_version: "1.0.0"
document_id: "ad3caa8c9dcce6fe599e032161cfb09dcf2f1ad78c6908e7ce6cb3daecaa89cd"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/what-to-consider-before-migrating-to-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:18.654833+00:00"
content_hash: "sha256:7406fda6bbe7114e053887d12744af6ff7502ca981663ba8d45cfae73b0d62b0"
---

# What to Consider before Migrating to Argo Workflows

[Argo Workflows](https://argoproj.github.io/argo-workflows/) is an open source tool for running and managing container-based workflows on Kubernetes. Argo Workflows allows users to define and manage complex workflows as a collection of interconnected steps. It's worth considering migration if you currently use a different workflow engine that does not support Kubernetes or want to take advantage of the advanced features provided by Argo Workflows, such as parallel execution and dynamic and nested workflows. Additionally, Argo Workflows may be a good option for anyone who is looking for a more efficient way to manage and automate their Kubernetes operations.


In this article, you'll learn about the features and benefits of Argo Workflows, as well as its use cases. The article also discusses the factors to consider before migrating to Argo Workflows. Finally, the article provides a short tutorial on how to install[Argo Events](https://argoproj.github.io/argo-events/) .


## What Is Argo Workflows and What Are Its Advantages?


Workload management before and after Pipekit, adapted from original diagrams from Pipekit


[Adapted from original images courtesy of Pipekit](https://pipekit.io/)


Argo Workflows provides a simple and powerful way to define and execute complex multistep pipelines by offering built-in support for dependencies, parallelism, and error handling. It allows users to define and execute complex multistep and multinode workflows as Kubernetes objects. Argo Workflows can manage the entire lifecycle of a workflow, including the steps of creating, submitting, monitoring, and troubleshooting a workflow.


In Argo Workflows, a workflow is defined using a YAML-based configuration file. This file describes the steps that have to be executed, as well as the required dependencies and other configuration options. Once the workflow is defined, it can be created and submitted for execution on a Kubernetes cluster. Once the workflow is running, Argo Workflows provides various ways to monitor its progress — for example, through a web-based UI, via a command line interface, or by querying the Kubernetes API. This way, information on the status of individual steps, the overall progress of the workflow, and any logs or outputs produced by the workflow can be monitored. If failures or errors are encountered in the workflow, Argo provides tools for troubleshooting the issue. The user can inspect the logs and outputs of the failed step and retry or skip failed steps. Additionally, Argo also provides error-handling capabilities like retries, backoff, timeout, etc.


In general, Argo Workflows is a strong solution for any organization that has to handle complex workflows that must be scaled and that require consistent and efficient automation and management. Argo Workflows is especially useful when you want to leverage the benefits of Kubernetes, such as scalability, high availability, and integration with other tools.


### Use Cases for Migrating to Argo Workflows


The following are a few[examples of when migrating to Argo Workflows](https://pipekit.io/blog/top-10-argo-workflows-examples) would be beneficial:


- **CI/CD pipelines:** Argo Workflows can be used to automate and scale the process of building, testing, and deploying code changes. This can help improve the speed and reliability of the software development process. Furthermore, CI/CD helps reduce the number of errors by catching them early in the development cycle through automated testing.[Here’s an example of basic CI leveraging Argo Workflows.](https://github.com/pipekit/argo-workflows-ci-example)
- **ETL and data analytics:** Argo Workflows can be used to automate and scale the process of extracting, transforming, and loading data from various sources. This can help improve the efficiency and accuracy of data analysis and reduce the risk of errors.
- **Data processing pipelines:** Argo Workflows can be used to automate and scale the processing of large amounts of data.


{% cta-1 %}


## Should You Migrate to Argo Workflows?


As previously mentioned, migrating to Argo Workflows can have many advantages. However, there are a few important factors you should consider before making the switch.


### Containers and Cloud-Native Knowledge and Experience of the Team


Before migrating to Argo Workflows, it's important to consider your team's experience with and knowledge of containers and cloud-native technologies. Argo Workflows is based on Kubernetes and uses containers to run and manage workflow steps. This means that a team already familiar with container technologies will likely find it easier to adapt to Argo Workflows.


### Kubernetes Knowledge and Experience of the Team


It's important to evaluate the Kubernetes expertise of your team before transitioning to Argo Workflows. Since it operates within the Kubernetes ecosystem, a team that is already familiar with Kubernetes will be better equipped to understand and utilize the features and functionality of Argo Workflows. Furthermore, since Argo Workflows uses Kubernetes resources ([such as pods and services](https://pipekit.io/blog/clean-up-pods-save-logs-argo-workflows) ) to run workflows, it's important to understand how these resources work and how to manage them within a Kubernetes cluster. Additionally, a good understanding of Kubernetes concepts (such as namespaces and RBAC) will be useful for managing access and permissions to Argo Workflows in the cluster.


### Organizational Structure: Kubernetes Might Need a DevOps Structure


You should also consider that Kubernetes may require a DevOps approach. Kubernetes, as an infrastructure orchestration tool, can be used to manage a large number of containers and services across a cluster of servers.


Kubernetes is quite a complex tool where multiple components need to be managed and coordinated, so a DevOps structure may be beneficial. In this context, DevOps practices like continuous integration, continuous delivery, and infrastructure as code can be used to ensure efficient and effective deployment, scaling, and management of applications on a Kubernetes cluster.


### Declarative Configuration and Workflows


Prior to moving to Argo Workflows, it's important to keep in mind that the workflows are configured using YAML. To ensure a successful migration, it's essential to have a clear understanding of how to write accurate YAML configurations that define a desired workflow, including tasks, dependencies, inputs, and outputs. Additionally, it's important to verify that any custom resources referenced in the YAML configurations are properly defined and supported by Argo Workflows.


### Deploying Argo Workflows to Your Cluster


Deploying Argo Workflows to your cluster is another important step that must be considered when migrating to it. As Argo Workflows is a Kubernetes-native tool, it needs to be installed and configured within your cluster to properly function. You need to ensure that your existing infrastructure, including your Kubernetes version, network connectivity, and resources, is compatible with Argo Workflows.


### Manageability: What Happens If You Need to Have a Multicluster Argo Structure?


Having multiple clusters can complicate the Argo Workflows migration process because each cluster will need to be configured and connected to the Argo Workflows system separately. Additionally, any workflows that are being migrated will need to be adapted to work across multiple clusters. This can add complexity and require additional development work. It may also require additional tooling and automation to ensure that data and resources are properly synced between clusters.


### Observability and Security: Monitoring, Logging, Security, Secrets Storage


Monitoring, logging, security, and secrets storage are important things to consider when migrating to Argo Workflows. Monitoring allows you to observe the status and performance of the workflow. Logging enables the tracking of events and the troubleshooting of any issues that may arise. Security controls access to the workflow and its resources, and secrets storage provides a secure way to store sensitive information used in the workflow, such as passwords, tokens, and other credentials. Without proper consideration and implementation of these elements, the workflow may not function correctly or may be vulnerable to security breaches.


{% related-articles %}


## How Do You Install Argo Workflows?


The first step in installing Argo Workflows is to install the Argo CLI. Instructions for doing so on a Mac are included below, or you can use {% c-line %}brew install argo{% c-line-end %}. You can find the setups for other operating systems[here](https://github.com/argoproj/argo-workflows/releases/tag/v3.2.8) .


Start by running this command:


```text


```


Then, verify the installation:


```text


```


Next, you will create an Argo namespace and deploy the Argo Controller as a Kubernetes {% c-line %}CustomResourceDefinition{% c-line-end %}:


```text


```


Here’s the output:


```text


```


Argo needs to communicate with Kubernetes resources using the Kubernetes API, and for that purpose, it will use a ServiceAccount to authenticate itself to the Kubernetes API. You’ll also want to configure RoleBinding by specifying the role (i.e., permission to a ServiceAccount) that Argo will use for its operation. The following command will grant the admin privileges to the default ServiceAccount of your Argo namespace:


```text


```


Then, you’ll connect to Argo UI. For the sake of this tutorial, you’ll be using a {% c-line %}port-forward{% c-line-end %} since you are working on a local Minikube instance. A complete, production-ready setup requires some extra network configurations:


- A domain name registered (like {% c-line %}argo.companyname.com{% c-line-end %}) so users can access Argo Workflows via a URL
- A Kubernetes Ingress object to connect the Argo server to that domain
- SSL configuration to secure communication with the server


The network configuration is very important, as it will help you secure your Argo Workflows. Since the CI server has access to so many elements in your infrastructure, it is worth hardening its security.


Now, let’s get back to your configuration and set up a {% c-line %}port-forward{% c-line-end %} so you can access the UI:


```text


```


You can now access the Argo UI at the[https://127.0.0.1:2746/](https://127.0.0.1:2746/) URL in your browser. Initially, you might see the following error on the login screen after accessing the URL. If so, you will be asked to log in with SSO or an Argo auth token.


Error image


To get the auth token for login, you’ll need to run the {% c-line %}kubectl -n argo exec argo-server-${POD_ID} -- argo auth token{% c-line-end %} command — or {% c-line %}argo auth token{% c-line-end %}, if you have the Argo CLI installed. Copy and paste the output of the command in the box on the login screen, as pictured here:


Login screen


## ## Conclusion


Argo Workflows is an open source tool for running and managing container-based workflows on Kubernetes. The tool allows users to define and manage complex workflows as a collection of interconnected steps and provides features such as parallel execution and support for multiple clusters. Organizations that are currently using a different workflow engine that does not support Kubernetes or that are looking for a more efficient way to manage and automate their Kubernetes operations may benefit from migrating to Argo Workflows. However, before migrating, it's important to consider factors such as the team's container and cloud-native experience, organizational structure, and manageability of Argo Workflows.


Pipekit homepage


‍


[Image courtesy of Pipekit](https://pipekit.io/)


[Pipekit](https://pipekit.io/) is an open source project that extends the functionality of Argo Workflows. Pipekit adds extra features and functionality to Argo Workflows, which can help to improve the efficiency, reliability, and security of your workflows, making it a more powerful and valuable tool for automating and scaling complex processes.


In particular, using Pipekit with Argo Workflows results in improved manageability and a better user experience. Pipekit provides an easy-to-use, declarative syntax for creating workflows that simplify the management process. Additionally, one of the key features of Pipekit is enhanced observability and security with detailed logging and monitoring, as well as built-in security features like secrets management and role-based access control. These capabilities make it easier to identify and troubleshoot issues and ensure compliance with industry regulations.
