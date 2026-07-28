---
schema_version: "1.0.0"
document_id: "afcc5803989e6cd93c85838aa8357dd7fcf94f32e05fbe0ee58d00220e5ecceb"
company_key: "yc-intryc"
company: "Intryc"
source_id: "yc-intryc-news-import-17b79f653bb0"
canonical_url: "https://www.intryc.com/blog/7-flavors-of-broken-qa"
published_at: "2026-05-13T00:00:00+00:00"
first_seen_at: "2026-07-22T00:22:23.516240+00:00"
fetched_at: "2026-07-28T22:00:13.771809+00:00"
content_hash: "sha256:be3200a682a62260bfcde03d20b186df9aeedfaae1d6c75758786fd736930421"
---

# 7 Flavors of Broken QA. Find Yours.

*A taxonomy of the QA status quo, built from conversations with 14 enterprise CX teams.*


Seven out of fourteen enterprise CX teams we interviewed run QA on less than 5% of their conversations. Three of them run it on 0%. One of them runs QA on 100% of conversations and is still flying blind, because the rubric does not measure the thing that matters.


These are not companies that don't care about quality. They are companies whose QA infrastructure has not kept pace with their scale. And here is the part nobody is saying out loud: "broken QA" is not one thing. A team at 0% coverage is not running the same operating mode as a team at 0.5% coverage run by managers. A wound-down program is not the same animal as one that was never built. The fix is different for each.


Below are the seven flavors of broken QA we have observed in the wild, plus an eighth inversion case that proves coverage alone is not the diagnostic. Find yours.


## What is the Absent-QA Status Quo?


The Absent-QA Status Quo is a family of operating states in which a CX team's QA program either does not exist or covers so small a fraction of conversations that it produces no statistically meaningful signal. Across 14 enterprise CX teams spanning travel, marketplace, fintech, and enterprise software, seven distinct flavors of this state were observed. Coverage ranged from 0% to roughly 5%. In each case, the team's own framing of the problem (not the coverage number) is the most reliable diagnostic.


The seven flavors: High-Discipline Blind Spot, Zero, Single-Channel, Self-Built Frankenstein, Wound-Down, Manager-Led, and Post-Acquisition Multi-Brand Zero. The eighth is the inversion: 100% coverage with zero depth.


## Flavor 1: The High-Discipline Blind Spot (Manual at less than 1%)


**Coverage: less than 1%. Segment: travel.**


> "Our process headline would be manual, inefficient, costly, no value add." - QA Director at a travel marketplace


This team did everything right. Weekly calibration sessions. A dedicated QA team. A Salesforce-form rubric built with discipline. And statistically, nothing. The team audits fewer than one in a hundred contacts.


The problem is not process maturity. It is throughput. Manual labor cannot scale beyond a few hundred reviews per week. Discipline without throughput produces strong process hygiene and zero data.


You are running this flavor if you have calibration sessions, a rubric, and a team doing the work, and your coverage has not moved in the last 12 months without adding headcount.


**Buyer takeaway:** The calibration culture is your asset. It compresses onboarding. The only lift is translating the human rubric into criteria a machine can evaluate consistently.


## Flavor 2: Zero (No tool, no scorecard, no process)


**Coverage: 0%. Segment: marketplace.**


> "Currently we have zero QA process, and there's no efforts being placed on measuring quality." - Head of CX at a consumer security marketplace


This team measures ticket volume, handle time, and tickets per agent per hour. Nothing else. The only artifact resembling QA is a Google sheet where the in-house team logs BPO mistakes and a team lead follows up privately. Nothing aggregable. No trend data. No coaching queue.


This flavor is what happens when the company scales faster than its support infrastructure. A new CX leader walks in and finds a team that is measuring everything except quality.


You are running this flavor if your customer finds your quality problems before you do.


**Buyer takeaway:** Do not try to evaluate everything in week one. Start with one workload, one scorecard, and a weekly digest. The starting model is the deliverable.


## Flavor 3: The Single-Channel Gap (Phone-only at 4%)


**Coverage: ~4% of phone calls. 0% of email and cases. Segment: premium B2C.**


> "We average like 4% of interactions right now to 100%." - QA Lead at a premium furniture retailer


This team has a rubric. Phone calls are graded. Email and cases are not. The rubric is tone-based and under-codified. Reviewers fill the gaps with tacit knowledge that is not written down anywhere. When a reviewer leaves, the rubric leaves with them.


This is the most common partial-implementation pattern. QA programs start with the channel that is easiest to audit (voice) and stall before they expand. The configuration lift on email, cases, and chat gets deprioritized every quarter.


You are running this flavor if your rubric only covers one channel, and that rubric was designed to score tone, not process compliance.


**Buyer takeaway:** Channel expansion alone is not enough. The tacit knowledge currently living in your reviewers' heads has to be codified as evaluable criteria first. Otherwise you will scale a rubric that does not actually capture what matters.


