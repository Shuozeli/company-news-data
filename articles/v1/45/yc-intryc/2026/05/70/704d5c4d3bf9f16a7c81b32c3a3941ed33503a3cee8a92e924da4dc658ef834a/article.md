---
schema_version: "1.0.0"
document_id: "704d5c4d3bf9f16a7c81b32c3a3941ed33503a3cee8a92e924da4dc658ef834a"
company_key: "yc-intryc"
company: "Intryc"
source_id: "yc-intryc-news-import-17b79f653bb0"
canonical_url: "https://www.intryc.com/blog/qa-tool-sees-5-percent"
published_at: "2026-05-13T00:00:00+00:00"
first_seen_at: "2026-07-22T00:22:23.516240+00:00"
fetched_at: "2026-07-28T21:44:24.455372+00:00"
content_hash: "sha256:fa080a8f1d9899df88c626cfac12ab729e22fc7bf6faba38a7d36f30fe2bd78c"
---

# Your QA tool sees 5%. Your AI chatbot handles 70%.

We interviewed 14 enterprise CX teams in 2026. Seven of them had an AI chatbot handling 50 to 80 percent of their support volume. None of them were evaluating it. Every one of them knew about the gap.


This is the structural blind spot most modern QA programs are running on right now. The AI agent went into the stack first. The QA program stayed pointed at the humans. The majority of support volume is accumulating without a single evaluation.


This piece names the pattern, shows the deflection numbers customers actually disclose on calls, walks through the seven ways the blind spot shows up, and gives you five steps and five buying criteria to close it.


## What is AI chatbot QA?


**AI chatbot QA is the practice of evaluating AI-generated customer service conversations against quality criteria, the same way human-agent conversations are evaluated in traditional QA programs.** It covers accuracy, adherence to SOPs, resolution quality, tone, and handoff behavior. Most legacy QA tools were built before AI chatbots were standard in support stacks. They evaluate human-agent conversations only. AI chatbot QA closes that gap by treating the AI agent as a unit of work to evaluate, not an upstream filter that routes the "real" work to humans.


## The inversion nobody planned for


QA programs were designed for human agents. AI chatbots entered the stack across 2023 to 2025 at most of the teams we talked to. The deflection layer landed before the QA function extended to cover it.


The result is an operational asymmetry we call AI-First, QA-Last. QA programs still point at humans. The AI deflection layer sits outside the QA boundary. This is not a failure of intent. Nobody decided not to evaluate the AI. The QA tooling simply did not cover it, and the QA boundary did not move.


> The buyer does not ask whether the QA tool can evaluate AI agents. They tell you, often as a closing-the-loop ask: "And of course we want to QA the AI too."


That ask is widely observed. Seven out of fourteen enterprise CX teams we interviewed in 2026 have an AI chatbot deployed. Zero evaluate it. The pattern is consistent across marketplace, fintech, and enterprise segments.


## What the numbers look like on your stack


Here are the deflection rates buyers disclosed on calls, anonymized by segment.


### AI deflection rates observed in 2026 enterprise CX teams


Company type AI chatbot vendor Deflection rate Currently evaluated by QA tool


Consumer cybersecurity SaaS Custom AI agent ~80% 0%


Premium B2C retail (voice) 11 Labs voice bot via Twilio ~50% 0%


LatAm consumer fintech Intercom AI ~55% 0%


Enterprise B2B SaaS Forthought ~70% 0%


US telecom (CPaaS) Intercom FIN "really good engagement" (not numerically disclosed) 0%


Pre-IPO B2B fintech Ada "contained chats" (not numerically disclosed) 0%


Source: Intryc customer voice research, 2026. N=14 enterprise CX teams interviewed.


Run the arithmetic against your own stack. If your chatbot deflects 70 percent of volume, your QA program is sampling from the 30 percent residual. At a consumer SaaS company we interviewed, the AI agent handles about 80 percent of roughly 2,000 tickets a day. The human team sees about 400 tickets a day. If QA covers 5 percent of the human slice, that is roughly 20 tickets evaluated out of 2,000 total. That is 1 percent of the real volume.


At a B2B SaaS platform we interviewed, the bundled chatbot handles 70 percent of the 4 percent of help-center traffic that creates a case. The human team QA'd 3 percent at peak before the program was wound down. The AI layer was never evaluated.


> AI deflection without AI evaluation is a blind spot the size of your AI deflection rate.


## The seven ways this shows up


This is not one pattern. It is seven distinct situations buyers arrive in. You will probably recognize one of them as your own.


**1. Deployed and dominant.** The AI handles 70 to 80 percent of volume. The humans see the residual. QA evaluates the residual only. Observed at a consumer cybersecurity SaaS where the AI agent processes ~80 percent of ~2,000 daily tickets.


**2. Voice AI with audio and transcript stitching.** The AI is a voice bot. Transcripts have to be stitched to downstream human cases when the conversation hands off. QA tools that handle text-only have a format problem before they have a coverage problem. Observed at a premium B2C retail brand running 11 Labs voice via Twilio at ~17,000 calls a month.


**3. AI deployed through a platform marketplace.** The chatbot came in through an integration marketplace alongside the helpdesk. The QA tool did not come in the same way. Coverage gap by default. Observed at a LatAm consumer fintech running their chatbot inside Intercom at ~55 percent deflection against 75,000 conversations a week.


