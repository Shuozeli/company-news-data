---
schema_version: "1.0.0"
document_id: "ae1bcdd7514dbf70543b6cc93851812eb8d81d0b99e9e7474b2a8c0895767d7f"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/kubecon-eu-2024-highlights-and-recap-from-paris"
published_at: "2024-04-20T23:27:39+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T21:00:24.623123+00:00"
content_hash: "sha256:82c07dd404e55f03bc64edcc20d04273046a885f3f3f652e9e5c82225a57a4da"
---

# KubeCon EU 2024: Highlights and Recap from Paris

This was our team’s second time attending KubeCon Europe, and what an event it was. From morning to night, it was a whirlwind of activity, and our days were full of insightful talks and exciting conversations with people across so many different industries. We got to connect with project experts, share our experiences, talk about what we’ve been building, and gain valuable insights into the latest ways Kubernetes and other cloud-native technologies are being put to use.


Now, for those of you who weren’t able to make it to this year’s event in Paris — or simply for those of you wanting to make sure you don’t miss a thing — we want to offer a recap of what we experienced and took away. Here is a roundup of some of the highlights from ArgoCon and KubeCon EU 2024.


## Pipekit at ArgoCon Europe


### The Argo rocketship isn’t slowing down any time soon


Have you ever been to ArgoCon? It’s a co-located event that takes place the day before KubeCon Europe and North America kick off. Twice a year, users, contributors, and maintainers of[Argo Project](https://argoproj.github.io/) (that includes Argo CD, Argo Workflows, Argo Rollouts, and Argo Events) come together to highlight new developments and use cases for each of the open source tools within the project. So, if you’re deploying and running applications and workloads on Kubernetes, this is the project and event for you.


Once again, Argo community leaders were able to share a number of impressive project statistics that highlight just how fast-growing Argo has become since becoming a graduated project a little over a year ago:


- Third-highest PR authors of CNCF projects
- 245,000+ contributions
- 14,000+ PRs and issues
- 8,000+ commits


Our own Alan Clucas delivered one of the[welcome addresses](https://www.youtube.com/watch?v=rAxmd9oPiFk) to kick off the event alongside AWS’ Carlos Santana and Intuit’s Michael Crenshaw and announced that[Argo Helm](https://github.com/argoproj/argo-helm) was recently promoted to become a full part of the Argo ecosystem.


### Watch our talks from ArgoCon Europe


Including that welcome address, our team delivered a total of seven talks at this year’s ArgoCon EU. These sessions covered a range of topics, from simplifying YAML complexity with Hera's Python-functions-as-templates to mastering the architectural intricacies of Argo Workflows. We broke down leveraging Argo Workflows for scalable ML platforms, explored the seamless integration of Jenkins with Argo CD and Rollouts, and provided practical guides on scaling effectively. We even highlighted the benefits of Argo CD plugins as services for enhanced scalability, security, and development iteration.


We covered it all, and we're excited to share these insights with you. You can watch all our talks on our dedicated[talks and demos page](https://pipekit.io/talks-and-demos) .


## Our recap of KubeCon Europe


If you were at this year’s KubeCon EU, we hope you got a chance to make it by our booth to say hi and see what we’ve been up to at Pipekit. We’re learning more and more each year, and not just about what swag is the most likely to encourage the greatest amount of attendees to visit our booth. By the way, it’s definitely the shiny, metallic stickers.


### Must-watch talks from KubeCon


If you’ve been to a big event like KubeCon before, you know how important it can be to plan your schedule each day. There are so many different talks to attend.


Based on the lists of talks our team members put together for each day, here are some of the must-watch talks from this year’s event.


[Shift-Left: Past, Present, and Future of Validation in CI for GitOps Workflows](https://www.youtube.com/watch?v=KaXIq8Qv77A)


One of the standout talks delved into the challenges and solutions of GitOps workflows, particularly focusing on the critical step of validation in CI. GitOps has undoubtedly become a dominant approach for managing configurations, but without robust validation, automated deployments can lead to unpredictable outcomes and increased maintenance costs. The speaker introduced` kubectl-validate` as a tool to locally and reliably validate Kubernetes manifests, offering insights to avoid common pitfalls in setting up CI for GitOps systems.


[The Party Must Go on - Resume Pods After Spot Instance Shut Down](https://www.youtube.com/watch?v=c2MbSM9-7Xs)


Another compelling session addressed the challenges posed by spot instances, which offer significant cost savings but are prone to frequent shutdowns. The talk presented a Kubernetes controller developed by QA Wolf that orchestrates the snapshot and recovery of containers from failing nodes to ensure near-zero downtime. This innovative solution demonstrates the potential to leverage spot instances without compromising data integrity, especially for long-running jobs like automated QA tests and data processing pipelines.


[Scaling up Without Slowing Down: Accelerating Pod Start Time](https://www.youtube.com/watch?v=RJ6Lt9bVNTw)


The topic of optimizing pod start times in Kubernetes was also a major highlight. Cold start times, particularly for pods with large container images, can lead to inefficient deployments and increased costs. The talk explored various open-source approaches, such as on-demand image loading and pre-warming nodes, highlighting how the optimal strategy varies depending on workload type and system scale. This session provided a valuable framework for deciding the most suitable approach for accelerating pod start times in Kubernetes workloads.


[Disintegrated Telemetry: The Pains of Monitoring Asynchronous Workflows](https://www.youtube.com/watch?v=GvF1ivr7RlA)


Monitoring asynchronous workflows presents unique challenges due to disintegrated telemetry pieces that make it difficult to trace the lifetime and impact of messages or events. This session delved into the complexities of distributed tracing solutions, exploring the strengths and weaknesses of different approaches. The speaker also discussed standardization efforts, including W3C context propagation drafts and messaging semantic conventions by the OpenTelemetry messaging workgroup, shedding light on potential solutions to this pervasive issue.


[Agent-Based Design for Automating Large-Scale K8s Operations](https://www.youtube.com/watch?v=Zkn7y6_pyVg)


Lastly, a fascinating talk showcased GitHub's approach to automating large-scale Kubernetes operations through an agent-based design. With a Kubernetes footprint spanning multiple clusters across various regions and thousands of nodes, GitHub has developed internal tools that codify operator tasks and ensure reliable changes and upgrades across the control plane and worker nodes. This session provided valuable insights into the challenges and strategies of managing large-scale Kubernetes infrastructures, featuring examples of how these tools power some of GitHub's most critical services.


## KubeCon North America 2024: See you in Salt Lake City


Another KubeCon down in the books! And now we turn our attention to[KubeCon NA](https://events.linuxfoundation.org/kubecon-cloudnativecon-north-america/) taking place in Salt Lake City, Utah.


We’ll be sharing more about KubeCon NA as announcements and news are released, so stay tuned. Until then, if you’re planning to attend KubeCon NA and want to connect with the team, don’t hesitate to[reach out — and don’t wait! We’d love to hear from you](https://book.vimcal.com/p/HtMJs9N9QZa8Rd3E) .
