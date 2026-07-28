---
schema_version: "1.0.0"
document_id: "ddff3b60ad2b10a1a6df6c64655b2c93e969f78fc1849e96e25b25a26e9fa49d"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/install-argo-workflows-on-aws-gcp-azure"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:86385bd28af6bfde86fd9aa4010840b6803163d211e42f20db38344439e2d561"
---

# How to Install Argo Workflows on AWS, GCP, and Azure

Argo Workflows, a container-native workflow orchestration tool, can orchestrate parallel jobs on Kubernetes in any cloud platform. A workflow is a frequently complex sequence of steps that performs specific tasks in order to execute a significant action. To simplify this process, an orchestration tool like Argo Workflows can automate and manage multiple workflows.


This tool can prove useful in a number of use cases, such as machine learning or data processing tasks or running CI/CD pipelines natively on Kubernetes.


In this article, you’ll learn more about Argo Workflows and what it can do. You’ll learn how to set it up in Kubernetes in a cloud provider like AWS, Azure, or GCP, as well as how to create and submit workflows in Argo.


## What Is Argo Workflows?


Argo is a[Cloud Native Computing Foundation (CNCF)-hosted project](https://www.cncf.io/projects/argo/) that enables you to programmatically author, schedule, and monitor workflows. Argo implements workflows as[\`CustomResourceDefinitions\`](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) (CRDs). Treating workflows as code makes them perfect for GitOps pipelines.


With Argo Workflows, each step is a container. Containerizing steps frees you up to develop language-agnostic workflows, meaning you’re not limited to specific programming languages. You can model complex workflows as[directed acyclic graphs](https://www.techopedia.com/definition/5739/directed-acyclic-graph-dag) (DAG), so that you can capture the dependencies and share artifacts between them.


Argo Workflows allows you to create and run cloud-scale, compute-intensive workflows such as those used in machine learning or[big data processing](https://pipekit.io/blog/dask-argo-workflows-big-data) . They’re made up of polyglot, composable tasks that deal with huge amounts of data. With Argo Workflows, these workflows can automatically scale vertically and horizontally.


## Setting Up Argo Workflows


To submit workflows in Argo, you’ll first need a Kubernetes cluster. Then install Argo Workflows and the associated tools that handle workflow interactions.


### Setting Up Kubernetes and Kubectl


One option to deploy, run, and manage a Kubernetes cluster is to[create one yourself](https://github.com/kelseyhightower/kubernetes-the-hard-way) . You can also opt for a managed environment. Amazon Web Services (AWS) offers a managed Kubernetes solution called[EKS](https://aws.amazon.com/eks/) , Google Cloud Platform (GCP) offers[GKE](https://cloud.google.com/kubernetes-engine) , and Azure offers[AKS](https://azure.microsoft.com/en-us/services/kubernetes-service/) .


To create a managed Kubernetes cluster, you’ll need an account with the cloud provider of your choice. You can manually deploy a cluster through the provider portal, or you can use solutions offered by the cloud provider like[CloudFormation](https://aws.amazon.com/cloudformation/) . You can also consider cloud-agnostic Infrastructure as Code (IaC) solutions like[Terraform](https://www.terraform.io/) or[Pulumi](https://www.pulumi.com/) . Follow the documentation of your chosen provider for details.


All communication with Kubernetes is handled through its[API server](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/) . There are[several ways](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/) to access the API server. To facilitate operations, you’ll need to install[kubectl](https://kubernetes.io/docs/tasks/tools/) , a command line tool for running commands against Kubernetes clusters. To configure kubectl’s access to the cluster, each cloud provider provides a way to export the[kubeconfig](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/) .


Check the cloud providers’ documentations to see how to set up kubectl:


- ‍[AWS EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html)
- [GCP GKE](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl)
- [Azure AKS](https://docs.microsoft.com/en-us/azure/aks/control-kubeconfig-access#get-and-verify-the-configuration-information)


Once kubectl is installed and configured, you can test it by accessing your cluster to get information, as shown in the code snippet below:


```text


```


Output:


```text


```


The sample cluster above has three nodes. The control plane holds all the administrative Kubernetes resources, while the worker nodes run the workloads.


{% cta-1 %}


### Installing Argo Workflows CLI


With a Kubernetes cluster up and running, you can deploy Argo Workflows and submit your first workflow. To submit, watch, and list workflows, you’ll need to install its[CLI](https://argoproj.github.io/argo-workflows/cli/) . You can download the latest Argo CLI version from the[releases page](https://github.com/argoproj/argo-workflows/releases) .


### Installing Argo Workflows


Argo Workflows has[several components](https://argoproj.github.io/argo-workflows/architecture/) . Your production setup should factor in elements like scaling, disaster recovery, high availability, and security. The fundamental components you need are:


- [Argo server](https://argoproj.github.io/argo-workflows/argo-server/) : exposes a UI for workflows and the API required to work with Argo
- [Workflow controller](https://argoproj.github.io/argo-workflows/architecture/#workflow-controller-architecture) : manages workflows
- [Artifact repository](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) : passes artifacts between jobs in a workflow


You’ll need to deploy these components in a Kubernetes[namespace](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) , or a logical isolation of resources in a cluster. Use the following command to create the Argo namespace:


```text


```


Aside from the infrastructure components, you’ll also need to set up the CRDs,[Service Accounts](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/) ,[\`ClusterRoles\`](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole) , and[\`RoleBindings\`](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding) .


These are parts of configurations that Argo Workflows needs these components configured to function properly. Each[Argo Workflow release](https://github.com/argoproj/argo-workflows/releases) has associated manifests that provide the necessary configurations. Although Argo Workflows is cloud agnostic, you may need to enable extra permissions on some cloud platforms. Your cluster configuration will dictate that. For example, on GKE, you will likely need to add the permission to create new \`ClusterRoles\` to your account.


The components will be installed as[deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) and exposed as[services](https://kubernetes.io/docs/concepts/services-networking/service/) . There are several options for the Artifact Repository. One of them is[MinIO](https://min.io/) , which you can install as a deployment. You can create a file named \`minio.yaml\` and paste the code below into that file:


```text


```


To create the resource you’ll run:


```text


```


In the same way, you can deploy the Workflow Controller:


```text


```


‍


```text


```


Finally, deploy Argo Server:


```text


```


‍


```text


```


Alternatively, you can leverage one of the several configurations available on the Argo Workflows[GitHub repository](https://github.com/argoproj/argo-workflows/tree/master/manifests) . The Argo Workflows team makes these configurations available and updated. That way you don’t have to create your own deployments from scratch.


These configurations will deploy all required resources simultaneously. However, they are not suitable for production because they contain hard-coded passwords. The snippet below shows kubectl deploying a minimal, quick-start configuration:


```text


```


Once it’s deployed, check that all components are up and running:


```text


```


Output:


```text


```


To quickly access the UI, you can[port-forward](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/) to the service:


```text


```


Then access it at[https://localhost:2746](https://localhost:2746/) .


There are[other ways](https://argoproj.github.io/argo-workflows/argo-server/#access-the-argo-workflows-ui) to access the UI, depending on your setup.


### Submitting a Workflow


Now you’re ready to deploy a workflow. The Argo CLI provides complete workflow management. Using the CLI, you can submit, list, get information, print logs, and delete workflows. The following configuration represents a simple workflow, illustrating its main components:


```text


```


A workflow can have[several parts](https://argoproj.github.io/argo-workflows/workflow-concepts/) . The term _kind_ specifies the workflow CRD; _entrypoint_ specifies the workflow template to be used; _name_ names the template.


With the workflow defined, you will submit it from the CLI:


```text


```


Output:


```text


```


And list the workflow:


```text


```


Output:


```text


```


Or get detailed information about it:


```text


```


Checking logs is simple:


```text


```


Output:


```text


```


You can also navigate through the UI and obtain the same information.


Argo main interface


Argo workflow information


Argo workflow logs


{% related-articles %}


The following example demonstrates how to pass an artifact from one step to the next. The workflow comprises two steps. The first will send the output of a command to a file that the second step will consume and print. This example was taken from the[argo-workflows documentation](https://github.com/argoproj/argo-workflows/blob/master/examples/README.md#artifacts) :


```text


```


You can now submit the workflow:


```text


```


Output:


```text


```


As before, you can check the workflow status and logs using the CLI.


```text


```


Output:


```text


```


‍


```text


```


Output:


```text


```


You can also use the UI to check your workflow:


Passing artifacts in an Argo workflow


You can now start exploring your Argo Workflows installation!


If you want to learn more about how to access and properly secure the Argo Workflows UI, check out[this article about installing Argo Workflows in production environments](http://pipekit.io/blog/production-install-of-argo-workflows) .


## Conclusion


Workflow orchestration can be complex. It involves different components and artifacts, and it can encompass different paths for the steps involved. Argo Workflows aims to make modeling, scheduling, and tracking complex workflows simpler by leveraging Kubernetes and being cloud agnostic. This makes it an attractive solution for running compute-intensive workflows.


However, deploying, configuring, and maintaining Argo Workflows in a production environment and scaling it across several clusters for increased workloads can be daunting. It can take a significant amount of time to set up the infrastructure, the workflows, and the configuration.


Pipekit can solve that problem. It’s a control plane for Argo Workflows that enables you to develop and run large, complex workflows. With Pipekit, you’ll be able to trigger workflows, collect logs, and manage secrets. It allows you to maintain pipelines across multiple environments and multiple clusters.


To learn more about Pipekit,[sign up for the waitlist](https://pipekit.io/) .
