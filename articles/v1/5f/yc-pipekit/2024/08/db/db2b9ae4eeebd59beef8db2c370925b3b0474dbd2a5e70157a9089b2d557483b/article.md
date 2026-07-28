---
schema_version: "1.0.0"
document_id: "db2b9ae4eeebd59beef8db2c370925b3b0474dbd2a5e70157a9089b2d557483b"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-and-airflow-dag-examples"
published_at: "2024-08-07T11:39:23+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:59:29.484597+00:00"
content_hash: "sha256:2b6942a339c861d4041ee6b64a478e909a207861284067e0b1cdc0b58e9735bf"
---

# Argo and Airflow DAG Examples

Directed Acyclic Graphs (DAGs) sit at the heart of workflow orchestration. We use them to tell our workflow tools how to process tasks. The graphs determine the order in which steps run, when they can be run in parallel, and when to end processing in the event of an error. While DAGs behave the same on different platforms, creating them is different depending on the workflow orchestrator you are using.


In this post, we'll look at both Airflow DAG examples and Argo DAG examples. Airflow and Argo are two of the more popular workflow orchestration tools, but they have very different user interfaces. In addition to using different methods for defining the graphs, they have different approaches to implementing the decisions inside a DAG. We will also show the equivalent Hera Python SDK version of the Argo Workflow for users who prefer Python.


This article assumes you are familiar with DAGs.


## ‍ **DAG 101**


Let's start with a simple DAG that runs four steps, with the last one dependent on the previous two.


### ‍ **Argo DAG Example**


This example is similar to the basic DAG example in Argo's documentation. It's an excellent example of a simple DAG workflow.


Here is the Argo YAML for the basic DAG workflow:


```text


```


The workflow specification starts on line #5, with the {% c-line %}spec{% c-line-end %} **** configuration value.


Line #6 tells Argo where to begin the pipeline. Then, lines #8 - #14 define the workflow's single task. Argo's workflows support[WorkflowTemplates](https://argoproj.github.io/argo-workflows/workflow-templates/) **,** {% c-line %}reusable{% c-line-end %} pieces of code similar to objects you create in each task definition.


The workflow is named "diamond," after the shape of its graphical representation. Each task has a {% c-line %}name{% c-line-end %}, {% c-line %}template{% c-line-end %}, and {% c-line %}arguments{% c-line-end %}. Three of them have {% c-line %}dependencies{% c-line-end %}.


- Task "1" calls {% c-line %}echo{% c-line-end %} with its name.
- Task "2" calls {% c-line %}echo{% c-line-end %} with its name. It has task "1" as its sole dependency.
- Task "3" calls {% c-line %}echo{% c-line-end %} with its name. It has task "1" as its sole dependency.
- Task "4" calls {% c-line %}echo{% c-line-end %} with its name. It has tasks "2" and "3" as its dependencies.


This configuration runs the tasks as depicted in the graph. Argo will execute task "1". When it finishes, it executes "2" and "3" in parallel. When both "2" and "3" are complete, it executes "4."


So, creating a DAG in Argo is straightforward:


- Define your workflow as a {% c-line %}dag{% c-line-end %}
- Add {% c-line %}dependencies{% c-line-end %} to the tasks that need them (omit them if they are not required)
- {% c-line %}Dependencies{% c-line-end %} are lists


{% cta-1 %}


### **Equivalent Hera DAG Example**


If you prefer writing Python code, you can use the Hera Python SDK for Argo Workflows. Here is a Python version of the same Workflow written in YAML above:


```text


```


Compare how the definition of the DAG is written using a special “right shift” operator, versus writing the depends attribute for each task in the YAML. Using Python also streamlines the re-use of the echo Container, where calling it like a function creates each of the tasks with different names and arguments.


### **Airflow DAG Example**


Airflow workflows are written in Python code. Here is an implementation of the same DAG for Airflow:


```text


```


After importing the required modules, this code defines default arguments for the Pythion DAG object. Defining the arguments at the top of your code is considered a best practice since it makes it easier to find and change them and makes the code more readable.


The second argument, {% c-line %}start_date{% c-line-end %} **,** is required, even though we don't need it for the example. All Airflow DAGs require a schedule, even if you only plan on running your workflow manually. For["partly legacy](https://airflow.apache.org/docs/apache-airflow/stable/faq.html#what-s-the-deal-with-start-date) ," you must specify a start date that the Airflow scheduler will use to decide when your workflow can be started.


On line #11, the script creates a {% c-line %}DAG{% c-line-end %} using with{% c-line-end %}, so everything inside the block belongs to the workflow. This makes the code compact and easy to read.


