---
schema_version: "1.0.0"
document_id: "73a1eb6ee2dd397055f03bb9a19b4155f520fa89f27a74bcea2a5861e450ef5c"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/panel-argo-ml-achieving-scalability-user-experience"
published_at: "2024-08-30T16:56:13+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T20:59:29.484597+00:00"
content_hash: "sha256:b9c8ee510bff94dc42a5606b4b602e450eb1c5835d792e71a1b98194f1f8b44e"
---

# Argo for ML: Achieving Scalability and User Experience

While at ArgoCon and KubeCon Europe in Paris, J.P. Zivalich, Pipekit, Elliot Gunton & Sambhav Kothari, Bloomberg, and Alina Schmidt, Centrica Energy, engaged in a panel discussion that highlighted the use cases at Bloomberg, Dyno Therapeutics, and Centrica where Argo Workflows met scalability challenges. Their focus was on the balancing act between achieving high scale and appropriately abstracting complexity so that each organization’s ML teams could operate efficiently.


**J.P.: What are the challenges with machine learning and orchestrating that you have been running into generally?**


Sambhav: Bloomberg is a financial data company. We provide high quality data and experiences to explore, tract, and analyze that data. As you can imagine, with this large amount of data, we also provide various AI integrations in our products, to better explore and make sense of that data.


To highlight the challenges, models tend to decay over time, unlike code. So they often need to be continuously trained and deployed. At Bloomberg they call this the model issue detection and remediation cycle. The issue with these remediation cycles is that they are almost never fully autonomous; there are always humans in the workflow loops. They require domain experts to come in and do appropriate QCs to provide appropriate input before they can be handed off again to an automated pipeline.


Apart from all of this, the AI landscape is evolving and rapidly changing. Every single day you have new ways to extract your features and train your models. What stays common is the actual step itself. Your training code might change, but the fact that the training code accepts feature vectors and outputs and models remains the same. You need an orchestration layer to glue all of these steps together, a glue that can remain stable yet flexible to all of these changes.


‍ **J.P.: Alina, what is Centrica’s experience with ML and orchestration?**


Alina: A brief preface on energy trading: We trade in different markets and have sharp deadlines. This means that we have to run a lot of Crons \[Jobs\] to get continuous data. We also trade in other markets, once every hour, thirty minutes, 15 minutes, where we have a lot of data. We have ML models that need to make new predictions based on this data as close to the deadline as possible. We have this spikey computation need, essentially.


‍ **J.P.: So why choose Argo Workflows, Sambhav will you dive into this first?**


Sambhav: Kubernetes is not new to Bloomberg. We built our Bloomberg ML platform on top of Kubernetes back in 2017. So we have 7 years of experience scaling and building multitenant ML platforms on top of Kubernetes. So when it came to choosing an orchestration platform, Argo Workflows fit in perfectly. So it brings in all the same things as Kubernetes does in terms of multi-tenancy in terms of scalability, and most importantly for us: vendor neutrality. This allows us to be sure of the future of the product but we can also come in and contribute and help with the product.


For us, apart from all of this, in terms of the core requirements that Argo really satisfied, a few of them were multitenancy. We needed ways where our AI developers could self-service and run their workflows without affecting other teams. These workflows included models with sensitive data. We go through the Principle of Least Privileges and ensure that only the people that need to access a data set have access to it. Kubernetes provides really great primitives for multitenancy, for work-load isolation, resource quotas, etc. Some other features, in terms of the ML space, are human-in-the-workflow loop, artifact visualization, and intermediate parameters — we use this heavily. Artifact visualization is great because if you are training a model and you have a report out that is due, on the evaluation metrics, you can see it right there, then combine it with intermediate parameters to figure out if you need to retry the loop with a different set of parameters or am I happy to proceed to the next step?


In addition, it is declarative, built on YAML, we can take it and adapt it to any user experience we want, it is not tied to one language, for some set of our users, Python is important, so we can provide an appropriate user experience using Python and Hera.


‍ **J.P.: It seems like the strong multitenancy with sensitive data is a common thread between the two companies. Alina can you touch on Centrica’s Argo Workflows adoption?**


