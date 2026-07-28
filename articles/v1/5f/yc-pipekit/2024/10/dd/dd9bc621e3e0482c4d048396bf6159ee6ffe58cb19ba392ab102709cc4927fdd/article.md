---
schema_version: "1.0.0"
document_id: "dd9bc621e3e0482c4d048396bf6159ee6ffe58cb19ba392ab102709cc4927fdd"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/how-to-get-the-most-out-of-hera-for-data-science"
published_at: "2024-10-03T12:21:34+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:01:06.812214+00:00"
content_hash: "sha256:0b112f6bcc6fd0139acf7f435f2349f91402665cfa6172caadac15a54b388482"
---

# How To Get the Most out of Hera for Data Science

## What's the Data Science Developer Experience like?


Python is the go-to language for Data Science,[top ranked](https://pypl.github.io/PYPL.html) for popularity in several indices, with numerous libraries for specialized Data Science functions:` pandas` ,` numpy` , and` sklearn` , to name a few. Data Scientists often use these libraries to iterate on code in a Jupyter Notebook, but this results in functions that are not tested beyond manual checks and visual inspections when using a library like` matplotlib` .


Once an algorithm or section of code has been tested in a Jupyter Notebook, the developer may move the function to a new Python file to build out a library of analyses functions, keeping the Notebook just to arrange the calls to these functions and visualize the results. When a dataset or computation gets too large and complicated for a local machine to handle, developers will usually turn to a cloud offering. Here, they can make use of features like auto scaling and workflow orchestration using cloud-native tools like Kubernetes and Argo Workflows, but then the setup can start to become complex and require a dedicated DevOps (or "MLOps") team.


## Argo Workflows for Data Science


[Argo Workflows](https://argo-workflows.readthedocs.io/en/latest/) is a popular workflow orchestration tool, native to Kubernetes, with a powerful backend for scaling your tasks through the use of DAGs (Directed Acyclic Graphs). It has applications in Machine Learning (ML), CI/CD (Continuous Integration/Continuous Deployment), and data and batch processing, meaning it is flexible for many use cases. In fact, in the[2023 Argo Workflows survey](https://blog.argoproj.io/argo-workflows-events-2023-user-survey-results-82c53bc30543) , CI/CD was the most popular main use case, with over 50% of respondents selecting this as one of their main use cases, while ML was the least popular out of the main use cases (28.8%).


We might infer that ML is a less popular use case for Argo Workflows for a few reasons, but the main one is that the default developer experience for Python developers is not ideal. Compared to a tool like Airflow where the orchestration logic is integrated into the business logic codebase, for basic Argo Workflows you will find yourself switching between Python and YAML, as well as your command line for building and pushing images, and actually running the Workflows.


So, while Argo Workflows is a popular Kubernetes-native workflow orchestrator, it lacked a good Python developer experience, which is important for applications in ML given the popularity of Python. Some users would prefer to not use YAML or learn the intricacies of Kubernetes and Argo Workflows, so YAML becomes a barrier to entry for these users.[Hera](https://hera.readthedocs.io/en/stable/) was initially released in late 2021 to address this limitation. Hera allows you to focus on writing business logic, independent of your orchestration logic, but all still within Python. This separation empowers data science teams to focus on their analyses and iteration while working with a powerful orchestrator that can scale up their analyses, bridging the domain gap between data scientists and infrastructure engineers by letting the scientists work in their preferred language.


## Hera for Data Science


Let's take a look at how we can use Argo Workflows with Hera for a more integrated data science developer experience.


### A Quick Intro to Hera


First, let's go over a basic Workflow in Hera:


```text


```


Here we have three functions decorated with` @script` – this turns the function into a basic Script Template for Argo, running on a` python3.12` image (set via the` global_config` ). In YAML, the` flip` template looks like:


```text


```


When using scripts like this, you cannot use code defined outside the function scope (such as imports or other functions), because the function code is dumped inline in the YAML as Python source code. Hence, in Hera, this is known as an "inline" script. Inline scripts can be cumbersome to maintain as they increase in length, but they are good for initial prototyping, so we can see how they might be useful in a Jupyter Notebook for quick iterations.


The Workflow definition is written using a context manager, and neatly wraps up the configuration of your Workflow into a single scope, separate to your business logic. Within the DAG context, we call the script functions to create Tasks, which have special properties we can use for orchestration logic, like the` on_other_result` property. Note that within a DAG or Steps context, the contents of your functions are not actually being run, as Hera only uses the function call to construct the appropriate Task:


```text


```


### Scripts Deep Dive


We've seen how inline scripts are good for initial prototyping, but how can we avoid writing such lengthy functions, which don't follow good Python practices of using imports outside of functions? We can use Hera's[Script Runner feature](https://hera.readthedocs.io/en/stable/user-guides/script-basics/#runnerscriptconstructor) .


The Script Runner allows you to write Script Templates using fully-native Python – you can use imports and functions from anywhere in your codebase! However, to run your code on Argo Workflows, you will need to build an image from your code and dependencies.


The easy part is changing your script to use the Runner, all you have to do is specify the` constructor` in the script decorator's arguments:


```text


```


This results in a YAML that looks like the following:


```text


```


We still have a` script` template, but now we have` args` and the` source` is the input parameters.


Let's go over the` args` : they are telling the` python` command in the` python:3.8` image to run the` hera.workflows.runner` module, which itself takes the` -e` (or` --entrypoint` ) option, which is passing the function to run in` module:function` format. The` source` being the input parameters is a result of a quirk of Argo Workflows for script templates, where the contents of` source` are copied into the running container as a file. In Hera, we exploit this to get the input values at runtime on Argo.


The benefits of using runner scripts include a fully-native Python experience of using functions and imports across the codebase, meaning you can write and test smaller functions, giving you more confidence in your Workflow. However, using the runner means you need to rebuild the image whenever you change your script functions (but not if you just change the Workflow code), which can result in a slower prototyping cycle, and the initial setup to get a suitable CI/CD pipeline can be more complex. Therefore, using the Hera runner is suited for long-lived or repeatedly-executed Workflows (such as WorkflowTemplates, CronWorkflows, or event-triggered Workflows) that you want to be sure are correct through rigorous testing in the development phase, rather than running one-off Workflows. You should also automate the setup of the Runner and CI/CD for new Workflows codebases to get started quickly (e.g.[using cookiecutter](https://cookiecutter.readthedocs.io/en/stable/) ), which can reduce the ramp-up gap of using the Hera Runner versus inline scripts.


#### Setting up CI/CD for the Hera Runner


As a quick aside, to help you get up and running with the Hera Runner, you can start by setting Hera's` global_config.image` to an environment variable. For example, in your Workflow code you can use:


```text


```


Then, you could build or submit your Workflow through a Python script on the command line, e.g. for a script at` ds_blog/run_workflow.py` such as:


```text


```


You can run this like so:


```text


```


In a CI/CD context, this means you could use something like[GitHub Actions](https://docs.github.com/en/actions) to set the build tag to something like the current release, or current PR number, so you can build and publish an image using this build tag, and then submit a Workflow which references the same build tag, all within CI, using an integration like[Docker Hub](https://docs.github.com/en/actions/use-cases-and-examples/publishing-packages/publishing-docker-images) .


```text


```


### Argo's Features for Data Science


A few of Argo's most useful features for data science include fan-out, artifact visualization and intermediate parameters, which enable you to automatically parallelize, inspect results such as graphs, and perform human-in-the-loop reviews and retries.


Fan-out, known as[loops](https://argo-workflows.readthedocs.io/en/latest/walk-through/loops/) in Argo, is how you can process data in parallel - the benefits for data science are clear: splitting data sets, or running experiments with different values, or tuning hyperparameters. It is simple to set up using the` with_items` or` with_param` variables in Hera tasks. The[loops guide](https://hera.readthedocs.io/en/stable/walk-through/loops/) in the Hera docs explains more about the syntax.


[Artifact visualization](https://argo-workflows.readthedocs.io/en/latest/artifact-visualization/) is offered by Argo Workflows out of the box, where all you have to do is output uncompressed files or folders from a task or step. In the context of data science, this would let you view full html reports, or individual graphs (as images). This combines well with[intermediate parameters](https://argo-workflows.readthedocs.io/en/latest/intermediate-inputs/) , where you could have a Workflow to retry model training with different values.


Let's see how these features combine in a data science scenario!


## Data Science Scenario


You have been brought on as a consultant for a hospital wanting to predict diabetes diagnosis.


You've been given[the dataset](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database) and a proof-of-concept script to load it, split it into train, test and validation sets, and run a logistic regression to predict the diagnosis. Let's adapt the script to run on Argo Workflows using Hera!


### Intro to the Code


The code you're given uses` pandas` to load the csv file, then` sklearn` to run the logistic regression. It does a single, simple split of the data into train, test and validation sets. Finally, it outputs the model's accuracy and other evaluation metrics, including an[ROC curve](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) .


```text


```


Running the code gets a matplot figure and the following on the command line:


```text


```


To get this working on Argo Workflows we'll need to recreate the code in functions for each part of the pipeline. We will also need to build an image from the code with dependencies (` hera` ,` pandas` and` scikit-learn` ) installed, and we'll need an S3 or other Argo-compatible cloud storage mechanism, so that Argo Workflows can automatically fetch the data for us.


### Adding Hera Components


We should first split up the script into logical steps: fetching data, splitting it, transforming (feature scaling), training, prediction and evaluation. Each of these can be a single task in a DAG, but we might combine fetching and splitting for convenience. We'll use Hera's Runner scripts which means we'll need to use` docker` to build an image, but we'll have more flexibility when defining and using inputs and outputs.


#### Create a Pipeline of Functions


First, let's update the code to use functions, and add a` __main__` section to run the "pipeline".


```text


```


Now, we'll go over how to turn each function into an Argo Workflows template using Hera.


First, the` load_and_split_dataset` function - we want to load the dataset CSV from S3, and we can use Hera's[Script Annotations](https://hera.readthedocs.io/en/stable/user-guides/script-annotations/) feature to automatically copy the Artifact to the container, and set the input variable to the path of the Artifact. So, for the function inputs, you'll want a` dataset_path` variable, with a type of` Path` , and by using` Annotated` , you can get the` S3Artifact` from your bucket. We can use annotations for the outputs too, and use a` NoneArchiveStrategy` so that the outputs aren't compressed. Your function signature would then look something like this:


```text


```


And the code in the function performs the same operations as the local code, but must return` json` strings for Hera to understand how to serialize them:


```text


```


Next, we have the` feature_scaling` function. For this, we'll be passing the` X_train` and` X_test` artifacts from the` load_and_split_dataset` , which means we won't need` S3Artifact` in the` Annotated` metadata to fetch them. We can also use an` ArtifactLoader` which is able to perform the JSON-deserialization for us. Then, holding a Python` dict` , we can reconstruct` pandas` DataFrames using` pd.DataFrame.from_dict` . We'll be outputting the transformed training and test sets as` numpy` arrays, serialized as lists:


```text


```


With our features scaled, it's time to train the model! A` LogisticRegression` object is not easily string-serializable, so we'll make use of the built-in` pickle` module to serialize the model as bytes, and write to the output Artifact. This is where we'll need to use Hera's[Outputs-as-Inputs](https://hera.readthedocs.io/en/stable/user-guides/script-annotations/#input-output-function-parameters) feature, letting us write to the path stored in the variable.


```text


```


Now, we can try making predictions on the test dataset and evaluating the model's performance. We don't need any new knowledge to write these templates, but we still need to be mindful of deserializing inputs and serializing to outputs correctly, and we need to provide a path with a file extension of` .png` to get the ROC curve for the Argo UI to recognise it as an image and display it. We can also output the report as an Artifact.


```text


```


#### Creating the Workflow


The hard part is over - you've got a bunch of functions doing the dataset loading and transformation, a model is trained on it, and you can evaluate it! Now, we want to run the pipeline on Argo Workflows, by writing a` Workflow` . We can create a` Workflow` using Hera's context manager pattern, and within that, create a DAG. Then, in the DAG context, we call the functions that we want to run as` Tasks` , and we can pass` arguments` in the function call where we can plumb together the outputs of one task as inputs to the next. Finally, we use the "right shift" operator (` >>` ) to tell Hera the dependencies between tasks. So, for the first two tasks, this will look like:


```text


```


With that, we can fill out the rest of the Workflow:


```text


```


### Running on Argo


First, you'll need to build a docker image and set` global_config` values, with the image set to the` name:tag` that you use when running` docker build` . Here, we use` docker build -t ds-blog:v1 .` , so we set the image to` ds-blog:v1` . We also need to ensure the` script_annotation` experimental feature is turned on:


```text


```


Then, to run the Workflow on Argo, you'll need a` namespace` and` WorkflowsService` . You may also need a "Bearer" token – see[the Authentication guide](https://hera.readthedocs.io/en/stable/walk-through/authentication/) in Hera for more details.


Then, you simply call` w.create()` and your Workflow will be running on Argo! Here, we have the creation under a` __main__` context so we can run` python model_pipeline.py` to create the workflow from the command line. We are also using a local installation of Argo Workflows, hence the` localhost` and not verifying SSL.


```text


```


We can use the Argo CLI to check the Workflow status:


```text


```


And we can see the ROC curve directly in the Argo UI!


## Conclusion


In this blog post, we've seen how Hera can be used for Data Science scenarios, and we have a basic Workflow running on Argo Workflows, using artifact fetching from S3 and artifact visualization in the Argo UI. The Workflow code can serve as a base to build on, where you can add intermediate parameters for retraining with different values, more artifact visualization, and you can also start to use other built-in features of Argo such as[looping](https://argo-workflows.readthedocs.io/en/latest/walk-through/loops/) over parameters and[retry strategies](https://argo-workflows.readthedocs.io/en/latest/retries/) to ensure jobs complete.
