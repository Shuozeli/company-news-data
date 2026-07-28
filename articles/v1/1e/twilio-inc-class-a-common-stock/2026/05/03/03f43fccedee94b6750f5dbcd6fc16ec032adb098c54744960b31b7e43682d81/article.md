---
schema_version: "1.0.0"
document_id: "03f43fccedee94b6750f5dbcd6fc16ec032adb098c54744960b31b7e43682d81"
company_key: "twilio-inc-class-a-common-stock"
company: "Twilio Inc. Class A Common Stock"
source_id: "twilio-inc-class-a-common-stock-news-import-801d48e1d714"
canonical_url: "https://www.twilio.com/en-us/blog/developers/introducing-ola-agent-control-communications-channel"
published_at: "2026-05-07T00:00:00+00:00"
first_seen_at: "2026-07-22T17:37:59.927743+00:00"
fetched_at: "2026-07-28T22:12:44.576485+00:00"
content_hash: "sha256:55a4aa895f66f26455d1da06ca391ca985a7506c583f17056e0602fdd5f27f7a"
---

# Introducing Ola: An Agent-Native Communication Channel and Oversight Platform from Twilio Forward

Time to read:


-
-
-
-
-


May 07, 2026


**Written by**[Rikki Singh](https://www.twilio.com/en-us/blog/authors/author.riksingh) Twilion


[Ryan Ferguson](https://www.twilio.com/en-us/blog/authors/author.ryferguson) Twilion


[Ryan Skinner](https://www.twilio.com/en-us/blog/authors/author.ryskinner) Twilion


---


## Introducing Ola: An Agent-Native Communication Channel and Oversight Platform from Twilio Forward


As AI agents grow in capability and autonomy, the gap between what they can do and what a user can effectively trust them to do expands.


Agents on platforms like OpenClaw, NemoClaw, and Claude can send messages, make purchases, and execute tasks across connected services – but there's no standard channel for an agent to reach you when it needs input or approval, no structured way to define what should and shouldn’t require approvals, and no way to intervene when something goes wrong. Existing channels like messaging and email were designed for *human-to-human* communication, forcing a choice between compliance requirements too rigid for autonomous agents or spam protections too weak to stop them.


Today, we're introducing Ola - an agent-native communication channel and oversight platform that puts you in control of your AI agents.


This is a[Twilio Forward](https://twilioforward.com/) initiative, Twilio’s incubation lab where we work on emerging technologies and build for and with the developer community.


## Introducing Ola


Ola sits between you and your AI agents, providing a single surface to communicate with, set boundaries for, and maintain oversight of your agents. Rather than retrofitting channels designed for human communication, Ola is purpose-built for how agents interact with the humans who set them up.


When an agent needs to take action on your behalf, it sends a structured request through Ola describing exactly what it wants to do. Ola evaluates the action against your permission preferences and either auto-approves, routes it to you for authorization, or blocks it. Every approval is cryptographically signed, creating a verifiable record of exactly what was authorized and when.


## What Ola gives you


Ola is designed as an end-to-end agent management system. Communication, permissions, approvals, and activity audits all work together to provide comprehensive oversight of your agents.


**Capability** **What it enables**


**Unified communication channel** Communicate with all of your agents through a single surface. Prompt new tasks, receive status updates, and review authorization requests in one place instead of switching between separate agent interfaces


**Verified identity** Every user and agent on Ola has a verified identity. You always know exactly which agent is acting on your behalf, and can confirm that any agent requesting authorization is genuinely who it claims to be


**Scoped permissions** You define and control what each agent can and can't do. Auto-approve low-risk actions like file reads, require approval for messages or purchases, and block sensitive categories like credential access


**Tiered approvals** The level of verification scales with the risk. A message sent on your behalf might require a tap, while a financial transaction requires Face ID. You control which actions fall into which tier


**Activity feed** You get a complete log of every intent that has passed through Ola. See what an agent requested, what you authorized or denied, and what was auto-approved or blocked. Every record is cryptographically signed


**Killswitch** If an agent behaves unexpectedly, shut it down immediately with a single action - no scrambling to find and kill processes


Ola lets you expand what you delegate to your agents - not by trusting them more, but by having the infrastructure to guide, authorize, and verify what they do.


## How it works


Here's an example. You're out running errands when your monitoring service flags a bug in production for your independent project. Your agent picks it up and starts investigating.


- **The agent reads logs and source code** to identify the issue. These are read actions – auto-approved based on your permissions. Ola sends you a notification so you know what's happening, but no approval is needed and the agent works uninterrupted
- **The agent identifies the root cause, writes a fix, and runs tests.** It opens a PR and requests your approval to merge. Ola then sends a push notification to your phone showing the diff, test results, and CI status. You review the details and approve with Face ID, since you’ve marked production merges as "high-stakes". All without losing your place in line at the coffee shop
- **The agent merges the PR and drafts a Slack message to your team** summarizing what happened and what was fixed. Ola shows you the proposed message content. You approve with a tap, and the agent sends on your behalf
- You put your phone back in your pocket. **The full sequence – what the agent read, what it changed, what it sent, and how each step was authenticated – is in your activity feed when you get home**


Without Ola, this either doesn't happen until you're back at your computer, or your agent makes these decisions on its own with no record of what it did. With Ola, your agent handles the task end-to-end – and you stay in control of the decisions that matter, from wherever you are.


## Trust by design


Ola is built on Twilio's[Agent-to-Human (A2H) protocol](https://www.twilio.com/en-us/blog/products/introducing-a2h-agent-to-human-communication-protocol) , an open standard that defines how agents securely communicate with and request authorization from their human principals. This foundation shapes how Ola handles security and trust:


**Cryptographic evidence.** Every approval generates a signed artifact linking the *intent* to the user's *decision* . This isn't a log generated by the agent - it's an independent, verifiable record produced by Ola.


**Biometric and passkey authentication.** High-stakes approvals use Face ID or device passkeys, *not* passwords or tokens that can be intercepted. The authentication method is tied to the approval tier you've configured, so the verification’s rigor matches the action’s risk.


**Verified identity.** Every user and agent on the platform has a verified identity. Agents authenticate with scoped credentials that are tied to a single user. One agent's credentials can't be used to send requests to a different user's account.


**Permissions and enforcement.** For supported agent platforms like Claude and OpenClaw, Ola provides runtime hooks that validate an agent's tool calls against what was authorized. Beyond supported agent platforms, you can still connect agents but they won’t have tool call monitoring. In these cases, Ola will evaluate every intent against your scopes and will enforce permissions as long as the agent routes the ask through the platform. These advisory permissions work well on their own, though the runtime hooks provide an additional layer of execution-level monitoring and enforcement.


## Get started


Ola launches today as a web app for non-commercial use by users in the United States. Connecting an agent takes seconds and works through the same MCP tool-calling patterns your agent already uses.


We're building Ola in the open with our developer community. Building experiences that don’t have “predecessors” is challenging. We believe that our developer community will provide the best signal to shape where we go next – and what Ola evolves into. So come help us build!


[Sign up for the waitlist](https://olachat.com/waitlist) to get early access, or[learn more at our Ola product page](https://twilioforward.com/projects/ola) .


---


###


### About Twilio Forward


Twilio Forward focuses on Horizon 2 and 3 initiatives focused on driving step-change innovation that empowers builders and unlocks Twilio’s next era of growth. As an incubation lab, we explore bold new ideas, from the most advanced, almost unimaginable technologies to emerging solutions that address today’s real-world challenges. Our mission is to push boundaries, reimagine what’s possible, and build what comes next.


---


**Team**


*Thank you to the broader Twilio Forward and the Platform Engineering Teams for their support: Chris Boran, Jesse Adametz, Mike Safarty, Kolby Allen,* Vladimir *Agushev, and Pranav Nutalapati*


**About the authors**


*Ryan Skinner is a product manager based in New York City. At Twilio, he leads product partnerships on the Emerging Technology and Innovation team, Twilio Forward, with a focus on delivering more effective agentic experiences. Outside of work, Ryan enjoys traveling and exploring different ski areas.*


*Ryan Ferguson is a Senior software engineer manager based in Boulder, Colorado. At Twilio, he leads engineering on Twilio Forward. Outside of work, Ryan enjoys running ultra marathons.*


*Rikki Singh is a product and engineering leader based in Bay Area, California. At Twilio, she leads the Emerging Technology and Innovation group, Twilio Forward. Outside of work, Rikki enjoys hiking and camping with her husband and toddler.*