Alina: Multitendancy was very important to us because we have different teams. With energy trading, even within the same company there are teams that often compete so total privacy is needed.


We needed Cron Jobs that could spawn, and big fan outs because we have a lot of data sources and we need to make predictions based on these sources separately.


‍ **J.P.: For Elliot, what is Hera, what is the role of Python on top of Argo Workflows?**


Elliot: Hera is a custom-written Python SDK mainly for Argo Workflows with some support for Events. It provides all of the extra functionality that you need to communicate with Argo Workflows entirely within Python. You can write your functions which become script templates, you can orchestrate them in your workflows, then you can submit them, all in Python.


If you want to use Argo Workflows it is pretty hard right now so you might steer towards alternatives. At Bloomberg, we thought we have Argo Workflows and we would like to use it. But our ML developers are a bit resistant to using it. How can we bridge the gap between them? Hera was the answer to that.


‍ **J.P.: How has Bloomberg changed and been affected by the decision to adopt Hera specifically.**


Sambhav: The Hera adoption was a massive turning point for Argo adoption within the company, especially for our ML teams. We have an in-house workflow orchestration team that provides Argo as a multitenant offering to the rest of the company. The initial set of users for this platform were largely CI/CD use cases or Cloud deployment pipelines.


Despite the fact that this was a well-supported platform offering, it was not gaining a lot of traction with our AI and ML teams. I think, even after all of this, the AI teams were so entrenched in Python that they would rather spin up their own custom Airflow clusters rather than use the common platform offering.


Hera was a massive change or shift. We have a lot of experience building ML platforms on top of Kubernetes. We know how to adapt Kubernetes paradigms to Python. Hera was our answer to that.


To give you some numbers, we have an AI group of over 300 engineers who now use Hera. We have been able to migrate and even have multiple teams adopt continuous training and deployment pipelines because of Hera — over 40 teams. In general people are very happy and productive. We have a support channel that gets more than five or ten questions a day.


‍ **J.P.: Ironically if the support channel is active it means that people are happy and using the product. Alina could you dive in into how adapting Hera has affected Centrica?**


Alina: We also, similar to Bloomberg, set up Argo Workflows and handed it off to them with YAML. After the brave, early adopters created workflows with YAML, it stalled out a bit, because people would rather use what they were used to.


We aren’t sure who found Hera, but one of the data scientists did. They started using it then it spread like wildfire. So we had to support it officially also. Even the early adopters now use Hera to better work with other teams.


‍ **J.P.: What have the challenges been for adopting Argo Workflows in Hera? How have you worked through it?**


Sambhav: I think where Bloomberg has found it challenging for adopting Argo is the developer experience, especially for people who are not familiar with Kubernetes paradigms. We operate very differently as a platform team: rather than just developing platform features we develop a feature, then we go through a cycle of actually working with our tenant teams, to help them on board to the platform, gather feedback, requirements, feature requests, iterate on them, then continue the cycle again.


Largely for us, concerning the developer experience aspect, we’ve tried to solve it in two ways: One is attacking the core of the problem: there is a set of common functionality or workflow templates that we provide to our users. We work with the team so we know what their requirements are, what workflow templates they are developing. As we see enough common sets of requirements bubble up from multiple teams we take that on as a platform offering and provide it as part of our internal workflow template library.


The other challenge is concerning the developer experience around Hera when we cannot provide functionality out of the box. So Hera is still maturing around its developer experience aspect, I’ll hand it over to Elliot.


Elliot: As a first time open source contributor, Hera is the first project I’ve been maintaining. It has been interesting seeing all of these patterns of people using it, how they are using it. For example, we didn’t think that people would be using Hera entirely to avoid YAML, and interacting with Argo entirely through Python. Another thing: at Bloomberg, I can see the code that people are writing. We’ve been seeing design patterns coming out, Hera design with all of these context manager things. Maybe we made some missteps here and there? Overall the project is maturing. We are getting there to see what we get to do next.


