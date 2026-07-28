---
schema_version: "1.0.0"
document_id: "a8a2f94d2f59315b319ee6d74f9cf5bed339b2f27533338f691442afa29d505c"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-workflows-spark"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:00:19.733210+00:00"
content_hash: "sha256:3fb966b1c0caae6ff4475d5b1d8256af6f81d7db8a0dc9c9deb3d348093352f1"
---

# How to Use Argo Workflows with Spark

As a data scientist, you frequently need a way to run several[big data operations](https://pipekit.io/blog/dask-argo-workflows-big-data) as fast as possible. These often cannot be run simultaneously using a single instance of your Spark application due to resource constraints and dependency conflicts. To get the jobs done faster, it’s helpful to run Spark on Kubernetes where you can easily parallelize jobs, using a workflow orchestrator like Argo Workflows to automate the process.


In this blog post, you will learn how to set up Argo Workflows to run Spark Jobs on Kubernetes.


## About Argo Workflows


As defined in GitHub, “Argo Workflows is an open source container-native workflow engine for orchestrating parallel jobs in Kubernetes.” It allows you to easily create, manage, and automate complex data workflows. With it, you can run intensive job operations on your Kubernetes cluster in a fraction of the time it would normally take. Such operations include batch processing jobs, machine learning, data analysis, transformation, and much more.


Argo Workflows features include:


- a full-featured user interface for creating and managing your workflows and for viewing the status of both completed and live workflows
- Cron Workflows that operate similarly to CronJobs in Kubernetes, that is, they allow you to schedule your workflow to run at a set time
- templating and composability that allow you to reuse workflow templates multiple times
- native artifact support for storing generated files and data during workflow operations, with different options provided


Storage options supported include AWS S3, Artifactory, Google Cloud, MinIO, and[more](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) .


## About Apache Spark


Apache Spark is an open source data-processing platform and unified analytics engine used for processing big data sets. The data processing task can also be distributed on multiple computing servers for faster processing. It provides APIs for SQL, streaming, graph processing, and machine learning and is available in Java, Python, R, and Scala, for processing workloads in your preferred language.


The benefits of Apache Spark include:


- fast execution of SQL queries for analytics reporting purposes; Apache Spark claims to run faster than any other data warehouse
- real-time data processing from different sources, such as Apache Kafka, Amazon Kinesis, etc.
- access to the Apache Spark Machine Learning Library that allows you to apply machine learning and graph analysis techniques to large data sets without worrying about the data scale


Spark can run on any operating system that supports Java; however, to benefit from the distributed architecture with minimal dependency complications, running Spark as a container on Kubernetes is a better option. Kubernetes has proven to be a great platform for the management and deployment of Spark applications. It guarantees that your Spark application can run efficiently on any OS that supports Kubernetes, and you can easily distribute Spark workloads on multiple different computing resources.


{% cta-1 %}


## How to Use Argo Workflows with Spark


You need to have a running Kubernetes cluster to run Argo Workflows with your Spark application. You can create a cluster on[AWS EKS or GCP GKE](http://pipekit.io/blog/production-install-of-argo-workflows) , or locally, on your computer using any of the following:


- MiniKube
- [K3s](http://pipekit.io/blog/how-to-run-argo-workflows-in-k3s)
- [Docker Desktop](http://pipekit.io/blog/argo-workflows-with-docker-desktop)


The[official Spark documentation](https://spark.apache.org/docs/latest/running-on-kubernetes.html) recommends 3 CPUs and 4 GB memory in your Kubernetes cluster, and you should enable the DNS add-on if you are using MiniKube.


### Installation of Argo Workflows in Your Cluster


Create a dedicated namespace for your Argo installation:


```text


```


Install Argo into the namespace by running the following command:


```text


```


To verify your Argo installation, you will be accessing the Argo web UI on your browser by port-forwarding the Argo-service deployment to any port available on your localhost. The following command forwards the Argo server to[https://localhost:2746](https://localhost:2746/) , but you can also configure[Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) so that you can have a dedicated and secured URL for your Argo dashboard:


```text


```


Argo Workflows UI before log in


Next, you will be creating a new rolebinding object that binds the admin cluster role to the default service account in the Argo namespace. This grants the Argo server permission to communicate with the Kubernetes API. Moreover, you can create your own custom roles, custom serviceaccount, and custom role bindings for communication between Argo and the Kubernetes cluster based on the security framework of your Kubernetes cluster.


```text


```


Extract the bearer token from the default service account in the Argo namespace. This will be used to authenticate your Argo Workflows UI.


```text


```


Copy the response into the text box and click the **Login Button** .


Argo Workflows UI after log in


Now, you are logged in to the Argo Workflows UI; it provides details of your workflows and you can perform several actions directly on the UI, such as delete workflows, retry workflows, etc.


You have successfully installed Argo Workflows on your Kubernetes cluster. Next, you will be installing Spark on your cluster and configuring it with Argo Workflows.


### Installation of Apache Spark in Your Cluster


Download the most recent release of[Apache Spark](https://www.apache.org/dyn/closer.lua/spark/spark-3.2.1/spark-3.2.1-bin-hadoop3.2.tgz) and extract the Tar archive.


At the time of writing, the most recent version was 3.2.1.


To be able to run Apache Spark in your Kubernetes Cluster using Argo Workflow, you will need to build and run Apache Spark images in your cluster. The Apache Spark you downloaded ships with default Dockerfiles for Java, Python, and R. You can access them in the Kubernetes directory:


```text


```


Dockerfile for Apache Spark (Java)


You can modify the Dockerfile on the basis of your requirements. It is important that you build the Docker image from the Dockerfile so that you are able to use it. If you are using a remote cluster, then it is also important to push it to your Docker repository. Apache Spark provides a script for building and pushing the Docker image:


```text


```


The command above builds a Docker image for running JVM jobs. If you want to opt-in for Python and R jobs then run the following commands:


```text


```


However, in this tutorial, we will be using the image that has already been pushed by Apache Spark, which can be found[here](https://hub.docker.com/r/apache/spark/tags) .


#### Running Spark Job Using Spark Submit on Kubernetes with Argo Workflows


Create a new file called argo-spark.yaml with the following content:


```text


```


To get the <k8s-apiserver-url> run


```text


```


The local:// URI scheme points to the example Spark application jar that exists already in the Docker image. The example jar file can also be found in this location of the extracted Apache Spark directory:


```text


```


More information on the spark-submit configuration can be found[here](https://spark.apache.org/docs/latest/running-on-kubernetes.html#submitting-applications-to-kubernetes) , whereas information on the Argo Workflows template can be found[here](https://github.com/argoproj/argo-workflows/blob/master/examples/README.md) .


Apply the argo-spark yaml file into your Kubernetes cluster:


```text


```


The progress of the workflow will be displayed on the Argo Workflows Web UI:


Argo Workflows UI shows Spark job status


{% related-articles %}


#### Running a Spark Job on K8s with Argo Workflows


The Spark Operator provides a declarative manner of deploying Spark applications in contrast to the Spark Submit approach.


To get started, ensure you have[Helm CLI](https://helm.sh/docs/intro/install/) installed on your computer already.


Now, open your terminal and add the spark-operator repo:


```text


```


You will also be creating this new Spark job in the same Argo namespace where you created the spark-submit Spark job:


```text


```


Next, you will be creating a new role for your Spark Operator, so that the Argo service account will be permitted to run the spark-operator job.


Create a file named spark-cluster-role.yaml and paste the following content:


```text


```


Then apply it to your cluster:


```text


```


Finally, bind the role to your default serviceaccount in the argo namespace:


```text


```


In your terminal create a file named argo-spark-operator.yaml and paste the following Argo WorkflowTemplate containing the spark-operator job:


```text


```


Then apply it to your Kubernetes cluster:


```text


```


You have successfully created the {% c-line %}spark-operator{% c-line-end %} job using Argo Workflows. Return to your Argo Workflows Web UI Browser, and you will see a new workflow added to the previous workflow.


Viewing Spark jobs in the Argo Workflows UI


## Next steps


Now that you're running your first Spark job with Argo Workflows, check out our[Spark with Argo Workflows GitHub repo](https://github.com/pipekit/talk-demos/tree/main/oss-2022) for more[examples of jobs you can run](https://pipekit.io/blog/top-10-argo-workflows-examples) on Kaggle data. It also includes a CRON workflow example and provides more useful resources for Spark users.


## Conclusion


In this article, you were introduced to how to use Argo Workflows to run Spark jobs on Kubernetes. You learned some of the benefits of both tools, and some practical guidance on how to install Argo Workflows in conjunction with Apache Spark.


You also saw two different options for running Spark jobs with Argo Workflows, that is, {% c-line %}spark-submit{% c-line-end %} and {% c-line %}spark-operator{% c-line-end %}.


Although the examples in this article were simple, you can use the same concepts to larger Spark jobs on Kubernetes using Argo Workflows.


Ensure you check out[Pipekit](https://pipekit.io/) , a control plane for Argo Workflows that enables you to set up massive data pipelines in minutes. It gives you production-ready workflows in minutes compared to setting up traditional workflows, saving time and cost.