## Flavor 4: The Self-Built Frankenstein (Excel plus Retool at 3-4%)


**Coverage: 3-4%. Segment: high-volume fintech.**


> "We use an Excel and a basic Retool form. And that's all. The operation is rustic." - Head of Ops at a LatAm consumer fintech


This team has 20 dedicated analysts. An in-house Excel form. A Retool workflow the engineering team built. And 75,000 conversations per week.


Do the math: 20 analysts running 10 to 15 evaluations each per week against 75,000 weekly conversations produces 3-4% coverage. This is not a coverage problem. It is a manufacturing problem. Doubling the analyst team gets to 6-8%. The math does not close arithmetically. Ever.


You are running this flavor if you built your QA workflow in-house and adding analysts is no longer moving the coverage number in any way you can defend in a budget review.


**Buyer takeaway:** AI evaluation is not an improvement to this workflow. It is a replacement. The unit economics of the entire QA function change once labor stops being the binding constraint.


## Flavor 5: The Wound-Down Program (Had QA. Killed it. Restarting smart.)


**Coverage: 0%, was ~3% before termination. Segment: enterprise SaaS.**


> "We've been using CSAT as a crutch where we can say, hey, this person isn't hitting their productivity targets, but their CSAT is 5.0, so they're rock stars. But if we peek under the hood, actually only 10% of their tickets are getting CSAT responses." - Support Ops Lead at an enterprise SaaS platform


This team ran a manual QA program with dedicated leads and vendor contractors. Peak coverage was around 3%. The program was terminated during a round of headcount reductions in late 2024. Now: "we feel like we're flying blind on 90% of our cases."


Manual QA is expensive, and it is an easy cut when budget pressure hits. What does not survive the cut is the institutional knowledge that the program was producing real signal. So the team restarts with more sophistication. They have already done the post-mortem.


You are running this flavor if you had QA, lost it, and are now restarting with a clear mandate to do it differently.


**Buyer takeaway:** You do not need to be sold on why QA matters. You need clarity on what makes an AI-augmented program structurally different from the manual program you just wound down. The pitch is the difference, not the category.


## Flavor 6: The Rubric Without a Team (Manager-led at 0.5%)


**Coverage: ~0.5%. Segment: developer infrastructure enterprise.**


> "Five per manager per week. We have 14 managers, so that's about 70 tickets, against an entirety of our ticket base of about 14 to 16,000 a month." - Senior Operations Leader at a developer infrastructure company


No dedicated QA team. Managers are the reviewers. Five reviews per manager per week. Fourteen managers. Seventy reviews per week on 14,000 monthly tickets. The rubric is fully designed: soft skills, documentation quality, escalation calibration, sentiment, solution relevance. Every criterion is named. There is just nobody to apply them at scale.


You are running this flavor if you have a complete rubric, organizational buy-in, and managers doing reviews as a secondary task they can't prioritize.


**Buyer takeaway:** The rubric is your accelerant. Onboarding time collapses because the criteria are already codified. The only lift is transferring the rubric to automated evaluation and removing the manager review burden. The 70-to-16,000 jump is the only story you need to tell internally.


## Flavor 7: Living in a World of Anecdote (Post-acquisition multi-brand zero)


**Coverage: 0% across all brands. Segment: enterprise field service software.**


> "We're living in a world of anecdote. I need to get to empirical data." - Head of Support at a multi-brand FSM group


This is a multi-brand group assembled through acquisition. No brand has QA deployed. Operating decisions (staffing levels, quality assessments, performance reviews) are made on informal observation. Anecdotally, volumes are increasing. Anecdotally, agents are overworked. Anecdotally, customers may or may not be satisfied.


M&A-assembled groups do not inherit a shared operating infrastructure. Each acquired brand brings its own support function, its own tooling, its own tribal knowledge. There is no group-level QA layer because there was no group-level support function to begin with.


This flavor looks like Flavor 2 from the outside. It is different. A zero-QA scale-up is building QA for the first time on a single product. A post-acquisition group is deploying QA across multiple brands at once, each with different stacks and different operating maturity. The tool has to be brand-agnostic and workspace-segregable from day one.


You are running this flavor if your operating language is "anecdotally" and your organization is a holding company.


**Buyer takeaway:** Start with the most mature brand. Prove the loop. Expand across the portfolio. The group-level strategy is the output of the first deployment, not the input.


## The Inversion: 100% Coverage, 0% Depth


There is an eighth flavor and it is the one that complicates the entire taxonomy.


A regulated telecom support team runs 100% automated QA coverage on every closed case via an incumbent vendor. Coverage is not their problem. Depth is. The rubric evaluates standard criteria: greeting, empathy, clarity, communication, resolution, sentiment. What it does not evaluate is whether agents followed the documented SOP step by step. In a regulated industry, SOP deviation is not a coaching issue. It is a compliance issue.


