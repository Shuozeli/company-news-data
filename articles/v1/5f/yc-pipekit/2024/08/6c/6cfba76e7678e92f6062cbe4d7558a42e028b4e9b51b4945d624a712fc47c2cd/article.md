---
schema_version: "1.0.0"
document_id: "6cfba76e7678e92f6062cbe4d7558a42e028b4e9b51b4945d624a712fc47c2cd"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/orchestrating-python-functions-natively-argo-hera"
published_at: "2024-08-28T06:57:38+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:59:29.484597+00:00"
content_hash: "sha256:dd0ac4b583b023c259d941a02a414e7b6802fb01c4e18cfe98209454e9b6bbc7"
---

# Orchestrating Python Functions Natively in Argo Using Hera

**Why use Argo Workflows?**


Argo Workflows is the de facto Kubernetes workflow standard, due to its features and scalability. Beyond the benefits of the code, Argo Workflows has an active and growing community and is vendor-neutral, reassuring its users of long-term support.


**Argo Workflows Obstacles**


Being built on Kubernetes, YAML is the default language to communicate with Argo. The use of YAML acts as a barrier to entry for developers who aren’t yet familiar with Kubernetes since it is difficult to test or inspect programmatically and data scientists are often more familiar with Python. In addition, it is a challenge to reuse code outside of the heavy-weight WorkflowTemplates and it is hard to maintain long workflows. But containers aren’t scary and YAML isn’t evil…


**Hera to the rescue!**


Hera is *the* Python SDK for Argo Workflows. With Hera, you can write your templates as functions, orchestrate, and test your work all in Python. You can test templates individually or the workflow as a whole.


The challenges of YAML sparked the creation of a “good Python DSL” known as Hera. Python already has a mature developer experience, extensive libraries, and is the preferred scripting language for many programmers. Rather than reinventing the wheel for Argo, Hera leverages the existing solutions and features of Python.


