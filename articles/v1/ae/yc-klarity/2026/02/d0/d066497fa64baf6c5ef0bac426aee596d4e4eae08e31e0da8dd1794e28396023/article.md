---
schema_version: "1.0.0"
document_id: "d066497fa64baf6c5ef0bac426aee596d4e4eae08e31e0da8dd1794e28396023"
company_key: "yc-klarity"
company: "Klarity"
source_id: "yc-klarity-news-import-eb5790299337"
canonical_url: "https://klarity.ai/resources/blog/human-side-of-context-graphs"
published_at: "2026-02-04T00:00:00+00:00"
first_seen_at: "2026-07-22T01:34:36.098678+00:00"
fetched_at: "2026-07-28T22:21:48.311987+00:00"
content_hash: "sha256:ad406d65a2da07109befceb2888084a8651b8218ac76bd481b4664390a1b97e7"
---

# The Human Side of Context Graphs

If you’re building with AI, you’ve probably heard about the “context graph”. It’s become central to the conversation about why enterprise AI succeeds or fails. Foundation Capital recently called context graphs “AI’s trillion-dollar opportunity”.


Their thesis is compelling: the next trillion-dollar platforms won’t be built by adding AI to existing systems of record—they’ll be built by capturing the decision traces—what Foundation Capital defines as “The exceptions, overrides, precedents, and cross-system context that currently live in Slack threads, deal desk conversations, escalation calls, and people’s heads.”


It’s clear that context graphs are critical for agents to work. But there’s an assumption baked into the thesis worth examining: that decision traces, once identified, can be captured as they surface.


That works for traces that are emitted—the Slack messages, the email threads, the recorded conversations. But most human reasoning doesn’t emit a trace. Someone makes a judgment call, takes an action, and moves on. The system still records the outcome, but the reasoning never surfaces.


Even the closest observation of what people write and say will only ever give you an incomplete view. The rest has to be actively extracted—through methods that surface the why behind decisions, not just the decisions themselves.


**That’s the gap. Everyone agrees human reasoning matters. But there’s never been a scalable way to capture it.**


## The Structural Challenge: Human Reasoning Doesn’t Emit Data


There’s a fundamental asymmetry in enterprise knowledge. System activity—clicks, API calls, workflow executions—generates structured logs automatically. Agent behavior can be instrumented and observed. When an agent evaluates a policy, routes an approval, or executes a decision, you can capture what happened and why.


Human reasoning doesn’t work that way. It lives in neurons, not databases. It surfaces in conversations, gets applied in the moment, and then vanishes. The system records the outcome—a discount was approved, a ticket was escalated, a contract was flagged—but not the thinking that led there.


For example, say a team handles revenue recognition reviews for contracts. On the surface, the process looks straightforward: receive contract → review terms → flag issues → approve deal. But senior team members had developed judgment about what constituted a “non-standard term” that needed flagging—knowledge built from years of seeing edge cases, understanding product combinations, and knowing which contract variations posed compliance risks.


Of course, that reasoning wasn’t written down anywhere—why would it be? This is the human knowledge problem. And it’s twofold:


1. It’s slow and it breaks: Uncaptured knowledge requires that people are always available to review the work. When those people exit the company, the knowledge goes with them.
2. It often doesn’t emit a signal: Unless someone explicitly captures it, it stays locked in the minds of the people who have it.


## Why This Problem Has Been so Expensive to Solve


This asymmetry between system activity (processes that are easy to capture) and human knowledge (decisions that are hard to capture) explains why enterprises still spend $600B per year on consultants who interview a few of your employees to tell you how work happens at your own company.


It’s not because consultants have superior technology. It’s because they have humans who talk to humans—and that has been the only interface that works for extracting tacit knowledge. Even though it’s painfully inefficient—months of calendar time, millions in fees, snapshots that are stale by the time they’re delivered—consulting has persisted because there’s been no alternative.


**The gap that remains is capturing human knowledge at scale, continuously, in a form that feeds directly into context graphs, which are critical to building, deploying, and maintaining an agentic enterprise.**


## The Three Modes of Knowledge Capture


At Klarity, we have found that for an AI to reason effectively, it requires three modes working in concert:


### 1. Work Artifacts


Some knowledge is already in the bank, so to speak—in documents, recordings, videos, SOPs. These act as the baseline. But most documentation is outdated and incomplete. Artifacts capture only what someone once decided to document—not the living knowledge that drives current work.


### 2. Observations


The most powerful capture mechanism is watching people work. When someone records themselves performing a task—walking through a process, explaining their screen, narrating decisions—they surface knowledge that wouldn’t emerge any other way. You see the workarounds, the “off-script” judgment calls, and the exceptions that have become routine.


### 3. Interviews


Some knowledge stays hidden even during observation. You might watch someone silently make a decision and have no idea why. This is where AI-led interviewing becomes essential. Not scheduled consultant interviews, but on-demand AI conversations that probe for detail to help people articulate knowledge they didn’t even realize they had.


**No single mode captures everything. You need Interviews for judgment, Observations for process flow, and Artifacts for historical context.**


## What This Looks Like in Practice


At Klarity, we combine three capture modes: an Observation Agent that silently watches how people work, an Interviewer Agent that surfaces reasoning through natural conversation, and artifact ingestion for existing documents, videos, and recordings.


Because all three modes run at scale, without the limitations humans are subject to, you can capture thousands of processes in days. The result is what we call a Process Index—a structured, queryable representation of how work actually gets done, automatically built and continuously updated.


At DoorDash, CAO Gordon Lee captured 3,800+ processes in mere weeks—with ownership, timing, geographic variation, and the why behind complex manual work all surfaced.


## The Unlock: Human-Centered, AI-Enabled Context Graphs


The entire enterprise tech stack has been built around an asymmetry that’s costing companies trillions: capture system data automatically, extract human knowledge manually.


Yes, context graphs change the game—but only if they fully include the dynamic, always-adapting human layer. Agents inherit their reasoning power from humans. If you aren’t capturing that human reasoning continuously and holistically, your context graph stops learning from its most important source.


**That’s a compounding asset and a trillion-dollar opportunity. Smart context graphs that capture how humans think.**
