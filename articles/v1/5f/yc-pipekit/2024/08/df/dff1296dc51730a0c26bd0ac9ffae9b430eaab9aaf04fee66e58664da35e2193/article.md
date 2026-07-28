---
schema_version: "1.0.0"
document_id: "dff1296dc51730a0c26bd0ac9ffae9b430eaab9aaf04fee66e58664da35e2193"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/demystifying-argo-workflows-an-architectural-deep-dive"
published_at: "2024-08-07T17:05:22+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:59:29.484597+00:00"
content_hash: "sha256:44712dc461021090bad069a8b89b75621c1f290fa16dde40e9339e3f89b56d68"
---

# Demystifying Argo Workflows: An Architectural Deep Dive

Darko Janjić, Pipekit & Becky Pauley, Venafi Jetstack Consult


# **The Fundamentals**


Argo Workflows is a powerful workflow orchestration tool that allows us to orchestrate workflows in Kubernetes. A workflow is a set of actions to be run. It can be as simple as a single step like this ‘Hello world,’ example:


Or a workflow can have multiple steps. When a workflow has multiple steps, there are numerous questions and possibilities. These possibilities include the options to run steps in sequence, in parallel, or a combination of both. A workflow can also be used to orchestrate other workflows in what is called a workflow of workflows pattern. This pattern is applicable if you have a complex pipeline where you need to manage multiple dependencies between different tasks. Argo does this latter, complex managing action using a DAG, or graph. The flexibility of Argo means that it is optimal for running compute-intensive jobs like machine learning, data processing, and automating infrastructure and CI/CD pipelines. For the user, a resource can be defined as a kind of workflow, then submitted to the Kubernetes API, then the user can observe Argo Workflows do its job. But what’s going on behind the scenes?


# **Installation of Argo Workflows**


When Argo Workflows is installed, a number of resources are created in a cluster. Here is a simplified installation:


