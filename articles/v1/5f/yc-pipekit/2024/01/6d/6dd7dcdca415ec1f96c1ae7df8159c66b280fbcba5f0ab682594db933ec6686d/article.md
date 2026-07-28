---
schema_version: "1.0.0"
document_id: "6dd7dcdca415ec1f96c1ae7df8159c66b280fbcba5f0ab682594db933ec6686d"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-workflows-the-best-way-to-run-kubernetes-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:00:19.733210+00:00"
content_hash: "sha256:f856baf1800337ef87c208474bbbbee334ec86d8270271becd66c3ab31511bd2"
---

# Argo Workflows: The Best Way to Run Kubernetes Workflows

Argo Workflows is a workflow engine implemented on top of a Kubernetes instance that allows you to create, manage, schedule, process, and automate your workflows.


Running your workflows on Kubernetes means taking advantage of its various features and benefits, including scaling of applications, canary deployments, application healing, and much more. While Kubernetes has plenty of baked-in functionalities (such as jobs, deployments, and services) that allow cloud engineers to deploy and manage containerized applications easily, you can also extend its functionality using[custom resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) and[custom controllers](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#custom-controllers) .


However, running your workflows on Kubernetes without a specialized workflow engine like[Argo Workflows](https://argoproj.github.io/argo-workflows/quick-start/) can quickly become difficult to manage and can even be problematic to scale. Using Argo Workflows to manage and run your workflows on Kubernetes provides[many benefits](https://argoproj.github.io/argo-workflows/) that make processing your workflows less complicated, including:


- Allowing you to define your workflows in YAML
- Offering[infrastructure as code (IaC) benefits](https://www.techadv.com/blog/5-benefits-infrastructure-code-iac-modern-businesses-cloud)
- Letting you run multiple commands with different parameters on a single workflow pipeline YAML definition


In this tutorial, you'll learn how to install and use Argo Workflows as a Kubernetes custom resource definition (CRD).


## What Is Argo Workflows?


Argo Workflows is an open source workflow engine used to orchestrate parallel jobs in Kubernetes. As it's a container-native application, it can run on both[self-managed Kubernetes](https://medium.com/@reezpatel/self-managed-kubernetes-c2080030a436) and managed Kubernetes clusters, like[Amazon EKS](https://aws.amazon.com/eks/) ,[AKS](https://azure.microsoft.com/en-us/products/kubernetes-service) , or[GKE](https://cloud.google.com/kubernetes-engine) .


Unlike[Kubernetes jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/) , Argo Workflows lets you run jobs in a complex workflow using[steps](https://argoproj.github.io/argo-workflows/walk-through/steps/) or[directed acyclic graphs](https://argoproj.github.io/argo-workflows/walk-through/dag/) (DAGs), among other features embedded in the workflow engine.


Argo Workflows is implemented using Kubernetes custom resource definitions (CRDs), making it easy to create and manage your workflows using your existing knowledge of managing[Kubernetes resources](https://kubernetes.io/docs/concepts/workloads/controllers/) . For instance, you can use the[kubectl client](https://kubernetes.io/docs/tasks/tools/#kubectl) to get all workflows, create workflows, and so on. You can also define a workflow and its dependencies using the YAML format, which is easy to follow.


Argo Workflows isn't the only workflow engine. Some other options include:


- [Apache Airflow](https://airflow.apache.org/) is an open source workflow engine. Unlike Argo Workflows, which uses YAML to write DAGs, Airflow uses Python. So, it might be a bit challenging for people with less Python experience to start using it right out of the box. It offers a good developer experience with its rich user interface, which helps manage and monitor complex workflows.
- [Prefect](https://www.prefect.io/) is another workflow orchestration tool with a large following on[GitHub](https://github.com/PrefectHQ/prefect) . You can run Prefect on your own infrastructure or use the Prefect cloud infrastructure. It also uses Python to declare workflows and supports various third-party integrations.
- [Tekton](https://tekton.dev/) is an open source, cloud-native solution for continuous integration and continuous delivery/deployment. Unlike Prefect and Airflow, Tekton also uses CRDs to declare its workflows. So, its learning curve is minimal for a Kubernetes developer or administrator. However, it's as not as well-established as the other tools.


{% cta-1 %}


## Ways to use Argo Workflows


While these are all viable tools for your workflow orchestration, Argo Workflows supports multiple languages, has a good developer experience, and has an active and growing community. So, it strikes a strong balance between flexibility and support and is a practical choice in many use cases. Here are just a few[examples of the ways you can use Argo Workflows](https://pipekit.io/blog/top-10-argo-workflows-examples) .


### CI/CD Pipelines


Continuous integration and continuous deployment (CI/CD) is a mandatory phase in the software development lifecycle that allows teams to develop applications in an agile flow and increases the quality of the application being built. While several solutions like GitHub Actions, Jenkins, and TeamCity can be used for orchestrating CI/CD pipelines, only a few are built on top of Kubernetes, like Argo Workflows. Using Argo Workflows for your CI/CD pipelines allows you to also take advantage of some of the[benefits of Kubernetes](https://kodekloud.com/blog/benefits-of-kubernetes/) .


### Data Processing


Argo Workflows'[directed acyclic graph](https://argoproj.github.io/argo-workflows/walk-through/dag/) (DAG) and[parameter](https://argoproj.github.io/argo-workflows/walk-through/parameters/) features make it an effective solution for orchestrating your data pipelines. Additionally, it can create[large-scale](https://argoproj.github.io/argo-workflows/running-at-massive-scale/) , complex workflows.


### Machine Learning


Like the data processing use case, Argo Workflows is suitable for running machine learning pipelines. It provides flexible tools for creating workflows and a user interface to monitor workflow stages. It also removes the risk of vendor lock-in, allowing you to build your machine learning pipelines on your infrastructure while taking advantage of Kubernetes benefits.


## Using Kubernetes Custom Resources to Implement Argo Workflows


In the following tutorial, you'll use a data pipeline example, as seen in the architectural diagram below, to learn how to implement Argo Workflows in your Kubernetes cluster:


Data pipeline


This data pipeline has three data sources, where two generate text files and the third generates a PDF. In this example, you need to analyze the data from these sources, but to do that, you need to extract the data from each source and aggregate it. As the aggregator in the example can only receive text input, there's an extra process between the PDF source and the aggregator that transforms the PDF to TXT format.


Two extra processes are included to transform the aggregated text data into SQL and NoSQL data, as the systems you'll use to analyze the data work in these formats.


The "Extract," "Transform," and "Aggregate" processes are jobs that you'll define in your Argo Workflow.


### Prerequisites


The following are required for this tutorial:


1. A[Kubernetes](https://kubernetes.io/) cluster. You can choose to use a local or managed Kubernetes cluster. Ensure that the Kubernetes instance is up and running.
2. The[kubectl CLI](https://kubernetes.io/docs/tasks/tools/) .
3. The[Argo CLI](https://github.com/argoproj/argo-workflows/releases/tag/v3.4.5) . This tutorial uses the latest Argo installation as of the time of writing, which is v3.4.5. You can use the kubectl client to create and manage your Argo Workflows; however, the Argo CLI provides some extra advantages over kubectl, such as YAML validation, parameter passing, workflow visualization, and so on.


### Installing Argo Workflows


First, install the Argo Workflows custom resources and controller in your cluster:


```text


```


You can visit[GitHub](https://github.com/argoproj/argo-workflows/releases/download/v3.4.5/install.yaml) to view the contents of the YAML file.


For the purposes of this tutorial, you'll be bypassing the client authentication so you can access the Argo Workflows UI without logging in. However, in a production environment, you'll need to specify your[authentication mode](https://argoproj.github.io/argo-workflows/argo-server-auth-mode/) .


Run the following command in your cluster to bypass the client authentication:


```text


```


To make the UI accessible via your web browser, you'll forward the deployment port to a port on your local server:


```text


```


Visit the Argo Workflows UI at[https://localhost:2746/](https://localhost:2746/) . As you've used a self-signed certificate, your browser will display a certificate error, so you'll need to manually approve the certificate before you can access the UI. The interface should look something like this:


Argo Workflows UI


### Creating the YAML Workflow Pipeline


Create a file named {% c-line %}data-pipeline.yaml{% c-line-end %} and paste in the following:


```text


```


Once you've added the above code, run the workflow using the following command:


```text


```


You'll receive a response similar to the following:


```text


```


Visit the Argo UI you opened earlier at[https://localhost:2746/](https://localhost:2746/) . You should see the pipeline already running on the dashboard:


Data pipeline running on dashboard


Click the **data-pipeline** workflow for a full view of the jobs currently running:


Data pipeline running on dashboard


After a short wait, the processes will complete:


Data pipeline completed


You can click **LOGS** to view the logs produced from each process:


View data pipeline logs


You can click **RESUBMIT** to restart the workflow process:


Resubmit data pipeline


{% related-articles %}


## Conclusion


[Argo Workflows](https://argoproj.github.io/argo-workflows/) is a very useful tool for orchestrating multiple jobs that are dependent on each other. By combining its CLI tool and its custom resource definitions, you can create complex workflows with less stress. Through a simple example, you learned how to install Argo Workflows and orchestrate jobs that were dependent on each other using a combination of YAML, the Argo CLI, and the Argo UI. Argo Workflows is also great for any Kubernetes developer or administrator looking for a workflow engine within the Kubernetes ecosystem.


The Argo Workflow data pipeline configuration used in this tutorial is available[on GitHub](https://github.com/tolustar/argo-workflows) .


If you want to take your Argo Workflows management to the next level with better cloud cost management, better scaling of your pipelines, and the ability to manage secrets and collect logs without having to spend months building the underlying infrastructure for your Argo Workflows engine, then Pipekit (a managed Argo Workflows service) is the right tool for you. For more information, visit the[home page](https://pipekit.io/) .
