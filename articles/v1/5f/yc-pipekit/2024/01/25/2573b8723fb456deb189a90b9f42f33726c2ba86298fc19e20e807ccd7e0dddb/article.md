---
schema_version: "1.0.0"
document_id: "2573b8723fb456deb189a90b9f42f33726c2ba86298fc19e20e807ccd7e0dddb"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/production-install-of-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:18.654833+00:00"
content_hash: "sha256:de2b55d32347fc008b3dfa0b28929e36850b1f21dc0c83043e6651d4e7e22a4c"
---

# What Does a Production Installation of Argo Workflows Look Like?

According to last year’s[CNCF annual survey](https://www.cncf.io/reports/cncf-annual-survey-2021/) , there was a notable 115 percent year-on-year increase in Argo’s production usage.[Argo](https://argoproj.github.io/) provides numerous Kubernetes native solutions for CI/CD, workflows, events, and deployment strategies.


[Argo Workflows](https://argoproj.github.io/workflows) is an incubating CNCF open source workflow engine for orchestrating parallel jobs on Kubernetes. It covers a wide range of use cases, such as executing compute-heavy jobs for machine learning, creating data processing, and running CI/CD pipelines.


In this tutorial, you will discover how to install and set up the Argo Workflows engine in your Kubernetes cluster. You will also install Argo CLI to[configure the Argo Workflows](https://pipekit.io/blog/top-10-argo-workflows-examples) , install artifact repositories, and learn more about the Argo Workflows user interface.


## What Is Argo Workflows?


Argo Workflows runs containerized, step-based workflows, and is implemented as a[Kubernetes CRD](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) . Here, each step leads to a pod being created in the Kubernetes cluster. You can arrange steps in a sequence or a directed acyclic graph (DAG), allowing for easy orchestration and parallelization of jobs on top of Kubernetes. Argo has similar Kubernetes characteristics: it’s declarative, configurable, and cloud-agnostic. As an end-user, you either use {% c-line %}kubectl{% c-line-end %} or Argo CLI to interact with it. You’ll learn more about both options in the coming sections.


Argo Workflows’ complete list of features can be found[here](https://github.com/argoproj/argo-workflows#features) , but let’s cover some of the highlights. It provides:


- A UI to visualize and operate workflows.
- Support for object storage using[S3](https://aws.amazon.com/s3/) ,[Artifactory](https://jfrog.com/artifactory/) ,[Alibaba Cloud OSS](https://www.alibabacloud.com/product/object-storage-service) , HTTP,[Git](https://git-scm.com/) ,[GCS](https://cloud.google.com/storage) , and raw.
- Templating to store typically used workflows in the cluster.
- A DAG or steps-based declaration of workflows.
- Timeouts and retry mechanisms (steps and workflow level).
- The ability to cancel, suspend, resume, and resubmit workflows.


In addition to the use cases referenced above, Argo Workflows can be used for several other purposes:


- ETL, data analytics, and data science
- Data and batch processing pipelines
- Fan-out/fan-in data processing
- Infrastructure automation
- Stream processing


{% cta-1 %}


## Setting Up Argo Workflows in Production


Now, let’s get started with the tutorial. Follow these step-by-step instructions for implementing Argo Workflows:


### Prerequisites


First, you’ll need a running Kubernetes cluster and the {% c-line %}kubectl{% c-line-end %} CLI. This tutorial will use minikube as the target Kubernetes cluster. Verify the setup of the minikube cluster by running the {% c-line %}minikube start{% c-line-end %} command:


```text


```


Output:


```text


```


**Note:** if you don’t want to go through the installation, you can try things out directly on a[demo environment](https://workflows.apps.argoproj.io/workflows/argo) . This playground environment allows you to test things quickly, but it is not recommended for production.


Argo demo UI


There’s also a[Katacoda course](https://www.katacoda.com/argoproj/courses/argo-workflows/) in which you can try out Argo Workflows in your web browser without needing to install anything on your computer. Check it out if you’d like. (Note:[Katacoda will be shut down](https://www.oreilly.com/online-learning/leveraging-katacoda-technology.html) by O'Reilly Media on June 15, 2022)


Now, let’s proceed with the Argo Workflows installation.


### Installing Argo Workflows


The first step in installing Argo Workflows is to install the Argo CLI. Instructions for doing so on a Mac are included below, or you can use {% c-line %}brew install argo{% c-line-end %}. You can find the setups for other operating systems[here](https://github.com/argoproj/argo-workflows/releases/tag/v3.2.8) .


Start by running this command:


```text


```


Then, verify the installation:


```text


```


You should see a version number as your output:


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


Now, let’s get back to your configuration and set up a {% c-line %}port-forward{% c-line-end %} so you can access the UI.


Run the {% c-line %}kubectl port-forward{% c-line-end %} command:


```text


```


You can access the Argo UI by accessing the[https://127.0.0.1:2746/](https://127.0.0.1:2746/) URL in your browser. Initially, you might see the following error on the login screen after accessing the URL. If so, you will be asked to log in with SSO or an Argo auth token.


Error image


To get the auth token for login, you’ll need to run the {% c-line %}kubectl -n argo exec argo-server-${POD_ID} -- argo auth token{% c-line-end %} command, or {% c-line %}argo auth token{% c-line-end %}, if you have the Argo CLI installed. Copy and paste the output of the command in the box on the login screen, as pictured here:


Login screen


### Setting Up Object Storage


Argo has support for many S3-compatible artifact repositories, such as AWS, GCS, and MinIO. In this section, you will set up an[artifact repository](https://pipekit.io/blog/configure-artifact-repo-argo-workflows) with[MinIO](https://min.io/) to store your workflow artifacts. MinIO is a high performance, Kubernetes-native object storage. It is ideal for storing files such as photos, videos, log files, backups, and container images.


Install MinIO using the following Helm command on your local Kubernetes cluster. This command will install MinIO in the {% c-line %}argo{% c-line-end %} namespace with the name {% c-line %}argo-artifacts{% c-line-end %} and create a bucket called {% c-line %}my-bucket{% c-line-end %}:


```text


```


**Note:** make sure you have sufficient resources (memory, etc.) on your local Kubernetes cluster; otherwise, your pod may remain in pending status. You can override the default memory requirement for MinIO by passing the {% c-line %}resources.requests.memory=2Gi{% c-line-end %} argument.


While installing MinIO using Helm, a default secret will be generated in the {% c-line %}argo{% c-line-end %} namespace. You’ll use these secrets to log in to the MinIO user interface.


To enable access to the MinIO UI, use the following {% c-line %}kubectl port-forward{% c-line-end %} command:


```text


```


Now, you can browse the MinIO UI by accessing the[https://127.0.0.1:9000/](https://127.0.0.1:9000/) URL.


[MinIO login screen](https://imgur.com/qnR4PMA.jpg)


You will need to provide login credentials, which can be obtained using the following {% c-line %}kubectl get secret{% c-line-end %} commands:


```text


```


MinIO setup is now complete, but you need to link {% c-line %}my-bucket{% c-line-end %} with your Argo workflow. Add the following snippet by editing the Argo {% c-line %}workflow-controller-configmap{% c-line-end %}:


```text


```


Use the following {% c-line %}kubectl edit{% c-line-end %} command to do so:


```text


```


### Submitting a Workflow


Now, you will submit a very simple workflow template to echo “hello world” using the docker/whalesay container image from Docker Hub.


For reference, here’s the YAML manifest of Argo Workflow's[Hello World workflow](https://raw.githubusercontent.com/argoproj/argo-workflows/master/examples/hello-world.yaml) :


```text


```


Use the {% c-line %}argo submit{% c-line-end %} command to submit a workflow.


```text


```


You should see the following output:


```text


```


Next, confirm the output by running the following command:


```text


```


You should see this:


```text


```


In the last section, you completed the setup for MinIO. Now, you can submit a workflow, which passes artifacts from one step to another. Once the workflow status is “Succeeded,” it will generate some artifacts that you will persist:


```text


```


The following output shows that workflow is completed successfully:


```text


```


Now you can verify the final artifacts on the MinIO UI. You could see the final artifact under {% c-line %}my-bucket{% c-line-end %}:


my bucket screen Minio


{% related-articles %}


### Implementing Production Best Practices


At this point, you have learned about installing Argo Workflows and submitted a simple workflow to confirm that your setup is working. Now, let’s explore some of the best practices you can implement for cost optimization and better resource utilization while using Argo Workflows.


To create your production setup, you will mainly add configuration to[{% c-line %}workflow-controller-configmap{% c-line-end %}](https://argoproj.github.io/argo-workflows/workflow-controller-configmap/) . This is the central place to operate Argo Workflow, and as such, you should keep this configmap under version control. This should be the first step in creating a production setup; each time you apply any changes to the configmap, the {% c-line %}argo-server{% c-line-end %} will automatically restart to apply your changes. You can find the final configuration for this tutorial on[Github](https://github.com/xNok/argo-workflow-production-setup) .


#### High Availability


Since the Argo server restarts every time you change a configuration in {% c-line %}workflow-controller-configmap{% c-line-end %}, you may affect users in production. Start by increasing the number of replicas of the {% c-line %}argo-server{% c-line-end %} deployment resource:


```text


```


#### Default Workflow Values


Each of the best practices covered in the rest of this section can also be included using aDefault Workflow Spec , which essentially creates a baseline that will be inherited in all other workflows. You can specify this by adding them under {% c-line %}workflowDefaults{% c-line-end %}. Note that those configurations can can also be overwritten later at the workflow level:


```text


```


#### Pod Garbage Collection


To avoid wastage of resources, the {% c-line %}podGC{% c-line-end %} field reference can be used to delete[pods after their completion](https://pipekit.io/blog/clean-up-pods-save-logs-argo-workflows) . The following code snippet uses the {% c-line %}OnPodCompletion{% c-line-end %} strategy:


```text


```


Pod garbage collection can also be used with any of the following alternate strategies:


- OnPodSuccess
- OnWorkflowCompletion
- OnPodCompletion


#### Workflow TTL Strategy


Because idle workflows still consume resources, this strategy helps by allowing you to automatically delete workflows after a specified period of time or after the workflow completes. {% c-line %}TTLStrategy{% c-line-end %} decides for how long workflows that are successful, not successful, or completed should live:


```text


```


#### Resource Request and Limit


It’s also helpful to set some resource limits (i.e., CPU and memory) for the {% c-line %}workflow-controller{% c-line-end %} and {% c-line %}argo-server{% c-line-end %}. You’ll need to edit the deployment resource to do so:


```text


```


You can also restrain the resources of executors (pods that run your workflow). To do so, edit {% c-line %}workflow-controller-configmap{% c-line-end %} as follows:


```text


```


Often, there is a need to limit the rate at which pods are created to mitigate flooding of the Kubernetes API server by workflows with a large amount of parallel nodes. To handle that effectively, you can use {% c-line %}resourceRateLimit{% c-line-end %} by editing the[workflow-controller-configmap](https://argoproj.github.io/argo-workflows/workflow-controller-configmap.yaml) :


```text


```


#### Non-Root Users


You may have noticed a warning in the first workflow you submitted that looks like this:


```text


```


It is recommended that the user follow[security best practices](https://blog.argoproj.io/practical-argo-workflows-hardening-dd8429acc1ce) by adding the following config under {% c-line %}workflowDefaults{% c-line-end %} in the configmap:


```text


```


#### Access Control


​​For security reasons, it is recommended in production that you consider using role-based access control (RBAC) and {% c-line %}RoleBinding{% c-line-end %} to limit the access to the default service account. You can further integrate this RBAC setting with[SSO](https://argoproj.github.io/argo-workflows/argo-server-sso/#sso-rbac) to give different users different access levels. It is a significant advantage for enterprise organizations, allowing admins to give teams privileges limited to their namespace in a multi-tenant cluster.


Consider a quick example. The following manifest represents the permission you want a service account to have:


```text


```


Create the service account and bind the role using the following {% c-line %}kubectl{% c-line-end %} commands:


```text


```


Finally, submit your workflow using that service account you just created:


```text


```


As a result, you can better control what a workflow can do in the cluster and apply the principle of[least privilege](https://www.cyberark.com/what-is/least-privilege/) .


## Conclusion


Argo Workflows is an excellent tool if you’re heavily invested in Kubernetes at an organizational level. It’s cloud-native, straightforward, and cost-effective for managing complicated workflows on Kubernetes. Finally, since it is Kubernetes-native, you get all the benefits of Kubernetes— resiliency regarding crashes and failures, autoscaling, and more.


Whether your organization is a startup or an enterprise, Pipekit can help you scale while saving time and money.