Hera lets you focus on your business logic. There is extensive documentation concerning the implementation of Hera to take you[from zero to Hera-Hero](https://hera.readthedocs.io/en/latest/walk-through/quick-start/) , and user guides for more complex features, like integrations with PyTorch or Apache Spark.


**Hera’s Features**


Hera provides many custom classes to help author your Workflow — which all come with code completion as standard.


Hera uses a context manager pattern for Workflows, DAGs, Steps, and more, which mirrors the YAML syntax, helping users move between Python and YAML.


Objects declared in the Workflow scope, such as Container templates, are automatically detected and added to the Workflow’s templates.


You can easily describe task dependencies with the right-shift operator.


But what if you don’t like using container templates or running commands? What if you just want more Python?


In Hera, Python functions *are* templates: you just need to decorate them with a script decorator, and Hera will do the rest.


If you don’t want to keep flicking between your IDE and Argo CLI to keep starting your workflows, you can add a WorkflowsService in your code which allows you to call the “create” function directly on your workflow.


**Introducing Type-Safety to Your Workflows**


If you use the[Hera Script Runner](https://hera.readthedocs.io/en/stable/user-guides/script-basics/#runnerscriptconstructor) to run your Python code, Hera will perform type checks on your parameters at runtime. To use the Hera Runner you’ll need to build an image from your code and dependencies, and then a Script template that uses the Hera Runner will produce a YAML spec that looks like this:


The spec shows we are running a Script template, which is running the hera.workflows.runner module through the python command. The entrypoint for your code is passed to the -e (or --entrypoint) option. The “source” value is actually where the input parameters are passed to the template in Argo.


So, using the Hera Runner we can write type-safe functions - you just need to specify the constructor as “runner” and build a suitable image.


It might look like only JSON types are allowed in the inputs, but the Hera Runner also integrates with[Pydantic](https://docs.pydantic.dev/latest/) for type validation, meaning Hera allows Pydantic classes in your template inputs and outputs. The Hera Runner ensures type safety for these Pydantic input objects at runtime, plus you can be sure you have a valid output object from any template outputs.


**Test workflows with normal Python tests**


Using a Pydantic class representing a rectangle, we can see that you can unit test your template logic with a tool like PyTest just like any other Python function:


With a completed workflow, we can inspect its status and make sure the phase is succeeded. We can even get individual nodes from the workflow and check their output.


## **Hera’s future goals**


We hope to bring automatic Python versioning to WorkflowTemplates. This way we can help teams manage their many interdependent WorkflowTemplates by leveraging Python dependencies.


## **How is Hera used?**


At Bloomberg, in the AI group, there are constant streams of data used to retrain models that need to remain up-to-date. This process is called model remediation or model drift. Even though Argo Workflows seemed like a strong contender to orchestrate and run pipelines for this model remediation, and despite having an in-house team at Bloomberg to support Argo Workflows, there was very low adoption across the AI group.


Teams which *had* adopted Argo created YAML workflows with entire chunks of Python code dumped into the script templates. This is untestable outside of end-to-end system tests.


To solve this, the ML platform team aimed to provide a Python experience for their AI developers to use Argo Workflows. They worked on Hera itself for the version 5 release, which was a complete rewrite of the library to bring it up to parity with, and then beyond, the YAML spec. They also provided accompanying tools for Hera to help developers get started.


Tools included a Cookiecutter template to provide a boilerplate Python package, a testing framework, and a documentation generator for WorkflowTemplates. They also held internal workshops and provided support channels in Slack. Hera now enables Bloomberg’s 300+ AI engineers to use Argo Workflows in development and production.


**How to manage Argo Workflows at scale? Pipekit can help.**


Pipekit is a services and software provider in the Argo Workflows ecosystem. A problem that Pipekit observed many companies run into is how to build a self-service data science or CI platform for their teams.


Pipekit provides numerous solutions, both open and closed source, which help with easy integrations with common tools to allow monitoring and observability for workflows.


For example, an open source tool created by Pipekit is the pipekit-sdk, which builds on Hera to allow users to submit to multiple clusters, interact with workflows, and to see logs from a Jupyter Notebook or any Python interpreter.


From the vendor perspective and from serving customers, Pipekit has learned that platform teams and data scientist teams have various needs and capabilities, and that these needs and range of skills should be addressed simultaneously for maximum efficiency.


Platform teams, who are often Kubernetes operators, are typically familiar with pods, deployments, service accounts, and various Kubernetes primitives. But data scientists just want to interact with code, models, and metrics.


If you try to force these data scientists into using YAML or tools they aren’t familiar with, there is a lot of mental overhead to overcome. These developers should be focusing on their models and data science, rather than the stress and uncertainty of adopting new working methods. Pipekit meets both platform engineers and data scientists where they operate and serves their respective needs with tools they prefer.


## **Use Case: ACCURE Battery Intelligence**


[ACCURE Battery Intelligence](http://accure.net/) , a customer of Pipekit, ensures exceptional battery performance — reliably and safely — with predictive battery analytics software built by battery experts. They process and analyze an enormous quantity of battery data to feed their models. They use a combination of Kubernetes and Dask deployments that are running on Kubernetes to achieve a high level of parallelism so their jobs complete as fast as possible.


At first, they were doing this with a native YAML Argo Workflow. A major problem they were running into was that the data scientist team simply didn’t like interacting in YAML because it wasn’t flexible enough for their development workflow, and YAML wasn’t a familiar programming language. To make a major modification, they had to take their workflows YAML and hand it off to the platform team, who then would make the change and give it back to the data scientists. This process slowed down iteration speed and even led to unintentional bugs.


Pipekit helped ACCURE migrate to Hera for a Python-native developer experience. Now their data scientists have more flexibility and control. They can use the Dask primitives, which are in Python, right alongside the Argo Workflow definition in Python using Hera. They can update their workflows on the fly (even concerning the setting of resource requests and limits, parallelism, etc.). Overall, this self-serve developer experience for Argo Workflows with Hera has led to greater productivity on the data science team.


## **Use Case: Energy Company**


Another customer of Pipekit, an energy company, needs to normalize their energy prices, compete in competitive and high-speed markets, and often uses algorithmic trading desks. Energy prices are subject to seasonality and macroeconomic events that make long-term planning difficult and hazardous. The company in question adopted Argo Workflows because they had to process an enormous quantity of historical returns. This level of scale was a scale that most companies wouldn’t be able to function at without Kubernetes, so Kubernetes and Argo Workflows was the obvious solution.


Since the energy company was competing in a high-speed market against other traders, they needed their data scientists to be able to act very quickly. So they adopted Hera to become more self-serve, give the data scientists the flexibility they needed, and to avoid hand-offs between the data scientist and the platform teams.


## **Key Takeaways**


‍ *Hera makes Argo Workflows easy*


‍ *Argo does the heavy lifting of orchestrating your Python functions*


‍ *Hera is used in production, operating at scale*


Alternative TL;DR: Argo Workflows and Hera can give you the best cloud-native workflow orchestration experience.


If you would like to connect:


**Q&A**


Q: Why build on top of Argo Workflows instead of another tool such as Dagster or Airflow?


A: (J.P. Zivalich): A core issue is the amount of scale. Argo Workflows is built on top of Kubernetes and uses all of the normal Kubernetes primitives that we are familiar with. We’ve seen that Kubernetes can scale well. It is not an infinite scaling solution, but it does achieve a level of scale that might be tougher with some legacy systems, like Airflow, where you are having to spin up multiple parts, figure out that some of them can run on Kubernetes, some of them cannot. Argo Workflows was built on top of Kubernetes, from the ground up, and is able to hit some scaling thresholds that some other tools cannot.


(This also means that Argo Workflows is as stateless as possible and leverages etcd to manage the workflow orchestration, leaving much less overhead to manage than comparable tools like Airflow and Dagster.)


Really then the question was: what is the developer experience like? That is something that platform engineers were fine with, writing YAML. If you are accustomed to writing YAML, that is great, you can still do this. But a lot of data scientists, and even other engineers, weren’t quite up to speed on it. We saw Flaviu, from Dyno Therapeutics, start working on Hera. Then Bloomberg adopted it, then we saw a broader community adoption, improving the Argo developer experience for Python developers.


Q: Is there a table comparing pipekit-sdk and Argo-Python-sdk?


A: (Elliot Gunton): The Argo-Python-sdk is autogenerated, so it has one-to-one parity with the YAML spec, but doesn’t have a customized developer experience. Hera auto generates the resources from the YAML spec as well, so you have a fall-back mechanism in case we haven’t implemented something yet, but we’ve been pretty up to date so far, and there hasn’t been anything missing. We’ve put in a lot of thought and effort to make the developer experience better with Hera and ensure complete feature parity with the YAML dev-ex in Argo Workflows.
