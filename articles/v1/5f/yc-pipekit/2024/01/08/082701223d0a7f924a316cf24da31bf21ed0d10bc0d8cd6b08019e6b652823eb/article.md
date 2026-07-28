---
schema_version: "1.0.0"
document_id: "082701223d0a7f924a316cf24da31bf21ed0d10bc0d8cd6b08019e6b652823eb"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/archiving-argo-workflows-postgres-database-setup"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:00:19.733210+00:00"
content_hash: "sha256:ee4e3015fa26bf8cd25756898a14c2fe4e1f5aade5b7ed8f0504a2cbb5aacb7e"
---

# Archiving Argo Workflows: Postgres Database Setup

If you’re[familiar with Argo Workflows](https://pipekit.io/blog/what-is-argo-workflows) , you already know that it can drive your CI/CD pipelines, manage your ETL processes, and orchestrate any set of tasks you can imagine for a Kubernetes cluster. But did you know that[Argo knows how to archive the results of its workflows](https://pipekit.io/blog/top-10-argo-workflows-examples) to a SQL database, too?


In this post, I'll show how Argo Workflows archives workflow state into persistent storage using a Postgres database. To do so, I'll present a quick summary of Argo components while showing what it means to have your workflow archived. We'll deploy Argo Workflows alongside a Postgres database on a local Kubernetes instance using[k3d](https://k3d.io/v5.3.0/) . Finally, we’ll discuss some important security considerations for your Argo Workflows deployment.


So, let's get started.


## **What is the Archive Option in Argo Workflows?**


The ability to store past workflow runs provides you with an accurate record of your past workflow states. This blueprint is a game changer, as it makes it possible to provision your task sets based on real-time metrics, such as spikes in processing needs from past deployments.


The workflow archive option stores your workflow states in either MySQL or Postgres. Once you have archives configured, you can use them to better understand how your jobs run and where you might be able to improve.


For example, they can help you know when it's a good idea to scale your traffic with the help of temporary instances, which will also have their states stored on the same database. With all your states held over time, you can apply rules to adjust your cluster size based on previous usage; a good time series analysis could even save you some money in the end.


The archive stores only the previous workflow states, not their detailed instance logs. Another thing to keep in mind is detailed audit logs. The artifact store option handles the detailed logs persistent option, storing it locally by[MinIO](https://min.io/) . But you can also configure any other object storage option. This is covered in[the Argo docs](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) , where you can see how to use options such as Google Cloud Storage buckets or AWS S3.


{% cta-1 %}


But before we start on the technical implementation, let's have a quick refresher on the components of Argo Workflows. It's necessary to know how they correlate with the persistent storage for your archived workflows;[this image](https://argoproj.github.io/argo-workflows/assets/diagram.png) from the[Argo Workflows documentation](https://argoproj.github.io/argo-workflows/architecture/) presents an overview of the environment where a workflow resides:


*Argo Workflows architecture diagram. Source: Argo Workflows GitHub repo*


## **How to Deploy Argo Workflows with Persistent Storage**


Now that we know what's in store for us let's get started. We'll be using[k3d](https://k3d.io/v5.3.0/) to manage our local Kubernetes environment (instead of[minikube](https://minikube.sigs.k8s.io/docs/) and[VirtualBox](https://www.virtualbox.org/wiki/Downloads) ). In addition to k3d, you'll need to install[Docker](https://docs.docker.com/get-docker/) as an additional dependency. Using[kubectl](https://kubernetes.io/docs/tasks/tools/) to interact with your Kubernetes cluster works fine, too. However, I would encourage you to take a deeper look at[how to deploy Argo Workflows to production here](https://pipekit.io/blog/production-install-of-argo-workflows) , as we won't be producing production-ready components on this tutorial. In our tutorial, we'll be using local Kubernetes deployment scripts.


First, we'll start our local control plane with the following command:


```text


```


The successful creation will provide a log similar to this one:


Once we have our **cluster-demo** , we'll deploy our Argo Workflows instance. To install Argo Workflows, you'll need to execute the following commands:


```text


```


The first one creates a namespace called **argo** in your cluster, and the following line will deploy the Argo Workflows components on your cluster, as you can see below:


‍ **Creating the workflow-controller Configuration**


To run the workflow with the archive option, you must first change the persistence configuration to **archive:true** on your Argo server deployment. Changing it will tell your Argo server to store your workflow execution states into the database reported by the key **postgresql.**


We'll apply a new ConfigMap into our current Kubernetes **argo** namespace with the Postgres instance to store your archived workflows. You can then archive your workflows by using the **archiveLogs** option.


We had a Postgres instance deployed with the Quickstart YAML we used earlier. You'll need it only to apply the following configuration to your deployment. Changing this configuration enables your Argo server deployment to accept the **archiveLocation.archiveLogs** notation while creating your workflows. We'll start by creating a new **workflow-controller-configmap.yml** with the following content and saving it locally:


```text


```


### **Deploy Your Environment with kubectl**


We'll expose the Argo Workflows web UI using a load balancer on our **argo** namespace. The load balancer will expose the pod executing the web-facing component to connections made from outside Kubernetes.


```text


```


Your Argo server will restart with the new configuration in a couple of minutes. Feel free to check its status by running {% c-line %} **kubectl get -n argo svc,pod** {% c-line-end %} on your Kubernetes cluster.


```text


```


You can then bind your Kubernetes cluster and your host to port **2746** by running the following on your cluster:


```text


```


Congratulations, you just deployed Argo Workflows on a k3d cluster. To confirm that your local instance is up and running, go to[https://localhost:2746](https://localhost:2746/) .


*Argo Workflows user info UI page*


{% related-articles %}


## **Testing Your Deployment**


Congratulations on installing your Argo Workflows instance on your local Kubernetes cluster with the archive option. And now that we have checked that off our list, let’s archive our workflows. Adding the **archiveLogs** annotation lets you specify which ones you want to archive, as demonstrated in the following template, which we'll call **workflow-archive.yml** .


```text


```


We need to execute {% c-line %} **argo submit -n argo --watch -f workflow-archive.yml** {% c-line-end %} on a terminal to deploy it.


```text


```


By doing so, you'll start the **archive-location** workflow under the **argo** namespace; the following output confirms that our example ran successfully:


*Argo Workflows archive example run output log*


It doesn't change on the command line; however, as we have persistent storage for our workflows, you can see their previous states on the console UI. That'll give you the previous workflow states that ran with the archive options enabled—and going to the Argo Workflows console UI athttps://localhost:2746 , as we saw before, you can access the archived workflow UI option from the left menu bar’s icons. Once you are there, you can see all the past executions of a workflow. Your workflow history can be found in the UI under “Archived Workflows” (see below).


*Argo Workflows archived workflow console*


## **Security Best Practices for Archiving Argo Workflows in Postgres**


In our work, we deployed an Argo instance with the archive option configured with a Postgres database. As mentioned previously, this code isn't production-ready. As a next step, I suggest managing your[access tokens](https://argoproj.github.io/argo-workflows/access-token/) to secure your Argo instance.


A good practice is to avoid hardcoded values for server runtime information when possible. Your infrastructure should generate data like your Postgres hostname on runtime instead of having it hardcoded. Your infrastructure should use secrets to store sensitive information like repository access keys.


Take a look[here](https://opensource.com/article/19/6/introduction-kubernetes-secrets-and-configmaps) for more details on what Kubernetes information should be discreet. Adopting security best practices like this in the early stages is easier for both your users and developers as you start to scale. In addition, having your configuration automated ends up narrowing the[attack surface](https://csrc.nist.gov/glossary/term/attack_surface) of your environment while also reducing infrastructure management tasks.


[Here’s a helpful blog post with more Argo security best practices](https://blog.argoproj.io/practical-argo-workflows-hardening-dd8429acc1ce) from the Argo Workflows maintainer, Alex Collins.


## **Conclusion**


We deployed Argo Workflows locally and archived a workflow using a Postgres database in this post. The scripts here are good starting points to understand and experiment with the archive option of Argo Workflows, but keep in mind that some critical factors are missing for a fully cloud native environment.


[Pipekit](http://pipekit.io/) can help you orchestrate your whole Argo Workflows system. Kubernetes deployments are well known for being complex by their nature. And that's where Pipekit solutions can help with all the nitty-gritty of configuring your development pipelines, leaving you slimmer and more secure systems. Book your demo to see how Pipekit can help you explore your data.


Special thanks to Eric Goebelbecker and Caelan Urquhart for help reviewing this post.
