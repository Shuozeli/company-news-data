---
schema_version: "1.0.0"
document_id: "421162fe4c54ae5571dab434ed8a2ca85525277dfad3e970126506cdadcb9078"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/how-to-configure-automated-salesforce-field-population-from-voice-n"
published_at: "2026-07-14T00:00:00+00:00"
first_seen_at: "2026-07-27T16:28:03.851214+00:00"
fetched_at: "2026-07-28T21:22:05.726331+00:00"
content_hash: "sha256:a8a6036707f56c40a2b4aeca8ce87ebbe00ff2018829ec584abe07d409ec179a"
---

# How to configure automated Salesforce field population from voice notes and meetings in Demodesk

## What and why


This guide shows you how to configure Demodesk's AI CRM Concierge to fill Salesforce Opportunity, Account, Contact, and Task fields from your sales calls, voice notes, and in-person meetings—with team-specific rules and an approval step before anything syncs. Your reps stop typing fields. Different teams run different logic on the same CRM instance.


## Who this is for


Salesforce admins and RevOps at sales-led companies running multiple product lines or sales teams that share one CRM instance but need different field logic per team.


## Prerequisites


- Demodesk **Coaching & AI** plan or higher (AI CRM Concierge is included)
- Salesforce admin access with permission to authorize third-party connections
- Your Salesforce object model reviewed—which fields on Opportunity, Account, Contact, and Task you want AI to fill
- User groups defined in Demodesk if you plan to run different rules per team
- Recording enabled across the channels you sell on (video, dialer, mobile app for in-person)


## Steps


1. **Connect Salesforce to Demodesk.** In Demodesk, go to **Settings > Integrations > Salesforce** and authorize the connection. Once authenticated, Demodesk pulls your object schema—including custom fields and picklist values—so field suggestions match your Salesforce setup, not a generic template.
2. **Choose which Salesforce objects AI CRM Concierge should fill.** Open **Agents > Automations > AI CRM Concierge** and select the objects to enable: **Opportunity** , **Account** , **Contact** , and **Task** . Enable only what your team uses. Fewer objects mean faster rep approval decisions and less noise.
3. **Map each Salesforce field to an AI suggestion source.** For every field you enabled, choose whether the value comes from the meeting transcript, the rep's voice note, or both. Demodesk's AI object detection matches conversations to the right Opportunity automatically. For each mapped field, add a short instruction—“Only fill this if the prospect confirmed a budget number”—and the AI follows it. Custom picklist fields inherit your Salesforce options. The AI selects the closest match rather than free-texting.
4. **Set the sync mode: approve before push, or auto-sync.** For each object or field, choose one of two modes:


- **Approve before push (default, recommended for launch):** the rep sees AI suggestions in Demodesk after every call, reviews or edits them via AI chat, and clicks approve. Nothing hits Salesforce until they do.
- **Auto-sync:** high-confidence updates push to Salesforce without approval. Best for low-risk fields—call disposition, next-step dates—once you trust the accuracy.


Most teams run approve mode for two to four weeks, watch accuracy, then flip specific fields to auto-sync.
5. **Create user-group-based rules for different sales teams.** If you run multiple product lines or sales teams on one Salesforce instance, user groups let you run different logic per team. In **Settings > User Groups** , create a group for each team, assign reps, then return to **AI CRM Concierge** and configure rules per group—different object sets, different field mappings, different approval modes. One CRM, two independent playbooks.
6. **Test on a live call before rolling out.** Have one rep record a real call, then open the meeting in Demodesk and review the CRM Concierge suggestion panel. Did AI pick the right Opportunity? Are the fields filled as expected? Adjust the field instructions from Step 3 and repeat with a second call. Ship to the team once two consecutive calls pass review with no edits needed.
7. **Monitor accuracy and expand to auto-sync.** In the **Insights** tab, review the CRM Concierge accuracy dashboard: how often reps approve suggestions unchanged, how often they edit, how often they reject. Fields at 95%+ approval-without-edits are safe for auto-sync mode.


## Tips


- **Start narrow, expand later.** Enable five to ten high-value fields at launch, not fifty. Reps trust the system faster when every suggestion is useful.
- **Write field instructions in your reps' language.** “Only fill 'Decision Timeline' if the prospect gave a specific quarter or month” works better than a generic prompt. The AI follows your instruction.
- **Use approval mode as a coaching signal.** When a rep edits an AI suggestion, that's data—either the AI missed a nuance (fix the instruction) or the rep caught something worth raising in a 1:1.
- **Combine with the mobile app for field sales.** Reps record voice notes on the Demodesk mobile app after in-person meetings. AI CRM Concierge fills the same Salesforce fields with the same rules. No separate configuration needed.
- **Keep your DPO in the loop.** AI CRM Concierge processes conversation data in the EU (Frankfurt) and never trains our models on your data. Share the DPA and works-council documentation before rollout—the compliance conversation is short when you have the paperwork ready.


## Related skills and agents


- [AI Coach](https://demodesk.com/agents/ai-coach-a-3-0) — score every call against your methodology once the CRM data is clean
- [AI Sales Assistant](https://demodesk.com/agents/ai-sales-assistant) — summaries and follow-up emails on the same conversation record
- [AI Sales Analyst](https://demodesk.com/agents/ai-sales-analyst) — ask any question across the Salesforce data AI CRM Concierge has populated
- [Marketplace skills for CRM hygiene](https://marketplace.demodesk.ai/agents)
