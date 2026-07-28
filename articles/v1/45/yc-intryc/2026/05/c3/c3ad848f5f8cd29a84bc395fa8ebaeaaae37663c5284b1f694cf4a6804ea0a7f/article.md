---
schema_version: "1.0.0"
document_id: "c3ad848f5f8cd29a84bc395fa8ebaeaaae37663c5284b1f694cf4a6804ea0a7f"
company_key: "yc-intryc"
company: "Intryc"
source_id: "yc-intryc-news-import-17b79f653bb0"
canonical_url: "https://www.intryc.com/blog/flying-blind-on-90"
published_at: "2026-05-13T00:00:00+00:00"
first_seen_at: "2026-07-22T00:22:23.516240+00:00"
fetched_at: "2026-07-28T21:44:24.455372+00:00"
content_hash: "sha256:60c6739d31032e2880495dd2d7ab656fe8c74157f48b7cfe6d6ffd52f3c2f706"
---

# Flying Blind on 90% of Your Cases

## Why a 98% CSAT Score Is Not a Quality Signal


Your CSAT score is built from roughly 10% of your cases. The customers who respond to a survey are not a random sample. They are the ones who felt strongly enough to fill it out. The other 90% said nothing. You do not know what happened in those conversations. You do not know whether your agents followed the right process, escalated correctly, or told the customer the right thing. You only know that those customers did not complain loudly enough to make themselves count.


That is what flying blind on 90% of your cases means. A 5.0 CSAT from 10% of your cases is not a quality signal. It is a signal about the customers who responded.


## Your CSAT Score Is a Survey of Your Most Opinionated Customers


CSAT is not broken. It is a lagging outcome metric built on a self-selected sample. Used correctly, it tells you whether the customers who chose to respond were satisfied with the experience they reported on. That is a useful thing to know. It is also a narrow thing to know.


At enterprise scale, CSAT response rates typically sit between 5% and 20% of closed cases. The customers most likely to respond are the ones with the strongest reactions: very happy, very angry. The large middle, the quiet majority of your interactions, never shows up in the score. The result is a metric that reflects the people who had an opinion, not the operation that produced the conversations.


CSAT tells you what the customer reported. QA tells you what the agent did. These are not the same question. One is a trailing outcome metric. The other is a leading process metric. If you only have one, you have a proxy, not a system.


The math makes the limit concrete. One enterprise team runs 14,000 tickets per month. Their CSAT score is 98%. Their QA program produces 70 manual reviews per week, all done by managers on top of their other work. That is 0.5% coverage. The number that gets reported up the chain is 98%. The number that reflects what the operation actually evaluated is 0.5%. Both are accurate. Only one is described.


## Three CX Operations Leaders Described the Same Problem, Independently


This is not a vendor argument. Three buyers at three different mature enterprise CX operations described the same structural problem in their own words within ninety days of each other. None of them were prompted. Each had diagnosed the ceiling before the conversation started.


The first, a senior CX Operations leader at a global enterprise B2B SaaS company, described his team's quality program this way: "We've been using CSAT as a crutch, where we can say, this person isn't hitting their productivity targets, but their CSAT is 5.0, so they're rock stars. But if we peek under the hood, actually only 10% of their tickets are getting CSAT responses." His team had a 5.0 CSAT score. They also had a manual QA program that had been wound down. His framing: "We feel like we're flying blind on 90% of our cases right now. And the 10% of the data we get is telling us we're doing great, but we'd like to validate if that's the case."


The second, a Support Operations lead at a large observability platform, described a 98% CSAT score against 0.5% QA coverage. Fourteen managers reviewing five tickets a week each, against a base of 14,000 tickets a month. His language: "Our currency set is CSAT at 98%. When we look at just the satisfaction scores, we're not really getting a lot to continue with operational excellence." A score, not a lever.


The third, a CX leader at a US cloud communications company, ran something different. He had 100% autoQA coverage on standard criteria: greeting, empathy, clarity, resolution. CSAT 94-95%. On paper, the most instrumented of the three. His problem was depth, not coverage: "Correlating CSAT or QA scores to satisfaction, we haven't connected those as a way to feed into that other KPI." His standard QA evaluated quality of response. It did not evaluate SOP adherence. Compliance-required steps inside the conversation were invisible to both the survey and the scorecard.


Three teams. Three operating states. Same blind spot.


Operating state CSAT score QA coverage The gap


