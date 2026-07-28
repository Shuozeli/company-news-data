---
schema_version: "1.0.0"
document_id: "f8f43840b361f6538c656de095fa34e77464975dbbd564a3b4ea02abbbc2a8da"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/how-to-install-argo-workflows-in-multiple-namespaces"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:18.654833+00:00"
content_hash: "sha256:bde3105d7ae1c304c139ed4da067c4810718ad1720eef4b67122f5f3c32c83e8"
---

# How to Install Argo Workflows in Multiple Namespaces

[Argo Workflows](https://argoproj.github.io/argo-workflows/) is a workflow engine for Kubernetes. In simple words, it lets you orchestrate multiple parallel jobs on a Kubernetes cluster. With[Argo Workflows](https://pipekit.io/blog/top-10-argo-workflows-examples) , you can run compute-intensive jobs like data processing pipelines or training machine learning models, all with the familiar declarative approach of Kubernetes. If you’re already using Kubernetes for application development, you can also use Argo Workflows to run CI/CD pipelines without spending valuable time configuring CI/CD software.


Argo Workflows is cloud-agnostic and can run on any Kubernetes cluster, whether it’s a local self-hosted cluster or a managed one like[AWS EKS, GCP GKE, or Azure AKS](https://pipekit.webflow.io/blog/install-argo-workflows-on-aws-gcp-azure)[‍](https://cloud.google.com/kubernetes-engine/) .


Typically, you’d install a single Argo Workflows in your cluster and then submit workflows. However, some specific use cases require you to have multiple Argo Workflows instances in the same cluster. This article will explain one approach to achieving this—using multiple namespace-scoped installations.


## Argo Workflows in Multiple Namespaces


There are two ways to run multiple Argo Workflows instances in the same cluster. But first, you need to understand the different installation methods of Argo Workflows:


1. **Cluster install:** This acts as a cluster-wide installation. Argo Workflows will watch and execute workflows across all namespaces in this setup.
2. **Namespace install:** This will only execute workflows in the namespace in which it is installed.
3. **Managed namespace install:** This is similar to the namespace install above, except it executes workflows only in a specified namespace that’s different from the one where it’s installed.


To run multiple Argo Workflows instances, you can either have multiple cluster-scoped installations or multiple namespace-scoped installations.


If you want to use multiple cluster-scoped installs, you must set the[instance ID](https://argoproj.github.io/argo-workflows/scaling/#instance-id) of each install. For multiple namespace-scoped installs, you simply need to install Argo Workflows in the different namespaces and[set the --namespaced flag to the Workflow Controller and Argo Server](https://argoproj.github.io/argo-workflows/managed-namespace/) .


## Benefits of Installing Argo Workflows in Multiple Namespaces


Kubernetes namespaces are often used to partition the cluster into distinct units that reflect the separation in the application environment. For example, you might have a development environment, a testing/QA environment, a staging environment, and a production environment. You can create separate namespaces for all these different environments and install Argo Workflows in each namespace. This separation helps to logically isolate the jobs for the different environments because each team gets their own Argo Workflows installation that they can execute workflows on.


For example, your development team can utilize the Argo Workflows instance in the development namespace to execute workflows related to development. The QA team can use the Workflows instance in the testing namespace to run workflows to test the applications. Finally, the DevOps team can use the Argo Workflows instance in the production namespace to deploy the applications to production.


{% cta-1 %}


## Limitations of Installing Argo Workflows in Multiple Namespaces


While it’s true that a multiple-namespaced setup can provide significant benefits in terms of workload isolation, it also comes with its downsides depending on your setup. Suppose you’re using multiple namespaces to run both development and production workflows in the same cluster. In that case, you could run into issues of development workflows impacting the production workflows, *eg* , by accidentally using up all resources in the cluster. It’s recommended to have a separate cluster altogether for production workflows and use the multiple namespaces approach to isolate the different stages of development ( *eg* , testing, staging, etc.).


It’s also extremely easy to inadvertently deploy a workflow to the wrong namespace. As you’ll see in the next section, all it takes is the wrong namespace name in the -n flag to the Argo CLI. If you have both development and production workflows in the same cluster, someone can accidentally submit a development workflow to the production namespace and break the production environment. The workaround, as mentioned earlier, is to just use a separate cluster for production.


## Installing Argo Workflows in Multiple Namespaces


In this section, you’ll learn how to install Argo Workflows in multiple namespaces. To follow along with the tutorial, you must have a Kubernetes cluster and ensure that kubectl is set up to communicate with the correct cluster.


You can use either a managed Kubernetes cluster in the cloud, or a local cluster option:


- [K3s](http://pipekit.io/blog/how-to-run-argo-workflows-in-k3s)
- [Docker Desktop](http://pipekit.io/blog/argo-workflows-with-docker-desktop)
- MiniKube


First, create the namespaces—one for each Argo Workflows instance. For this tutorial, create two namespaces, argo-1 and argo-2:


```text


```


Next, install Argo Workflows in both of the namespaces. You’ll be using the[quick-start-postgres.yaml](https://raw.githubusercontent.com/argoproj/argo-workflows/master/manifests/quick-start-postgres.yaml) manifest, which helps you get Workflows up and running quickly.


**If you’re deploying Argo Workflows to a production environment, using the quickstart manifests is not recommended.** Instead, you can follow our guide on[deploying Argo Workflows in a production environment](https://pipekit.io/blog/production-install-of-argo-workflows) .


Run the following commands to deploy Argo Workflows in your cluster:


```text


```


### Accessing the Workflows UI


To access the Workflows UI, you need to open a port-forward. The following command opens a port-forward to the Workflows UI in the argo-1 namespace:


```text


```


Visit the Workflows UI at http://localhost:2746 in your browser. Notice that the namespace field mentions running in the argo-1 namespace.


Argo Workflows UI for argo-1 namespace after log in


Similarly, you can expose the Workflows UI in the argo-2 namespace to a different port:


```text


```


### Using the Argo CLI


You can also use Argo CLI to interact with the different Argo Workflows instances. First,[install the Argo CLI](https://github.com/argoproj/argo-workflows/releases/latest) . You can run argo version to check if it’s installed correctly. If you see no errors, you’re good to go!


To interact with Argo Workflows running in a specific namespace, you must supply the -n argument and the namespace’s name. The following command submits the[Hello, World!](https://raw.githubusercontent.com/argoproj/argo-workflows/master/examples/hello-world.yaml) workflow to the Workflows instance in the argo-1 namespace:


```text


```


The workflow will be scheduled on a pod in the argo-1 namespace when you run the command. The --watch flag allows you to view the status of the workflow as it runs.


Workflow status with --watch flag


After a few seconds, the workflow will run to completion, and you should see the Succeeded status in the console.


Workflow succeeded status


{% related-articles %}


To list all the workflows, you can use the argo list command. As before, pass the -n flag to scope the list to a specific namespace:


```text


```


You should see the following output:


```text


```


Following exactly the same steps, you should be able to submit a workflow to the argo-2 namespace. You only need to change the value of the -n flag to argo-2:


```text


```


Once again, use argo list to list the workflows in the argo-2 namespace:


```text


```


You can pass the --all-namespaces flag to list all the workflows irrespective of the namespace:


```text


```


The -n flag also works with almost all[argo commands](https://argoproj.github.io/argo-workflows/cli/argo/) , giving you complete control over the different Workflows instances.


## Conclusion


Argo Workflows is a game-changer for Kubernetes users. The ability to orchestrate workflows on Kubernetes through a simple UI and a powerful CLI makes it a great tool. In this article, you learned when you need to install Argo Workflows in multiple namespaces and how to do so.


Don’t want to deal with the complexities of installing and configuring Argo Workflows yourself? Book your personalised demo with Pipekit - a managed Argo Workflows service that does the heavy lifting for you and allows you to massively scale your data pipelines.
