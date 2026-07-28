---
schema_version: "1.0.0"
document_id: "e43588f64d43f2ac1cb0c3cb0e9047f9a389a524664d18cdad953758356a91c0"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/configure-artifact-repo-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:7e1cb8a1a4fd63d2f66a93c816697a80f5f89bfa513f4af332d95e43323654ef"
---

# How to Configure an Artifact Repo for Argo Workflows

When it comes to orchestrating parallel jobs on Kubernetes, no other tool offers the power of[Argo Workflows](https://argoproj.github.io/argo-workflows/) . This is because Argo Workflows was created as a cloud-native engine implemented as a Kubernetes custom resource definition (CRD), which makes it fast, lightweight, and highly flexible.


Its performance and ability to run many tasks in parallel make[Argo Workflows ideal for diverse use cases](https://pipekit.io/blog/top-10-argo-workflows-examples) , including:


- Running compute-intensive jobs for machine learning or data processing
- Executing CI/CD pipelines natively on Kubernetes
- Running jobs on hybrid and multi-cloud environments


To a large extent, these benefits are closely related to the use of artifact repositories. But what are artifact repos? And more importantly, how can you configure them? Those and other points will be addressed in this article.


## What is an Artifact Repo?


An artifact repository securely stores artifacts that are generated during continuous integration (CI) processes. It also allows these artifacts to be available for other automated processes such as Argo Workflows.


## How Do Artifact Repos Work in Argo Workflows?


Argo Workflows stands out for its ability to transparently pass data from one workflow step to another, either via parameters or via artifacts. Using parameters when working with large data sets is not practical, though. Artifact repos are important because they allow you to store any kind of data that can be later used by various steps or even other workflows as needed.


Another advantage of Argo Workflows is its flexibility to use[different object storage providers](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) for artifact repositories. Some of the object storage services supported by Argo are:


- AWS
- GCS
- OSS
- MinIO
- Artifactory
- Any other S3-compatible solution


## What are the Use Cases of Artifact Repos?


Artifact repositories are useful for storing large data sets, but this is far from their only use case. There are multiple advantages to using artifact repositories for Argo Workflows, including:


- Reducing duplication in templates
- Removing secrets from templates
- Storing inputs, outputs, and logs


{% cta-1 %}


## How Do You Configure Artifact Repos?


Now that you know more about what artifact repositories offer, you’ll now learn how to configure them properly. You’re going to use Argo’s[quick start](https://argoproj.github.io/argo-workflows/quick-start/) manifest for a simple example.


Start by creating a namespace called argo:


```text


```


Next, deploy the quick start manifest using the following command:


```text


```


The manifest installs in your Kubernetes cluster all the necessary components: the argo-server, the workflow-controller, and the MinIO object storage preconfigured as the default artifact repository.


### Using the workflow-controller-configmap


One of the easiest ways to configure an artifact repository is by editing the workflow-controller-configmap, which is used to set controller-wide settings.


First, check the current state of the ConfigMap using the following command:


```text


```


Note that the workflow controller is configured to use MinIO as the artifact repository. Also, note how the authentication information is part of the configuration:


Argo Workflows controller


To exit the edit mode, type :x and press **Enter** .


Now, if you need to change the configuration of the workflow-controller-configmap, for example to switch your endpoint to AWS S3 object storage, you can do it by either modifying the existing ConfigMap or creating a new one similar to the one shown in the[documentation example](https://argoproj.github.io/argo-workflows/workflow-controller-configmap/) :


```text


```


Note that this example uses the default workflow-controller-configmap. However, you can use your own if required.


To set up a new workflow-controller-configmap, you must create a ConfigMap in the same namespace as the workflow-controller. An example is shown below:


```text


```


Keep in mind that if you change the name of the workflow-controller-configmap, you will have to create or modify your deployment to reflect the changes in the argo-server:


```text


```


For more information on how to configure other object storage services to be used as Argo artifact repositories, refer to the[Argo Workflows documentation](https://argoproj.github.io/argo-workflows/configure-artifact-repository/) .


### Setting Up Secrets for Authentication


You’ve learned how to set up your artifact repo, but you may have noticed that the authentication data is exposed. In Kubernetes, the best practice is to use secrets to protect sensitive information.


Fortunately, Argo Workflows comes prepared out of the box to handle secure authentication mechanisms. Starting from Argo v2.9, it’s possible to use the federated OpenID Connect provider,[Dex](https://github.com/dexidp/dex) , for authentication. In other words, you can configure Argo Workflows to use Argo CD’s Dex server.


To get started, create the secrets required by OAuth2, client-id and client-secret:


```text


```


In the code shown above, kubectl is used to store the foo and bar secrets. For more information on how you can create secrets using resource configuration files, Kustomize, and kubectl, read[Managing Secrets](https://kubernetes.io/docs/tasks/configmap-secret/) in the Kubernetes documentation.


Next, you need to modify the settings of the workflow-controller-configmap to enable OAuth2 authentication and include the newly created secrets. In the[documentation](https://argoproj.github.io/argo-workflows/workflow-controller-configmap.yaml) , you will find all the options you can use in the workflow-controller-configmap.yaml file. The ones most relevant for SSO authentication are listed below:


```text


```


Additionally, in the Argo CD documentation, you will find guides on how to use your[existing OIDC provider](https://argo-cd.readthedocs.io/en/stable/operator-manual/user-management/#existing-oidc-provider) .


Regardless of the procedure you use, once you have made the changes, you’ll need to restart the Argo server and tell it to use SSO mode:


```text


```


For more information on how to use the Argo CD Dex instance for authentication,[check the documentation](https://argoproj.github.io/argo-workflows/argo-server-sso-argocd/) .


{% related-articles %}


## Using Key-Only Artifacts to Improve Security


As of Argo Workflows v3.0, you can take advantage of an alpha feature known as[key-only artifacts](https://argoproj.github.io/argo-workflows/artifact-repository-ref/) . According to the Argo documentation, “a key-only artifact is an input or output artifact where you only specify the key, omitting the bucket, secrets, etc.” Instead, the configured artifact repository’s bucket/secrets are used.


As you can imagine, this approach offers several advantages:


- It improves performance thanks to smaller workflows
- It decouples the artifact location configuration from the workflow, which allows you to configure the artifact repository without changing your workflows or templates
- It allows users to have their own artifact repository configuration


Implementing a key-only artifact is straightforward. The following is the sample workflow provided in the documentation:


```text


```


## Conclusion


In this article, you learned what artifact repos are and their role in Argo Workflows, as well as their benefits. You should now have a better sense of how to configure artifact repos and how to improve security using Kubernetes secrets and the Argo CD Dex server for authentication.


Argo has multiple moving parts that must be configured properly to avoid issues. This is where Pipekit can help you set up production-ready Argo workflows in minutes, thanks to its powerful control plane. You can go live much faster and even enable multicluster workloads. Pipekit enables better automation and scalability for organizations from startup to enterprise.