Airflow uses[operators](https://airflow.apache.org/docs/apache-airflow/stable/concepts/operators.html) as reusable tasks, similar to Argo's templates. Airflow's {% c-line %}BashOperator{% c-line-end %} is the perfect operator for this example. Lines #16 - #31 create four jobs that call {% c-line %}echo{% c-line-end %} with the task name.


Finally, this workflow uses Airflow's[chain](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/models/baseoperator/index.html?highlight=chain#airflow.models.baseoperator.chain) operator to establish the dependencies between the four tasks. Airflow has several different operators for defining relationships. In this case, {% c-line %}chain's{% c-line-end %} syntax resembles the graph.


So creating a DAG in Airflow requires these steps:


- Create a {% c-line %}DAG{% c-line-end %} object
- Create your steps using {% c-line %}operators{% c-line-end %}
- Place your steps in the {% c-line %}DAG{% c-line-end %} object's graph


## **DAG Branching**


A DAG can run tasks in a specific order based on dependencies. It can also direct execution down a particular path or branch based on a result. Here’s what that looks like (below).


‍


‍


This workflow uses the output of the {% c-line %}start{% c-line-end %} step to decide whether or not to run the {% c-line %}success{% c-line-end %} or {% c-line %}fail{% c-line-end %} step.


### **Equivalent Hera Branching DAG Example**


Here is a Python equivalent of the same Workflow written in YAML above:


```text


```


See how we’re using the special @script decorator which lets us define the script code directly in Python. We also have a simplified “when” expression using f-strings and the result property of the “begin” task.


### **Argo Branching DAG Example**


Let's start with the Argo Workflow again.


```text


```


Argo uses[conditional artifacts and parameters](https://argoproj.github.io/argo-workflows/conditional-artifacts-parameters/) to implement branching DAGs. You can also use these tools outside of DAGs. But by placing them in a DAG workflow spec, you have more control over how Argo runs the tasks.


This time there are two templates. It's reusing the {% c-line %}echo{% c-line-end %} template from the first example on line #17. The workflow defines a new one on line #8 that generates a {% c-line %}random{% c-line-end %} number between one and five.


The new template is an excellent example of how easy it is to run Python code inside an Argo workflow. By using a[script](https://argoproj.github.io/argo-workflows/workflow-concepts/#script) block **,** the task can define a script inside its {% c-line %}source{% c-line-end %} field. Argo passes the code into the Python interpreter and executes it in the container. So, you don't have to create a new Docker container for every task: you can reuse containers like {% c-line %}python:Alpine{% c-line-end %} to run simple scripts.


So, the {% c-line %}begin{% c-line-end %} task on line #28 uses the {% c-line %}random{% c-line-end %} template to generate a number. Then, Argo executes the next two tasks based on the results of their {% c-line %}when{% c-line-end %} fields (these are defined on lines #32 and #38).


These fields use the[expr](https://github.com/antonmedv/expr/blob/master/docs/Language-Definition.md) syntax to evaluate the random number from {% c-line %}begin{% c-line-end %}. It's a similar syntax to what we used to pass parameters to {% c-line %}echo{% c-line-end %}, but since the {% c-line %}script{% c-line-end %} block in the {% c-line %}random{% c-line-end %} template exports the {% c-line %}outputs{% c-line-end %}, we don't have to define them in advance.


```text


```


Expr uses scalar values, so Argo implicitly casts {% c-line %}result{% c-line-end %} to an integer and compares it to {% c-line %}3{% c-line-end %}.


{% related-articles %}


### **Airflow Branching DAG Example**


Here is the Python code for the same workflow in Airflow.


```text


```


With Argo, we didn't have to define a branching step. Its ability to conditionally execute tasks took care of the branching for us. With Airflow, we have to write the branching logic with a special operator.


Let's go over the code step-by-step instead of top-to-bottom.


The **start** task is a[PythonOperator](https://airflow.apache.org/docs/apache-airflow/stable/howto/operator/python.html) which can call any Python callable. Rather than calling {% c-line %}random.randint{% c-line-end %} directly, the code has a function on line #10 to better illustrate the idea of calling code from outside the step. Of course, this is Python, and {% c-line %}PythonOperator{% c-line-end %} can call any code in scope.


The {% c-line %}decide{% c-line-end %} task is a[BranchPythonOperator](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/python/index.html#airflow.operators.python.BranchPythonOperator) **.** It's a subclass of {% c-line %}PythonOperator{% c-line-end %} that returns the names of the next task to execute in the graph. So on line #14, a function does exactly that. The returned tasks should be directly downstream from the branching task. Line #51 places the tasks in the graph, so that's true.


The branching function uses[xcom_pull](https://airflow.apache.org/docs/apache-airflow/stable/concepts/xcoms.html) to extract the return value from {% c-line %}start{% c-line-end %}. Since the default behavior for {% c-line %}PythonOperators{% c-line-end %} is to make their context available to the next task, the return value is available without any extra work.


Finally, the code creates the dependency chain so the branching operation can find the next step to execute. For this workflow, we used the[>>](https://airflow.apache.org/docs/apache-airflow/stable/concepts/dags.html#task-dependencies) operator.


So like the Argo example, {% c-line %}success{% c-line-end %} or {% c-line %}failure{% c-line-end %} is executed based on the random number returned at the start of the workflow.


## ‍ **Argo and Airflow DAGs**


We've looked at Airflow DAG examples and Argo DAG examples that illustrate how to build a simple graph and a graph that branches based on a task result. You can use this code to put together a DAG for nearly every situation.


DAGs are valuable frameworks for running workflows like MLOps and CI/CD pipelines. They make it easy to arrange work in logical steps based on dependencies and outcomes. Create some graphs today!
