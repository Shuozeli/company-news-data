---
schema_version: "1.0.0"
document_id: "a0dfefd4dea21ca4ba93305aa86f0ad3b22ba3fe05610687a500ef155b5172b9"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/building-backtesting-pipeline-python-argo-workflows"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:96efcc45f4b68b81f8c6f85f962b44fa2faa8cbcf05afe26629b92b7afbac44d"
---

# Building a Backtesting Pipeline with Python and Argo Workflows

Python and Argo Workflows help you to manage and scale your backtesting activities quickly and efficiently. Argo Workflows is a powerful tool for creating and managing complex workflows for your applications. Python provides traders with a robust set of libraries and tools for working with data, creating models, and testing them.


With Python, you develop and test your financial and machine learning models, automate data extraction and preprocessing tasks, and quickly set up backtesting activities. Adding Argo Workflows equips you with the power of task orchestration for those backtesting activities since the workflows are highly configurable and can be rapidly modified and managed.


Let's put together a simple backtesting solution with Python and Argo Workflows so you can see it in action.


## **Backtesting with Python and Argo Workflows**


### **Prerequisites**


In order to follow this tutorial, you'll need a few things:


- Know how to run a workflow on Argo Workflows.
- A cluster with Argo Workflows installed. You can follow the[quickstart](https://argoproj.github.io/argo-workflows/quick-start/) with any system capable of running Docker Desktop, a Docker install with minikube, or a Kubernetes cluster.
- An Artifact Repository for passing data between steps in your workflow. Learn more about that[here](https://pipekit.io/blog/configure-artifact-repo-argo-workflows) .
- A Docker registry that your cluster can pull images from. For this tutorial, I'll be pushing containers to my personal Docker Hub account.


We'll be keeping things simple, so you don't need more than one worker node. The source for this tutorial is available in two GitHub repos. The market data downloader is[here](https://github.com/egoebelbecker/argo_python_backtest_downloader) , and the backtester is[here](https://github.com/egoebelbecker/argo_python_backtester) .


### **Backtesting with Python**


For the sake of scaling backtesting with Argo workflows, we can break backtesting down into two major steps: downloading pricing data and processing it with our trading models. But, once you understand how to write a simple workflow, you can add more steps if they make sense for your process.


We're going to write two scripts. One will download end-of-day equities data, and the other will apply a simple moving average. You can, of course, plug in the best data source and your algorithms once you understand how the parts go together.


For downloading data, we're going to use[Quandl](https://demo.quandl.com/) .


Here's the script:


```text


```


This script looks for a ticker, start date, and end date on the command line. It downloads the data and places the results in a file named for the ticker and data range. As you'll see below, the command line works well for passing arguments to a task in Argo Workflows. You'd want to add error checking in a production environment to ensure the arguments are valid. For now, we're keeping the code simple.


{% cta-1 %}


For backtesting, we'll use[Backtesting.py](https://kernc.github.io/backtesting.py/) with code right out of one of their samples.


```text


```


### **Building Backtesting Containers**


Now it's time to put these scripts into Docker containers so Argo can run them in Kubernetes. Here's the Dockerfile for the downloader:


```text


```


The requirements file adds Quandl. Build the container with a tag for your Docker registry.


```text


```


Then push the container.


```text


```


Here's the Dockerfile for the backtester:


```text


```


It's nearly identical to the previous file.


Build and push it to your container registry. In both cases, the Dockerfile uses the "slim" image as the base because it provides the OS support required for the underlying Python libraries that Alpine lacks.


Then it installs and upgrades pip before installing the required libraries and copying over the Python source files.


### **Writing a Python Backtest Workflow**


Now that we have our two containers, we need a workflow to execute the backtest. Let's go over it section by section. First, we need to define the workflow and give it a name.


```text


```


This sets the document type as a workflow, specifies that the workflows Argo creates should be named {% c-line %}equity-backtest-XX{% c-line-end %}, and names three workflow parameters: {% c-line %}ticker, start_date{% c-line-end %}, and {% c-line %}end_date{% c-line-end %}. These are the arguments our Python scripts are looking for.


Code reuse is one of our primary objectives here, and the parameters make this workflow reusable. You can pass them[via the command line](https://argoproj.github.io/argo-workflows/walk-through/parameters/) or copy the workflow file, edit the three parameters in one place, and check them into source control. You could even use Python code to generate new workflow files on demand.


Next, we need the templates that run the containers. Here's the downloader:


```text


```


Line #17 specifies the container with the full path from the Docker registry. Lines #19 - #22 add the three input parameters on the command line. Up on line #6, the template identifies the output file as a named artifact. Here's that output file code again:


```text


```


The file name is built from the input parameters, matching the way Python creates it. We also tell Argo to not create a zipped archive with the **none: { }** setting. The backtester's template looks for a file with the same name:


```text


```


This template has four inputs: the ticker, both dates, and then on line #8, a file with the same name as produced by the previous template. While the file name is the same, we haven't tied the templates together yet, though. Backtest produces another output file, defined on line #13. Finally, we need the workflow steps to get these templates to work together:


```text


```


This runs the containers, one after the other. Lines #7 - #12 and #17 - #22 refer back to the workflow parameters. So, whatever values you plug into the bottom (or pass to the command line) are what the tasks see. On line #23, the workflow tells the backtest step to use the file produced by the download step. Let's run this workflow.


{% related-articles %}


### **Running a Python Backtest Job**


Here's the entire workflow in one file:


```text


```


Submit it to your cluster. Here's what I see in the web GUI after running the job on my cluster:


The GUI illustrates the output files using the names we gave them in the workflow as part of the tree structure. Click on the results. Argo doesn't have a widget to display CSV files but click **view anyway** to see the raw output.


### **Concurrent Backtest Jobs with Argo Workflows**


So, we've put together a backtesting workflow with two steps. It uses parameters to select the tickers and dates, so you could easily use Argo to run multiple concurrent jobs and with a cluster, scale your resources up and down depending on the load. With a few small additions, you can set this workflow up as a[cron workflow](https://argoproj.github.io/argo-workflows/cron-workflows/) and run your backtest jobs daily, weekly, or monthly.


But what if your tests are more complex? For example, you may have a processor that needs to wait for two or more download jobs to complete. Or, you may want to have two jobs triggered by a single download. For this, you can use a[DAG](https://argoproj.github.io/argo-workflows/walk-through/dag/) . Let's rewrite the workflow as a DAG:


```text


```


The changes start at line #62. Instead of steps, we have tasks, and the download task is now a dependency of the backtest test. This allows us to add additional tasks that can run in parallel with tasks it doesn't rely on, or wait until the end of another task that it needs output from. If you run this, you'll see the same result as the previous workflow, but now you have the foundation for more complex workflows.


### **Scalable Python Backtesting with Argo Workflows**


In this post, we built two Python containers and ran them inside two different Argo workflows. We saw how easy it is to pass the output of one container to another and take advantage of Argo's ability to orchestrate tasks on a Kubernetes cluster. Argo Workflows makes creating scalable and robust workflows simple. Put your k8s cluster to work on your backtesting tasks today!
