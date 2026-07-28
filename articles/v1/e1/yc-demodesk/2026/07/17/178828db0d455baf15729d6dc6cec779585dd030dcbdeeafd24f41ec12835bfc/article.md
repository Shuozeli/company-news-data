---
schema_version: "1.0.0"
document_id: "178828db0d455baf15729d6dc6cec779585dd030dcbdeeafd24f41ec12835bfc"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-set-up-ai-powered-deal-insights-and-account-health-alerts-in"
published_at: "2026-07-20T00:00:00+00:00"
first_seen_at: "2026-07-27T16:28:03.851214+00:00"
fetched_at: "2026-07-28T21:21:02.928028+00:00"
content_hash: "sha256:4e0ac0456e192ec08502943d63b088ac067c2689d5555c4bd9431fc59a180bf7"
---

# How to set up AI-powered deal insights and account health alerts in Slack with Demodesk

## What and why


Demodesk posts deal insights and account health updates directly into Slack after every call. Your team sees deal health, risks, and next steps where they already work. This guide covers how to configure Slack routing, use the default Deal Insights skill, and build custom skills for sales and CS workflows using AI Analyst.


Your AEs, CSMs, and managers get the signal in a Slack channel the moment a call ends. No dashboards to chase. No waiting for the weekly pipeline review.


## Who this is for


Sales and CS teams on Salesforce, HubSpot, or Pipedrive who use Slack for daily collaboration and want deal risks and account health coaching pushed to them, not pulled by them.


## Prerequisites


- Demodesk **Coaching & AI** plan (AI Analyst and custom skills are included at this tier)
- Admin access to your Demodesk workspace
- A Slack workspace where you can install apps (or an admin who can approve it)
- At least one Slack channel per use case (e.g.` #deal-insights` ,` #account-health` )
- Meetings being recorded by Demodesk on your channels of choice (video, dialer, mobile)


## Steps


### 1. Connect Slack to Demodesk


In Demodesk, go to **Settings → Integrations** and install the Slack app. Authorize the workspace and grant permission to post to the channels you'll use.


### 2. Create the channels you want to route to


In Slack, create separate channels for each workflow. A common setup:` #deal-insights` for new business,` #account-health` for CS and renewals,` #deal-risks` for anything flagged at-risk. Keep them narrow so signal doesn't drown in noise.


### 3. Open the Skill Library


In Demodesk, go to **Agents → Skills** . This is where the default Deal Insights skill lives and where you'll build custom skills on top of AI Analyst.


### 4. Turn on the default Deal Insights skill


The default skill posts a structured summary after every sales call: deal health, licenses discussed, close probability, and identified risks. Enable it, then assign` #deal-insights` as the target Slack channel in the skill settings.


### 5. Add a custom skill for account health (CS workflow)


Click **Create skill** , select AI Analyst as the underlying agent, and name it something like “Account Health Coaching”. In the prompt, specify what to extract from CS and renewal calls: sentiment shifts, feature requests, expansion signals, churn risks, and a recommended next step for the CSM. Route the output to` #account-health` .


### 6. Add a custom skill for deal risk alerts (sales workflow)


Create a second custom skill focused on red flags only: champion going quiet, procurement stalling, competitor mentions, budget objections, timeline slippage. Route it to` #deal-risks` so managers see only the calls that need intervention, not every summary.


### 7. Configure which calls trigger which skill


In each skill's settings, scope it to the right meeting type or team. Deal Insights runs on AE calls. Account Health runs on CS calls. This keeps` #deal-insights` clean and prevents CS calls from cluttering the sales channel.


### 8. Test with one live call


Record a real call, wait for post-call processing, and confirm the Slack post shows up with the expected fields. Adjust the prompt if the output is too long, too vague, or missing a field your team needs.


### 9. Roll it out to the team


Share the channels in your next standup, explain what each one is for, and pin an example Slack post so people know what to expect. Adoption dies when people don't know why a channel exists.


## Tips


- **Keep prompts specific and structured.** Ask AI Analyst for named sections (Deal health, Risks, Next step) rather than a free-form paragraph. Structured Slack posts get read. Paragraphs get scrolled past.
- **One channel per use case.** Resist sending everything to` #sales-general` . Separate channels for insights, risks, and account health mean each notification has a clear meaning.
- **Tag the deal owner in the Slack post.** In your skill prompt, include an instruction to @mention the AE or CSM tied to the deal so notifications land with the right person, not the whole channel.
- **Review skills monthly.** After 30 days, look at which posts got reactions or replies and which got ignored. Tighten prompts on the ones nobody reads.
- **Use` #deal-risks` for pipeline reviews.** Every risk your team logged that week is already there, with call context one click away. No deck required.


## Related skills and agents


- [AI Analyst](https://demodesk.com/agents/ai-sales-analyst) — the agent powering custom skills, ad-hoc questions across your call data, and the structured Slack summaries.
- [AI CRM Concierge](https://demodesk.com/agents/ai-crm-concierge) — pairs with Slack alerts: the risk lands in Slack, the CRM update lands in Salesforce or HubSpot, both from the same call.
- [AI Coach](https://demodesk.com/agents/ai-coach-a-3-0) — for post-call scorecards, route those to a` #coaching` channel using the same skill setup.
- [Demodesk Marketplace](https://marketplace.demodesk.ai/) — 158+ pre-built skills including account health templates, MEDDIC scorecards, and CS handover workflows.
