---
schema_version: "1.0.0"
document_id: "40afa0030fd1d44793adf55c4c306d52a4484ab44f16efa901510f9989755f62"
company_key: "avepoint-inc-class-a-common-stock"
company: "AvePoint Inc. Class A Common Stock"
source_id: "avepoint-inc-class-a-common-stock-rss-485a4e1b5f08"
canonical_url: "https://www.avepoint.com/blog/manage/shadow-ai"
published_at: "2026-06-04T22:24:00+00:00"
first_seen_at: "2026-07-20T23:21:42.943226+00:00"
fetched_at: "2026-07-28T21:11:40.706155+00:00"
content_hash: "sha256:f9917a33394a96ec17adbcf94435baea8790fda0489a7cc61806d05dda9f930f"
---

# What Is Shadow AI and How Do You Govern Shadow AI Agents Across Multicloud and SaaS?

## Key Takeaways


- **Shadow AI is unsanctioned AI use.**


Includes employees pasting work data into public chatbots and using AI features inside approved tools without re-review.
- **Shadow AI agents accelerate and expand risk.**


They're autonomous, persistent, and hold their own non-human identities — not just one-off prompts.
- **Low-code platforms across every major cloud are at the forefront.**


Any worker can spin up an enterprise-data-connected agent through Microsoft Power Platform, Salesforce Agentforce,[Google Gemini Enterprise](https://www.avepoint.com/blog/strategy-blog/gemini-enterprise-ai-agents-enterprise-operations) , Amazon Web Services (AWS) Bedrock — in minutes with the same level of access as the user.
- **Risks compound across the cloud estate.**


Data exfiltration, ungoverned non-human identities (NHIs), GDPR, and EU AI Act exposure, orphaned agents that survive employee departures.
- **You can't block your way out.**


Bans push usage underground. Effective programs shift from "block" to "manage." You can’t block what you can’t observe.
- **Identity is the only consistent control plane.**


Network controls can't keep pace with agents that act across clouds and SaaS. Identity-centric governance works everywhere.
- **Treat every agent as an identity.** Shadow AI becomes governed AI through continuous discovery, assigned ownership, scoped permissions, and lifecycle policy.


## What Is Shadow AI?


Shadow AI is the use of AI tools, large language models (LLM), or AI features inside an organization without formal IT or security approval. It includes employees pasting work data into public chatbots, using AI features inside approved SaaS apps that were never re-reviewed, or relying on browser-based assistants to handle sensitive content — all outside any governance review.


Shadow AI usually starts small:


- A product manager pastes a strategy document into ChatGPT to summarize it before a vendor meeting.


- A finance analyst feeds quarterly numbers into Claude to draft commentary.


- A developer uses an open-source model through OpenRouter to prototype an internal tool.


None of it goes through procurement, security, or legal. Most of it is well-intentioned. The problem is structural: These tools touch enterprise data, run outside enterprise controls, and leave no audit trail. Recent industry data points to the scale of this:[McKinsey reported](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai) that in 2025, 88% regularly use AI in at least one business function, compared with 78% a year ago.


Shadow AI is the broader category. Inside it sits a faster-growing and more consequential problem: shadow AI agents.[Gartner sees](https://www.gartner.com/en/newsroom/press-releases/2025-11-19-gartner-identifies-critical-genai-blind-spots-that-cios-must-urgently-address0) that by 2030 over 40% of enterprises will experience security or compliance incidents linked to unauthorized shadow AI.


## What Is a Shadow AI Agent?


A shadow AI agent is an autonomous AI system that operates inside an organization without formal governance — typically built with low-code tools, granted persistent access to enterprise data through API tokens or delegated permissions, and never registered with IT or security. Unlike a chatbot prompted by a user, an agent acts on data across systems on its own.


The distinction matters. A chatbot is per-session: a user prompts it, it responds, the session ends. An AI agent is persistent; it holds credentials, executes multi-step workflows, and can act across systems on its own — pulling data from one platform, summarizing it, posting results to another, all without continuous human input.


That persistence creates a second-order problem: every shadow AI agent is an NHI. It authenticates with API keys, open authorization (OAuth) tokens, or service accounts that often outlive the employee who created it. Cloud Security Alliance research published in early 2026 found that[78% of organizations](https://cloudsecurityalliance.org/press-releases/2026/01/27/79-of-it-pros-feel-ill-equipped-to-prevent-attacks-via-nhi-csa-oasis-survey-finds) lack formally adopted policies for managing non-human identities, which means AI-driven identities sit largely ungoverned.


A common example: A sales operations analyst uses a low-code platform to build an agent that pulls deal data from the customer relationship management (CRM) system, summarizes it nightly, and posts a digest to a chat channel. The agent uses a long-lived API key, then the analyst leaves the company eight months later while the agent keeps running and nobody on the security team knows it exists.


## What Is the Difference Between Shadow AI and Shadow AI Agents?


Shadow AI refers to any unsanctioned AI tool use, usually per-session and prompt-driven. Shadow AI agents are a subset: Persistent, autonomous AI systems that hold their own credentials and act on enterprise data without ongoing human prompting. The key difference is lifespan and identity — agents become NHIs with their own access footprint.


**Characteristic**


**Shadow AI Tool**


**Shadow AI Agent**


**Interaction model**


Prompt → response Autonomous, multi-step action


**Lifespan**


Per-session Persistent, always-on


**Identity**


User User impersonation


**Data access and Control**


User input (prompt, attachment, paste, etc.) Same as user by default


**Primary risk**


Data leakage on input Persistent access plus oversharing amplification


**Retention**


Subject to the tool’s retention policies (Typically 30 –180 days, but indefinite for some tools) Default retention policies (30 –180 days) or managed by organization


## Why Is Shadow AI Accelerating in 2026?


Shadow AI is accelerating because AI features are now embedded in tools employees already use, while shadow AI agents are accelerating because low-code platforms across every major cloud – Microsoft, Google, Salesforce, AWS – let any employee build an autonomous agent in minutes. Most organizations have no formal review process for either.


Three forces are compounding at once:


- **Zero-infrastructure adoption.** GenAI is browser-accessible. An employee can sign up for a consumer-tier model, install a browser extension, or activate an AI feature inside an approved SaaS app in under a minute. No procurement, no provisioning, no security ticket.
- **Low-code agent platforms.** Building an autonomous AI agent used to require a developer. It no longer does. Low-code and no-code platforms across the major clouds – Microsoft Copilot Studio, Power Platform, Salesforce Agentforce, Google AppSheet and Apps Script with Gemini, and AWS Bedrock Agents – let business users build agents that authenticate with their own credentials and act on enterprise data.
- **Quiet AI feature rollouts.** Approved SaaS vendors are shipping AI features into existing products without triggering re-review. A platform that passed security review in 2023 may now generate, summarize, or act on data through AI features that weren't in scope at the time. These quiet rollouts are one of the most common shadow AI entry points.


On top of those, AI agents in 2026 increasingly talk to each other through emerging standards like Model Context Protocol (MCP). An employee can connect a custom agent to multiple data sources – files, calendars, ticketing systems, code repositories – through MCP servers that the security team has never seen. The agent becomes a hub for cross-system data movement that traditional data loss prevention (DLP) cannot inspect.


## What Are the Risks of Shadow AI?


Shadow AI introduces concrete risks across security, compliance, and decision quality. The most consequential are data leakage through prompt inputs, regulatory violations when regulated data is processed outside approved workflows, intellectual property exposure when source code or strategic documents reach external models, loss of audit and lineage, hallucinated outputs feeding decisions, and reputational exposure when documented misuse surfaces.


- **Data exfiltration through prompts.** Public AI providers may retain user inputs depending on account type and provider policy. Free-tier and consumer accounts often retain data for logging or training. Once a confidential document is pasted into a public model, recovery is not an option.
- **Regulatory exposure.** GDPR, Health Insurance Portability and Accountability Act (HIPAA), the California Consumer Privacy Act (CCPA), and the EU AI Act set strict requirements on how regulated data can be processed. Shadow AI bypasses the data processing agreements (DPAs) that make those workflows compliant. For organizations subject to the EU AI Act, deploying AI systems in high-risk contexts without documented controls is itself a violation.
- **Intellectual property exposure.** Source code, product roadmaps, pricing models, and mergers and acquisitions (M&A) documents become liabilities the moment they touch a consumer AI tool. Provider terms vary widely on whether inputs are retained, logged, or used to improve models.
- **Loss of audit and data lineage.** Organizations lose visibility into what data was used, by whom, and for what purpose. That undermines audit obligations, e-discovery, and any post-incident investigation.
- **Hallucinations driving decisions.** Outputs from unvetted models can be confidently wrong. When employees treat shadow AI output as authoritative – without retrieval grounding or human review – flawed information enters strategic and operational decisions.
- **Reputational and legal exposure.** Documented misuse of AI by employees can trigger litigation, regulatory action, and brand damage that long outlasts the original incident.


## How Do Shadow AI Agents Amplify Enterprise Risk?


Shadow AI agents are not a worse version of shadow AI — they are a categorically different risk. They hold persistent credentials, inherit broad permissions from their makers, act across multiple systems on their own, and amplify any existing data oversharing in SharePoint, Drive, Salesforce, or wherever the agent reaches. The result is an ongoing, auditable-only-in-hindsight exposure surface.


- **NHI sprawl.** Every agent is an identity that authenticates with credentials. Without an NHI inventory, organizations cannot tell how many agents exist, what they can access, or who owns them.
- **Credential persistence.** Agents commonly use long-lived API keys or OAuth tokens that outlive the employee who created them. An employee leaves; their agents and their access remain.
- **Privilege inheritance.** An agent built with a maker's credentials inherits the maker's permissions. A finance manager's agent can read anything the finance manager can read — including everything outside the use case the agent was built for.
- **Data oversharing amplification.** Most organizations have significant latent oversharing in SharePoint sites, shared Drive folders, Salesforce records, and Slack channels. A shadow AI agent does not create that exposure — but it scales it. The agent surfaces and redistributes overshared content at machine speed, turning a dormant access problem into an active data leak.
- **Cross-system audit gaps.** When a single agent acts across CRM, file storage, and chat, no single audit log captures the full chain of activity. Traditional logging frameworks were not designed for autonomous cross-system actors.
- **Prompt injection through untrusted inputs.** An agent that ingests external content – emails, web pages, support tickets, files from outside the organization – can be manipulated by hidden instructions in that content. The attack surface is the agent's input pipeline, not its credentials.


## How Mature Is Your Shadow AI Exposure?


Most organizations sit at Tier 1; they don't know what AI is in use, who built which agents, or what data those agents touch. Tier 2 organizations have an inventory but limited enforcement. Tier 3 organizations apply continuous discovery, identity-centric controls, and lifecycle policy to every AI agent across their cloud and SaaS footprint.


**Tier 1: Low Control**


**Tier 2: Moderate Control**


**Tier 3: Governed**


**Discovery**


Unknown what's in use Inventory of approved tools only Continuous discovery across all clouds and SaaS


**Agent inventory**


None Manual list of known agents Automated registry with assigned ownership


**Identity**


Shared API keys, no rotation Per-agent service accounts Scoped NHIs with lifecycle policies


**Policy**


None or blanket ban Acceptable use policy Role-based, data-classified policy


**Auditability**


None Periodic log review Real-time monitoring with alerting


**Lifecycle**


Agents persist indefinitely Manual cleanup Automated retirement of stale agents


## Where Does Shadow AI Live in a Multicloud and SaaS Environment?


Shadow AI lives wherever employees can access AI features without security review — which today means almost everywhere. Public AI chatbots, AI features inside major SaaS platforms like Salesforce and Google Workspace, low-code agent builders across every major cloud, deployed agents in AWS Bedrock and Azure OpenAI, and emerging MCP-based custom integrations all host shadow AI activity.


Generic SaaS discovery tools miss most of this surface. Each environment hides shadow AI differently:


### Public AI Tools and Consumer Accounts


The most visible layer: ChatGPT, Claude, Gemini, Perplexity, and Canva AI accessed through personal accounts or browser extensions. Activity often appears as routine web traffic. Browser extension logs and SaaS discovery tools catch some of it; AI plug-ins inside approved tools usually escape detection entirely.


### Salesforce Agentforce


Agentforce lets builders create autonomous agents that act on Salesforce records like leads, opportunities, cases, and accounts. Agents inherit the builder's data visibility, which under Salesforce sharing rules, can be significantly broader than the agent's documented use case. CRM data – customer records, pipeline, sales forecasts – is often the highest-value data in an organization and the easiest to exfiltrate through a poorly scoped agent.


### Google Workspace


Gemini side panel access reads Drive, Docs, Gmail, and Meet content. Apps Script with AI calls and increasingly direct Vertex AI integrations give citizen developers a way to wire Workspace data into custom agents through service accounts. Workspace's permission model is comparatively permissive: A shared Drive folder accessed by one agent can expose data across hundreds of users.


### Microsoft 365 and Power Platform


Copilot Studio and Power Platform make agent-building accessible to any maker with a license. Agents built this way authenticate as the maker, inherit the maker's Microsoft Graph permissions, and can read across SharePoint, Teams, OneDrive, and Exchange. SharePoint Agents, a newer category, operate directly on document libraries with minimal admin oversight.


### AWS, Azure, and Google Cloud Deployed Agents


Bedrock Agents, Azure OpenAI Assistants, and Vertex AI Agents are infrastructure-deployed and typically built by developers or platform teams — but the data they access often crosses into production systems, customer data stores, and analytics platforms. Long-lived service-account credentials are the norm. Without workload identity federation or ephemeral credentials, a compromised agent becomes a persistent foothold.


### Custom Integrations Through MCP, n8n, Zapier, and Make


The emerging MCP layer lets agents connect to multiple data sources through a standard interface. Automation platforms like n8n, Zapier, and Make increasingly include AI nodes that call public LLMs from inside otherwise-approved workflows. Both create AI activity that looks like ordinary integration traffic to traditional monitoring tools.


## How Do You Discover and Govern Shadow AI Agents?


To govern shadow AI agents, treat every agent as a registered identity. Continuously discover agents across all cloud and SaaS platforms, assign every agent a named human owner, scope its permissions to least privilege, monitor its activity in real time, and apply lifecycle policies that retire stale or orphaned agents before they become persistent risks.


A workable governance process runs in five steps:


1. **Discover what already exists.** Most organizations significantly underestimate their agent footprint. A meaningful inventory pulls from every relevant admin surface — Microsoft 365 admin center and Power Platform admin center, Google Workspace admin and Vertex AI consoles, Salesforce setup and Agentforce builder, AWS IAM and Bedrock consoles, plus SaaS integration catalogs and connected app lists in the identity provider. Most cloud estates have between five and 10 times more agents than security teams expect.
2. **Assign ownership to every agent.** Every agent gets a named human owner who is accountable for what the agent does. Orphaned agents – those whose creator has left the company – get retired or reassigned, not ignored. This single control catches most of the persistence risk.
3. **Scope permissions to least privilege.** Replace inherited maker permissions with scoped service accounts or, where supported, workload identity federation. Long-lived API keys get rotated or replaced with short-lived credentials. The principle is the same as for human identities: an agent should only access what its task requires.
4. **Monitor agent activity in real time.** Track what data each agent touches, what actions it takes, and which systems it crosses. Flag anomalies like sudden privilege escalation, unusual data volumes, and cross-tenant access. Identity-centric monitoring is more effective than network-based monitoring for autonomous agents because agent traffic often looks like normal application traffic.
5. **Apply lifecycle policy.** Reassess agent inventory at least quarterly. Auto-retire agents that have been dormant for a defined period. Tie agent governance into existing identity governance workflows so AI agents are reviewed in the same access certifications as human accounts.


## What Are the Best Practices for Managing Shadow AI?


The most effective shadow AI programs replace blanket bans with managed enablement. They invest in continuous discovery rather than periodic audits, treat every agent as a first-class identity, classify data before classifying tools, and educate the makers and citizen developers who actually build agents — not only the central IT team that reviews them.


- **Don't ban — manage.** Blanket bans push usage underground, where it becomes harder to detect and impossible to govern. Sanction safe alternatives and define what data may and may not be used with each.
- **Lead with identity, not network.** Network controls cannot keep pace with agent-driven workflows. Identity is the only enforcement layer that works consistently across clouds and SaaS.
- **Classify data before classifying tools.** Define what data – customer records, source code, regulated personally identifiable information (PII), financial forecasts – is off-limits and tie those classifications to AI policy. People follow data rules more reliably than tool rules.
- **Treat agents as first-class identities.** Apply the same lifecycle management to AI agents that you apply to human accounts: provisioning review, periodic certification, retirement on departure or inactivity.
- **Educate the makers.** Citizen developers building agents in low-code tools rarely have security training. Short, role-specific guidance – what data is in scope, what credentials to use, when to involve security – reduces risk more than centralized review.
- **Pair AI governance with data governance.** Sensitivity labels, retention policies, and access reviews are upstream of safe AI use. Without them, every AI policy is built on sand.
- **Consider an independent AI Control Plane.** Hyperscalers and other large vendors are building control planes to govern their own systems with limited coverage and interoperability with third parties to lock customers into their ecosystem
- **Remember that agents are connected.** Solve your operational governance, security, and resilience problems across your digital estate, because agents are connected to apps, data, users, sites, workspaces, and so much more, that may be source of governance risks and breaches.


## Frequently Asked Questions


### What is the difference between shadow IT and shadow AI?


Shadow IT refers to any unsanctioned technology, apps, services, or infrastructure, used without IT approval. Shadow AI is a more specific category that involves unauthorized use of AI tools, models, or agents. The distinction matters because shadow AI introduces unique risks around data ingestion, autonomous action, and non-human identity sprawl that traditional shadow IT controls were not designed to handle.


### What is the difference between shadow AI and shadow AI agents?


Shadow AI is the broad category of unsanctioned AI tool use — typically per-session, prompt-driven activity. Shadow AI agents are a subset characterized by autonomy and persistence. An agent holds its own credentials, runs without continuous human input, and acts on enterprise data across systems. The risk profile is sharper because agents create non-human identities that survive their creators.


### Is shadow AI illegal?


Shadow AI is not inherently illegal, but it routinely violates regulatory requirements. Pasting personal data into a public model can breach GDPR, HIPAA, or CCPA requirements depending on the data type and provider terms. Deploying AI systems in high-risk contexts without documented controls violates the EU AI Act. Most organizations also have internal acceptable use policies that shadow AI bypasses.


### How does shadow AI affect Salesforce, Google Workspace, and Microsoft 365?


Shadow AI appears in different forms across each platform. In Salesforce, Agentforce agents built without security review can access broad CRM data through the builder's sharing permissions. In Google Workspace, Gemini side panel access, and Apps Script integrations can read across Drive, Gmail, and Meet. In Microsoft 365, Copilot Studio, and Power Platform agents inherit Microsoft Graph permissions across SharePoint, Teams, and Exchange.


### How do I detect shadow AI agents in my environment?


Detection requires inventorying agents across every platform-specific admin surface, not relying on network monitoring alone. Pull agent registries from each cloud and SaaS admin console, cross-reference with identity provider connected-app lists, and review service accounts and API keys for indicators of AI agent activity. Identity-centric discovery surfaces agents that network-based tools miss.


### What is a non-human identity and how does it relate to shadow AI?


A non-human identity (NHI) is any identity used by software rather than a person — service accounts, API keys, OAuth tokens, workload identities. Shadow AI agents are NHIs by definition: they authenticate with credentials and act on data without a logged-in user. Industry research published in early 2026 found that most organizations lack formal NHI governance, which is why shadow AI agents accumulate undetected.


### How often should I review my organization's AI agent inventory?


AI agent inventories should be reviewed at least quarterly, with continuous automated discovery in between. Quarterly is the minimum because low-code platforms allow new agents to be created daily, employees leave (creating orphaned agents), and platform vendors ship new AI features that reclassify previously-approved tools. High-regulation industries should review monthly.


### How does shadow AI affect data loss prevention (DLP)?


Shadow AI degrades DLP effectiveness because it creates new data egress paths that traditional DLP cannot inspect. Prompts to public models, agent-to-agent communication through MCP, and AI features inside approved SaaS all bypass classic DLP rules. Effective AI-era DLP requires content inspection at the prompt level, identity-aware monitoring of agent activity, and policy enforcement at the data classification layer rather than only at the network edge.


## Related Questions


[→ What is AI agent governance?](https://www.avepoint.com/solutions/agentic-ai-governance)


[→ How do you secure Microsoft Copilot?](https://www.avepoint.com/blog/protect/what-is-dark-data)


[→ What is the difference between Copilot and Copilot Studio?](https://www.avepoint.com/blog/strategy-blog/what-are-copilot-studio-agents-why-they-matter-future-of-work)


[→ What is data loss prevention for AI?](https://www.avepoint.com/blog/protect/the-best-recovery-is-no-recovery-at-all-your-2025-dlp-strategy)


[→ What does the EU AI Act require for AI agents?](https://www.avepoint.com/blog/protect/eu-ai-act-compliance-101-obligations-risks-and-best-practices-for-eu-and-global-organizations)


## AI Adoption Is Inevitable. Ungoverned AI Is Not.


[AvePoint AgentPulse](https://www.avepoint.com/solutions/agentic-ai-governance) discovers and governs AI agents across Microsoft 365, Google Workspace, and connected SaaS, including agents built in low-code platforms and the non-human identities they create. It assigns ownership, flags overprivileged access, and applies lifecycle policy to agents your security team didn't know existed.