[(For real life installations, we recommend that you go look at the charts in the Argo Helm repository.)](https://github.com/argoproj/argo-helm)


We will look into more detail at our two deployments, our Workflow Controller and Argo Server, in addition to eight Customer Resource Definitions (CRDs). CRDs are what allow us to extend the Kubernetes API, to create customer resource types.


# **Customer Resource Definitions (CRDs)**


Some CRDs handle the creation and management of workflows. For example, a CRD can be created for a Workflow, and this allows interaction with a new Workflow customer resource as if it was a pod or a deployment. A CronWorkflow CRD can also be created, which allows workflows to be run on a schedule. Or, the WorkflowTemplate and ClusterWorkflowTemplate can be created, which would allow a library to be defined, made up of reusable workflows for use within either a Namespace or a cluster. The remaining CRDs in the photo above handle exchange of data between the main workflow controller and the Argo Executor, storing the output of Workflow tasks, automated garbage collection of Workflow artifacts, and Workflow event bindings, which allows events to be specified that can trigger Workflows.


# **How do we orchestrate Workflows?**


Now that we have context on the CRDs defined in Argo Workflows, and now that these resources exist in our cluster, how do these workflows happen? Enter the Workflow Controller.


# **Workflow Controller**


The Workflow Controller is the main component of Argo Workflows. It does all the heavy lifting. Its job is to interact with CRDs. It manages Workflows and everything Argo Workflows related.


The Workflow Controller implements the Kubernetes operator pattern; it is basically a Kubernetes operator. It defines the way for configuring, deploying, and orchestrating instances on behalf of a human.


When you need to manage a complex application, the various tasks that require monitoring can take up time, resources, and energy. Operators automate these monitoring tasks so you focus your work elsewhere.


Since the Workflow Controller is an operator, it mostly talks with Kubernetes. You can run the Workflow Controller in high availability mode or you can have namespaced deployments.


In high availability deployment, one instance is a leader and others are in standby mode. When a leader goes down, an election happens, and a new leader is selected. This selected leader continues the work.


You can also deploy the Workflow Controller per namespace. In this case, each Workflow Controller is responsible for Workflows in its own namespaces. This way, the pressure on a single Workflow controller is decreased.


If you’re familiar with the operator pattern and the inner workings of the Workflow Controller, this will be familiar to you. If not, here is a brief overview:


When a Workflow is created, a Workflow Custom Resource (CR) is actually what is being created behind the scenes. This CR is going to exist even without the Workflow controller. It will exist in Kubernetes in the etcd, but there will be nothing to make the Workflow run. So the Workflow Controller detects that there is a Workflow CR and it acts upon it. This process happens using informers. An informer is an abstraction that allows the Controller to not constantly talk to the Kubernetes API, but to only act on change. This relieves pressure on the Kubernetes API. In the end, a Workflow CR is added to the Workflow queue and workers are processing your Workflow.


Workers are the components that are doing the actual job. They inspect the Workflow CR and they perform the appropriate actions such as creating pods or pod reconciliation.


You can interact with the Workflow Controller using kubectl, but Argo Workflows has another solution to make your life easier. This component is the Argo Server.


# **Argo Server**


The Argo Server is mostly used for communication with the outside world and is usually used by users not familiar with Kubernetes. The Argo Server provides an API that people can use.


For example, if you do not like kubectl, but you still want to manipulate Workflows using a terminal, you can use Argo Workflow CLI via Argo Server. Meanwhile, the Workflow Controller is not exposing anything that can interact with an end-user. Without the Argo Server and its API layer, you cannot use the Argo CLI.


The Argo Server is not a mission-critical component, but it has some functionalities that are important and highly useful.


The Argo Server is also responsible for authentication. You can use the standard Kubernetes authentication or you can use single sign-on using[Dex](https://dexidp.io/) . Dex is a tool responsible for authentication and supports a wide-range of identity providers and protocols.


But the Argo Server also has features like Workflow Archive, Offloading large Workflows, and Events. Concerning Workflow Archive, you can use kubectl to list your workflows, but you will only get Workflows that exist inside Kubernetes, not Workflows that exist in your archive. You need to use CLI, UI, or Argo Server API to retrieve them.


You can also trigger your Workflows using Workflow Events. You just need to create a WorkflowEventBinding CRe with the appropriate selectors.


# ‍ **How is a Workflow Created?**


First, you submit the workflow using the CLI, UI or API, then the Argo Server receives your request and creates a Workflow CR using the Kubernetes API. The Workflow Controller detects that there is a CR that requires action and starts examining that CR, creates all the pods that are needed, then monitors the workflow status.


# **A Closer Look at the Pod**


An understanding of the Kubernetes pod is useful and important for deeply understanding Workflows. Regardless of how simple or complex our Workflow is (single step vs. numerous steps), a step in our Workflow is almost always equal to one running pod. Each step, or task, in our Workflow runs as its own pod. Of course there are a few exceptions that include using a suspend template or a Workflow of Workflows pattern.


But it is important to keep in mind that a step is almost always a pod. This concept is essential to grasp because when it is understood that a step is simply a pod running in Kubernetes it helps the user approach questions differently. Even if a user has little knowledge of Argo Workflows, perhaps they have a good understanding of Kubernetes. If they can do a certain task in a normal Kubernetes pod, they can also do it in a Workflows step.


‘Podness’ improves an understanding of setting resource requests and limits, thinking about quality of service classes, and node sizing. For pods to perform actions they need to be given the correct RBAC permissions. Volumes and containers can be mounted to each step and metrics can be gathered about each step because it is a pod.


Each step has its own workspace. This means that it is important to think about saving off and fetching artifacts, and the parameters between steps. The wait or init containers can help with these processes.


The Argo Workflows GitHub repo has some great examples of these processes. You can also[read our other blog posts on how to do this using Minio or your Cloud Object Storage provider of choice](https://pipekit.io/blog/how-to-set-up-a-minio-artifact-repository-for-argo-workflows) .


# **What is going on inside the Pod for each step in my Workflow?**


If we zoom in to our pod running our Workflow step, then we will see three containers. First, we have an init container. The init container runs first when our pod starts, fetching artifacts and parameters, and making things available. Once we have those dependencies, our main container can run. The main container is what is actually executing the desired actions for our step. Depending on the step template that we use, the main container can function in different ways.


If we look at the step template available to us, we can see how the main container works more clearly in some cases than in others. When using the container template, the script template, or the container set template, we define the main containers (container where our steps should run) in a way that looks a lot like a pod spec:


There is still some level of abstraction: Argo exec is mounted as a volume to our main container so it’s the Argo exec utility that actually serves as the main command for our container, and it calls the command we configured as a subprocess.


But what about templates where we don’t explicitly define a container in our Workflow, such as a HTTP template or resource template? These still run inside a pod. In these cases, although we don’t explicitly define a container for our step to run in, Argo handles this for us. It contains its own main container inside a new pod for our step, using the Argo exec image. So for these step templates, a step is still a pod, but the container used is abstracted away from us in the template definition.


The wait container waits and performs tasks that are needed for clean up; so saving off parameters and artifacts for object storage.


# Wrapping up


By understanding the workings and infrastructure behind Argo Workflows, we hope that you can now better orchestrate your workflow pods within your Kubernetes cluster. Remembering that a step in a Workflow is almost always equal to one running pod will help you ask the right questions and execute the right processes to achieve your workflow needs.
