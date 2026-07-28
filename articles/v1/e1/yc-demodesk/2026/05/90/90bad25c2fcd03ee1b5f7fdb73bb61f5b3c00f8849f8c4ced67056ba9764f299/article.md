---
schema_version: "1.0.0"
document_id: "90bad25c2fcd03ee1b5f7fdb73bb61f5b3c00f8849f8c4ced67056ba9764f299"
company_key: "yc-demodesk"
company: "Demodesk"
source_id: "yc-demodesk-news-import-5cd66572c62f"
canonical_url: "https://demodesk.com/blog/introducing-the-demodesk-mcp"
published_at: "2026-05-19T00:00:00+00:00"
first_seen_at: "2026-07-24T10:56:31.944359+00:00"
fetched_at: "2026-07-28T21:43:32.355791+00:00"
content_hash: "sha256:ee8ccadcec6de5ffc00413552e02b340ca41c859a0e883b5d4865ba0d82742b9"
---

# Introducing the Demodesk MCP: Your Sales Conversations, Inside Any AI Tool

G


G


enerally available May 19, 2026. The Demodesk MCP gives Claude, Cursor, Codex, and every other MCP-compatible AI assistant direct access to your Demodesk meetings, transcripts, summaries, and coaching scorecards. OAuth setup in under a minute.


Today we are launching the Demodesk MCP, a Model Context Protocol server that connects every MCP-compatible AI assistant to your Demodesk sales conversations. From May 19, 2026, you can ask Claude, Claude Desktop, Claude Code, or Codex to pull your meeting recordings, transcripts, summaries, and coaching scorecards without leaving the AI tool you already use.


Sales data has always been the bottleneck for sales AI. The most useful context, what was said in your calls, sits behind a UI that AI assistants cannot reach. Reps copy-paste transcripts. Managers summarize calls into Slack threads. RevOps leaders rebuild the same reports week after week. The Demodesk MCP cuts that out. Any AI tool you trust can now query your Demodesk meeting data on demand.


## What MCP is


The Model Context Protocol is an open standard, released by Anthropic in 2024, for connecting AI applications to external systems. It works like a common plug between AI assistants and the tools they need to be useful. Without MCP, every AI integration is bespoke. With MCP, the AI knows how to ask, the tool knows how to answer, and you can swap either side without re-wiring the connection.


A MCP setup has three parts:


- **Servers** expose data and actions from a specific tool. The Demodesk MCP is the server side for your meeting data.
- **Clients** are the AI applications that call the server. Claude.ai, Claude Desktop, Claude Code, Cursor, and Codex are all clients today.
- **Hosts** manage permissions and discovery. Your laptop's MCP configuration tells your client which servers it can talk to.


The benefit is portability. The same query, “show me the last ten demos where the prospect asked about pricing,” works the same way from Claude on the web, from Cursor in your editor, or from any new MCP client a developer ships tomorrow.


## What the Demodesk MCP gives you


The Demodesk MCP exposes six functions that map to the data revenue teams care about:


- **` list_recordings`** · Search meetings by host, date, attendee, or other filters.
- **` get_recording`** · Pull full details for a specific meeting.
- **` get_transcript`** · Access the full transcript with speaker identification.
- **` batch_transcripts`** · Fetch up to 100 transcripts at once for pattern analysis.
- **` list_summaries`** · Retrieve AI-generated meeting summaries.
- **` list_scorecards`** · Get coaching scorecards with performance scores and feedback.


Every function honors your existing Demodesk permissions. The MCP does not expand access. A rep sees what they could see in the Demodesk UI. A manager sees what they could see. A CRO sees what they could see.


## What you can do with it


A few patterns we have already seen from early users:


**Pre-meeting briefs.** Ask Claude Desktop: “Summarize the last three meetings with Acme Corp, focusing on objections and next steps.” A brief that used to take twenty minutes lands in five seconds.


**Coaching audits across the team.** Ask Claude Code or Cursor: “Pull the 50 most recent demo recordings, score each against our MEDDIC scorecard, and surface the top five gaps.” Full-team pattern recognition without opening Demodesk.


**Customer voice analysis.** Run` batch_transcripts` from any MCP client and surface the top five customer phrases of the past quarter, broken down by ICP segment. Useful for content briefs, sales-deck rewrites, and positioning refreshes.


**Forecast review prep.** Ask Codex: “Pull every churn-call transcript from this quarter and surface the recurring objections.” Faster than re-listening to every recording.


**Sales engineering workflows.** AEs can ask their editor's AI to draft a follow-up email referencing the exact technical questions raised in the demo, pulled straight from the transcript. No more “let me re-listen to that part.”


## How to set it up


Four steps:


1. **Use this server URL:**` https://demodesk.com/mcp` . That is the entire endpoint.
2. **Add it to your AI client.** Claude Desktop, Claude.ai, Cursor, and Codex all expose an MCP settings panel that accepts a server URL.
3. **Authenticate via OAuth.** Sign in with your existing Demodesk account. A manual API key flow is available for clients that do not yet support OAuth.
4. **Restart the client.** The Demodesk tools appear in your AI assistant's tool list.


