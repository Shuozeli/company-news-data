---
schema_version: "1.0.0"
document_id: "8c8e7dbe2e563c7a9dc5e6860650d36cb23a37960428bcb6a5548ebeafcab605"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/how-to-run-argo-workflows-in-k3s"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:c0ac174ee73f4261954ea4ac9087f76f3b61e3d4191892cc928567a4bf268109"
---

# How to Run Argo Workflows in K3s

[Argo Workflows](https://argoproj.github.io/workflows/) is a powerful Kubernetes-native workflow engine used to create, manage, and orchestrate parallel jobs in your Kubernetes clusters.


Argo also works well with[K3s](https://k3s.io/) , a lightweight, simplified version of Kubernetes designed for IoT and edge computing. In this tutorial, you will learn how to deploy Argo Workflows to a Kubernetes cluster in K3s.


## About Argo Workflows


Argo Workflows offers a number of key features:


- Web-based UI
- Native artifact support (MinIO, S3, Artifactory, HDFS, OSS, HTTP, Git, GCS, raw)
- Templating and cron workflows
- Workflow Archive
- REST API, Argo CLI


The {% c-line %}Workflow{% c-line-end %} resource is used to define the execution of a workflow as well as its storage state. Workflows consist of instructions that operate like functions, known as templates in Argo. Templates detail the steps of execution in the workflow.


The {% c-line %}spec{% c-line-end %} is the most important part of the {% c-line %}Workflow{% c-line-end %} manifest file. It contains two properties:


- ‍ **templates** : **** This defines the types of templates that you want to use in your workflow. **‍**
- **entrypoint** : This determines which template will be executed first.


There are multiple types of templates available, such as:


- **Container** : The most common template type, this schedules a container. Its spec is identical to that of a Kubernetes container spec. **‍**
- **Script** : This is a convenience wrapper around the container. The spec is the same as the container, but it has a {% c-line %}source{% c-line-end %} field that allows you to define a script. The script is saved to a file and executed from there. **‍**
- **Resource** : This performs create, read, update, and delete (CRUD) operations directly on resources in the cluster. **‍**
- **Suspend** : This suspends the execution of a workflow either for a specified duration or indefinitely. **‍**
- **DAG** : This allows you to define the tasks in a workflow as a graph of dependencies. **‍**
- **Steps** : This allows you to define the tasks in your workflow as sequential steps. It consists of inner and outer lists; inner lists run in parallel, while outer lists run one after the other.


{% cta-1 %}


## Prerequisites


In order to follow this tutorial, you’ll need the following:


- [K3s](https://k3s.io/) ‍
- [kubectl](https://kubernetes.io/docs/tasks/tools/)[‍](https://helm.sh/docs/intro/install/)
- [Helm](https://helm.sh/docs/intro/install/)[‍](https://k9scli.io/)
- [K9s](https://k9scli.io/) (optional)


## Getting Started with K3s


First download the installation script and start up the Kubernetes server with the below command:


```text


```


You can check the status of your single-node cluster by running {% c-line %}sudo k3s kubectl get node{% c-line-end %}. By default, the kubeconfig file is written to {% c-line %}/etc/rancher/k3s/k3s.yaml{% c-line-end %} with privileged permissions. However, you can use kubectl to communicate with your cluster instead by either copying the content of the default {% c-line %}k3s.yml{% c-line-end %} configuration file to your main kubeconfig file, which is typically located at {% c-line %}~/.kube/config{% c-line-end %}, or updating the KUBECONFIG environment variable path.


```text


```


K9s can also be used as a complementary tool for cluster visibility:


K9s cluster pods


### Installing Argo CLI


The next step will be to install the Argo CLI. You can use either the latest version or select a previous one from the[Argo CLI releases GitHub page](https://github.com/argoproj/argo-workflows/releases) . The commands you run will vary depending on your operating system. The two code blocks below are for Mac and Linux, respectively. If you’re using Windows, you can download the relevant executable from the **Assets** section on the Argo releases GitHub page.


For Mac:


```text


```


For Linux:


```text


```


#### Installing Argo Controller and UI


Before installing the Argo Workflows resources, you need to create an {% c-line %}argo{% c-line-end %} namespace:


```text


```


When the Workflow Controller and the Argo Server have successfully rolled out, you can follow the steps below to access the Argo Workflows UI.


Argo Resources


You can access the UI in multiple ways, but for this tutorial, use the[port-forwarding method](https://argoproj.github.io/argo-workflows/argo-server/#kubectl-port-forward) :


```text


```


Open your browser and go to[https://127.0.0.1:2746](https://127.0.0.1:2746/) . You will be redirected to a page for authentication.


Argo workflows login


To log in to the Argo Workflows server, you will need to generate a {% c-line %}ServiceAccount{% c-line-end %} access token that you will use to manage your workflows. For this, you need to create[a {% c-line %}Role{% c-line-end %} and a {% c-line %}RoleBinding{% c-line-end %}](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) , and then a[{% c-line %}ServiceAccount{% c-line-end %}](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/) .


**Role:** The {% c-line %}Role{% c-line-end %} resource is used to determine a set of permitted operations on certain Kubernetes resources in a given namespace.


Below is an example of a {% c-line %}Role{% c-line-end %} manifest:


```text


```


‍ **RoleBinding** :{% c-line %}RoleBinding{% c-line-end %} is used to determine which users or {% c-line %}ServiceAccounts{% c-line-end %} are authorized to carry out specific operations on certain resources in a given namespace. The details of the permissions are outlined in the {% c-line %}Role{% c-line-end %} that the {% c-line %}RoleBinding{% c-line-end %} is attached to.


Below is an example of a {% c-line %}RoleBinding{% c-line-end %} manifest:


```text


```


‍ **ServiceAccount** : A {% c-line %}ServiceAccount{% c-line-end %} is used to authenticate machine-level processes to gain access to your Kubernetes cluster. The API server in the control plane manages authentication for the processes[running in the Pod](https://pipekit.io/blog/clean-up-pods-save-logs-argo-workflows) .


Below is an example of a {% c-line %}ServiceAccount{% c-line-end %} manifest:


```text


```


Finally, we since Kubernetes 1.24, we must manually create a secret to hold the serviceAccountToken:


```text


```


You can create a manifest file for each of these resources using the code snippets detailed above.


Create resource with kubectl and manifest files:


```text


```


Next create an access token and store it in an environment variable (such as {% c-line %}ARGO_TOKEN{% c-line-end %}):


```text


```


Copy the printed Bearer token from your terminal and paste it in the text area of the Argo Workflow UI login.


Argo workflows popup


Now you can explore the sidebar menu and select **Workflows** .


Workflows page


## Executing Workflows


In this section, you will create both a basic and an advanced workflow example.


#### Secret Template Example


This type of workflow template supports the same secret syntax and mechanisms as the Kubernetes pod specification. You can access a secret that serves as an environment variable or volume by using this template.


First you'll deploy a secret workflow template, which works the same way and supports the same syntax as the Pod specification accessing a secret in Kubernetes. You can access the secret as either an environment variable or a volume.


Start by creating a secret in your cluster with the following command:


```text


```


Next you'll create a manifest file for the workflow that will access this secret.


```text


```


Now you can use the Argo CLI tool to create the workflow. Argo uses the existing kubeconfig configurations to know which cluster to interact with. To create your first workflow, run the following command:


```text


```


You can review it in the Argo Workflow UI.


Top secret workflow example


‍


Top secret workflow review


‍


Top secret logs


{% related-articles %}


#### Volume Example


Next you’ll deploy a workflow that is used to manage volumes. In the example below, a volume will be dynamically created and used in a multi-step workflow.


Create the following manifest file:


```text


```


As you did before, create this workflow using the Argo CLI:


```text


```


Once the workflow has completed, you can review the results in the UI and delve into the logs to see the results of the generated message in the mounted volume.


Completed volume workflow example


‍


Multi-step volume workflow


‍


Mounted volume logs


‍


Generated message


## Conclusion


In this tutorial, you learned the fundamental concepts around Argo Workflows and how to use it with a single-node K3s cluster. As demonstrated, this workflow engine operates well even in a lightweight version of Kubernetes.


In an enterprise context, however, your Kubernetes jobs could become more complex.[Pipekit](https://pipekit.io/) allows you to manage these jobs at scale. The control plane configures Argo Workflows for you in your infrastructure, enabling you to optimize multi-cluster workloads while reducing your cloud spend.