The takeaway: broken QA has two axes. Coverage is one. Depth (whether the criteria you score are the criteria that matter) is the other. A program can be broken at 0% coverage or at 100% coverage. The fix is different. The name for the problem is the same: your QA program is not producing the signal you need.


## QA coverage benchmarks across 14 enterprise CX teams (2026)


Team type QA coverage observed Volume base


Travel / mature CX team Less than 1% Manual Salesforce-form audit


Scale-up SaaS / no QA 0% No infrastructure


Premium B2C / phone-only ~4% phone; 0% email and cases ~17,000-18,000 calls/month


High-volume fintech / self-built 3-4% 75,000 conversations/week


Enterprise SaaS / wound-down 0% (was ~3% at peak) ~3,000 cases/week


Developer infra / manager-led ~0.5% ~14,000 tickets/month


Post-acquisition FSM group 0% ~120 agents, growing


Regulated telecom / 100% autoQA 100% (standard rubric); 0% on SOP depth High-volume regulated support


## How to find your flavor (a 7-question diagnostic)


1. **What is your current QA coverage rate?** Pull the last 30 days of completed evaluations divided by total conversations closed. If you cannot produce this number in under 5 minutes, your answer is effectively 0%.
2. **Do you have a QA infrastructure at all?** If no tool, no scorecard, no dedicated reviewer, you are in Flavor 2.
3. **Did you have a program that was terminated?** If you are restarting after a wind-down, you are in Flavor 5.
4. **Who is doing the reviews?** If reviewers are managers with other day jobs, you are in Flavor 6.
5. **How many channels does your QA cover?** If only one channel (usually voice) is being graded, you are in Flavor 3.
6. **Did you build your QA workflow internally?** Excel, Retool, Google Sheets, custom code: Flavor 4.
7. **Are you a multi-brand group assembled through acquisition?** Flavor 7.


If you have 100% coverage but you cannot prove SOP compliance, you are in the inversion case. Coverage is not your problem. Depth is.


## FAQ


**What is a QA coverage benchmark for enterprise CX teams?** Based on conversations with 14 enterprise CX teams in 2026, the median QA coverage rate is under 5%. Teams at the low end run 0%. Teams with manual programs and dedicated reviewers typically reach 3-5%. Teams with manager-led QA without a dedicated function average around 0.5%. A statistically meaningful QA coverage rate (one that produces reliable signal for coaching and operations decisions) requires consistent evaluation across a representative sample of every agent's work. Most teams are not there yet.


**Can manual QA programs scale beyond 5% coverage without additional headcount?** No, not in practice. Manual QA is a labor-bounded function. The clearest demonstration is the Self-Built Frankenstein flavor: 20 dedicated analysts against 75,000 weekly conversations produces 3-4% coverage. Doubling the analyst team gets you to 6-8%. The math does not close arithmetically at the volumes most enterprise CX teams run. AI evaluation lets the team design coverage rather than negotiate it with finance.


**What should I look for in a QA tool evaluation if I'm starting from zero?** Three things. First: will it translate your existing criteria (or help you build them) into rubric language an AI can evaluate? If the answer requires significant vendor customization, your onboarding will be slow. Second: what is the accuracy benchmark on a real sample of your tickets, not a demo sample? Third: how does it handle your channels? If you have an AI chatbot deflecting 50-80% of your volume, the tool needs to evaluate the bot, not just the human agents. Most QA tools only evaluate humans. That is the next coverage gap after you close the first one.


**Why is CSAT not a substitute for QA coverage?** CSAT only captures the subset of customers who respond to a survey, typically 10-15% of total cases. That 10-15% is not representative. Customers with strong feelings (positive or negative) are over-represented. Customers whose interactions were completed without emotional resonance are under-represented. A 5.0 CSAT from 10% of cases tells you about the responders, not about the quality of your team's overall work. QA evaluates every case (or a statistically representative sample) against specific criteria: whether the agent followed process, whether the escalation was handled correctly, whether the documentation was accurate. CSAT cannot produce that signal.


**How do I know which QA flavor my team is in?** Follow the diagnostic above. The two fastest signals are coverage rate and reviewer type. Together they map to six of the seven flavors. The seventh (post-acquisition multi-brand zero) is identified by organizational context, not by the coverage number alone.


## Know your flavor. Then fix the right problem.


The coverage number is the symptom. The flavor is the diagnosis. Getting from 1% to 100% QA coverage is not the same project for every team. A team with a strong calibration culture and a mature rubric has a different lift than a team building from zero. A wound-down program restarts with institutional memory. A manager-led program needs to remove the review burden from people who have other jobs to do. A multi-brand group needs a workspace-segregable starting point.


If you recognize your team in one of these flavors, see what evaluation at full coverage looks like for your specific one. Bring your coverage rate and your reviewer model. The demo shows you what the first 90 days produce and where the math actually closes.


[See the demo.](https://www.intryc.com/#demo-section)