Wound-down QA program 5.0 / 5.0 (10% response rate) 0% (program shut down) Flying blind on 90% of cases


Manager-led manual QA 98% 0.5% (70 reviews/week on 14,000 tickets/month) Math kills the signal


100% autoQA on standard criteria 94-95% 100% (standard criteria only) Depth gap: SOP adherence invisible


All three teams had strong CSAT scores. All three had described their current state as inadequate. Not because they had done something wrong. Because they had correctly diagnosed what CSAT cannot measure.


## CSAT Is a Lagging Outcome Metric. It Is Not a Process Compliance Signal.


CSAT and QA answer different questions. Conflating them is the source of the blind spot.


**CSAT** is a post-interaction survey response that reflects the customer's reported satisfaction. It is a lagging outcome metric. It tells you how the customer felt after the interaction was over. It does not tell you which steps the agent took, whether the agent followed the correct process, whether the resolution was correct, or whether the handling was compliant with your SOPs.


**QA** is a systematic evaluation of agent conversations against a defined scorecard. It evaluates process adherence, response quality, resolution accuracy, and in more advanced implementations, SOP compliance and soft criteria such as tone, empathy, and escalation judgment. QA is a leading process metric when deployed at meaningful coverage.


A high CSAT score does not confirm any of the following:


1. Agents followed the right process.
2. Agents gave accurate product information.
3. Escalation criteria were applied correctly.
4. SOPs were followed in the right sequence.
5. Compliance-required steps were completed.


For regulated industries, telecom, fintech, healthcare, the stakes on item 5 extend past service quality into regulatory exposure. A 98% CSAT score and a missed compliance step can coexist in the same conversation. The customer was happy. The auditor will not be.


> "We're looking for problems that aren't coming up in a large scale situation, which is why we can only do about five per manager per week."


This is the core of the problem. Manual QA at low coverage surfaces anecdote. You find individual problems, not systemic ones. A 98% CSAT score can coexist with a systemic SOP failure that has never shown up in a survey response, because the customers affected by the failure either did not respond, did not notice, or did not connect it to their satisfaction rating.


## From CSAT as a Proxy to QA as a System


The operating model that closes the gap is not complicated. It is just different from the one most teams inherited.


QA coverage moves from anecdote to signal when the sample is large enough to surface patterns. The goal is not necessarily 100%. The goal is enough coverage to distinguish a systemic problem from a one-off. Five reviews per manager per week does not get there. Five hundred per agent per month does.


Scorecards evaluate the process, not just the outcome. What did the agent do, in what order, against what criteria? Hard criteria handle resolution correctness. Soft criteria handle empathy, communication, and escalation judgment. Both matter. AI-assisted evaluation makes both gradable at scale.


CSAT and QA are used together, not as substitutes. CSAT validates the direction. QA explains why the direction is what it is. When CSAT moves, QA tells you which process change moved it.


The coverage math has changed. One enterprise team described their goal as moving from 70 manual reviews per week to evaluating every conversation, human-handled and AI-handled, against the scorecard their team defined. The capacity ceiling is no longer the headcount of your QA reviewers. The question moves from "how many cases can my team review per week?" to "what criteria do I want to evaluate, and at what coverage?" Intryc evaluates every conversation, human and AI agent, against the scorecard you define.


## Why We Call It the CSAT Mirage


The pattern has a name. The CSAT Mirage is the operational condition in which a mature CX team posts a high CSAT score, typically 90-98%, while running QA on less than 5% of their actual case volume. The score creates confidence. The coverage means the source of that confidence is structurally limited.


The mirage is not a failure of the team. It is a natural consequence of using a lagging outcome survey as the primary quality instrument. The team is doing what the metric allows. The metric has a ceiling.


The shift happens when a CX Operations leader asks the question CSAT cannot answer: what is happening in the 90% of cases that never surfaced a survey response? That question is the beginning of a QA program.


Run the diagnostic on your own operation:


1. What is your current CSAT response rate? Not your score. Your response rate. The percentage of closed cases that receive a survey response.
2. What is your current QA coverage rate? The percentage of cases reviewed against a defined scorecard each week.
3. If your QA coverage is below 5% of your case volume, you have a CSAT Mirage. A high score built on a small, self-selected sample.
4. If you have no formal QA program running, your CSAT score is the only quality signal you have, and it covers less than one in five of your conversations.


## Definitions


