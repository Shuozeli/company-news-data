---
schema_version: "1.0.0"
document_id: "3cd88cefd1cca120924f684ff552a2deed4b982cf9fa3d625744a12a561c40c6"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/how-to-set-up-a-minio-artifact-repository-for-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:bd4332a6db177b0d69c200abc0ae6995c4603bbf98af312a8f94d317873593a0"
---

# How to Set Up a MinIO Artifact Repository for Argo Workflows

It's no surprise that Argo Workflows is a popular tool for CI/CD pipelines, ETL systems, and training ML algorithms. With just a few lines of YAML, you can create robust orchestration scenarios that are scalable and dependency-aware.


All these applications have one common requirement: artifact storage. Each stage transforms data or prepares an artifact for delivery, and passes it to the next step.[Argo Workflows](https://pipekit.io/blog/what-is-argo-workflows) makes passing artifacts between steps easy with artifact repositories. Workflows can use a specific location, defined in the workflow script, or rely on a default repository.


In this post, you'll learn how to configure a default repository with MinIO, an open-source, Kubernetes-native storage solution.


## ‍ **Why Do You Need an Artifact Repository?**


One of Argo Workflows' primary benefits is its ability to execute a workflow on any cluster, regardless of configuration or topology. But, that means the clusters need a flexible mechanism for managing artifacts and logs. That's where your artifact repository comes in.


An artifact repository is essential for managing and tracking workflow run data. When Argo Workflows runs a job, the repository stores all of the run information and artifacts it produces, including logs, parameters, outputs, results, and any artifacts the workflow generates. This makes it easier to analyze and debug workflow runs, as well as reproduce past results if necessary. Additionally, an artifact repository provides a centralized place to store artifacts and makes it easier to share them with other users. Finally, an artifact repository can help increase the stability and reliability of workflow runs, since all necessary data and artifacts are stored in a single, dedicated repository.


## **Why MinIO?**


Argo Workflows supports several options for archive repositories, including Amazon S3, Google Cloud Storage, and Azure Blob Storage. Why use MinIO?


MinIO is a high-performance object storage solution that runs on your Kubernetes cluster, alongside Argo Workflows. So, you can use it anywhere: public clouds, private clouds, or on-premises. This means you can use the same configuration anywhere, regardless of differing hardware or networking constraints.


It's also Amazon S3 compatible, so you can access your logs and artifacts using S3 tools, or with S3's well-documented API.


{% cta-1 %}


## **Setting Up a MinIO Artifact Repository for Argo Workflows**


Installing and configuring MinIO for Argo Workflows is a simple process.


### **Prerequisites**


To follow this tutorial you'll need a cluster with Argo Workflows installed. Since MinIO supports any type of Kubernetes installation, you can use minikube, Docker Desktop, or K8s.


You'll also need[helm installed](https://helm.sh/docs/intro/install/) and running on your system.


### **Install MinIO**


First, add the MinIO repository to your local helm configuration:


```text


```


Then, install MinIO:


```text


```


Helm installs the software and prints a help message with your next steps.


Let's log in to the MinIO web console. The helm charts install the credentials as secrets in the default namespace. They're encoded with base64, so you'll need to decode them, too.


Retrieve your ACCESS_KEY. Wrapping the command from the help screen in backticks with the echo command will make the keys easier to copy.


```text


```


Next, get your SECRET_KEY:


```text


```


Finally, get the URL for the MinIO console with kubectl:


```text


```


Or, if appropriate, minikube:


```text


```


Point your browser at the URL and it will take you to the login page:


!login_page.png


Log in with your access and secret keys.


!minio_console.png


Click the + icon in the bottom right-hand corner and add a bucket named "my-bucket."


MinIO is ready. Now, we'll add it to Argo Workflows.


### **Add MinIO to Argo**


First, we need to install a secret in the {% c-line %}argo{% c-line-end %} namespace, so Argo Workflows can retrieve it. Next, put these two values into this command:


```text


```


Now you can add the default repository configuration to the {% c-line %}argo{% c-line-end %} namespace. Edit {% c-line %}workflow-controller-configmap{% c-line-end %} with {% c-line %}kubectl{% c-line-end %}.


```text


```


The initial configuration looks like this:


```text


```


Add the artifact repository definition.


```text


```


With this map, we're telling Argo:


- Archive the workflow logs in MinIO
- Look for the "my-bucket" bucket we created above
- The endpoint to reach MinIO is argo-artifacts, on port 9000, in the default namespace
- We're not using SSL
- The names and values of the access and secret keys


Save it, and you're ready to run workflows with default artifact storage.[1](https://docs.google.com/document/d/14R6oEkfyhYr9ZhtYU5ASgZOZmU3gbp_3dv7KMiaGLPo/edit#bookmark=id.gjdgxs)


## **Passing Artifacts with a Default Repository**


Let's test the repository with a simple workflow. It has two steps: one to save a value to a text file, and another that uses the file to create a new value. You can find the code[here](https://github.com/egoebelbecker/argo_artifacts) .


### **Workflow Steps**


Here's the Python code for the first step:


```text


```


And a Dockerfile to containerize it:


```text


```


The repo has a script that saves it as {% c-line %}random_number{% c-line-end %}. Adjust it for your repository name. Here's the second:


```text


```


And its Dockerfile:


```text


```


The script saves it as {% c-line %}difference{% c-line-end %}. Adjust it for your repository name.


### **Workflow**


Let's use these containers in a workflow:


```text


```


The first template, {% c-line%}python-random{% c-line-end %}, creates an artifact named {% c-line %}output{% c-line-end %}. It's a text file named {% c-line %}random.txt{% c-line-end %}, located in {% c-line %}/tmp{% c-line-end %}.


The second, {% c-line %}python-diff{% c-line-end %} takes that file as an input artifact and uses it to create a second output artifact: {% c-line %}result.txt{% c-line-end %}.


Both of these artifacts are configured to not be archived and compressed with this:


```text


```


The workflows do this, so it's possible to view the artifacts without downloading and unarchiving them. The workflow also runs as the {% c-line %}argo{% c-line-end %} serviceaccount user:


```text


```


This is important, as the default serviceaccount does not have the entitlements required to pass artifacts between steps.


{% related-articles %}


### **Running the Workflow**


If you run this in the GUI, it renders a picture that shows the steps, with the {% c-line %}random.txt{% c-line-end %} artifact passed from the first step to the next:


Click on {% c-line %}random.txt{% c-line-end %} and you'll see its contents:


‍


Likewise, you can view {% c-line%}result.txt{% c-line-end %}:


‍


The log output from {% c-line %}python-diff{% c-line-end %} matches the contents of the files:


## **MinIO and Argo Workflows Artifacts**


In this post, we installed MinIO and set it up as the default artifact repository for Argo Workflows. Then we ran a simple workflow to verify that the repository is working. MinIO is a robust storage solution for Kubernetes and Argo Workflows, and as you've seen in this tutorial, it's easy to manage and install.


Argo Workflows makes it easy to build workflows, and MinIO makes your workflows more capable with artifact storage. Put them both to work in your cluster jobs today!


1 There is an[outstanding issue](https://github.com/minio/minio-go/issues/1776) with Argo Workflows and MinIO where artifacts over 5MB are not saved.
