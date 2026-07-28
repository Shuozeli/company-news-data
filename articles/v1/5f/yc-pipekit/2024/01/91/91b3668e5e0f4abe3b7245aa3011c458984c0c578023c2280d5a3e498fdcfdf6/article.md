---
schema_version: "1.0.0"
document_id: "91b3668e5e0f4abe3b7245aa3011c458984c0c578023c2280d5a3e498fdcfdf6"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/debug-argo-workflow"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:19c950856d5eb226c77a78036886ff07591b74eb08eb8741b622f6e6a7c21e65"
---

# Two Ways to Debug an Argo Workflow

Let’s look at two different approaches to debugging your[Argo Workflow](https://argoproj.github.io/argo-workflows/) deployments.


First, we’ll use the[Argo CLI](https://argoproj.github.io/argo-workflows/cli/argo/) . Argo’s CLI commands cover many of the more common errors you see with workflows, such as misconfigurations. Then, we’ll see how to debug workflows using the Argo Workflows UI. After we’re finished with Argo’s native tools, we’ll wrap up with how to debug your environment using kubectl.


## **The Argo Workflows Command Line Interface**


Argo Workflows command line interface (CLI) makes interactions with your cluster simple. Below I will present how to run Argo commands directly from your Kubernetes cluster on a namespace called **argo** . Remember that you can quickly adapt the code shown below to your environment. To reproduce it in your environment, change the option to **-n <namespace>** where **<namespace>** is the Kubernetes namespace where you have Argo deployed.


### **Workflow Status with \`argo list\`**


I want to cover two commands: **argo list** and **argo get** . With **argo list** you can quickly identify the status of all the workflows deployed on the supplied Kubernetes namespace. And you can take a close look at each workflow with the **argo get** command. While both controls aren't dependent on each other, their combination should answer most of your questions about running pods. I suggest using the **-A** flag as shown below. Doing so will widen the search of all your namespaces.


```text


```


As you can see, the command returns in a tabular format an updated status of all workflows in your environment by namespace. Having it presented like this is useful for automated health checks of your services.


In cases where you want to focus your search on a specific namespace, the **argo list** command can also look for a single namespace thanks to the **-n** tag. This is useful when you have similar workflows deployed on different namespaces, a widespread scenario when managing[multi-tenant environments](https://whatis.techtarget.com/definition/multi-tenancy) . So, in cases like these, it's best to run **argo list -n <namespace>** , where **<namespace>** is the audited namespace **.** ‍


{% cta-1 %}


### **More Detail with \`argo get\`**


Once you have the service you need and its namespace, you can see more details with the **argo get** command. Executing the following command will give you a consolidated message per step of the Argo workflow. In our example, the workflow **dag-swtgb** exists on the **argo** namespace.


```text


```


Running the same command without the **-o yaml** option will return an output like the one below with a more consolidated view. It's helpful to see the message produced by your problematic pods.


*Argo get command output with errors*


### ‍ **Go Deeper with \`argo logs\`**


‍[Argo deployments](https://pipekit.io/blog/top-10-argo-workflows-examples) share the workflow deployments of every pod over the **main, init,** and **wait** containers. I will cover how to access them using kubectl in a bit, but you can also access them using Argo logs on the desired pod.


I should also point out that if your pod didn't start, those containers wouldn't start either.


You can follow a workflow’s logs with **argo logs.**


Consider this command line session:


```text


```


Output:


```text


```


When you submit a new workflow, Argo gives you its name.


Pass that name to **argo logs** with the namesapce and the **–follow** option:


```text


```


Output:


```text


```


Argo will echo the logs to the screen as the workflow progresses.


If you don’t want to use the command line, you can do this via the Argo Workflows UI, too.


### **View Your Argo Workflows Events in the Console UI**


You can also debug your Argo environment using the console UI it provides. This service is accessible by following one of the steps mentioned in[their docs](https://argoproj.github.io/argo-workflows/argo-server/#access-the-argo-workflows-ui) , but in this case, we will do a simple port forward between the Kubernetes deployment and the host. The code presented here can run flawlessly on Linux and macOS machines. These environments allow you to bind the port between your workstation and your Kubernetes cluster as a background process with this command: \\


```text


```


With the service accessible from the host, you can point any web browser to the address **https://localhost:2746.**


## **Auditing Your Workflows with kubectl**


There are scenarios where the Argo CLI output doesn't provide enough information for complete analysis of a pod.


For example, in some cases, your Argo server won't be able to access your token key, and It would be helpful to see how your control plane resolved this value. To do so, you can use kubectl commands to explore the configuration and health of your Argo Workflows instance. If dependent services aren't accessible, this method will help you.


Argo Workflows deploys three containers in each pod, and all are accessible using kubectl commands, as mentioned before.


{% related-articles %}


### **Getting your Argo deployment details with Kubernetes native commands**


Here we’re looking at the k8s cluster as a whole. Using the command below, you can retrieve high-level info about the health of your deployed services.


```text


```


This presents you with information about the k8s control plane for your **argo** namespace. From here, you can use {% c-line %}kubectl describe{% c-line-end %} for more detailed information.


Argo and Kubernetes use the same pod name for their deployed components. Bear that in mind if you plan to automate your pipelines with a mix of kubectl and Argo Workflows CLI combinations for your observability strategy.


So, use **kubctl describe** to view how Kubernetes sees your pod deployment. This should resemble what you see on the Argo console UI.


Kubectl generates a lot of output, so pipe it through **more** or **less.**


```text


```


It is good to note that the pod name will be the same in both kubectl and Argo CLI commands. You won't have any surprises when choosing which one you prefer to use in your analysis as long as you use the same pod name. So, running **kubectl logs -n argo pod/dag-swtgb-320908401 -c main** or **argo logs -n argo dag-swtgb dag-swtgb-320908401 -c main;** will then print the audit trace of your **main** container inside the Kubernetes pod **dag-swtgb-320908401** but using different command-line interfaces.


You can also explore the init and wait containers the same way as using the Argo workflow CLI commands. Though slightly different, it will return the detailed data from Kubernetes deployments. It's a personal choice whether you want to use kubectl or Argo native commands.


### Conclusion


You saw how to debug Argo Workflows components using the Argo CLI and Argo UI, or kubectl commands. The steps I described here can help you understand what's happening in your environment.


If you want more time to focus on your business and spend less time dealing with data leakage and your pipelines' security constraints, book your personalized demo with Pipekit. Pipekit can help you thoroughly understand your infrastructure with the correct automation pieces that will help you focus on your business instead of wrangling your data pipelines.


Special thanks to Eric Goebelbecker and Caelan Urquhart for help reviewing this post.