**What is the CSAT Mirage?** The CSAT Mirage is the operational condition in which an enterprise CX team reports a high customer satisfaction score (typically 90-98%) while evaluating fewer than 5% of their actual conversation volume through formal quality assurance. Because CSAT is a self-selected survey metric, customers must choose to respond, high scores can reflect the sentiment of a small, motivated minority rather than the performance of the full operation. The result is false confidence: the team believes quality is high because the metric says so, without visibility into what is happening in the majority of interactions that never generated a response.


**What is QA coverage rate?** QA coverage rate is the percentage of agent conversations reviewed against a formal quality scorecard in a given period. A coverage rate of 1-5% means one in twenty to one in one hundred conversations is evaluated. At this level, QA produces anecdote, individual case feedback, rather than systemic signal. Meaningful QA coverage starts at a statistically significant sample across each agent, team, and channel.


**What is responder bias in CSAT?** Responder bias in CSAT is the distortion that occurs when survey responses come disproportionately from customers with strong opinions, either very satisfied or very dissatisfied, leaving the large neutral or mildly satisfied majority unrepresented. In enterprise CX contexts, CSAT response rates typically range from 5-20% of closed cases. The customers who respond are not a random sample. The resulting score reflects the responders' experience, not the operation's full performance.


## How to Audit Your CSAT Mirage


1. Pull your CSAT response rate for the past 90 days. The percentage of closed cases that received a survey response.
2. Pull your QA coverage rate for the same period. Cases reviewed divided by total cases closed.
3. If your CSAT response rate is below 20%, your score reflects less than one in five interactions.
4. If your QA coverage rate is below 5%, your formal process evaluation covers less than one in twenty interactions.
5. Identify the gap. Which channels, which agent groups, and which case types have zero QA coverage?
6. Define the questions CSAT cannot answer for you. Did your agents follow the correct SOP? Did they give accurate product information? Did they escalate correctly?
7. Map those questions to a scorecard. That scorecard is the start of your QA program.


## FAQ


**Is high CSAT a sign that QA is not needed?** No. CSAT and QA measure different things. CSAT measures whether the customer reported satisfaction. QA measures whether the agent followed the correct process, gave accurate information, and met the operational criteria your team has defined. A team can have a 98% CSAT score and simultaneously have systemic SOP failures that never surface in a survey response. Both metrics are useful. They are not substitutes for each other.


**What is a healthy QA coverage rate?** There is no universal number, but QA programs that evaluate fewer than 5% of interactions typically produce anecdote rather than systemic signal. Enterprise teams that have moved to AI-assisted QA evaluation typically aim to evaluate every conversation, or a statistically significant sample across each agent and channel. The goal is coverage that lets you identify patterns, not just individual outlier cases.


**What does it mean to evaluate an AI agent's conversations?** Most QA tools were designed to evaluate human agents. If you have an AI chatbot handling 50-80% of your interaction volume, a common configuration in 2025-2026 enterprise CX stacks, and your QA tool only evaluates the remaining human-handled conversations, you have a blind spot the size of your AI deflection rate. AI-assisted QA tools like Intryc evaluate both human and AI agent conversations against the same scorecard.


**How do you improve QA coverage without adding headcount?** Manual QA scales with headcount. At 5 reviews per manager per week, 14 managers produce 70 reviews per week, 0.5% coverage on a 14,000-ticket-per-month base. AI-assisted QA evaluation removes the headcount ceiling. Coverage becomes a configuration decision, not a staffing decision.


**My CSAT is 5.0, why would I need QA?** A 5.0 CSAT from the 10% of cases that received a response tells you the responding customers were satisfied. It does not tell you what happened in the other 90%. It does not tell you whether agents followed the right process, gave accurate information, or escalated correctly. CSAT is a signal about customer sentiment. QA is a signal about operational performance. You need both to know if your team is actually doing it right, not just to the satisfaction of the customers who bothered to respond.


## Run the Diagnostic on Your Own Operation


Pull your CSAT response rate. Pull your QA coverage rate. If your QA coverage is below 5% and your CSAT response rate is below 20%, you have a CSAT Mirage. We built Intryc specifically for teams in this position.


98% CSAT and 0.5% QA coverage are the same number from two angles. One tells you about the customers who responded. The other tells you about the agents you evaluated. Neither tells you about the 90% in between.


That is the gap. See what closes it - every conversation evaluated, human and AI, against the scorecard you define.


[See the demo.](https://www.intryc.com/#demo-section)
