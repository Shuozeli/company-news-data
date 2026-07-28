---
schema_version: "1.0.0"
document_id: "0a4a7f541c167f68da72a5eecd209af4dba57deeea95763b19ab5c3be2dd0391"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-customize-ai-agent-rules-and-skills-for-deal-health-scoring"
published_at: "2026-07-20T00:00:00+00:00"
first_seen_at: "2026-07-27T16:28:03.851214+00:00"
fetched_at: "2026-07-28T21:21:02.928028+00:00"
content_hash: "sha256:ba46af1a4edb158f263c41727c86e05fa10d2fdf14a9eac3e39a245b8af3bd96"
---

# How to customize AI agent rules and skills for deal health scoring with Demodesk AI Crew

## What and why


Demodesk AI Crew lets you shape how agents score deal health across three layers: rule trees that branch on meeting context, skill editors where you paste your own playbook, and a chat interface where you refine agent behavior in plain English. This guide shows you how to configure all three so your deal health scores reflect your methodology, not a generic template.


## Who this is for


RevOps leads and Heads of Sales who want deal risk scoring aligned to their own qualification framework — MEDDIC, BANT, Command of the Message, or a custom playbook.


## Prerequisites


- Demodesk account on the **Coaching & AI** plan or **Enterprise** (AI Crew is included with every plan, but deal health scoring requires AI Deal Insights, which lives in Coaching & AI).
- Admin or RevOps permissions to edit agents.
- Your written qualification framework or deal health criteria ready to paste.
- At least one CRM connection (Salesforce, HubSpot, or Pipedrive) so scored deals sync back.
- 10–15 recent recorded meetings for testing.


## Steps


### 1. Open the agent you want to customize


Go to **Agents** in the top navigation, then open the **Automations** sub-tab. Select **AI Deal Insights** — the agent responsible for deal health and risk scoring. You'll layer rules, skills, and chat instructions on top of the default configuration.


### 2. Build a rule tree for meeting context


Add branching logic so the agent applies different scoring criteria depending on the meeting type. A typical setup:


- **If** the meeting is **external** (prospect or customer on the call), apply **Rule 1** — score against your full qualification framework (MEDDIC, BANT, etc.).
- **If** the meeting is **internal** (deal review, forecast call), apply **Rule 2** — skip qualification scoring and focus on next-step commitments.


Add branches as needed. Common ones: deal stage (discovery vs. negotiation), deal size (SMB vs. enterprise), and product line.


### 3. Paste your playbook into the skill editor


Open the **Skills** sub-tab under Agents. Create a new skill or edit an existing one. In the skill editor, paste your qualification framework in plain text — for example:


> Score every discovery call on the following MEDDIC dimensions (1–5):
>
>
> - **Metrics:** did the prospect quantify the business impact of solving the problem?
> - **Economic Buyer:** was the economic buyer identified and, ideally, on the call?
> - **Decision Criteria:** are the criteria explicit and written down?
> - ...


The agent uses this text as its scoring rubric. Skills are Markdown-based (` SKILL.md` ), so you can version them, share them across teams, and reuse them across other Demodesk agents.


### 4. Refine agent behavior via chat


Open the agent's chat configuration. This is where you adjust behavior in plain English without touching rules or skills. Example prompts:


- “Only flag a deal as high risk if the champion has been silent for more than 10 days and no next step is scheduled.”
- “When scoring Metrics, weight quantified ROI statements twice as heavily as qualitative pain.”
- “If the prospect mentions a competitor by name, add a note to the deal insight but don't lower the score automatically.”


The chat interface writes these adjustments back into the agent's instructions so they persist across every future call.


### 5. Test on recent recordings


Before rolling out, run the customized agent against 10–15 recent recorded meetings. Compare its scores to what your team would have scored manually. Adjust the skill text or chat prompts wherever the agent is over- or under-scoring.


### 6. Enable auto-scoring and CRM sync


Turn on the automation so AI Deal Insights scores every new external meeting and pushes the risk flag to the relevant deal in your CRM. AI CRM Concierge handles the push with human-in-the-loop approval — no score syncs without a rep review.


### 7. Review weekly and iterate


Every week, review deals where the agent's score and the actual outcome diverged. Update the skill text or chat instructions accordingly. That's how the scoring gets sharper over time.


## Tips


- **Keep skill text short and specific.** A one-page rubric beats a ten-page playbook. The agent applies specific criteria more reliably than abstract ones.
- **Use chat for exceptions, skills for the core rubric.** Skills define the framework. Chat handles edge cases and weightings.
- **Version your skills.** When you change scoring criteria, save the old version. If deal quality drops, you can roll back.
- **Pair with AI Coach scorecards.** Deal health scoring looks across the deal. Call scoring looks at each conversation. Both together give you the full picture.
- **Bring RevOps in early.** The framework belongs to RevOps; the agent executes it. If RevOps doesn't own the rubric, adoption will stall.


## Related skills and agents


- **AI Deal Insights** (Automations) — the agent this guide configures.
- **AI CRM Concierge** — syncs the risk flag to your CRM with approval before push.
- **AI Coach** — scores individual calls against the same framework for coaching.
- **Marketplace: MEDDIC / BANT / Command of the Message skills** — pre-built rubrics you can install and customize.
