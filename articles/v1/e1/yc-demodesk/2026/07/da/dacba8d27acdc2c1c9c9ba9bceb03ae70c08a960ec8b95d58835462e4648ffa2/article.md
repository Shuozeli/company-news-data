---
schema_version: "1.0.0"
document_id: "dacba8d27acdc2c1c9c9ba9bceb03ae70c08a960ec8b95d58835462e4648ffa2"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-request-alternative-meeting-summary-templates-in-demodesk"
published_at: "2026-07-13T00:00:00+00:00"
first_seen_at: "2026-07-24T10:56:31.944359+00:00"
fetched_at: "2026-07-28T21:38:32.326002+00:00"
content_hash: "sha256:3cacaefafdbbb5cccac6b3cd9025d4c8d8c71fe61dece69e2f05198fcce2822b"
---

# How to request alternative meeting summary templates in Demodesk

## What and why


Demodesk generates a SPICED summary by default after every recorded call. The Library Catalog contains additional templates — Executive Summary, MEDDIC, and more — you can request manually for any meeting. This guide shows you how to switch templates on a per-meeting basis so the summary matches your qualification methodology, your stakeholder audience, or the deal stage.


## Who this is for


Sales reps, AEs, and account managers who use methodologies other than SPICED, or who need different summary formats for different audiences — an Executive Summary to forward to a VP, a MEDDIC breakdown for pipeline review.


## Prerequisites


- A Demodesk seat with Coaching & AI enabled
- At least one recorded meeting with a completed transcript


## Steps


### 1. Open the meeting in your Meeting Hub


Navigate to **Meeting Hub** in the top nav and click the meeting you want to re-summarize. The default SPICED summary appears in the summary pane on the right side of the transcript view.


### 2. Open the Library Catalog


Click **Library** in the meeting view, then select the **Catalog** tab. All available summary templates live here — Demodesk defaults and any custom templates your admin has published.


### 3. Browse available templates


The Catalog lists every template you have access to. Common options include:


- **SPICED** — default sales methodology summary (Situation, Pain, Impact, Critical Event, Decision)
- **Executive Summary** — condensed overview for leadership forwarding
- **MEDDIC** — Metrics, Economic Buyer, Decision Criteria, Decision Process, Identify Pain, Champion


Each template shows a short description of what it produces and which audience it fits.


### 4. Select a template


Click the template name to open its preview, then click **Request summary** . The AI Assistant runs against the existing transcript using the new template’s prompt structure.


### 5. Wait for the summary to generate


Alternative summaries render in under a minute. The new summary appears alongside the original. Requesting a second template does not remove the SPICED version.


### 6. Copy, share, or sync


Once the alternative summary is ready:


- **Copy** the text directly into an email or Slack
- **Sync to CRM** if your admin has mapped that template to a Salesforce, HubSpot, or Pipedrive field
- **Share the meeting link** with the alternative summary visible


## Tips


- **Request multiple templates for the same call.** An Executive Summary for your VP and a MEDDIC breakdown for your pipeline review can coexist on the same meeting record.
- **Use MEDDIC for late-stage deals.** It surfaces the Economic Buyer and Decision Process fields that late-stage forecasting depends on — fields SPICED does not always emphasize.
- **Use Executive Summary for forward-heavy meetings.** If your champion will forward the recap to a VP or CFO, an Executive Summary saves them the work of skimming a full SPICED write-up.
- **Ask your admin about custom templates.** Demodesk supports custom summary templates built to match your team’s methodology or industry vertical. If none of the defaults fit, request one from your RevOps or Enablement lead.
- **Trigger alternative summaries automatically.** For repeating workflows — for example, “always run MEDDIC on opportunities in Stage 4+” — an AI Crew agent can request the right template based on deal stage or meeting type.


## Related skills and agents


- **AI Assistant** — generates and re-runs summaries against your transcripts
- **AI CRM Concierge** — pushes structured fields from any template (SPICED, MEDDIC, custom) into Salesforce, HubSpot, or Pipedrive
- **AI Crew** — build a custom agent that auto-selects the right summary template based on meeting type, deal stage, or attendee list
- **Marketplace collections** — browse the MEDDIC and Executive playbook collections at[marketplace.demodesk.ai](https://marketplace.demodesk.ai/)
