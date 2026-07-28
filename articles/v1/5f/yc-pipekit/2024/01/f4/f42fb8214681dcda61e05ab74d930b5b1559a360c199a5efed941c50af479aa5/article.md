---
schema_version: "1.0.0"
document_id: "f42fb8214681dcda61e05ab74d930b5b1559a360c199a5efed941c50af479aa5"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/top-10-argo-workflows-examples"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:d1ba4fc6bd66554d02c3e6652529452e574f4a0e8a4112f942f710f645ad83b5"
---

# Top 10 Argo Workflows Examples

We all know how[Argo Workflows](https://argoproj.github.io/argo-workflows/) makes it easy to orchestrate parallel jobs on Kubernetes. While it’s most often associated with data processing and ETL projects, it’s useful for a lot more! These 10 workflows will change the way you see this Kubernetes orchestrator.


Let’s dive in!


## **Argo Workflows Setup**


If you don't currently have a workflow running, I suggest you[create your first Argo Workflow](https://pipekit.io/blog/what-is-argo-workflows) to understand what we'll discuss in this post. To do so, follow the instructions[here](https://argoproj.github.io/argo-workflows/quick-start/) to create a local Argo Workflows deployment on your cluster. I also suggest using k3d for your local Kubernetes control plane; this tutorial uses a[k3d](https://k3d.io/v5.3.0/#install-script) cluster named argo. Feel free to reproduce the command below to create it in your environment:


```text


```


Now let's jump into looking at our first example!


{% cta-1 %}


## **1. Enhancing Your Workflow Using Parameters**


Argo uses[custom resource definitions](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) stored on YAML files to manage its deployments. So no need to learn new specs to manage your infrastructure; you can follow the same pattern used on your Kubernetes and[Kustomize](https://kustomize.io/) scripts, which helps you remain consistent. Below we can see how to use parameters on your workflows, and passing parameters is handy when your configuration uses runtime values. As a result, you will know some components only after creating them, such as[access tokens](https://en.wikipedia.org/wiki/Access_token) .


```text


```


In our template, the parameter **message** will have the default value of **Message string default value** . However, this value can be overwritten at runtime, as we can see by running the command below:


```text


```


We can validate the output from the Argo Workflows Logs UI. (You can access the UI by default at[https://localhost:2746/](https://localhost:2746/) if you quickly follow the port forwarding instructions while creating your cluster.)


*Log of Argo Workflows with dynamic parameters*


## **2. Pulling Images From Your Secured Repository**


One of the features I like when automating an ecosystem is using rotational access keys while managing my services' access. This is useful in cases where your company uses private container repositories to host your container images. Argo Workflows helps you achieve this with the native support of Kubernetes secrets. In our example, we can see that the secret **docker-registry-secret** will pull the image **docker/whalesay:latest** .


```text


```


## **3. Using Sidecar Containers**


One of my favorite things to do is to use sidecars while starting my[pods](https://pipekit.io/blog/clean-up-pods-save-logs-argo-workflows) . Kubernetes sidecars are useful helpers that can handle recurring tasks, such as syncing your Git repositories, as shown[here](https://github.com/kubernetes/git-sync) . Argo Workflows has this covered with neat support for sidecar containers out of the box.


```text


```


To deploy it, save the above code as **sidecar-nginx.yml** and submit it:


```text


```


And as a result, you'll deploy an NGINX's reverse proxy sidecar instance.


Pro-tip: you might need to pay some extra attention to your workflows if you’re using[Istio](https://istio.io/) . Look at this[GitHub thread](https://github.com/argoproj/argo-workflows/issues/1282) if you're thinking of using it as a[service mesh](https://en.wikipedia.org/wiki/Service_mesh) .


## **4. Archiving Your Current Workflow State on Persistent Storage**


Workflow Archive is a nice feature that Argo Workflows provides so you can have previous workflow states stored on a relational database (Postgres or MySQL for now). However,[Argo's archive](https://argoproj.github.io/argo-workflows/configure-archive-logs/) won't keep detailed execution logs; you'll need to configure an[artifact](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) repository, like MinIO, to do so.


To use the archive feature, you'll first need to configure your Argo server's persistent storage option. You'll need more information about how to configure it to do so. Following[this link](https://argoproj.github.io/argo-workflows/access-token/#token-creation) will help you with the authentication piece required for the Argo archive; then base your configuration on[this file](https://argoproj.github.io/argo-workflows/workflow-controller-configmap/) . You'll need to have them appropriately configured with your Argo server to benefit from this feature. Once it's configured, you can store your workflows with the **spec.archiveLocation.archiveLogs** as demonstrated below.


```text


```


## **5. Passing a Git Repository as an Input Artifact**


Another cool feature that Argo Workflows provides out of the box is the possibility to sync your Git repository without the need for extra sidecars or init containers. The code below connects to the[https://github.com/argoproj/argo-workflows.git](https://github.com/argoproj/argo-workflows.git) repository. You can choose from HTTP or SSH pull requests for the authentication piece. In the first template, **git-clone** , you'll need to use the combination of **usernameSecret** and **passwordSecret** Kubernetes secrets to access a URL in its HTTP format. You can see an example of an HTTP Git configuration in the code below.


```text


```


Argo Workflows also supports SSH connectivity (e.g., **git@github.com:argoproj/argo-workflows.git** ). However, it needs the URL format following the SSH connectivity and the **sshPrivateKeySecret** Kubernetes secret instead of the **usernameSecret** and **passwordSecret** ones.


## **6. Creating Directed Acyclic Graph Workflows**


I feel the directed acyclic graph (DAG) is now getting the attention it deserves on the analytics domains because of how it impressively handles data processing workload steps on[Apache Spark](https://spark.apache.org/docs/3.2.1/index.html) and its use as a common data orchestration pattern with Apache Airflow. With Argo Workflows, you'll have a Kubernetes-friendly interface instead of the need to configure a Kubernetes executor for Airflow which is less stable.


I suggest checking this[link](https://www.techopedia.com/definition/5739/directed-acyclic-graph-dag) to learn more about how a DAG works. Below, you can see how Argo Workflows instantiates it.


```text


```


Each task will be passed to the Argo server using the **target** parameter name, with the target names separated by spaces. Argo Workflows will execute only the ones you specify; however, it'll run each dependency until it reaches the informed targets. In plain English, say we save our file as **dag-targets.yml** and execute using the following command:


```text


```


It will skip only **target D** , as demonstrated below:


*Argo Workflows DAG execution results*


## **7. Execute Python Scripts**


Containers already make it easy to manage runtime environments. So, it’s easy to build a Python container with the libraries and version you need for your Python-based workflow steps.


With Argo Workflows you can call a Python script that’s already installed on the container by name, or pass in code via a **source** field in workflow description. You can specify any valid code in the source block.


Here’s an example:


```text


```


## **8. Implementing a Retry Strategy**


Sometimes, multiple targets can implement some retry logic, and Argo Workflows configures your[retry strategy](https://argoproj.github.io/argo-workflows/retries/) on the Workflow level.


```text


```


In our example, the target **retry-container** will try to restart three times in the cases that it finishes with an Error status on Kubernetes.


## **9. Adding Conditional Workflows**


Conditional workflows are also among my favorites and are so simple to implement. You can deploy your architecture based on the return statuses of previous steps, which is very handy when orchestrating a set of containers. Argo Workflows grants you the possibility of executing targets based on a boolean condition. Under the hood, it uses[govaluate](https://github.com/Knetic/govaluate) to allow you to use Golang's[expr statements](https://github.com/antonmedv/expr) .


So you'll be able to orchestrate your conditions in the same way you handle your Golang helpers on your Kubernetes ecosystem—another nice extra benefit of using Kubernetes CRDs.


```text


```


Saving the above code as **cond.yml** and executing with **argo submit** will give the following output:


```text


```


*Argo Workflows conditional execution results*


## **10. Managing Kubernetes Resources From Your Workflow**


Argo Workflows can create Kubernetes components; this is very handy when you need to develop temporary kubelet actions in a declarative way. This feature follows the same principle of the inline scripts to deploy Kubernetes components responsible for applying patches to your environment. However, Argo Workflows handles this code's[Kubernetes CRD](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#customresourcedefinitions) YAML inline files.


```text


```


This feature covers you as you directly run all kubectl actions, which allows you to create/update/delete any Kubernetes resource on your cluster using inline[Kubernetes API groups](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/) definitions.


{% related-articles %}


## **Conclusion**


The advances we’ve seen in systems management and development give us many reasons to be optimistic. For instance,[infrastructure as code](https://en.wikipedia.org/wiki/Infrastructure_as_code) allows you to have the same infrastructure on your scalable servers and your local workstation. Tools like Argo Workflows help us create scalable production-ready infrastructure on our local workstation, and that by itself is something to cherish.


With constant infrastructure requirement changes such as[dynamic DNS](https://en.wikipedia.org/wiki/Dynamic_DNS#:~:text=Dynamic%20DNS%20(DDNS)%20is%20a,hostnames%2C%20addresses%20or%20other%20information.) , you need to adapt your deployments to a more modular approach. These workflows are the must-haves for any DevOps admin. But this list is only the beginning. I would highly suggest implementing these scripts in your development and data pipelines.


Book your demo with Pipekit if you want to have them orchestrated seamlessly without the need for in-house capacity. Give your users the peace of mind of experimenting and developing new features for your application with a better cost ratio for your ROI.


Special thanks to Eric Goebelbecker and Caelan Urquhart for help reviewing this post.


Until next time!
