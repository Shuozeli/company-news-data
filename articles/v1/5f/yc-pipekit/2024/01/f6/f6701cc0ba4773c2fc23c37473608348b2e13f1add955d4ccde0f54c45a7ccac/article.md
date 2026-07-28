---
schema_version: "1.0.0"
document_id: "f6701cc0ba4773c2fc23c37473608348b2e13f1add955d4ccde0f54c45a7ccac"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-workflows-with-docker-desktop"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:00:19.733210+00:00"
content_hash: "sha256:98fa0f92ad6b6b6259a02f8c9fefa489a59e719fc5461cfbb2e0061ffe5a7f78"
---

# How to Run Argo Workflows with Docker Desktop

[Argo’s](https://argoproj.github.io/) ecosystem of Kubernetes-based open source tools is increasingly popular in the cloud-native community because the tools can be combined to create powerful Kubernetes-native workflows, rollouts, and continuous delivery (CD) tasks.


*Argo Workflows* is a workflow engine used to create, manage, and orchestrate parallel jobs in Kubernetes. These workflows are implemented as Kubernetes {% c-line %}CustomResourceDefinitions{% c-line-end %} (CRDs) and enable you to carry out functions such as the following:


- Define container-based steps in workflows
- Execute compute-intensive extract, load, transform (ELT) operations, machine-learning tasks, and data processing tasks
- Create Kubernetes-native CI/CD pipelines


In this tutorial, you’ll learn how to deploy Argo Workflows to a Kubernetes cluster in[Docker Desktop](https://www.docker.com/products/docker-desktop/) .


## About Argo Workflows


Argo Workflows offers a number of useful features, including the following:


- Web-based UI
- Native artifact support (MinIO, S3, Artifactory, HDFS, OSS, HTTP, Git, GCS, raw)
- Templating and cron workflows
- Workflow archive
- REST API, Argo CLI


The {% c-line %}Workflow{% c-line-end %} resource is used to define the execution of a workflow as well as its storage state. Workflows consist of instructions that operate like functions, known as *templates* in Argo.


Templates detail the steps of execution in the workflow. The {% c-line %}spec{% c-line-end %} is the most important part of the {% c-line %}Workflow{% c-line-end %} manifest file. There are two sections to the spec:


- **Templates:** This is where you define the different types of templates you want to use.
- **Entrypoint:** The entrypoint determines which template will be used first.


A template can be any of the following:


- **Container:** This is probably the most common template type, and as the name implies, it schedules a container. Its spec is identical to that of a Kubernetes container spec.
- **Script:** This is a convenience wrapper around the container. The spec is the same as the container, but it has a {% c-line %}source{% c-line-end %} field that allows you to define a script. The script will be saved to a file and executed from there.
- **Resource:** This template can be used to perform create, read, update, delete (CRUD) operations directly on resources in the cluster.
- **Suspend:** This template is used to suspend the execution of a workflow either for a specified duration or indefinitely.
- **Directed Acyclic Graph (DAG):** This template allows you to define the tasks in a workflow as a graph of dependencies.
- **Steps:** This template allows you to define the tasks in your workflow as sequential steps. It consists of inner and outer lists; inner lists run in parallel, while outer lists run one after the other.


## Prerequisites


In order to do this tutorial, you’ll need the following:


- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- Enable Kubernetes in Docker Desktop
- Increase memory resource allocation to at least 12 GB (for[MinIO](https://min.io/) )
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)
- [K9s](https://k9scli.io/) (optional)


## Running Argo Workflows Using Docker Desktop


Once you have your prerequisites, open Docker Desktop and begin.


{% cta-1 %}


### Connecting to Kubernetes Cluster


Once Docker Desktop is running, go to the preferences menu to increase memory resource allocation to at least 12 GB and enable Kubernetes. When your cluster is up, make sure that you’re connected to the {% c-line %}docker-desktop{% c-line-end %} Kubernetes cluster.


Docker Desktop resource allocation


‍


Docker Desktop


Run the below commands to list, select, and verify the cluster context, respectively:


```text


```


‍


Cluster context view in K9s


### Installing Argo CLI


The next step will be to install the Argo CLI. You can either use the latest version or select a previous one from the[Argo releases GitHub page](https://github.com/argoproj/argo-workflows/releases) . The commands you run may vary depending on your operating system. The two code blocks below are for Mac and Linux, respectively. If you are using Windows, you can download the relevant executable from the **Assets** section of the releases GitHub page.


For Mac:


```text


```


For Linux:


```text


```


#### Installing Argo Controller and UI


Before installing the Argo Workflow resources, you need to create an {% c-line %}argo{% c-line-end %} namespace:


```text


```


To access the Argo Workflows UI, you will need to expose it. This can be done in multiple ways, but for this tutorial, use the[port-forwarding method](https://argoproj.github.io/argo-workflows/argo-server/#kubectl-port-forward) :


```text


```


Open your browser and go to[https://127.0.0.1:2746](https://127.0.0.1:2746/) . You will be redirected to a page for authentication.


Argo Workflows login


To log in to the Argo Workflows server, you will need to generate a {% c-line %}ServiceAccount{% c-line-end %} access token that you will use to manage your workflows. For this, you need to create[a {% c-line %}Role{% c-line-end %} and a {% c-line %}RoleBinding{% c-line-end %}](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) , and then a[{% c-line %}ServiceAccount{% c-line-end %}](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/) .


**Role:** The {% c-line %}Role{% c-line-end %} resource is used to determine a set of permitted operations on certain Kubernetes resources in a given namespace.


Below is an example of a {% c-line %}Role{% c-line-end %} manifest:


```text


```


**RoleBinding:** {% c-line %}RoleBinding{% c-line-end %} is used to determine which users or {% c-line %}ServiceAccounts{% c-line-end %} are authorized to carry out specific operations on certain resources in a given namespace. The details of the permissions are outlined in the {% c-line %}Role{% c-line-end %} that the {% c-line %}RoleBinding{% c-line-end %} is attached to.


Below is an example of a {% c-line %}RoleBinding{% c-line-end %} manifest:


```text


```


**ServiceAccount:** A {% c-line %}ServiceAccount{% c-line-end %} is used to authenticate machine-level processes to gain access to your Kubernetes cluster. The API server in the control plane manages authentication for the processes running in the Pod.


Below is an example of a {% c-line %}ServiceAccount{% c-line-end %} manifest:


```text


```


Finally, we since Kubernetes 1.24, we must manually create a secret to hold the serviceAccountToken:


```text


```


You can create a manifest file for each of these resources using the code snippets detailed above. Alternatively, you can create the resources directly using the kubectl CLI.


Create resource with kubectl and manifest files:


```text


```


After that, you can create an access token and store it in an environment variable (such as {% c-line %}ARGO_TOKEN{% c-line-end %}):


```text


```


Take the printed Bearer token and paste it into the text area of the login section on the landing page of the Argo Workflow UI.


Argo Workflows pop-up


Now, you can explore the sidebar menu and select **Workflows** .


Workflows page


## Executing Workflows


In this section, you will create both a basic and an advanced workflow.


#### Hello World Example


For starters, you will deploy a basic {% c-line %}hello world{% c-line-end %} example to familiarize yourself with the Workflow manifest file:


```text


```


In order to submit this workflow, ensure that your kubeconfig context is still set to {% c-line %}docker-desktop{% c-line-end %}. Argo will use these credentials when communicating with the API server. Once you’ve verified this, run the following command:


```text


```


Upon completion, review the workflow in the Argo Workflow UI.


Completed workflow


‍


Selected completed workflow


In addition to this, the container that was executed prints a whale with the text {% c-line %}hello world{% c-line-end %}, which is visible in the logs of the Pod. You can view the logs via the Argo Workflows UI or by running the {% c-line %}kubectl logs{% c-line-end %} command.


Argo UI logs


Pod logs


{% related-articles %}


Artifact Passing Example


Next, you’ll deploy a more advanced workflow that consists of generating an artifact and passing it into and out of containers in sequential steps. The artifact will be stored in *MinIO* , a Kubernetes-native object storage solution.


With Argo Workflows already running in your Docker Desktop cluster from the previous step, you just need to install MinIO on your cluster using {% c-line %}helm{% c-line-end %}:


```text


```


After MinIO has been deployed, your artifact server will be up and running. To access your artifact server, you can set up port forwarding with the following command:


```text


```


‍


Local MinIO


‍
You will need to use the credentials (access key and secret key) from the generated {% c-line %}argo-artifacts{% c-line-end %} secret to log in. These values are base64 encoded by default and will need to be decoded. To do this, run the following commands:


```text


```


‍


MinIO artifacts page


Next, configure Argo to use MinIO as its[artifact repository](https://pipekit.io/blog/configure-artifact-repo-argo-workflows) and use the relevant credentials for authentication. To do this, you can either follow the steps outlined[here](https://argoproj.github.io/argo-workflows/configure-artifact-repository/#configuring-miniohttps://sourcegraph.com/github.com/argoproj/argo-workflows@095d67f8d0f1d309529c8a400cb16d0a0e2765b9/-/blob/demo.md#5-install-an-artifact-repository) or you can use the simple patch manifest file below, created by[Stephen Bailey](https://github.com/stkbailey) :


```text


```


Run the following command to execute the patch above:


```text


```


Finally, run the {% c-line %}artifact-passing{% c-line-end %} example stored in the Argo GitHub repository:


```text


```


Passing artifact workflow


Passed artifacts


Download the generated artifact and view it from your local Downloads directory.


Downloaded Main.log


## Conclusion


As you saw in this tutorial, Argo Workflows can function as a powerful tool for creating Kubernetes-native workflows for various use cases. You should have a better understanding of how to implement basic Workflows concepts in a single-node Kubernetes cluster with Docker Desktop. More complex, enterprise-level projects, though, might cause difficulties around scaling and optimization.


[Pipekit](https://pipekit.io/) presents a solution. The control plane for your Argo Workflows offers a cost-effective model that supports your larger Kubernetes jobs. You can quickly set up your data pipeline infrastructure and get expert help as you scale.
