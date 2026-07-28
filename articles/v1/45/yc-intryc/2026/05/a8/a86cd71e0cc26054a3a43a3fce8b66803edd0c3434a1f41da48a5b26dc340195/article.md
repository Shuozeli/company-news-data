---
schema_version: "1.0.0"
document_id: "a86cd71e0cc26054a3a43a3fce8b66803edd0c3434a1f41da48a5b26dc340195"
company_key: "yc-intryc"
company: "Intryc"
source_id: "yc-intryc-news-import-17b79f653bb0"
canonical_url: "https://www.intryc.com/blog/sop-evaluation-gap"
published_at: "2026-05-13T00:00:00+00:00"
first_seen_at: "2026-07-22T00:22:23.516240+00:00"
fetched_at: "2026-07-28T21:44:24.455372+00:00"
content_hash: "sha256:5111d6fdd208b5cba3915dd8d271ac3a88f24190fb660688540a004794e3bdc2"
---

# Your QA tool sees quality. Intryc sees compliance.

Most QA tools score how agents communicate. Intryc scores whether they followed the right process.


Your current QA tool scores greeting, empathy, and resolution quality, the standard rubric every platform ships with. If those scores are green, your dashboard says your support function is performing. But in telecom, healthcare, financial services, and insurance, that dashboard misses the number that matters to your regulator: did your agent follow your SOPs, step by step, on every case?


That is not a coverage problem. You may already have 100% automated QA coverage. It is a depth problem.


## You probably do not have a coverage problem. You have a depth problem.


Standard QA rubrics evaluate four to six criteria: greeting, empathy, clarity, resolution, call closing. These are quality-of-response criteria. They answer one question: was this a good conversation? They do not answer the question that matters in regulated industries: did the agent follow the correct process for this case type, in the correct order, under this SOP?


There are two distinct gaps in support QA, and conflating them is why most teams in regulated industries are underserved by their current tool.


The coverage gap is the share of conversations you actually evaluate. If you sample 2% of cases manually, you have a coverage gap. Most automated QA platforms exist to close it. They score 100% of closed cases on a standard rubric. For many teams, this is solved.


The depth gap is what your rubric evaluates. Standard criteria cover communication quality. They do not cover process adherence. A team can have 100% QA coverage and zero SOP-adherence evaluation at the same time. These are two different numbers.


In telecom, healthcare, financial services, and insurance, the depth gap is not a coaching problem. It is a compliance risk. If an agent deviated from your SOP and a regulatory audit surfaces that case, your QA record showing 94% quality scores does not help you. The auditor is not asking whether the agent was polite. The auditor is asking whether the required disclosure was made before the ticket closed.


A VP of Support & Operations at a US cloud communications company put it directly in a recent conversation:


> "We're not capturing that level of detail. SOPs, like how you follow into that A to Z. We're not capturing that."


His team runs autoQA on every closed case. The dashboard is green. The signal he needs is still missing.


## What SOP-adherence evaluation means (and what it does not mean)


**SOP-adherence evaluation** is the automated assessment of whether a support agent followed the steps in an operating procedure for a given case type, in the required sequence. It is distinct from quality-of-response evaluation, which scores communication criteria like empathy, clarity, and resolution. It is also distinct from coverage, which is the percentage of conversations evaluated. A team can have 100% QA coverage and zero SOP-adherence evaluation simultaneously.


Consider a concrete example. A telecom SOP for a number-porting case typically requires the agent to verify the account holder's identity, confirm the receiving carrier, disclose the porting timeline and any associated fee, and log the confirmation ID in the case record. A standard QA rubric can score whether the agent was polite and resolved the issue. It cannot tell you whether the fee disclosure was completed before the ticket closed. If it was not, and the customer later disputes the charge, your QA record is silent on the compliance question.


SOP-adherence evaluation reads the SOP. It evaluates whether the agent's actions in the conversation match the required sequence. The result is a compliance record alongside the quality record. You get both.


This is not about replacing your existing QA program. SOP-adherence evaluation adds a compliance layer on top of quality evaluation. You do not have to choose one over the other.


## 100% automated QA coverage and 0% SOP-adherence evaluation are not a contradiction


Some teams reading this already run automated QA on every conversation. Every closed case is scored. The team has dashboards. The numbers look good. They still have zero SOP-adherence signal.


This is not a failure of their current tool. Standard autoQA platforms are built to evaluate quality criteria. They do not ingest your SOPs. They do not know that a healthcare enrollment call requires a specific sequence of disclosures. They do not know that a financial services complaint case requires escalation within a specific timeframe. They cannot score adherence to a process they were not given.


What standard autoQA tells you:


- Greeting quality
- Empathy and tone
- Issue resolution
- Call closing


What standard autoQA does not tell you:


- Did the agent follow the correct process for this case type?
- Were the required disclosures made?
- Was the escalation path followed?
- Is there a process-adherence record you can produce in an audit?


The same operator framed the stakes plainly:


> "Otherwise you can do, you know, regulatory trouble."


Regulatory trouble is not a coaching gap. It is exposure. The QA record your tool produces today is not the record your compliance team needs.


## How Intryc evaluates SOP adherence at scale


Intryc connects your knowledge base to specific evaluation criteria. You point it at the SOP documents that govern each case type. The platform reads the SOPs, builds the evaluation logic, and applies it to every case in that category. Each evaluation produces both a quality score on standard criteria and a compliance score on SOP adherence, side by side.


