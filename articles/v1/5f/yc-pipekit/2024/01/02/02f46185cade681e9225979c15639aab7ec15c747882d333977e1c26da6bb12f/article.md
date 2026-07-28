---
schema_version: "1.0.0"
document_id: "02f46185cade681e9225979c15639aab7ec15c747882d333977e1c26da6bb12f"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/set-up-retries-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:47f718b96c136f2a32161294bc445fe99f2a4883bba2a3e15d177a0f7f6403b3"
---

# How to Set Up Retries for Your Argo Workflows

# How to Set Up Retries for Your Argo Workflows


[Argo Workflows](https://argoproj.github.io/argo-workflows/) , the workflow orchestration engine for Kubernetes, enables your business to run parallel jobs on a cluster based on a[directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (DAG) structure. You can build complex jobs like[ETL pipelines](https://en.wikipedia.org/wiki/Extract,_transform,_load) using simple, containerized, and maintainable steps in a workflow that’s easy to understand.


To create robust workflows, though, you also need to be able to manage errors. If you understand what is going wrong within and between steps, you can implement retry mechanisms to avoid job execution failures.


In this tutorial, you’ll learn about using retries in Argo Workflows to improve your projects.


## About Retries in Argo Workflows


The Argo Workflows retry system uses errors reported by the Kubernetes cluster to decide the next action to take, based on the retry strategy you have configured for that step. The following flowchart summarizes how this works:


Argo Workflows retry path


### Use Cases


The Argo Workflows retry system is useful for locating and managing specific errors that can be resolved with a retry and that don’t pose any risk to the system in terms of availability or integrity.


For example, when starting a large system such as a database, you might have to wait and poll its status before continuing the workflow. You could use a simple container to poll the database status and exit with a success code when the system is ready, or with an error code when it’s not. In this case, implementing a simple retry strategy in Argo Workflows to poll every X seconds with a limit would offer a clean solution.


[Another example](https://pipekit.io/blog/top-10-argo-workflows-examples) would be a task that queries an external API with a rate limit. Using Argo Workflows with a retry strategy and a backoff factor would allow your workflow to recover without overloading the remote API.


{% cta-1 %}


### Retry Policies


The Argo Workflows retry policy allows you to configure the type of errors that should be retried. There are four available policies:


- OnFailure is the default policy. It stipulates that Argo Workflows will only retry a step if the container reports a non-zero exit code. Other errors, such as a failure to initialize the container, will not trigger a retry and will instead cause the step and workflow to fail.
- Argo Workflows classifies any external Kubernetes or internal errors outside the containers in the OnError category. OnError does not include OnFailure errors, so it will not retry if the container is started but returns a non-zero exit code (use Always if you need both conditions).
- The OnTransientError policy will only retry the step on[specific transient errors](https://github.com/argoproj/argo-workflows/blob/master/util/errors/errors.go) , such as networking errors thrown when connecting to the Argo Workflows database or the Kubernetes cluster. This is a subcategory of the OnError policy.
- With the Always policy, Argo Workflows will attempt to retry the step on any kind of error reported by Kubernetes. This is equivalent to using both OnFailure and OnError.


You can also use[conditional expressions](https://argoproj.github.io/argo-workflows/retries/#conditional-retries) to control retry decisions if the policies above are not sufficient. A conditional expression allows you to use specific environment variables to determine if the Argo Workflows engine should retry the step.


## How to Set Up Retries in Argo Workflows


This tutorial assumes you have a functioning Kubernetes cluster and that you are using kubectl.


You can create a cluster on[AWS EKS or GCP GKE](http://pipekit.io/blog/production-install-of-argo-workflows) , or locally, on your computer using any of the following:


- MiniKube
- K3s
- Docker Desktop


### Installing and Setting Up Argo Workflows


Install Argo Workflows on Kubernetes with the following commands:


```text


```


This will create the Argo Workflows namespace, services, and an embedded PostgreSQL service to store all permanent states. For[production installation of Argo Workflows](http://pipekit.io/blog/production-install-of-argo-workflows) , refer to the[installation documentation](https://argoproj.github.io/argo-workflows/installation/) , which includes provision for security, scalability, and disaster recovery.


Next, install the Argo command line app from the[release page](https://github.com/argoproj/argo-workflows/releases/tag/v3.3.1) . You can verify the installation with the following command:


```text


```


Optionally, you can make the Argo Workflows web interface available on the running instance:


```text


```


Connect to the Argo Workflows interface at https://localhost:2746. You’ll see the following welcome page:


Argo Workflows welcome page


### Configuring the Default Workflow Retry Strategy


Start by creating a successful workflow. The examples here will use an Alpine image and some bash commands.


Create a file called test-001-no-retry.yaml:


```text


```


Run the workflow with this command:


```text


```


This will run the workflow, refresh the console, and exit successfully. If you change exit 0 to exit 1, though, the output will confirm that the step is failing due to the lack of retries:


```text


```


Next, add a simple retry strategy. Create a file named test-001-simple-retry.yaml with the following content:


```text


```


Remember that by default, the retry policy used by Argo Workflows is OnFailure and that Always includes OnFailure and OnError.


Next, run the below command:


```text


```


After the initial attempt, Argo Workflows will retry the same step three more times and eventually fail:


```text


```


Note that any error in the command, arguments, or the container itself will generally fall into the OnFailure category. This includes the following conditions:


- The Docker image command binary is not found.
- The Docker image command binary file is not executable.
- You pass invalid arguments to the executable in the workflow configuration.
- You specify an invalid image architecture (such as trying to run a non-ARM64 compiled image on an AMD64 system).


### Using the OnError Retry Strategy


OnError is mainly for “external” errors happening to the Kubernetes cluster outside of Argo Workflows’ control and logic. One example is if the pod started by Argo Workflows is deleted during its execution due to external factors like compute node termination.


To demonstrate the difference in retry behavior, create a new workflow file called test-002-delete-pod.yaml:


```text


```


Now run it:


```text


```


If you wait around 50 seconds, you’ll see the container starts, sleeps for 30 seconds, and then exits with a non-zero exit code. As the Argo Workflows retry policy is only {% c-line %}OnError{% c-line-end %}, container errors are not caught and the workflow will be marked as {% c-line %}Failed{% c-line-end %}:


```text


```


But if you rerun the workflow with the command below and kill the pod while it’s running:


```text


```


Followed by this command in a separate window (replacing the pod name for your use case):


```text


```


You’ll see that Argo Workflows will retry the step, because pod deleted falls into the OnError category:


```text


```


{% related-articles %}


### Using the OnTransientError Policy


It’s difficult to reproduce and provide a workable demo of the transient error, but in general:


- OnTransientError is a subset of OnError, so using OnError covers all transient errors.
- The following error messages are classified as transient errors:
- Exceeded quota
- The operation cannot be fulfilled on resource quota
- Connection closed by foreign host
- NET/HTTP: TLS handshake timeout
- I/O timeout
- Connection timed out
- So are the following Golang error classes:
- [net.DNSError](https://golang.google.cn/pkg/net/#DNSError)
- [net.OpError](https://golang.google.cn/pkg/net/#OpError)
- [net.UnknownNetworkError](https://golang.google.cn/pkg/net/#UnknownNetworkError)


These errors are external to the container and thrown during the Argo Workflows orchestration, either when making API calls to Kubernetes or when accessing its database.


You should use the OnTransientError policy when the other two policies are not suitable for the retry operation, yet you still want to avoid any issues in the workflow due to a temporary glitch in the Kubernetes infrastructure.


### Using a Backoff Period between Retries


When external resources like third-party APIs cause failures, you should configure a backoff system to avoid flooding the external API and improve the odds of a successful retry.


You can configure the backoff system with three values:


- The duration must be configured as a[string](http://docs.golangjob.cn/pkg/time/#ParseDuration) . The default unit of duration, if not provided, is in seconds, but it can be in minutes, hours, or even days. This is the initial duration to wait for the first retry.
- The factor is the number to multiply the duration with between each retry. So, 1 would indicate the same duration between every wait period, while 2 would indicate doubling the retry duration between each consecutive wait period (see example below). This must be an integer.
- The maxDuration is a circuit breaker value similar to the retry limit. It’s used to abort retries if the duration becomes too large due to the values you set for factor and the number of retries. maxDuration is calculated from the start time of the first attempt on the step.


The duration is the only mandatory parameter when using backoff, and if used by itself, there’s no maxDuration and the factor is 1.


The following are some configuration examples.


This setting configures a constant wait time of 30 seconds between each retry, with a limit of four retries:


```text


```


Here, the step will be executed five times at most with a sleep between each retry of 30, 60, 120, and finally, 240 seconds.


```text


```


In the following example, the step will retry every 30 seconds as many times as possible, but overall, not spend more than 75 seconds on it. If the step takes more than 75 seconds, both the step and the workflow will be marked as Failed. The limit is needed for the retry strategy to work but is set to an arbitrarily large enough value to be ignored.


```text


```


## Conclusion


The retry function is an important tool to help you scale up your Argo Workflows projects in Kubernetes. As demonstrated above, Argo Workflows provides a robust and straightforward mechanism to retry any workflow step in a controlled fashion.


By using an appropriate policy like Always or OnFailure, setting a limit via limit or maxDuration, and optionally using a backoff mechanism between retries, you will be able to configure a good retry strategy on every step of your workflow.


There are ways to automate this process as well. Pipekit offers an orchestrated control plane for quickly and easily managing multiple workflows, either on your self-hosted Kubernetes cluster or on Pipekit’s managed environment.
