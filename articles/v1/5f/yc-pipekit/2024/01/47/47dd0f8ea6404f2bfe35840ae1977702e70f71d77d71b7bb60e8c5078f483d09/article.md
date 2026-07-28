---
schema_version: "1.0.0"
document_id: "47dd0f8ea6404f2bfe35840ae1977702e70f71d77d71b7bb60e8c5078f483d09"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/orchestrating-elt-with-argo-workflows-and-dbt"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:37c6fe2ba0c95d166e146d3ac791083e49d6fac007deabfa9a4706cd50050b89"
---

# Orchestrating ELT with Argo Workflows and dbt

ELT, or Extract-Load-Transform, is a preferred method for data processing, especially in industries like e-commerce, healthcare, banking, and engineering. Being a cheaper compute than ETL (Extract-Transform-Load), ELT is particularly useful when applied to tasks like data warehousing, cleaning, migration, and transformation. ETL, on the other hand, generally takes more time to transform the data before loading, which has the potential to more negatively impact businesses in these industries.


ELT involves extracting data from its source, loading it into a central repository like a data warehouse, and then transforming it for use in downstream processes such as analytics and reporting. Within the data warehouse, data is usually transformed via SQL scripts, which aggregate and join tables, making them suitable for analytics purposes. However, this approach is tedious. Someone has to maintain the schedule and ensure the SQL scripts are available to every analytics engineer that requires them.


