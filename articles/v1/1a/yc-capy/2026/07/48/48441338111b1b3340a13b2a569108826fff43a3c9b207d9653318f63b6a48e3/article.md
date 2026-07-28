---
schema_version: "1.0.0"
document_id: "48441338111b1b3340a13b2a569108826fff43a3c9b207d9653318f63b6a48e3"
company_key: "yc-capy"
company: "Capy"
source_id: "yc-capy-news-import-ccb8c20193bf"
canonical_url: "https://scrapybara.com/blog/speed-scale-stability"
published_at: null
first_seen_at: "2026-07-23T04:45:19.830543+00:00"
fetched_at: "2026-07-28T21:20:09.527818+00:00"
content_hash: "sha256:dd736546295a712bd1882063a58888215eed8eb238811129e3cb82ae057d7407"
---

# Speed, Scale, Stability

Over the last few weeks, we've been working heads down on enhancing our infrastructure to support bigger and more performance intensive deployments of computer-use models. This kind of undertaking comes with unique challenges, and we've made major improvements in 3 main areas. We are currently and will continue rolling these improvements out in the coming days.


## Speed


Speed is crucial (and it's fun). If these agents are to eventually perform meaningful work alongside humans, they need to be at least as fast as the humans they work with. On the model side of things, this means a faster multimodal inference stack and smaller models. This isn't yet in our purview but we've already seen providers start moving in this direction. On the infra side, it means two things for us:


Instances should spin up faster


Spinning up instances with a full GUI is possible with existing container and cloud provider infrastructure, but is generally slow. Spin up times of 1-2 minutes aren't uncommon, and have been acceptable for most applications that they're used for. For AI Agent applications, we need this to be sub-second.


Our initial implementation was hacky, and even after optimizations, instances would often take 5-10 seconds to come online.


Old implementation: Instances would take 5-10 seconds to come online


With our new infra stack, our start times are now comfortably sub-second even for instances with a full ubuntu desktop.


New implementation: Instances come online in less than 1 second.


Speed optimizations are still rolling out and we anticipate even faster start times in the coming days, on the order of 200ms or less.


Actions on instances should execute faster


Once a model spits out an action to be executed, the results after execution should be returned as quickly as possible.


This is trickier to get right, because we need to wait a certain amount of time after dispatching an action for it to execute and the resulting state of the desktop to be fully visible for the agent to process and understand.


To achieve a speedup here, we analysed how long different actions take to complete and for their results to be visible under different circumstances. With our new action execution implementation, which follows our newly released[standard action space](https://scrapybara.com/blog/unified-action-space) , we were able to achieve approx. 50% speedup in action execution across the board.


## Scale


Working with quota limits is somewhat unpleasant. Our deployment and orchestration stack now scales across multiple clusters and to different providers. This is an active area of work for us (and the founding team has had to learn a lot about infra from scratch); so if this is something that excites you, come work with us:[careers page](https://scrapybara.com/careers)


## Stability


A fact of life for early stage startups and early stage tech like computer use is that things will break and/or misbehave a lot. We've been hard at work trying to mitigate a lot of this. Standardizing our computer-use action space was an important step in this direction. Another major facet of this will be implementing robust and graceful exception handling (which can be quite wide because we're working with inherently stochastic stuff here).


On the agent side of things, backtracking and error handling is something most models are yet to become effective at. We've seen huge improvements in recent weeks, and are confident this will keep getting better quite rapidly.


## GET STARTED TODAY


Visit our docs and join our Discord community to see what others are building with Scrapybara. We would love to hear your feedback and see what you build next!
