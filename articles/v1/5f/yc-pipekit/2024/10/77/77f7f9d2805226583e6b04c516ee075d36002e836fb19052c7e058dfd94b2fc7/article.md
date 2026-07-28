---
schema_version: "1.0.0"
document_id: "77f7f9d2805226583e6b04c516ee075d36002e836fb19052c7e058dfd94b2fc7"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/colocalized-documentation-software"
published_at: "2024-10-28T11:27:37+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:01:05.353137+00:00"
content_hash: "sha256:b816d48f9b43be3fdb21e023315cbbb170ea929e741cf46dbb32058d3c428cf2"
---

# Colocalized documentation and software

Organizations that build and commercialize software are constantly faced with issues of documentation and example software being out of date. Documentation tends to become out of date soon after it is written as the actual underlying code changes, and that causes contributors to search for working code in tests, ask teammates for help, or simply spend time working through software to understand how it is implemented before using it or contributing to it. While organizations likely encourage collaboration, they also want to preserve the independence of contributors by facilitating their ability to find working documentation, which saves contributors’ time and increases productivity.


Tools such as continuous integration and continuous deployment (CICD) help us test and integrate contributions quickly. However, CICD does not help us write effective documentation that can be tested in CICD. Tools such as[doctest](https://docs.python.org/2/library/doctest.html) are fantastic for checking small examples but documentation is typically much more comprehensive, covering areas that are more akin to integration testing than unit testing, which is what CICD is primarily oriented towards. Examples of heavier workloads we wish to document and run are running a single epoch of training a machine learning model; running a heavy E2E business critical process, etc. To facilitate bringing documentation to code and having *runnable code as documentation* evaluated in the style of integration tests, we can use a combination of Argo Workflows and Hera!


For the rest of the post we will make the following assumptions:


1. Your organization values working software accompanied by colocalized documentation to support productivity
2. Your organization has internal knowledge for managing Argo Workflows, K8s, and CICD
3. Your internal customers do not care for how example software runs just that it does run when they use it and they have documentation at their fingertips
4. Comfort with Python, though you can implement the same architecture in any programming environment


‍


‍ **Argo Workflows**


The popularity of Argo Workflows has been covered extensively in other[posts](https://pipekit.io/blog/what-is-argo-workflows) . For the purposes of this blog it’s important to acknowledge the flexibility of Argo Workflows - since it runs on Kubernetes (K8s) we can run anything on it! This means it’s a perfect engine candidate for an initiative to bring documentation closer to working software. In addition, we can interact with an Argo Workflows server from within CICD, which means we can have asynchronous workflows that evaluate documentation and software examples separately from the environment where CICD runs. Lastly, to set up workflows, images, the DAGs, notifications, and more, we can write plain Python using[Hera](https://github.com/argoproj-labs/hera) , the go-to SDK for Argo Workflows.


‍


**Architecture**


The essential components of the architecture are:


- Kubernetes
- Argo Workflows
- A CICD-enabling platform like GitHub Actions
- Hera


‍


**Examples** ‍


The first thing we want to do is add an examples folder to each of our Python modules. This will serve as the main collection of ‘code as documentation’ we want to store and continuously execute post-CI. Therefore, our folder structure will look like:


```text


```


Some of our examples might require specific resources so we have a simple object that holds the necessary resource configuration and is accessible by Hera:


```text


```


‍


**Assembling the Workflow**


To create the workflow necessary to launch each example on Argo we make a small CLI that can serve as the entrypoint to assemble the Workflow. The CLI command takes the path to the directory of examples to launch (this can be specified by CI), whether to issue a notification, and whether to wait for the examples workflow to finish. The workflow consists of a single DAG that has multiple parallel tasks, where each task is an execution of a container that takes a path to the example to execute, name of the example, and resource configurations.


```text


```


You’ll notice that this script takes into account the *_config file for each example, which contains the default resources for running an example. This is what allows us to set up things like CPU, memory, and GPUs! The container definition uses pod spec patching to set up resources dynamically. In this example you will note we use a local k3d image registry for the image, but you can supply your own!


```text


```


In our case it’s a simple print statement but there’s nothing stopping us from running the exit handler script template in a container that provides us with dependencies to interact with Slack, DataDog, Grafana, and others. The script to collect examples and construct workflows is launched by a CICD job that relies on commands in the Makefile.


```text


```


If we launch the second module from our local machines we should see something like this! A workflow that represents the 2 examples from the foo module running in parallel:


While this sample project invokes the script that assembles workflows with paths to the examples that need to be launched you can write a CICD action that detects the examples to launch as workflows based on files that have changed. This can be achieved using git diff, getting the module parent directories, e.g. module1, module2, etc., and launching the example workflow creation script just for those modules. Once CICD launches the examples they go to Argo Workflows and execute on K8s! We can optionally make CICD wait for all these examples to finish or we can simply get CICD to only submit those workflows to Argo and forget about them. There are other details that are part of this sample project but they are adjacent to the central components.


‍


**Conclusion**


The biggest benefits we get from colocalized documentation are:


1. Documentation stays up to date thanks to applying the same general rules - lint, type checking, testing - we have in place for the rest of the repository
2. Some software examples can be very complex and have long running processes unsuitable for regular CICD – we now have an environment that can execute them
3. Our usage documentation sits with the code our internal stakeholders care about. Our fellow contributors likely have access to the repository already, which means they get access to documentation right in the environment they are used to, without any external platforms, dependencies, or other credentials


In this post we evaluated a simple and powerful illustration of how Hera, Argo Workflows, and K8s can empower your organization to have *documentation that stays up to date* ! The approach consists of a CI and K8s-based setup to capture modules with code changes and construct a workflow that evaluates all examples of the respective modules. This approach can easily be extended to many complex use cases, with advanced retry mechanisms, rollbacks, and other Argo Workflows features, while at the same time satisfying the need to have working, documented, example, software that’s constantly evaluated with the same rigor as regular production software to help independent contributors.
