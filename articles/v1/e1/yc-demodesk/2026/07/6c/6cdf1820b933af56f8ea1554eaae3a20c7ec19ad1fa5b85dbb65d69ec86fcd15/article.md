---
schema_version: "1.0.0"
document_id: "6cdf1820b933af56f8ea1554eaae3a20c7ec19ad1fa5b85dbb65d69ec86fcd15"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-set-up-slack-notifications-for-ai-agent-outputs-in-demodesk"
published_at: "2026-07-13T00:00:00+00:00"
first_seen_at: "2026-07-24T10:56:31.944359+00:00"
fetched_at: "2026-07-28T21:38:32.326002+00:00"
content_hash: "sha256:ca3ebf023d457a51d58f103e9270e2e1217f73e43a23a66bc4601affc641e70f"
---

# How to set up Slack notifications for AI agent outputs in Demodesk

## What and why


Demodesk sends AI agent outputs directly into Slack—call summaries, Deal Health Scores, coaching scores, deal risk alerts—routed by meeting type. Set it up once in agent settings using **Add Notification** , and every relevant call posts to the right channel automatically. No more digging through the app to find what happened on a call. No more reps forgetting to share outcomes with the team.


## Who this is for


Sales managers, RevOps, and CS leaders who want AI agent outputs in Slack where their teams already work, without asking reps to copy-paste anything.


## Prerequisites


- A Demodesk workspace on the Coaching & AI plan or Enterprise
- Admin access to Demodesk agent settings
- A connected Slack workspace (via **Settings → Integrations → Slack** )
- Meeting types already configured in Demodesk (Discovery, Demo, Closing, QBR, etc.)
- Slack channels created for each destination (e.g.` #deals-at-risk` ,` #new-discoveries` ,` #cs-renewals` )


## Steps


### 1. Connect Slack to Demodesk


Open **Settings → Integrations** and connect Slack. Authorize Demodesk to post to public and private channels. If your workspace already has Slack connected, skip to step 2.


### 2. Open the agent you want to configure


Go to **Agents → Automations** in the top nav. Pick the agent whose output you want in Slack:


- **AI Assistant** for call summaries and follow-ups
- **AI Coach** for scorecards and coaching scores
- **AI CRM Concierge** for CRM update previews
- **Deal Insights** for Deal Health Scores and risk alerts


Click into the agent to open its settings.


### 3. Click “Add Notification”


Inside the agent settings, find the **Notifications** section and click **Add Notification** . This is where you define one routing rule: which meeting type triggers it, what content gets posted, and which Slack channel receives it.


### 4. Select the meeting type


Choose the meeting type this rule applies to—Discovery, Demo, Closing, QBR, Renewal, or a custom type your team has created. One rule per meeting type means discoveries go to` #new-discoveries` while closings go to` #deals-closing-this-week` .


To route the same output to multiple channels, add multiple notifications. To route multiple meeting types to the same channel, add multiple notifications or use “All meeting types”.


### 5. Pick the output to send


Select what the agent pushes to Slack. Options depend on the agent:


- **AI Assistant:** call summary, action items, follow-up email draft, recording link
- **AI Coach:** scorecard results, overall score, coaching flags
- **AI CRM Concierge:** proposed CRM updates (preview before push)
- **Deal Insights:** Deal Health Score, deal risks, competitor mentions, next steps


One output per notification rule. To get both a summary and a Deal Health Score in the same channel, add two rules.


### 6. Choose the Slack channel


Search for the channel in the dropdown. Public channels appear by default. For private channels, invite the Demodesk Slack app to the channel first (` /invite @Demodesk` inside Slack).


Send Deal Health Scores below a certain threshold to` #deals-at-risk` and everything else to` #deals-general` . That keeps the signal-to-noise ratio right for managers.


### 7. Save and test


Save the notification. Run a test by joining or uploading a recording tagged with the matching meeting type. The output should appear in Slack within a few minutes of the call ending. If it doesn't, check three things: the meeting type on the call matches the rule, the Slack app is in the channel, and the agent is enabled for that meeting type.


### 8. Repeat for other meeting types and agents


Add one notification rule per meeting type × output × channel combination. Most teams end up with 5–10 rules across all four agents. Once configured, it runs on autopilot.


## Tips


- **Route by outcome, not just meeting type.** Send only Deal Health Scores under 60 to` #deals-at-risk` —managers get a curated feed instead of every call.
- **Use a dedicated` #demodesk-firehose` channel** for the first two weeks to see everything, then split into targeted channels once you see the volume.
- **Tag the account owner** in the Slack message so ownership is clear.
- **Combine with AI CRM Concierge preview-before-push.** Reps get the CRM update proposal in Slack, approve or edit it, and only then does it sync to Salesforce or HubSpot.
- **Give CS its own routing.** Renewal and QBR calls should post to` #cs-signals` , not to sales channels—different teams, different signals.


## Related skills and agents


- [AI Assistant](https://demodesk.com/agents/ai-sales-assistant) —call summaries and follow-ups
- [AI Coach](https://demodesk.com/agents/ai-coach-a-3-0) —scorecards and coaching scores
- [AI CRM Concierge](https://demodesk.com/agents/ai-crm-concierge) —CRM updates with human-in-the-loop approval
- [AI Sales Analyst](https://demodesk.com/agents/ai-sales-analyst) —deal risks and pipeline insights
- [Demodesk Marketplace](https://marketplace.demodesk.ai/) —158+ skills for sales workflows
