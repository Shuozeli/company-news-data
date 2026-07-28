---
schema_version: "1.0.0"
document_id: "64f0b6c4a18a9df3e78f5c00c8c5329600d59624b25622d5f0e578a71911087b"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-create-custom-ai-agents-in-demodesks-skill-library-using-the"
published_at: "2026-07-14T00:00:00+00:00"
first_seen_at: "2026-07-27T16:28:03.851214+00:00"
fetched_at: "2026-07-28T21:22:05.726331+00:00"
content_hash: "sha256:44ea7ee6dc2ff2a890057ef6cef3dfbf757e43ca79201f0df98221b600079543"
---

# How to create custom AI agents in Demodesk's Skill Library using the AI Analyst

## What and why


Demodesk's Skill Library lets you build custom AI agents that run on your sales conversations without writing code. Chat with the AI Analyst, describe what you want the agent to do — score account health, flag churn signals, coach on discovery quality — and it builds the prompt and routing for you. This guide walks you through creating a custom skill end-to-end, using an Account Health Coach as the worked example.


## Who this is for


RevOps leaders, sales managers, and CS leads who want AI agents tailored to their playbook, not generic templates.


## Prerequisites


- A Demodesk account with access to the Skill Library.
- At least one recorded conversation in your workspace so the agent has something to run on
- A Slack workspace connected to Demodesk if you want alerts routed there (optional but recommended)
- A clear idea of what you want the agent to do — one sentence is enough, the AI Analyst refines it with you


## Steps


### 1. Open the Skill Library


Navigate to the Skill Library. This is where all your skills live: the pre-built ones and any custom skills your team has already created.


### 2. Click ‘New Skill’


Click the **New Skill** button. Two paths appear: build from scratch or use **Create with AI** . Pick **Create with AI** — it drops you into a chat with the AI Analyst that handles most of the setup.


### 3. Describe the skill to the AI Analyst


Tell the AI Analyst what you want the agent to do. For an Account Health Coach, try:


> “Score every customer conversation on account health signals — engagement level, product adoption mentions, churn risk language, expansion openings. Flag any call where risk signals appear.”


The AI Analyst will ask follow-up questions to sharpen the definition: which conversations should it run on (all CS calls, only QBRs, specific accounts), which signals matter most, what score or output format you want. Answer in plain language. You're describing the job, not writing a prompt.


### 4. Review and configure the prompt parameters


Once the AI Analyst has enough context, it generates the underlying prompt and shows you the parameters. Review:


- **Trigger:** when the skill runs (after every meeting, on demand, scheduled)
- **Scope:** which conversations it applies to (all, filtered by tag, filtered by deal or account)
- **Output format:** score, summary, structured fields, or free text
- **Custom fields:** specific data points you want extracted (e.g., “mentioned competitor”, “champion still engaged”)


Edit any of these directly.


### 5. Set up Slack routing


Decide where the output goes. Two main options in the routing section:


- **Direct message:** send results to a specific person (the account owner, the CS lead, the AE)
- **Channel:** post into a Slack channel (e.g.,` #account-health` ,` #deal-risks` ,` #cs-alerts` )


For an Account Health Coach, a channel like` #customer-health` works well — the whole CS team sees the signals. For deal-risk agents, direct messages to the deal owner drive faster action.


### 6. Test on a past conversation


Before going live, run the skill on one or two recent conversations you already know well. Check that the output matches what you'd expect a human reviewer to flag. If it misses signals or over-flags, return to step 3 and refine the description with the AI Analyst.


### 7. Save and activate


Save the skill and switch it on. It runs on every conversation that matches your scope, and results land wherever you routed them.


## Tips


- **Start narrow, then broaden.** A skill that scores one specific thing well beats one that tries to score everything. Build an Account Health Coach first, then a separate Churn Risk Detector — not one giant agent.
- **Use your team's language, not generic sales terms.** If your CS team calls it “expansion signal”, say that. The AI Analyst will match your vocabulary in the output.
- **Route by urgency, not by role.** High-risk signals go direct-message. Trend data goes to a channel. Weekly rollups go to a summary channel or email.
- **Iterate weekly for the first month.** Review the skill's output every week, flag false positives and misses back to the AI Analyst, and let it refine the prompt.
- **Reuse across teams.** A skill built for CS often works for the AE team on renewal and expansion conversations with small tweaks. Duplicate and adjust rather than rebuilding.


## Related skills and agents


- **AI Coach** — real-time scoring of sales calls against your methodology (MEDDIC, BANT, custom scorecards)
- **AI CRM Concierge** — updates Salesforce, HubSpot, or Pipedrive fields based on what the skill detects
- **AI Deal Insights** — pipeline-wide risk detection across every conversation
- Marketplace: browse 158+ pre-built skills at[marketplace.demodesk.ai](https://marketplace.demodesk.ai/) for CS, discovery, objection handling, and account management
