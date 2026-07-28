---
schema_version: "1.0.0"
document_id: "1c45083735b73d8ad2599676a91d8f5e079bb1ee474ed287e49df32931d5f214"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-set-up-demodesk-with-microsoft-outlook-teams-and-hubspot-for"
published_at: "2026-07-06T00:00:00+00:00"
first_seen_at: "2026-07-24T10:56:31.944359+00:00"
fetched_at: "2026-07-28T21:38:32.326002+00:00"
content_hash: "sha256:eda58bee2c6478a46dc54d8d978987489c6de8139ef7a9d739d348056157d0d0"
---

# How to set up Demodesk with Microsoft Outlook, Teams, and HubSpot for a German SaaS sales team

## What and why


This guide walks you through setting up Demodesk for a German SaaS sales team running Microsoft Outlook, Teams, and HubSpot. You'll cover admin approval, team roles, recording preferences, HubSpot sync, and automation rules that apply the SPICED framework to every external meeting — so reps stop taking manual notes and HubSpot fills itself.


## Who this is for


Sales operations leads and admins at 20–200 person SaaS companies in the DACH region running Microsoft 365 and HubSpot, who want Demodesk live for the whole team in under an hour.


## Prerequisites


- Microsoft 365 admin account with permission to approve third-party apps
- HubSpot admin account (Enterprise or Sales Hub Pro recommended)
- List of team member email addresses grouped by function (Sales, Partner Management, CS)
- Internal agreement on who should see whose recordings (see Step 2)
- Works council or DPO sign-off on recording and consent workflow (recommended before rollout)


## Steps


### 1. Approve Demodesk in Microsoft Outlook (admin only)


Sign in to Demodesk with a Microsoft 365 admin account and approve the app permissions when prompted. One-time step — once approved, every user in your tenant can connect their calendar without separate IT approval.


> **Tip:** You can approve with a dedicated admin account and still invite yourself as a regular user afterward. Both accounts will show up separately in Demodesk.


### 2. Add team members and assign role-based access


Go to **Team members** in the left sidebar and invite users by email address. Demodesk has three permission levels:


- **User** — sees only their own recordings
- **Manager** — sees their team's recordings
- **Administrator** — sees all recordings across the company


For most German SaaS teams: start everyone as **User** , then promote Sales Managers and RevOps to Manager or Admin once you've confirmed the internal access policy with your works council.


Assign users to **Groups** (e.g. Sales, Partner Management, Customer Success). Groups drive automation rules later, so get them right now.


### 3. Configure the Notetaker branding and behaviour


Navigate to **Recording & AI** in the left sidebar.


- **Notetaker name:** By default it uses the host's first name (e.g. “Selinas Notetaker”). Override this with a company-branded name.
- **Logo:** Upload your company logo so the Notetaker appears branded to external prospects.
- **Consent message:** Customise the on-screen text explaining why the Notetaker is present. For DACH audiences: *“Dieses Meeting wird zur Erstellung automatischer Notizen aufgezeichnet. Sie können der Aufzeichnung jederzeit widersprechen.”*


> **Note:** The “Powered by Demodesk” line appears during the free trial. On paid plans with custom branding enabled, it can be removed.


### 4. Set recording preferences (external only, 2+ minutes)


Still under **Recording & AI** , scroll to the recording rules:


- **Meeting type:** Select **Online meetings only** if you're not using Demodesk for phone calls yet. You can enable calling later.
- **Minimum duration:** Keep the default of **2 minutes** . No-shows and quick reschedules won't be transcribed or counted.
- **External meetings only:** Enable this so internal syncs and 1:1s are excluded. Anyone in your email domain (e.g.` @zep.de` ) counts as internal. Add additional owned domains if your company uses more than one.


This combination — external, 2+ minutes — is the safest default for GDPR-conscious German teams. Internal conversations stay private, short calls don't clog your data, and every external touchpoint gets captured.


### 5. Configure internal access and retention


Under **Internal access** , choose who can view recordings across the org. For German teams: **Host, Manager, and Admin** — it satisfies the “need-to-know” principle most works councils expect.


Under **Storage & retention** , set your retention window. Options range from 12 hours to 1 year. **90 days** balances coaching value against data minimisation. Bookmarked recordings are excluded from auto-deletion, so managers can flag high-value calls for longer-term coaching use.


### 6. Connect HubSpot at the company level


Go to **Integrations > HubSpot** and connect using a HubSpot admin account. Connecting company-wide means every rep's meetings sync automatically — no per-seat setup.


Once connected, choose which HubSpot object types Demodesk should update:


- **Contacts** — matched by email
- **Companies** — matched by domain
- **Deals** — auto-detected based on associated contacts and companies


Enable **AI CRM Concierge** to have Demodesk fill custom fields (deal stage, next step, decision criteria, close date) with preview-before-push. Reps review and edit each suggestion in AI chat before anything syncs to HubSpot.


### 7. Apply SPICED to all external meetings via automation


Go to **Agents > Scorecards** and create a scorecard using the SPICED framework (Situation, Pain, Impact, Critical Event, Decision).


Then go to **Agents > Automations** and create a rule:


- **Trigger:** All external meetings
- **Groups:** Sales (or “All users” if your whole team runs the same framework)
- **Action:** Apply SPICED scorecard, generate AI summary using SPICED structure, push summary to the HubSpot activity timeline


Every external call — regardless of who runs it — gets scored and summarised in the same structure. Managers coach against a consistent standard. HubSpot activities become searchable in SPICED language.


### 8. Configure CRM sync for meeting summaries


Under the HubSpot integration settings, map Demodesk's summary output to HubSpot's **Meeting activity** object. Enable:


- **Push AI summary to meeting notes** — the structured SPICED summary populates automatically
- **Push follow-up email draft to Deal timeline** — reps see the draft next to the deal
- **Update deal fields** — via AI CRM Concierge with human-in-the-loop approval


### 9. Set personal preferences: lobby handling and consent


Each user completes their personal setup under **Settings > Personal** :


- **Lobby handling:** Configure whether the Notetaker auto-admits itself or waits for host approval. For Teams meetings hosted by external parties, waiting for approval is safest.
- **Consent workflow:** Enable **verbal consent capture at meeting start** for German-speaking prospects. Demodesk detects the consent statement in the transcript and logs it.
- **Language:** Set to German for German-speaking reps so summaries and follow-ups generate in German by default.


## Tips


- **Group users before writing automations.** Automation rules trigger by group. Five minutes on group assignment saves an hour of debugging later.
- **Roll out SPICED in one automation, not per rep.** Consistency across the team is what makes coaching scalable.
- **Set retention to 90 days, then bookmark strategically.** This satisfies data minimisation while preserving the calls your managers actually coach against.
- **Get works council sign-off on your consent script before go-live.** Demodesk gives you the infrastructure; the wording should come from your DPO.
- **Test the HubSpot sync on one deal first.** Confirm the mapping matches your team's custom fields before enabling for everyone.


## Related skills and agents


- [AI CRM Concierge](https://demodesk.com/agents/ai-crm-concierge) — autonomous HubSpot updates with human review
- [AI Coach](https://demodesk.com/agents/ai-coach-a-3-0) — SPICED, MEDDIC, BANT, or custom scorecards
- [AI Sales Assistant](https://demodesk.com/agents/ai-sales-assistant) — recording, transcription, summaries, follow-ups
- [Marketplace agents](https://marketplace.demodesk.ai/agents) — 30+ pre-built agents including HubSpot deal enrichers