For operations with multiple verticals, different SOPs for different issue types, you can route criteria to specific case types. A telecom operation with separate SOPs for voice, messaging, and number porting gets separate compliance records per vertical. An insurance operation with different disclosure requirements for claims versus renewals can evaluate each correctly. Healthcare operations with separate workflows for enrollment, billing, and clinical handoff get an evaluation layer that respects the difference.


You can also evaluate active cases, not just closed ones. If an agent is mid-case and has already skipped a required disclosure, the compliance record can surface that before the ticket closes. This is the difference between a coaching tool and a control layer. Catching a missed step after the case closes is documentation. Catching it before the case closes is prevention.


The buyer above asked the question directly in a demo: can I evaluate active tickets, not just resolved ones? The answer was yes. His response: "Now this looks good."


## Your compliance team will ask about this. Here are the answers.


In regulated industries, adding a QA tool that touches customer interaction data triggers a compliance review. We have been through this review with teams in telecom, financial services, and enterprise B2B SaaS. The questions come in a small number of predictable forms. Here are the answers before your InfoSec team asks.


**Where is the data processed?** Intryc runs on AWS with region selection. Enterprise deployments can be pinned to a specific region. UK and EU residency requirements are supported.


**Does Intryc use customer interaction data to train its models?** No. Evaluations are run against your data. Your data is not used for model training. For customers with enterprise clients who have LLM-exclusion clauses in their DPAs, Intryc supports tag-based ticket exclusion. Specific tickets can be flagged to bypass AI evaluation entirely, producing an auditable record of exclusion.


**How does the knowledge base integration work? Does it pull our entire KB?** You control the scope. You can connect specific pages, sections, or articles, not the full KB instance. This matches the scoping model your IT or InfoSec team likely already approved for your helpdesk vendor.


**What certifications does Intryc hold?** SOC 2, HIPAA, GDPR. Sub-processor list available for MSA review. InfoSec questionnaire turnaround is standard enterprise.


The compliance gate is not the obstacle most teams treat it as. It is a checkpoint with known answers. The question is whether the vendor on the other side has been through it before with peers in your industry.


## This is for teams that already have QA infrastructure and still have a compliance gap


This page is not for teams building QA from scratch. If you have zero QA coverage, the first move is to add coverage. That is a different problem with different vendors.


This is for you if:


- Your team runs automated QA on every conversation, or close to it
- Your rubric scores communication quality: greeting, empathy, resolution, closure
- You operate in telecom, healthcare, financial services, or insurance
- A regulatory audit could ask you to produce a record proving an agent followed your SOPs on a specific case, and today you cannot produce that record


If that is your situation, the gap is not coverage. It is depth. Your current tool is doing its job. It is not built for the job you need done next.


## Frequently Asked Questions


**What is SOP-adherence evaluation?**


SOP-adherence evaluation is the automated process of checking whether a support agent followed the steps in your standard operating procedures for a given interaction, in the correct order, at the correct stage of the call or ticket. Most QA tools score the quality of an agent's communication: empathy, clarity, resolution. SOP-adherence evaluation scores whether the agent followed the correct process. These are two different assessments. You can have high quality scores and zero SOP-adherence signal at the same time.


**How is SOP-adherence evaluation different from regular quality QA?**


Regular QA evaluates how well an agent communicated: did they greet the customer, show empathy, resolve the issue, and close the call professionally? SOP-adherence evaluation checks whether the agent took the right steps in the right sequence according to your written operating procedures. For example, a financial services QA rubric might score communication quality at 9 out of 10 while missing that the agent failed to deliver a required fee disclosure in the correct sequence. The standard QA score reads as a pass. The SOP-adherence record flags the compliance gap.


**Can automated QA tools evaluate SOP compliance?**


Most automated QA tools are built for quality-of-response evaluation and cannot evaluate SOP adherence because they do not ingest your operating procedures. SOP-adherence evaluation requires connecting the QA platform to your knowledge base, specifically the SOP documents for each case type, and building evaluation criteria that check for process sequence, required disclosures, and mandatory steps. Intryc supports this connection at the article and page level, allowing you to scope evaluation criteria to specific case categories and the SOPs that govern them.


**Why does SOP compliance matter more in regulated industries?**


In telecom, healthcare, financial services, and insurance, your operating procedures exist in part because regulatory requirements mandate specific steps: required disclosures, identity verification sequences, escalation timeframes, documentation standards. A quality QA record showing high empathy and clear communication does not demonstrate process compliance. If a regulatory audit surfaces a case where the correct disclosure was not made, your QA dashboard will not help you. A compliance-aware QA record, one that shows the agent followed the SOP on that case, is the record that matters.


**What does Intryc do differently for regulated industries?**


Intryc connects your knowledge base to your evaluation criteria. You specify which SOP documents govern which case types. The platform evaluates whether each agent's actions in a conversation match the required sequence for that case type. It produces both a quality score and a compliance record per evaluation. For teams in regulated industries, this means you get the coaching signal you already have (quality scoring) plus the compliance record your current tool cannot produce (SOP adherence, with an auditable trail per case).


See what your current QA tool cannot score. The demo walks through SOP-adherence evaluation against a real case type from your industry, with both a quality score and a compliance record side by side. No pitch deck. Just the product.


[See the demo.](https://www.intryc.com/#demo-section)