‍ **J.P.: You work closely with developers at Bloomberg, and build out that workflow template library to help them down that golden path. At Centrica, the teams are competing against each other, so you may have to limit yourself concerning the code you see or don’t see that they’re working on. How does that compare with Hera being adopted like wildfire, since you have to let the data scientists do what they do?**


Alina: There is a lot of pressure on the data scientists themselves too because they have to independently make their workflows. We can’t be too hands-on. Hera has improved, and has nice user-friendly documentation. It is very good. It is almost too good. A lot of people using just Hera don’t really know about Argo’s core concepts. They haven’t had to — in teams they share code. So everything just works until it doesn't, then we’re not sure what is going on.


‍ **J.P.: Can I quote you on the documentation being too good? I think that’s the only time I’ve ever heard that in an open-source project. Our final topic is about the future: The ML/AI field is quickly evolving. What is in store for the future of ML in Argo Workflows specifically? What does a complete ML stack look like? How does Argo Workflows play into it?**


Sambhav: In my opinion, how do I see Argo Workflows and the ML field evolving? For Bloomberg, as I mentioned, Hera adoption and Argo Workflow orchestration adoption has spread like wildfire. We have hundreds of models that are continuously trained. The problem becomes: How do we track which model is deployed? How do we make sure that we have an accurate picture of what data went into, what parameters were used. It becomes a deep cataloging and provenance problem, not just for finding out what is running in production, but what issues can occur, how can we fix it, alert people, and so on.


Provenance tracking is becoming very important. Workflows, the orchestration platform, has a big part to play there. As the piece that is gluing everything together, it is the perfect source of truth for figuring out what exactly ran and connected multiple steps together. So if there are some deep integrations between being able to export workflow parameters, outputs, inputs, to a common ML metadata store, where the user doesn’t even have to write the code, but it automatically exports itself that would be great in terms of provence tracking.


The other question, how do we see this fit into the entire stack? The other side we haven’t talked about is production monitoring, eventing. This is one part of the problem: catalog everything. The next part is being able to automatically detect drift issues then redo the cycle all over again where you can continuously train and deploy without humans in the loop.


‍ **J.P.: Getting to a fully self-serve automated system. It will be good to see when that future comes about. Alina, thoughts on the future of Argo Workflows, ML, and where Argo Workflows fits into the stack.**


Alina: Much like Bloomberg, we’re definitely looking into production metrics and monitoring and tracking of different models. Beyond that, we are looking at Argo events, testing that out, so we can react directly to new data coming in rather than relying on Crons that are hopefully after the data came in — so to speed things up a little. And also some visualization of metrics — hopefully data scientist friendly - that they can set up themselves, especially for the development of new models.


‍ **J.P.: Metrics and observability seems to be a hot point - hopefully there is some progress on that in the future.**


Alina: Yes, once it works you have to actually check that it works, like track it.


‍ **John Knych: Three of you used the phrase that Hera spread like wildfire and it seemed like adoption was smooth and effective. Despite that, at Bloomberg, when the 300 engineers adopted Hera, was there any resistance, and how did you meet that resistance? And perhaps how will that affect how you improve Hera for the future?**


Elliot: An interesting question. We went into it with goodwill. So once we publicized that we are all working on this project and that we’d have a new way to use Argo Workflows coming out, and we publicized that there would be a new workshop coming out where you could get stuck in and get a kickstart to using it - that helped to avoid any major resistance. Then within Bloomberg we directed towards certain teams that we knew would benefit from writing these model remediation pipelines more easily, so they were our initial adopters, and then teams started adopting it by themselves.


‍ **Caelan Urquhart: Do you have any vision for Hera to expand to any of the other Argo Projects and any thoughts if that’s possible, what’s your thinking there?**


Sambhav: We’ve certainly explored the idea. We do have some support for Argo Events. I think largely focused on Workflows because I think we can improve a lot there and that’s what we’re most familiar with at this point. I think definitely — we have seen a lot of response from this community that the way we have married Kubernetes concepts, especially with Pydantic and some of the features like Script Runners, sort of makes these platforms and systems more Python native and people want the same experience for other things. We’re certainly open to it. I think it largely depends on where the community drives us.