Full setup instructions and screenshots are at[help.demodesk.com/en/articles/15080605-demodesk-mcp](https://help.demodesk.com/en/articles/15080605-demodesk-mcp) .


## Built on the four-agent foundation


The Demodesk MCP exposes the same data layer that powers our four AI agents:


- **AI Assistant.** Recording, transcription in 98 languages, summaries, follow-up drafts, CRM sync.
- **AI Coach.** Call scoring against MEDDIC, BANT, Challenger, SPIN, or custom scorecards.
- **AI Analyst.** Pipeline insights, deal risk detection, win-pattern surfacing, automated re-engagement.
- **AI CRM Concierge.** Autonomous CRM updates with 99% field accuracy and human-in-the-loop approval.


Inside Demodesk, the agents do the work for you. Outside Demodesk, the MCP gives your AI tools the same data to work with. The intelligence is the same. The surface area expands.


## Quote from leadership


> “Sales intelligence used to mean a dashboard. Then it meant an AI feature. Now it means a protocol your team can plug into any AI tool they trust. The MCP is how we make our data work for our customers everywhere they work, not just inside Demodesk.”
>
>
> Veronika Wax, Founder & CEO, Demodesk


## Availability and pricing


The Demodesk MCP is generally available from May 19, 2026 to all Demodesk customers, including 14-day free trial users.


- **Demodesk platform.** EUR 49/user/month on annual billing, EUR 59/user/month monthly.
- **MCP access.** Included on every plan. No per-call charges, no separate seat fees, no usage caps.
- **Viewer seats.** Free for managers, customer success, and other non-sales users.


A 14-day free trial is available at[demodesk.com/pricing](https://demodesk.com/pricing) . No credit card required. The trial includes full MCP access.


## FAQ


### What is the Demodesk MCP?


The Demodesk MCP is a Model Context Protocol server that lets any MCP-compatible AI assistant (Claude.ai, Claude Desktop, Claude Code, Cursor, Codex, and any other MCP client) query your Demodesk meetings, transcripts, summaries, and coaching scorecards. It exposes six functions covering recording search, transcript retrieval, summary access, and coaching scorecard data.


### Which AI tools work with the Demodesk MCP today?


Claude.ai (web), Claude Desktop, Claude Code, Cursor, and Codex are confirmed working at launch. Any MCP-compatible client that supports OAuth or accepts a manual API key configuration can connect. The MCP standard is open, so client coverage grows with the protocol.


### How does authentication work?


OAuth with your existing Demodesk account is the primary flow. Sign in once and your client stays connected. For clients that do not yet support OAuth, a manual API key setup is available. The MCP respects your existing Demodesk permissions and does not expand what data you can see.


### Is my sales data shared with Anthropic, OpenAI, or anyone else?


No. The Demodesk MCP is a server. It returns data only when your AI client requests it. The AI client (Claude, Cursor, Codex, others) handles its own data policy, and you control which clients you connect to your Demodesk account. Customer data is never used to train Demodesk's own models, and the MCP does not change that.


### Does the MCP support EU data-residency requirements?


Yes. All Demodesk data remains in EU data centers (Azure Frankfurt) per our ISO 27001:2022 certification and GDPR-native architecture. The MCP serves data from the same regional infrastructure. What your AI client does with the data after retrieval is governed by your AI vendor's own data policy.


### How much does the MCP cost?


The MCP is included at no additional cost on every Demodesk plan. No per-call charges, no seat fees, no usage caps.


### What is the difference between the Demodesk MCP and Demodesk AI Crew?


[AI Crew](https://demodesk.com/blog/introducing-demodesk-ai-crew) is the no-code workspace inside Demodesk where you build autonomous agents that run on schedule or trigger. The MCP is the protocol that lets external AI tools query Demodesk meeting data. Use AI Crew for actions inside Demodesk. Use the MCP for queries from your favorite AI tool.


### Where do I get help setting it up?


Full setup steps and screenshots are at[help.demodesk.com/en/articles/15080605-demodesk-mcp](https://help.demodesk.com/en/articles/15080605-demodesk-mcp) . For OAuth issues or client-specific quirks, contact support through the in-app chat or write to support@demodesk.com.


## Try the Demodesk MCP on your own workflow


[Try Demodesk free for 14 days](https://demodesk.com/pricing) . The trial includes full MCP access and OAuth setup in under a minute.


[Book a demo](https://demodesk.com/pricing) . See the MCP working with your AI tool of choice.


## About Demodesk


Demodesk is the AI sales platform built for action. Four AI agents handle the work that consumes a revenue team's day, including CRM updates, coaching, follow-ups, and deal rescue. The Demodesk MCP opens that same data to every AI tool your team already uses. Founded in Munich in 2018, Demodesk serves over 300 customers and 20,000 users including European companies in automotive, marketplaces, HR tech, and energy. All customer data is stored in EU data centers (Azure Frankfurt) under ISO 27001:2022 certification. Demodesk is rated 4.9/5 on G2 and named Capterra Best Value 2026. For more information, visit[demodesk.com](https://demodesk.com/) .
