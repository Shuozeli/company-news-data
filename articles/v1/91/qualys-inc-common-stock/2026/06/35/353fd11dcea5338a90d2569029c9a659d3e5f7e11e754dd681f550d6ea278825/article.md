---
schema_version: "1.0.0"
document_id: "353fd11dcea5338a90d2569029c9a659d3e5f7e11e754dd681f550d6ea278825"
company_key: "qualys-inc-common-stock"
company: "Qualys Inc. Common Stock"
source_id: "qualys-inc-common-stock-news-import-04a5e6e88fc1"
canonical_url: "https://blog.qualys.com/qualys-insights/2026/06/04/from-operating-model-to-product-how-we-built-the-roc-for-detection-speed-remediation"
published_at: "2026-06-04T21:17:17+00:00"
first_seen_at: "2026-07-22T10:38:12.541071+00:00"
fetched_at: "2026-07-28T21:42:44.602232+00:00"
content_hash: "sha256:092e6e3656c0baa45dbbb32176e9aa0d04ea74244911d6c5037f943ac9b72d14"
---

# From Operating Model to Product: How We Built the ROC for Detection-Speed Remediation

#### Table of Contents


- Why Aggregation Was Not Enough
- Tying Risk to the Business
- Knowing Is Not Enough You Have to Be Able to Fix It
- Why This Cannot Wait


