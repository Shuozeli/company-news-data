---
schema_version: "1.0.0"
document_id: "6bfb98b75620db60e214973679d5ac048b5a29b9b40975dfdbb9009af380d514"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-create-custom-meeting-type-detection-rules-in-demodesk-sc1-s"
published_at: "2026-07-06T00:00:00+00:00"
first_seen_at: "2026-07-24T10:56:31.944359+00:00"
fetched_at: "2026-07-28T21:38:32.326002+00:00"
content_hash: "sha256:eb1482c50018956025ce603b0337b6ce7267a2a804d77d7e393973e413fb586f"
---

# How to create custom meeting-type detection rules in Demodesk (SC1, SC2, etc.)

## What and why


Demodesk lets you define automation rules that detect the type of every meeting — a first sales call (SC1), a follow-up (SC2), a demo, a renewal — and apply the right scorecard and summary template. Set the rules once. Every rep gets the right coaching criteria and the right CRM notes on every call, without touching a setting. That's how sales teams scale coaching across dozens of reps without asking managers to tag calls by hand or reps to remember which template to pick.


## Who this is for


RevOps leads, sales enablement managers, and Heads of Sales at 50–500 person teams running structured sales processes (MEDDIC, BANT, or custom) with multiple defined meeting stages.


## Prerequisites


- Admin access to your Demodesk workspace
- At least two scorecards created (e.g., one for SC1 discovery, one for SC2 demo)
- At least two summary templates created (or plan to create them alongside the rules)
- A clear list of meeting types your team runs and how to distinguish them (naming conventions, calendar patterns, or content signals)
- Optional: user groups configured if you want rules to apply per team or region


## Steps


### 1. Open the Automations tab


Go to **Agents > Automations** in the top nav. All meeting-triggered rules for AI Assistant, AI Coach, and AI CRM Concierge live here.


### 2. Create a new automation rule


Click to create a new rule. Give it a name that matches your internal terminology — “SC1 — Discovery Call” or “SC2 — Demo & Deep Dive.” This name appears in reports, so keep it consistent with how your team already talks about each stage.


### 3. Define the trigger conditions


Choose one or more conditions that identify the meeting type. Demodesk supports three condition types you can combine:


- **User group** — Applies the rule to specific teams (e.g., DACH AEs, US SMB team, Customer Success). Use this when different regions or segments run different playbooks.
- **Meeting name keywords** — Matches words in the calendar event title (e.g., “SC1”, “Discovery”, “Intro Call”, “Demo”, “Deep Dive”). The fastest, most reliable trigger when your team follows a naming convention.
- **Semantic context** — The AI classifies the meeting based on what was discussed. Use this when calendar titles are inconsistent or reps use generic names like “Chat with \[Company\].” The AI reads the transcript and decides whether the call fits the meeting type you described.


Stack conditions with AND/OR logic. A common setup: “meeting name contains 'SC1' OR AI detects a discovery conversation.”


### 4. Attach the scorecard for this meeting type


Select the coaching scorecard that scores every call matching this rule. This is where SC1 and SC2 diverge. A discovery scorecard grades pain identification, budget qualification, and stakeholder mapping. A demo scorecard grades product fit, objection handling, and next-step commitment. AI Coach runs the right rubric based on whichever rule fires.


### 5. Attach the summary template


Pick the summary template AI Assistant generates after the call. Discovery calls typically need a MEDDIC-style summary covering pain, champion, and decision criteria. Demo calls need a summary focused on product feedback, objections raised, and agreed next steps. Different stages deserve different CRM notes.


### 6. Set the follow-up behavior (optional)


If your follow-up email templates or CRM field mappings differ by meeting type, attach them here. An SC1 might trigger a follow-up with a discovery recap and a link to book the demo. An SC2 might trigger a mutual action plan template.


### 7. Save and test on a live call


Save the rule and run a test call that should match the trigger. After the call, check three things: the correct scorecard appears in AI Coach, the correct summary template ran in AI Assistant, and the call is tagged with the right meeting type in reports. If the wrong rule fires, tighten the keyword match or refine the semantic description.


### 8. Repeat for every meeting type in your funnel


Most teams end up with 4–8 rules: SC1, SC2, demo, negotiation, closed-won kickoff, QBR, renewal. Build them in the order your reps run them so you can validate each stage as it happens.


## Tips


- **Start with two rules, not eight.** Get SC1 vs SC2 right first. Adding more rules before you've validated the basics creates rule-collision problems.
- **Use rule priority to handle overlap.** If a call could match two rules (e.g., “Demo” keyword plus semantic discovery signal), set an explicit priority so the right one wins.
- **Use semantic detection for reps who don't follow naming conventions.** Some AEs never rename calendar events. Semantic conditions catch what keyword matching misses.
- **Review misfires weekly for the first month.** Filter reports by rule and check that the right meetings got tagged. Adjust keywords or semantic descriptions based on what you find.
- **Pair meeting-type rules with scorecards built for your methodology.** MEDDIC on discovery, Challenger on demos, mutual action plan on late-stage — one framework rarely fits every stage.


## Related skills and agents


- [AI Coach](https://demodesk.com/agents/ai-coach-a-3-0) — runs the scorecard your rule attaches
- [AI Assistant](https://demodesk.com/agents/ai-sales-assistant) — generates the summary template your rule attaches
- [Marketplace: coaching scorecards and skills](https://marketplace.demodesk.ai/agents) — pre-built MEDDIC, BANT, and Challenger scorecards you can attach to your rules
