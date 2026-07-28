---
schema_version: "1.0.0"
document_id: "a396db180a863d6416211b675d6869d853bab3598e3e6dd92725ac00a685d1b0"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/unlock-workflow-parallelism-by-configuring-volumes-for-argo-workflows"
published_at: "2024-03-19T19:22:19+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:07.231499+00:00"
content_hash: "sha256:49210c0376b4f1ee443df5878eebda69612335e1f8fef72360dafc19f31864d8"
---

# Unlock Workflow Parallelism by Configuring Volumes for Argo Workflows

Combining Argo Workflows and Kubernetes generates a world of possibilities for achieving parallelism in workflow execution. However, one of the common challenges teams encounter is making the read-write-many access mode work seamlessly with volumes. Given only a single pod can access the volume at any given time, parallelism is limited. What’s more, cloud-managed Kubernetes clusters often require additional configuration to ensure smooth integration with Persistent Volumes used in Argo Workflows.


In this blog post based on my ArgoCon Europe talk with AWS’ Lukonde “Luke” Mwila, we will explore an alternative approach to handling artifacts in Argo Workflows using a read-write-many disk. I will also briefly cover setting up a Kubernetes cluster with an NFS provisioner using Argo CD to enable dynamic volume provisioning, allowing pods within a workflow to access volumes in parallel.


## Choosing the right storage type for your data


In another ArgoCon Europe talk, my colleague Caelan Urquhart and Intuit’s Julie Vogelman discussed using buckets for Argo Workflows artifact storage. While Luke and I encourage using volumes, the same problems of sharing data between steps in workflows and between workflows themselves exist. Questions that arise include:


- How do I efficiently get from workflow step A to workflow step B?
- How do I efficiently share the same data with multiple steps in parallel?
- How can I use semi-persistent data across many workflows in parallel?


Before jumping into what Luke and I believe to be one of the better solutions when working with volumes, there are two storage options worth highlighting. First is[Amazon EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html) (Elastic Block Store). While EBS is really good for persistent storage and can be used as a good back-end solution for MinIO, the problem is that EBS doesn’t allow you to carry out tasks for read-write-many. The second is Amazon EFS (Elastic File System), which does give you read-write-many capabilities. However, it restricts you to that particular environment and can be a bit tricky to set up.


### The benefits of choosing an NFS server provisioner for storage


So, why choose an NFS server provisioner?


In the same way that MinIO is the self-hosted alternative for Amazon Simple Storage Service (Amazon S3), an NFS server provisioner is a self-hosted alternative for EFS. That’s what we use at Pipekit to create volumes capable of parallel access. You can backend it onto EBS or something similar to turn a read-write-once disk into a read-write-many disk, or you can backend it onto your ephemeral node storage. This would allow you to achieve the same goal, but without any persistence, and to use the spare disk you’re already paying for to handle transient data loads.


**Pros:**


- Offers the same advantages as EFS
- Can be dynamically provisioned by a PVC
- Can be used on-prem as well as in-cloud
- Setup is easy


**Cons:**


- Can be slower at very large scale (similar to EFS)
- Small maintenance overhead in keeping the NFS server provisioner instance running (similar to MinIO)


There are a number of options out there. We use[NFS Ganesha Server and Volume Provisioner](https://github.com/kubernetes-sigs/nfs-ganesha-server-and-external-provisioner) .


[Head to our repo](https://github.com/pipekit/talk-demos) to run and compare this setup using disks alongside a full CI workflow using buckets in your local environment to see how they work.


## How to get started with an NFS server provisioner


Here’s a quick, high-level overview of the steps involved in setting up an NFS server provisioner for semi-persistent data. (You can find details about the software used[here](https://github.com/pipekit/argo-workflows-ci-example) .)


1. NFS server provisioner is deployed as a Helm chart, creating a pod and new storageClass
2. The pod creates a PVC to grab a determined amount of EBS disk
3. You create your own PVCs using the new stroageClass
4. You are allocated read-write-many persistent volumes backed by EBS
5. Start a workflow and mount the new volumes into the appropriate steps, reading and writing data


At Pipekit, we install the nfs-server-provisioner twice. The second installation is the same as above but without the PVC backing it. This way it is pointing at your ephemeral storage instead. This is for transient data.


Then start a workflow containing a volumeClaimTemplate to create PVCs that exist for the life of the workflow, and then drops the data at the end of the workflow.


## Tips to consider for working with NFS Server Provisioners


During the talk, we highlighted the results of two tests designed to demonstrate the workflow speed capabilities of Amazon S3 and an NFS server provisioner. The test was comprised of a simple workflow that creates a 10GB block of data, stores it in the artifact repository of your choice, then completes a second step that runs three steps in parallel to create 10GB of additional data. Overall, a total of 40GB of data is generated.


S3 took seven minutes to handle 40GB of data, and most of that time was taken up by turning the data into a tar file. The NFS server provisioner took just 20 seconds. So, if your team is working at scale, this is an especially important detail to consider.


You’ll also want to think about the amount of storage you will actually need. Consider increasing the size of the storage disks for your particular nodes. Next, if you have a lot of read and write tasks that you intend to carry out in parallel, have that data copied from your NFS disk to your ephemeral storage beforehand. And finally, as mentioned above, consider installing the NFS server provisioner twice — the first installation is for the EBS backend for semi-persistent data while the second installation is for ephemeral node disks for transient data.


### Comparing cost differences between S3, EBS, and EFS


In a quick rundown of cost, it's important to note that despite the effectiveness of the approach in terms of performance and speed, EBS doesn't necessarily translate to cost efficiency. Based on the experiment we conducted, S3 was the most economical option and then EFS, while EBS proved to be significantly pricier. This highlights that while EBS might seem like the optimal choice, its higher cost makes it less of a silver bullet solution, urging consideration of other options like S3 for more economical outcomes.


## Conclusion


Throughout this post, we’ve highlighted just some of the benefits of using volumes for storage in Argo Workflows and noted some of the steps to help you set up a Kubernetes cluster with an NFS provisioner using Argo CD. Making use of an NFS server provisioner is an incredibly efficient and powerful way to share data between steps in workflows and between workflows themselves.


Watch our full talk below, and[head to our repo](https://github.com/pipekit/talk-demos/tree/main/argocon-demos/2023-configuring-volumes-for-parallel-workflow-reads-and-writes) for the resources shared within this post.