In the[first article](https://blog.qualys.com/qualys-insights/2026/04/06/why-every-enterprise-needs-a-risk-operations-center-roc) in this series, we made the case for a prevention-led operating model. This article is about what happened next: the decision to build something that did not exist, and what it took to make it real.


Turning an operating model into a product sounds straightforward until you are standing in front of the actual problem. For us, it was this: every organization we spoke to was managing risk signals that lived in completely separate systems, each scored by a different tool, each using a different definition of what critical actually means. Network risk, identity risk, software risk, asset risk, cloud risk — all of it siloed, all of it speaking a different language. No single team had the full picture. No single platform had been built to create one.


That fragmentation was not a reporting inconvenience. It was the core structural problem underneath everything else. If you cannot see risk as a whole, you cannot prioritize it intelligently. And if you cannot prioritize intelligently, you are always reacting to whatever is shouting loudest rather than what actually matters most to the business. And in today’s AI-driven vulnerability landscape, the ability to sift through the noise and remediate at speed is no longer a nice-to-have; it’s business-critical.


The first product we built for the ROC was an[enterprise risk management platform](https://www.qualys.com/apps/enterprise-trurisk-management) designed to change that: every risk signal in one place, evaluated consistently, and tied directly to business consequences.


***Fragmentation was not a reporting inconvenience. It was the core structural problem underneath everything else.***


---


**Find out how Qualys solutions prepare you for the post-Mythos era of risk.**


[Find Out More](https://www.qualys.com/post-mythos-autonomous-remediation)


---


## Why Aggregation Was Not Enough


The first challenge we hit was one that sounds technical but is fundamentally a governance problem. Bring findings from a dozen different tools into one place, and you quickly discover they are not speaking the same language. One vendor’s critical is another vendor’s high. A score that means confirmed, weaponized, and actively exploited in one tool means theoretical maximum impact in another. Placing those scores side by side and treating them as equivalent produces decisions that are no more reliable than the inconsistent inputs they came from.


Normalization had to be foundational to the platform — not just aggregating findings but standardizing how they were evaluated so that an organization could compare risk across its entire environment on a level basis. Every score carries a lineage. Every comparison traces back to its source. That transparency was not a feature we added later. It was a requirement from the beginning, because boards will not act on a risk view they cannot explain, and they will not explain one they do not believe in.


## Tying Risk to the Business


Once findings were normalized, the next challenge was making them meaningful to the people who needed to act on them. That meant tying risk back to the applications and business functions that generate real-world consequences. We worked with finance teams to assign business value to individual applications: if this system went down or was compromised, what would it cost? What revenue would be affected? What operations would stop?


That exercise changed the shape of every prioritization conversation we had. A vulnerability that seemed minor in isolation suddenly carried material weight when set against the business process it could disrupt. A misconfiguration that would have sat in a queue for weeks moved to the top of the list the moment its business context was visible.


***A vulnerability that seemed minor in isolation suddenly carried material weight when set against the business process it could disrupt.***


That exercise also revealed the scale of what we were dealing with. A single business application might depend on thousands of components: users, containers, microservices, networks, firewalls, third-party services, system accounts, each carrying its own risk signals. Stitching that picture together manually consumed entire teams and still produced an answer that was stale before it was delivered. The platform existed to do it continuously, automatically, and in a form that a board member could read without a translator.


## Knowing Is Not Enough — You Have to Be Able to Fix It


Detection and prioritization tell you what matters. They do not make you safe. The gap between knowing about a risk and actually closing it is where most security programs quietly lose ground, and it is the gap we were determined to close.


Qualys was among the first vulnerability management platforms to integrate patch deployment directly alongside detection. The reasoning was simple: if you find a vulnerability and then hand it off to a separate system, a separate team, and a separate workflow, you have introduced latency at exactly the point where speed matters most. Putting detection and remediation in the same platform, with the same data, removes that handoff. Fewer steps between knowing and fixing means a smaller window for an attacker to walk through.


Over time, what started as patching evolved into something more complete. Patching is not always the answer the situation demands. A server that cannot come offline during business hours, an asset locked behind a change control window, infrastructure where a patch carries a real risk of breaking something in production — for all of these, a patch is the right long-term fix and the wrong short-term response. The platform grew to offer virtual patching, WAF rules, compensating controls, configuration changes, software removal, and asset isolation. Not workarounds. Deliberate remediation paths matched to the asset and the moment.


Today, with the exploitation window at[negative seven days median](https://cloud.google.com/security/resources/m-trends) and Claude Mythos Preview capable of chaining vulnerabilities into working exploits within hours of disclosure, this capability is not a convenience feature. It is the difference between an organization that can respond at the speed of the threat and one that cannot. The[80 percent reduction in average time to remediate](https://www.brighttalk.com/webcast/11673/667239) that customers see on the platform is not just a product of faster patching. It is the product of having the right remediation option available for every asset, every environment, every constraint.


The logical next step in that journey is knowing not just what to remediate but what actually needs remediating in your specific environment — which vulnerabilities are genuinely exploitable given the controls you have in place, and which are theoretical risk that no attacker is going to reach. That is the question TruConfirm and Agent Val were built to answer, and it is what the next article in this series is about.


## Why This Cannot Wait


On April 7, 2026,[Anthropic announced Claude Mythos Preview](https://www.anthropic.com/glasswing) — a frontier AI model that autonomously discovers and exploits software vulnerabilities by chaining multiple CVEs within hours of disclosure. In initial private testing, it surfaced thousands of zero-days, including a 27-year-old OpenBSD flaw and a 17-year-old FreeBSD remote code execution. More than 99 percent remain unpatched.[As of May 22, 2026](https://red.anthropic.com/2026/cvd/) , the model has found more than 23,000 vulnerabilities. Other frontier models will follow, CVE volume is expected to surge two to three times, and the exploitation window will compress further. The argument for a different operating model was already strong before this happened. Mythos made it urgent. The ROC powered by the Qualys TruRisk Management Platform provides the AI-speed detection, hyper-prioritization, and machine speed remediation to achieve autonomous remediation as required in the Frontier AI era.


---


**Sign up for a demo of Qualys Enterprise TruRisk Management to see how you can set up your own ROC for detection-speed remediation.**


[Sign Up Now](https://www.qualys.com/demo/enterprise-trurisk-management)


---


*In the next article in this series, we look at how the ROC handles the question that sits underneath all of this: not just which vulnerabilities are dangerous in theory, but which ones are actually exploitable in your environment today.*
