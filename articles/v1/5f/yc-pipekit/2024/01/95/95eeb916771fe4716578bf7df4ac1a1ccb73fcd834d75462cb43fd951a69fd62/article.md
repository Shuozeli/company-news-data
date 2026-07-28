---
schema_version: "1.0.0"
document_id: "95eeb916771fe4716578bf7df4ac1a1ccb73fcd834d75462cb43fd951a69fd62"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/fine-tune-llm-argo-workflows-hera"
published_at: "2024-01-31T03:37:01+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:16.511012+00:00"
content_hash: "sha256:148e18450956afe49bacacb556edc7b9d5e00c1563eb18842f2262e37fe047fd"
---

# How to Fine-Tune an LLM with Argo Workflows and Hera

LLMs (large language models) are incredibly valuable tools that can do a ton to support data engineering teams in running and managing the applications they build. However, training LLMs to function for a team's specific requirements isn't as simple as flipping a switch. We need to take foundational models and fine-tune them for our specific needs.


In our[ArgoCon North America talk](https://www.youtube.com/watch?v=nRYf3GkKpss) , Flaviu “Flav” Vadan, Staff Engineer from Dyno Therapeautics, and I did a deep dive into just that: how to train LLMs, and the intricacies that come with them, using Argo Workflows and Hera. We shared insights into the transformative potential of foundation models and the fine-tuning process.


So, if you’re looking to use LLMs and you know you need additional customization or you’re interested in distributed model training, this talk and blog post are for you. Dive in to discover how these models provide a strategic advantage in language processing.


# Foundation models and how we fine-tune them for specificity


Foundation models are a new idea. They're open-source models trained on big datasets for tough tasks like making images or text. These models are huge and cost a lot to train, so we use a process called fine-tuning.


Fine-tuning is a transfer learning technique. It involves feeding models with specific data to enhance their performance. But before that, you need to do two things. First, you need to set up your infrastructure, and then you need access to existing models.


In our talk, we talked about how this idea works for many things, like medical notes or support tickets. It makes these models good at Q&A and other jobs. When you’re looking to use foundation models effectively, this process is really important. It allows teams to tailor the model's understanding and performance to meet their specific needs.


As for examples, LLaMA2 is a great foundational model — it’s a collection of foundation language models. While it won’t be trained on your team’s proprietary data, you can give it some examples to make it better for your work.


## Building the foundation: Infrastructure for LLM fine-tuning


In this demo, we first walked through the Hera code needed to perform the fine-tuning, then explored activities within the Kubernetes cluster. The cluster has three prerequisites:


1. Custom storage class
2. GPUs
3. Argo Workflows installed (this is how you connect each of the components)


Beyond the Kubernetes cluster, the infrastructure extends to essential external components. We’ll need a[HuggingFace](https://huggingface.co/meta-llama/Llama-2-7b-hf) account. This acts as a gateway to all of the resources and tools needed for fine-tuning. But the complexity doesn't end there. Getting approval from Meta is crucial, especially if you plan to use LLaMA2. These infrastructure aspects highlight the detailed planning needed to create an environment suitable for refining and customizing foundation models.


Here’s an example of what this might look like.


In the illustration, the workflow starts with a data engineer ("You") submitting it to the Argo Workflows server. This server is a vital wrapper for the Argo Workflows controller, managing the workflow's state across the designated Kubernetes cluster.


The workflow comprises three key components. First, creating a distributed key-value store for essential metadata in model training. The emphasis on using a separate etcd instance over the Kubernetes-built version is notable. Second, establishing four dedicated server nodes, each having four GPUs, outlines specific hardware needs for optimal performance. Third, the workflow ends by carefully deleting all resources, highlighting the temporary nature of these workflows.


### Workflow steps for distributed training


As the etcd deployment blends into the cluster, the workflow progresses with containers, each equipped with four GPUs, totaling 16 GPUs. Once the workflow begins, these containers quickly communicate with etcd, ensuring a synchronized start when all peers are ready.


The next steps involve feeding data into the model, spreading it across GPUs, and breaking down the model itself to fit the scale of models like LLaMA2 with 7 billion parameters. This breakdown enables parallelized training, optimizing data flow through specific shards on assigned GPUs. The workflow highlights the widespread nature of training, improving efficiency across the extensive GPU infrastructure.


Here’s how all of that actually works.


### Data parallelism in action


The mechanics of this process, as shown in the PyTorch illustration above, called Fully Sharded Data Parallel, explain the complexities of distributed training. Two parallel processes, each on a GPU, manage different data portions and parts of the model. Synchronization, made possible by etcd's metadata storage, ensures consistency across GPUs that is needed for steady parameter processing.


As data moves through specific model sections, synchronization steps, like gathering weights, handle parameters across varied datasets processed on GPUs. After completing a portion, there's an option to transfer it to CPU memory before the next processing phase. While Kubernetes effectively sets up the necessary infrastructure, the budget-friendly approach involves occasional deactivation, aligning with the financial limitations of extended operation.


### Why we tear down workflows and how to do it


In the dismantling process, considering workflow instances as temporary is very important. We initiate the conclusion by stopping the training etcd instance using an exit handler in Hera or Argo Workflows. This cleanup step ensures the removal of leftover elements.


The concept of an exit handler in Hera or Argo Workflows manages post-execution actions, regardless of the workflow's success or failure. At the same time, the cluster auto-scaler efficiently takes apart the now unnecessary GPUs, aligning resource usage with current needs and minimizing unnecessary costs. This method ensures an organized conclusion, emphasizing the dedication to temporary practices for efficient resource use and financial responsibility.


## Using Hera to transform foundational models into tailored solutions


So, what does this all look like in action? At the end of the talk, Flav gave a demonstration of how to accomplish this using Hera. You can[access all of this in the public repository](https://github.com/pipekit/talk-demos/tree/main/argocon-demos/2023-how-to-train-an-llm-with-argo-workflows-and-hera) . Let’s dig in.


For the talk, we wrote a wrapper. There were requirements, such as setting the host of your Argo server, your token in case it’s necessary, a Kubernetes namespace where all of these resources will be provisioned, and (for this demo) a single Docker file being used for all of the resources that have been set globally.


### Spinning up etcd resources with Argo Workflows


Flav demonstrated how versatile Argo Workflows can be by explaining the dynamic creation of etcd resources. When Argo doesn't have a built-in service, users can define a YAML file to generate resources on demand. A look into defining an etcd stateful set shed light on the process, highlighting the significance of mounting SSDs to improve etcd's disk-intensive operations.


### Defining dependencies and orchestrating workflows


To set up dependencies, the initial step is defining the SSD storage class essential for etcd. At the same time, we created the etcd stateful set and load balancer. After launching an independent container waiting for a designated load balancer IP, the container is furnished with an argument called "etcd service name." Then, in parallel and through iterations, the fine-tuning process is activated, making up to four calls or as needed based on the number of nodes. This involves passing crucial parameters like rendezvous ID, node rank, node volume for mounting, and the specific etcd IP each container should connect to.


It's worth noting, as highlighted during the talk, that the dynamic resources generated during the training necessitate careful management. To address this, an exit Directed Acyclic Graph (DAG) in Argo Workflows is triggered, ensuring the deletion of all dynamically created etcd resources, a crucial step irrespective of the workflow's outcome.


# Tearing it all down


At the end of the demo, we highlighted how best to go about tearing down dynamically spun-up resources. This crucial aspect was achieved through an exit DAG in Argo Workflows, ensuring all of the etcd resources were deleted regardless of workflow success or failure. Showcasing the Hera code offered a compelling narrative, ultimately sharing practical insights into the deployment, customization, and deconstruction of foundation models in the pursuit of finely tuned, application-specific solutions.


# Watch the full presentation


[Access our public repository](https://github.com/pipekit/talk-demos/tree/main/argocon-demos/2023-how-to-train-an-llm-with-argo-workflows-and-hera) to start your own journey of exploration and implementation, and[click here to watch the full talk](https://www.youtube.com/watch?v=nRYf3GkKpss) .


Interested in getting support from some of the experts on the Pipekit team so you can discover all of what Argo Workflows can do for your team? Check out[our service offerings](https://pipekit.io/services) , or reach out to us so we can[set up a brief consultation](https://pipekit.io/pricing) . We’d love to hear from you.


‍