**4. Bundled QA module from the chatbot vendor.** The chatbot vendor offers a QA module. The buyer ran the POV. The module covered the AI conversations but with limited rubric control, no self-serve configuration, and no SOP-adherence evaluation. The buyer in an active evaluation described the bundled module as lacking self-serve configuration capability. The bundled-QA path is real, and so is its ceiling.


**5. AI migration in flight.** The chatbot is not yet deployed. The buyer is mid-migration. They are already factoring AI deflection into their headcount model. QA decisions get deferred until the AI settles. Coverage gap before day one.


**6. High-touch identity tension.** The AI is deployed and engagement is strong. The brand competes on high-touch service. The buyer's fear is not about the AI failing. It is about the AI diluting the service identity. QA of the AI is the mechanism that keeps the brand promise measurable. Observed at a regulated US telecom running Intercom FIN where the buyer flagged that deflection cannot erode the "high-touch experience" differentiator.


**7. RLHF-style feedback loop.** The buyer is not just asking for evaluation of the AI's past conversations. They want a feedback loop that makes the AI better over time. "This was wrong. Let's critique that so it becomes more accurate." This is closer to model tuning than traditional QA. Observed at a pre-IPO B2B fintech running Ada at scale across ~20,000 cases a month.


Each of these is a different shape of the same gap. The QA boundary stops at the human agents. The AI agent sits outside it.


## How to close the gap


You can start on this without buying anything. Here are five steps that work in order.


1.


**Identify what your AI chatbot is evaluated on today.** For most teams the answer is "nothing," or "vendor-native engagement metrics only." Write down what is currently in scope and what is not. Make the gap explicit on paper.


2.


**Define evaluation criteria that mirror your human-agent scorecard.** Accuracy, resolution, tone, SOP adherence, handoff quality. If your humans are scored on whether they followed the refund SOP, your AI should be scored on the same SOP. One scorecard, two agent types.


3.


**Map the AI-to-human handoff.** The core configuration question, raised on multiple calls in our research, is this: do you evaluate the AI bot in isolation, or stitch the AI plus human handoff into a single end-to-end interaction? Answer this before you evaluate any QA tool. It determines what shape of data the tool needs to ingest.


4.


**Set sampling thresholds against deflection, not against random tickets.** At 70 percent deflection, you have more AI volume than human volume. Sample by deflection outcome. The conversations that ended in the AI are a distinct population from the conversations that handed off, and both are distinct from the ones humans handled end-to-end.


5.


**Establish a feedback loop.** Evaluation findings should route back to whoever manages the AI chatbot's configuration or training. The most sophisticated version of this, observed in a pre-IPO fintech we interviewed, is an evaluation-and-correction loop that routes QA findings back to the chatbot's configuration team. Evaluation becomes the mechanism for improving the AI over time, not just auditing it.


## What to look for in a QA tool that actually covers this


If you are evaluating QA vendors, here are the five questions that separate tools that close the gap from tools that ignore it. Every criterion below traces to a specific buyer quote in our research corpus.


1. Can the tool ingest AI chatbot conversation transcripts, not just human-agent tickets?
2. Can it evaluate AI-generated responses against the same scorecard used for human agents, without a separate workflow?
3. Can you evaluate the AI-to-human handoff as a single stitched interaction when you need to?
4. Is rubric configuration self-serve, or does it require the vendor to manage evaluation parameters on the backend?
5. Does it support SOP-adherence evaluation, not just tone and empathy scoring?


A QA tool that answers no to any of these is evaluating the human slice of a stack where the AI is doing most of the work.


## Frequently asked questions


**Q: Can QA tools evaluate AI chatbot conversations?**


A: Most legacy QA tools cannot. They were designed for human-agent conversations and do not ingest chatbot transcript data or evaluate AI-generated responses against quality criteria. A small number of newer QA platforms, including Intryc, evaluate both human agents and AI agents against the same scorecard.


**Q: What is the average AI chatbot deflection rate in enterprise support?**


A: Based on Intryc's 2026 research across 14 enterprise CX teams, AI chatbot deflection rates range from 50 to 80 percent of total support volume. Teams using Forthought, Ada, Intercom FIN, and custom AI agents all disclosed rates inside that range.


**Q: Does Forthought have a QA module?**


A: Yes. Forthought offers a bundled QA module. Based on buyer feedback from an active evaluation we observed, the module was described as a little bare bones and lacking self-serve configuration capability at the time of the assessment. Buyers who need rubric customization, Salesforce attribute evaluation, or SOP-adherence scoring typically evaluate dedicated QA platforms alongside or instead of bundled modules.


**Q: How do you evaluate Ada or Intercom FIN with a QA tool?**


A: The core requirement is that the QA tool can ingest AI chatbot conversation logs as a transcript and apply the same evaluation criteria used for human agents. Some teams also want a feedback loop that routes evaluation findings back to the chatbot vendor or configuration team. Intryc supports evaluation of AI-generated conversations alongside human-agent conversations in the same platform.


## Close the loop


If your support stack includes an AI chatbot and your QA tool only evaluates humans, you have a specific gap. We built Intryc to close it. See how it evaluates the bot, not just the humans.


[See the demo.](https://www.intryc.com/#demo-section)


*Based on Intryc customer research, 2026. Fourteen enterprise CX teams interviewed across marketplace, fintech, and enterprise segments. All companies anonymized unless explicitly approved.*
