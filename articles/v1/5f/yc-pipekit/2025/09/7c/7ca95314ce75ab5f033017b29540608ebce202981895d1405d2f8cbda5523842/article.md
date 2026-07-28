---
schema_version: "1.0.0"
document_id: "7ca95314ce75ab5f033017b29540608ebce202981895d1405d2f8cbda5523842"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/quick-guide-argo-events"
published_at: "2025-09-11T19:31:40+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T21:59:45.283870+00:00"
content_hash: "sha256:9c071a06f8adba605807747027b4967e1c27ad7089fcb26b2115bb22362d72bc"
---

# A Quick Guide to Argo Events

Asynchronicity is at the heart of event-driven, decoupled, cloud-native applications. As applications cover more features and use cases, they expand internally and externally in terms of service integrations. Consequently, application workflows get more complex with more interdependencies. This makes independently scaling applications' various components challenging, especially with unpredictable workloads. Container-based deployments, with the help of efficient workflow automation engines like[Argo Events](https://argoproj.github.io/argo-events/) , can help solve this problem.


Argo Events is an event-driven workflow automation engine that helps you define and manage dependencies for Kubernetes from multiple event sources. Argo Events can help you take action and trigger Kubernetes objects for further processing based on the data consumed from these various event conceptions. This gels perfectly well with another Argo project called[Argo Workflows](https://argoproj.github.io/workflows/) , which helps you create complex workflows in Kubernetes.


This article will take you through the basics of Argo Events and some of its prominent use cases.


## Why Do You Need Argo Events, and How Does It Work?


Argo Events helps you mimic the complexity of real-world scenarios with the power of Kubernetes. You can create dynamic, event-driven workflows for all your data and web applications. Argo Events has three main components: EventSources, sensors, and triggers.


EventSources, as the name suggests, are the various sources that your application might receive events from, such as[Amazon S3](https://aws.amazon.com/s3/) ,[Amazon SNS](https://aws.amazon.com/sns/) ,[Amazon SQS](https://aws.amazon.com/sqs/) , webhooks, message queues, and[Google Cloud Pub/Sub](https://cloud.google.com/pubsub/docs/overview) . The messages received from these event sources are stored in an EventBus, which acts as a publish-subscribe system in Argo. All the events from EventSources get accumulated in the EventBus and are then consumed by various sensors.


Sensors are at the core of dependency management in Argo Events. A sensor listens to the EventBus for certain events, conditional triggers, and actions. Based on their business logic, sensors can trigger various actions to complete your event workflow. Some examples of these actions include invoking an AWS Lambda function, creating Kubernetes resources, or triggering an Argo Workflow or an[Argo Rollout](https://argoproj.github.io/argo-rollouts/) .


## How Do You Get Started with Argo Events?


You only need to follow a few simple steps to get started with Argo Events, but before that, please make sure that you have the following installed on your machine:


- A local[Kubernetes](https://kubernetes.io/) cluster using[minikube](https://minikube.sigs.k8s.io/docs/)
- [Docker Engine](https://docs.docker.com/engine/install/)
- The[kubectl](https://kubernetes.io/docs/tasks/tools/) command line tool


Once you have these tools, you can start installing Argo Events using the steps described in the next section.


### Installing Argo Events


You have several options for installing Argo Events. This tutorial will take you through the installation process using {% c-line %}kubectl{% c-line-end %}. Alternatively, you can use[Kustomize](https://argoproj.github.io/argo-events/installation/#using-kustomize) or[Helm](https://argoproj.github.io/argo-events/installation/#using-helm-chart) to complete the installation.


#### Deploy Kubernetes on Your Local Machine Using minikube


Before installing Argo Events, you need to ensure that the minikube context is up and running on Docker Engine. You can use the following commands to install and start minikube on your machine:


```text


```


Once you run these commands, you'll see an output similar to the one in the image below:


Starting minikube


Alternatively, you can also check your Docker Engine containers to see your minikube instance's status, as shown in the image below:


Checking Docker Engine containers


You're now ready to install Argo Events.


{% cta-1 %}


#### Create the Namespace


Namespaces in Kubernetes are used to isolate groups of resources in a cluster. Kubernetes comes with a {% c-line %}default{% c-line-end %} namespace, but it's good practice to create a separate namespace. Using the following command, create a namespace called {% c-line %}argo-eventsdefault{% c-line-end %}:


```text


```


All services and pods related to EventSources, sensors, and triggers will be created in this namespace. To check if the namespace was successfully created, run the following command:


```text


```


The command should have the following output:


Getting namespaces


#### Run the Installation in the argo-events Namespace


The[Argo Events documentation](https://argoproj.github.io/argo-events/) provides an installation manifest that you can use to deploy the following resources:


1. **Argo Events service account:** This helps Argo Events communicate with the Kubernetes API.
2. **ClusterRoles:** These specify what permissions the service account has, and you can create role bindings based on your requirements.
3. **Controllers:** These control Kubernetes resources for sensors, EventSources, and the EventBus.


You can use the following command to run the installation:


```text


```


The above command will create a controller-manager pod, as shown in the following image:


Checking controller-manager pod status


Now that the service account, cluster role bindings, and controllers are created, you need to deploy at least one instance of each to see Argo Events in action.


#### Deploy the EventBus


A Kubernetes custom resource called the EventBus delivers messages from EventSources to sensors. It's essentially a source- and target-agnostic pub-sub system, where EventSources publish events and sensors subscribe to those events to take further action (for instance, trigger Argo Workflows).


The following command retrieves the configuration file from the[Argo Project website](https://argoproj.github.io/) and creates the EventBus:


```text


```


The EventBus specification defaults the number of replicas to three, so one service and three pods are created after you run the command:


Checking EventBus installation status


#### Deploy a Webhook EventSource


EventSources are responsible for publishing messages accumulated in the EventBus for sensors to consume. As mentioned earlier in the tutorial, there are several EventSources, such as Amazon SNS, Amazon SQS, Google Cloud Pub/Sub, GitHub, Slack, webhooks, etc.


The following command installs a basic webhook EventSource:


```text


```


Checking webhook EventSource pod status


A webhook source is an EventSource that works via a general-purpose REST API context, which is used in many other EventSources, such as Stripe, Slack, Amazon SNS, GitLab, GitHub, Bitbucket, and so on.


#### Deploy a Webhook Sensor


Sensors don't just listen to events; they also act on those events to trigger actions. Sensors, therefore, are a combination of events and triggers. For example, AWS Lambda is a sensor; it will listen to any given EventSource and trigger an action based on the events from that EventSource.


Use the following command to create a webhook sensor:


```text


```


This command deploys the webhook sensor, which runs in a new Kubernetes pod:


Checking webhook sensor pod status


Now that you have the basic framework for listening to events, passing them on, and triggering workflows based on those events, you should be able to trigger workflows using sample events. The next section will take you through working with Argo Events.


### Using Argo Events


If you've succeeded in running the commands in the previous sections, you should be able to test your installation using the following command, which will list the service for the EventSource:


```text


```


Getting the list of services in the \`argo-events\` namespace


While the services and pods are up and running, you'll need to set up port forwarding for message delivery and consumption over HTTP.


To set up port forwarding, you need to get the pod name of the webhook EventSource and store it in the {% c-line %}EVENT_SOURCE_POD_NAME{% c-line-end %} variable using the following command:


```text


```


Now, use the following command to establish port forwarding:


```text


```


Once port forwarding is successfully set up, your Argo Events should be able to receive requests and trigger the creation of Kubernetes resources to service those requests.


{% related-articles %}


### Triggering Pod Creation


In the following example, you'll submit a POST request to the EventSource pod, listening at port 12000:


```text


```


This POST request to the EventSource triggers a message to be published to the EventBus, which, in turn, triggers the sensor to create a new pod to complete the process. The above command should result in an output similar to the one shown in the image below:


Showing the creation of a new pod for a workload generated by an HTTP POST request


Sending the POST request a second time should create a second workload pod, as shown below:


```text


```


Use the following command to see the pod scheduling, creation, and run in action:


```text


```


Showing the creation of a new pod for a workload generated by another HTTP POST request


For a more detailed version of events along with the pod details, use the following command:


Running the {% c-line %}kubectl describe{% c-line-end %} command will give you all the details of a pod, from specifications to events, as shown in the command's output:


Describing a workload pod to see more details


### Validating Workloads


Finally, you can find out whether your process succeeded by checking whether the message was published in the new pod using the following command:


```text


```


This lists all the pod instances created for POST requests on the {% c-line %}app{% c-line-end %} hosted on your local machine, communicating over port 12000. It lists the outputs of all the workloads one after another in ascending order:


Validating workload pod outputs


This concludes the walkthrough for creating a webhook-based EventSource and sensor in Argo Events to generate a simple workload to receive and print a message. You can also use[this GitHub repository](https://github.com/kovid-r/a-quick-guide-to-argo-events) to get the installation and usage commands for this tutorial.


## Conclusion


This article took you through the basics of Argo Events with a guided tutorial on its installation and usage. It also discussed some prominent Argo Events use cases.


Argo is open source and free to use; you can deploy it yourself, but opting for[Pipekit's](https://pipekit.io/pricing) managed Argo Events offering can have some significant benefits. Pipekit allows you to run multicluster workflows from a central user interface or an API. Additionally, it can help you efficiently manage custom namespaces. It also supports all major cloud platforms, so if you're going for a multicloud setup, you could benefit greatly.
