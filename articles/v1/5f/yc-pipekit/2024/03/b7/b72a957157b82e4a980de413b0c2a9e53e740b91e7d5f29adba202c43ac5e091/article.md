---
schema_version: "1.0.0"
document_id: "b72a957157b82e4a980de413b0c2a9e53e740b91e7d5f29adba202c43ac5e091"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/migrate-ci-cd-fjenkins-argo"
published_at: "2024-03-19T19:19:56+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:07.231499+00:00"
content_hash: "sha256:48e4575d2dfdfafe14a25ff9c085f6afe7fcdc30c63c01bb08315c5f5f0cf9bc"
---

# Why it’s Time to Migrate Your CI/CD from Jenkins to Argo

While at ArgoCon and KubeCon North America, I teamed up with Bertrand Quenin, Staff Software Engineer at Intuit, to present a more efficient solution for CI/CD pipeline management. We wanted to show Jenkins users a reliable alternative — Argo — and demonstrate how to go about the migration process.


‍[During this talk](https://www.youtube.com/watch?v=kKLIuAEc5Zw) , Bertrand and I explored the challenges our teams encountered while running CI/CD using Jenkins, addressed the benefits of Argo Workflows as an alternative, and highlighted the pros and cons of the two solutions. In this post, we’ll recap the key takeaways from the presentation and share with you all you need to know to decide if it’s time for you and your team to make the switch and start migrating your CI/CD from Jenkins to Argo Workflows.


## Challenges using Jenkins on Kubernetes


Running Jenkins on Kubernetes as Intuit does is powerful, but it is not without its challenges, as Bertrand revealed. In order to support a whopping 6,000 developers handling 100,000 jobs daily, they’re running a Kubernetes cluster with about 150 nodes on which there are 200 Jenkins controllers. In addition, at any given time roughly 1,500 Jenkins agents are running those builds.


Along with the success Intuit has managed with Jenkins, their challenges include:


- **Lack of troubleshooting insights** — Identifying issues becomes a puzzle, as the system lacks critical insights for effective troubleshooting
- **Decreased performance with increased jobs** — Jenkins experiences a slowdown as job numbers increase, impacting operational efficiency
- **Extended failover time** — Failing over takes up to an hour, leading to significant downtime
- **Plugin updates and permissions management** — Managing plugin updates and permissions adds complexity
- **No unified control plane** — Treating Jenkins instances as individual "pets" instead of a unified system complicates management and deployment
- **Not cloud-native** — When Jenkins is run on Kubernetes it results in suboptimal resource utilization: idling compute while waiting for other steps in the pipeline to finish


Intuit faced significant user experience challenges with Jenkins. It was hard to troubleshoot failed processes, and users thought the interface was complex and slow.


Using the open source version of Jenkins added hurdles when implementing high availability and disaster recovery features. This meant the team had to develop several custom-built solutions. The failover process for large Jenkins servers when transitioning between regions took up to an hour and didn’t meet standard service level agreements (SLAs). Furthermore, not having a unified control plane made tasks like deploying new Jenkins instances or upgrading plugins tedious, even with automated processes in place.


## How Pipekit overcame CI challenges with Argo


At Pipekit, we had challenges with Jenkins similar to what Bertrand described. As a startup, our primary focus is crafting a lean and adaptable CI approach. With our product serving as a control plane for Argo Workflows, one of our key value propositions is delivering a centralized solution that empowers users to manage their workflows as well as any tools and integrations they plug into their workflows. Our team started encountering more significant challenges as we shipped more integrations and features, quickly expanding our CI.


Similar to Intuit, we had long build times, slow CI and test pipelines for each pull request, and the limitation of pipeline sizes due to running all containers in a pod, wasting cloud resources. What’s more, leveraging spot nodes and handling plugin complexities made our challenges even greater.


What we wanted was to increase our ability to autoscale and minimize our costs. Our ideal scenario was to adopt a “set it and forget it” model that would allow us to reduce the ongoing effort required for Jenkins pipeline tuning. Furthermore, given our plans to deploy with Argo CD, seamless integration with Argo CD, Argo Rollouts and Argo Events was an absolute must-have.


Running each step in a pod by default with Argo Workflows allowed for dynamic resource provisioning, allowing us to scale efficiently and granularly. Argo Workflows’ default parallelism streamlined pipeline speed without the need for intricate configurations, standing in stark contrast to Jenkins' more prescriptive approach.


Ultimately, our transition to Argo Workflows streamlined our CI pipelines and offered the agility and efficiency needed as a startup. On the maintenance front, its lightweight deployment, reduced plugin dependencies, and seamless integration with the Argo ecosystem translated to less time spent on maintenance and more time spent on product development. The flexibility of writing in YAML and using the Hera SDK for Python developers added an extra layer of accessibility for our team.


## Weighing the advantages and disadvantages of Argo and Jenkins


As popular a tool as it is, Jenkins boasts a comparatively robust community and ample resources. For users, this means more resources for quick problem-solving with just a simple search online. Argo is still building its community, and it’s growing strong, though it lacks the extensive online documentation that can be found with Jenkins.


When getting started, Jenkins' plugins initially made it possible to ensure a smooth start. However, over time, they led to the accrual of technical debt and maintenance overhead. This shift turned what once was an advantage into a drawback, prompting us to prioritize feature development over managing CI dependencies.


From a UI/UX perspective, Jenkins caters specifically to CI, so we were used to some of its primitives. In contrast, Argo Workflows offers a more generic interface that is suitable for CI, data pipelines, and infrastructure automation.


For our team, overall, we really felt the benefits of autoscaling and parallelism were significant advantages when switching to Argo Workflows. While we had to consider how we would pass objects between steps in our pipelines, our initial investment in figuring out the process of using persistent volume claims instead of artifacts paid off. As we found out, if you put in the upfront effort, you’ll be able to achieve better scale, faster pipeline runtimes, and reduced costs using Argo Workflows instead of Jenkins.


# Watch the full talk


Before diving into an example of how Jenkins pipeline maps to an Argo Workflows pipeline, Bertrand and I identified how a handful of key concepts mapped between the two solutions.


To watch this presentation in full and to watch Bertrand and I walk through a basic CI/CD pipeline with Jenkins and Argo Workflows, click to watch the video below. If you are interested in reviewing the slides alongside the talk,[visit our repo](https://github.com/pipekit/talk-demos/tree/main/argocon-demos/2023-migrating-cicd-from-jenkins-to-argo) .