A better approach is to use[dbt (data build tool](https://www.getdbt.com/) for your data transformation. dbt adds Git collaboration, test runners, and seeders to your analytics engineering toolkit. It also includes a library of prebuilt data transformation functions and a compiler for creating custom transformations. You can use[Argo Workflows](https://argoproj.github.io/workflows/) in conjunction with dbt to orchestrate your ELT pipelines; it extracts data from your source, loads the data into your warehouse, and runs the dbt commands that transform the data.


Let’s cover some practical tips for how exactly you can run ELT workloads with[Argo Workflows and dbt](https://pipekit.io/blog/top-10-argo-workflows-examples) . Follow along step by step, and by the end of this article, you’ll have learned how to build a pipeline that extracts and loads customers, orders, and payments data into a PostgreSQL database and transforms the data using dbt scripts.


## What’s an ELT Pipeline?


In general terms, a **pipeline** typically includes extracting data from its source, loading it into a central repository, and then transforming it for downstream processes. An ELT pipeline refers more specifically to the steps involved in the ELT process.


An ELT pipeline requires an agent that can:


- Talk to the data sources
- Store data in an appropriate format within the warehouse
- Run the scripts that transform the data in the warehouse


Since Argo Workflows satisfies all these requirements, it’s a good runner for ELT pipelines. The extract-load steps are handled by the runner while the transform step is relegated to a tool like dbt.


dbt in itself cannot perform data extraction and loading; its single responsibility is data transformation. Without a tool like Argo Workflows, you would need to manually run a script to extract and load data from your source to your warehouse. If the script run fails, you need to handle retries. If you need to run it on a schedule, you need to write the crontab jobs yourself. That’s a lot of hassle when you can just use a tool like Argo Workflows.


### A Couple Common Use Cases for ELT Pipelines


As mentioned earlier, ELT pipelines are widely used to integrate, transform, and load data into warehouses for reporting and analysis. This lends itself to a few fairly common use cases.


In business, think of an e-commerce application that allows payments using different methods (credit card, coupons, gift card, bank transfer, and so on). A data analyst might need a {% c-line %}total_payments{% c-line-end %} field that can be obtained by aggregating all the payment methods of an order. The result might be a combination of the orders and payments table with an additional {% c-line %}total_payments{% c-line-end %} field that represents the total payments.


A use case in healthcare would be a hospital's electronic health records (EHR) system, containing patient information such as demographics, diagnoses, medications, and lab results. The hospital’s billing system has information about payments per patient visit, such as the total amount paid and the payment method. Using dbt, a data analyst can join patient information from the EHR system with payment information from the billing system.


{% cta-1 %}


## Implementing an ELT Orchestration with Argo Workflows and dbt


You can keep either of those scenarios in mind as you follow along with this build for an ELT pipeline using[Argo Workflows and dbt](https://pipekit.io/blog/top-10-argo-workflows-examples) .


To ensure you're off on the right track, please check that you have all the prerequisites listed here:


1. A Kubernetes instance running locally, such as[Minikube](https://minikube.sigs.k8s.io/docs/start/) ,[kind](https://kind.sigs.k8s.io/) , or[k3s](https://docs.k3s.io/quick-start)
2. The[dbt container for PostgreSQL](https://github.com/dbt-labs/dbt-core/pkgs/container/dbt-postgres)
3. The[kubectl CLI](https://kubernetes.io/docs/tasks/tools/) and[Argo CLI](https://github.com/argoproj/argo-workflows/releases/tag/v3.4.4) installed on your machine
4. Git for cloning the project’s starter code


### Architecture Overview


In this ELT pipeline, Argo Workflows handles E and L, and dbt serves as the T. Data is extracted from CSV files into a PostgreSQL database, which serves as the warehouse containing the raw data. The data is then loaded into another PostgreSQL database which serves as the analytics database. Finally, the data is transformed from the raw tables in the analytics database into analytics tables using dbt.


Architecture diagram of ELT diagram


The complete ELT process might be too complex due to the use of two databases; you can simplify it by using a single database that contains the raw data tables and the analytics tables created by dbt.


Simplified architecture diagram of ELT pipeline


### Setting Up Your Kubernetes Environment


All the work you’ll do on Kubernetes will be done in an {% c-line %}argo{% c-line-end %} namespace. If you haven’t already, create the {% c-line %}argo{% c-line-end %} namespace using the command below:


```text


```


Apply the Argo Workflows[CRD](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) to your Kubernetes environment. This ensures that the Argo CLI can connect to and run Argo Workflows on Kubernetes. If you haven't already, run the command below to apply Argo Workflows CRD to your Kubernetes environment:


```text


```


### Deploying a PostgreSQL Instance to Your Kubernetes Cluster


First, create a PostgreSQL deployment on your Kubernetes cluster. Create a new file called {% c-line %}postgres-deployment.yml{% c-line-end %} and paste the following manifest into it:


```text


```


Next, create the PostgreSQL deployment on Kubernetes by running the following command:


```text


```


This command should pull the PostgreSQL images and start a PostgreSQL server in the {% c-line %}argo{% c-line-end %} namespace. The server has a default Postgres user with a password of **12345**.


{% related-articles %}


### Loading Data into the PostgreSQL Database


Now that the PostgreSQL deployment is ready, load it up with raw data. Copy the YAML content below into a file called {% c-line %}load-data.yml{% c-line-end %}. This is an Argo Workflow that downloads the raw CSV files from {% c-line %}raw.githubusercontent.com{% c-line-end %} and loads them into the PostgreSQL deployment.


```text


```


Run the workflow:


```text


```


If the workflow runs successfully, you should see checkmarks next to each step.


Workflow successful run


### Setting Up Your dbt Project


Now that you have data in your PostgreSQL deployment, set up a dbt project and create an Argo Workflow that executes the {% c-line %}dbt run{% c-line-end %} command to execute all models in your dbt project. You can create your dbt project using {% c-line %}dbt init{% c-line-end %}, but that will take a lot of configuration.


Instead, clone this {% c-line %}jaffle_shop{% c-line-end %} GitHub repository:


```text


```


The repository contains all the models that can transform your data. After cloning the repo, create a file called {% c-line %}profiles.yml{% c-line-end %} in a ~/.dbt/ directory and add the following to it:


```text


```


{% c-line %}profiles.yml{% c-line-end %} will point dbt to your postgres database so you can run the workflow


### Port Forward the Postgres Deployment


You need to expose your PostgreSQL database to your local machine so that dbt can run scripts against it. Use the command below to port forward your deployment to {% c-line %}port 5432{% c-line-end %}.


> Ensure you change {% c-line %}<your postgres deployment>{% c-line-end %} to the value of your PostgreSQL deployment. You can obtain this value by running {% c-line %}kubectl get[pods](https://pipekit.io/blog/clean-up-pods-save-logs-argo-workflows) -n argo{% c-line-end %} on your terminal.


```text


```


### Running the Transform Workflow


The transform workflow is by far the simplest workflow — it just runs the {% c-line %}dbt run{% c-line-end %} command on the Kubernetes cluster. After the command is run, the data from the {% c-line %}raw_customers{% c-line-end %}, {% c-line %}raw_orders{% c-line-end %}, and {% c-line %}raw_payments{% c-line-end %} tables are transformed into two tables: {% c-line %}customers{% c-line-end %} and {% c-line %}orders{% c-line-end %}. These tables contain the joined data that’s ready for analytics.


YCreate this workflow by adding a new file to your local directory called {% c-line %}transform-data.yml{% c-line-end %}. After creating the file, paste the following content into it:


```text


```


> Ensure that you replace {% c-line %}/path/to/local/dbt/project{% c-line-end %} and {% c-line %}/path/to/local/.dbt/directory{% c-line-end %} with the path to your cloned repository and the path you saved your {% c-line %}profiles.yml{% c-line-end %} to.


You can run the workflow using the following command:


```text


```


## Conclusion


[Argo Workflows](https://argoproj.github.io/argo-workflows/) offers you a versatile workflow engine that you can use to execute ELT pipelines. Features such as parallelism, concurrency, and error handling can help you compose your workflows, leading to robust pipelines.


And you’ve just seen how to orchestrate an ELT pipeline using[Argo workflows and dbt](https://pipekit.io/blog/top-10-argo-workflows-examples) . Note, however, that you did have to run the {% c-line %}argo submit{% c-line-end %} command for each workflow you needed to run. Consider using[Pipekit](https://pipekit.io/) for that instead.


Pipekit is a control plane for Argo Workflows, allowing you to automate your ELT workflows and run commands with ease. Be sure to[schedule a call](https://pipekit.io/) to learn more about Pipekit and how it can help your organization manage its data pipelines.
