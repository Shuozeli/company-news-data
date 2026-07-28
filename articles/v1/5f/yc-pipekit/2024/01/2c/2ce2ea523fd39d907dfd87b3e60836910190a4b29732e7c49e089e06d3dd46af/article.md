---
schema_version: "1.0.0"
document_id: "2ce2ea523fd39d907dfd87b3e60836910190a4b29732e7c49e089e06d3dd46af"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-workflows-etl-examples"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:00:19.733210+00:00"
content_hash: "sha256:bc1ca6f028461c5a523d2c784a1a3a2903b77c6bc9e036e5447396c32d4bf39e"
---

# Argo Workflows ETL Examples

This post explores using[Argo Workflows](https://argoproj.github.io/argo-workflows/) to orchestrate your data pipelines. To start, let's refresh on what ETL is while designing our work's high-level architecture. I'll demonstrate how to set up your data pipelines to follow the structure more naturally. Then, we'll see how to achieve the same result using[directed acyclic graphs](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (DAGs). Last, I'll summarize what we saw and present reasons to guide your choice of approach based on your project complexity. So, let's start.


## **What Does ETL Stand for?**


First, let's remember what ETL is before[starting on our ETL examples](https://pipekit.io/blog/top-10-argo-workflows-examples) .[Extract, transform and load](https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/etl-architecture-34-subsystems/) consists of tasks to clean your data, and it wrangles the data from your applications into a conformed database. Imagine this conformed database as the single source of truth of your data. This centralized repository helps you gain insights into your products and your customers.


However, each application has its structure to handle the data. Each ETL task makes the application data more palatable for analysis, having explicit dependencies as your[data wrangling](https://en.wikipedia.org/wiki/Data_wrangling) process becomes more robust. Our code will deploy four ETL tasks and their relationship, as reflected by the image below:


*High-level architecture of ETL tasks*


## **Understanding Each ETL Task**


This workflow supports two different data formats: column or row-based. These different formats require different parsers: parquet for columns and avro for rows. We can also refer to them as batch or stream, respectively.


So, the workflow starts with a request handler that identifies the data type. Based on the value of a data type flag, it passes the job to either the batch or stream parsing tags.


The parsers pass their output to the Load Data task, where it is loaded in persistent storage, based on the source and data type.


While it seems like this is a single workflow with two different code paths, there are advantages to processing both data types in the same set of tasks. Sharing a loading tasks between the data streams makes it easier to manage overlaps and relationships. For example, the columnar data store may need to be updated with foreign keys from new row-based data. It’s also easier to share a single ETL workflow between different teams


Now that we know what we'll be building, let's start by seeing how to implement it using Argo Workflows steps.


{% cta-1 %}


## **Build an ETL Pipeline Using \`steps\` in Argo Workflows**


In this approach, the data pipeline will follow a list of steps to clean and treat the data from your data sources. Your ETL code becomes even more robust when we use conditionals to inform which ETL flow your data should take. Sounds good, right? So, let's get our hands dirty and see how it works in practice.


The code below will create a workflow in a namespace called **argo.** This namespace must exist before this workflow is executed with **argo submit** . Doing so will avoid security issues, such as your user not having permission to create namespaces. It will also prevent error messages warning you not to break your Kubernetes deployment. For our example, we'll generate a random value on a Linux machine and load the upcoming data based on this value.


While both parser steps are triggered simultaneously, only the one informed by the handle requests step will execute. Using automated code like this will reduce the chances of having problems with our ETL data flow. Automation on your workflow steps handles common errors such as mismatch types in your database.


```text


```


Save the file above as **etl_steps.yml** and start your workflow with this command:


```text


```


We can now get our workflow status by executing this **argo get** command **:**


```text


```


**‍** The last five digits will differ in each environment. And by running the previous command, your output log should be similar to the image below; as stated, our workflow will execute the **parser** **stream** task based on the value returned by the **handle requests** task.


*ETL steps returned by running \`argo get\` command*


Now that we've seen how to build an ETL with tasks, let's explore how to use DAGs for your ETL.


## **Building an ETL Pipeline with DAGs Instead of Steps**


Now, let's explore how to achieve the same work using DAG templates instead of steps in Argo Workflows. Even though the DSL looks similar at first glance, DAGs give you more power to specify dependencies between steps and run tasks in parallel.


In a DAG, any task can run when its dependencies are satisfied. If more than one task’s dependencies are fulfilled, all of them will run in parallel. If a task has no dependencies, it will run as soon as the workflow is started. DAGs are excellent for processing ETL, and I strongly suggest you familiarize yourself with all options that a DAG task can provide by looking at[the Argo docs here](https://argoproj.github.io/argo-workflows/fields/#dagtask) .


```text


```


Save the file above as **etl_dag.yml** and submit your workflow to start it:


```text


```


As demonstrated below, you can check its evolution with **argo get:**


```text


```


**‍** In this scenario, our workflow executed the **batch** **stream** task instead of the **stream-flow** based on the value returned by the **handle requests** task.


*DAG output from running \`argo get\` command*


Congratulations on your work! You can now design your ETL data flows using a DAG or structured list of steps within Argo Workflows.


Don't forget to clean your environment with **argo delete -n argo <workflow name>,** where you should inform the **"workflow name"** of your deployed workflows **.**


```text


```


{% related-articles %}


## **Conclusion**


While it's commonly used for infrastructure management, Argo Workflows can also orchestrate your ETL tasks. Using it like this removes the need for different tools to achieve the same goal, i.e. Argo for CI/CD and Airflow for ETL jobs.


The DAG approach is often better than the steps approach for running ETL pipelines. For starters, DAG task processing is optimized at runtime. You'll have fewer decision points for some of your pipelines simply by informing the desired data flow.


For simple tasks, sequential flows (as you get with the steps approach in Argo Workflows) work fine. However, they become harder to maintain in cases where you need to target a subset of your data flow and manage complex dependencies over time.


Another perk of using DAGs is to specify the exact step at runtime. Running it gives you more liberty to create conditional code with fewer indented loops while optimizing the code and the infrastructure resources.


I urge you to go deeper into[Argo Workflows' documentation around DAGs](https://github.com/argoproj/argo-workflows/tree/master/examples#dag) . Mastering how DAGs work can increase the quality of your ETL pipelines, allowing you to manage your ETL tasks more dynamically compared to the steps method.


For more optimized ways of managing your Kubernetes resources, explore how Pipekit can help you orchestrate your whole Argo Workflows deployment.


Special thanks to Eric Goebelbecker and Caelan Urquhart for help reviewing this post.


See you next time!
