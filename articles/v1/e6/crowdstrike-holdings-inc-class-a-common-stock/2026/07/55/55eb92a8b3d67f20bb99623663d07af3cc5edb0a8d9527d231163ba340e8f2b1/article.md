---
schema_version: "1.0.0"
document_id: "55eb92a8b3d67f20bb99623663d07af3cc5edb0a8d9527d231163ba340e8f2b1"
company_key: "crowdstrike-holdings-inc-class-a-common-stock"
company: "CrowdStrike Holdings Inc. Class A Common Stock"
source_id: "crowdstrike-holdings-inc-class-a-common-stock-news-import-26dc963e5592"
canonical_url: "https://www.crowdstrike.com/en-us/blog/crowdstrike-announces-continuous-identity-for-ai-agents/"
published_at: null
first_seen_at: "2026-07-25T01:07:09.054440+00:00"
fetched_at: "2026-07-28T21:36:14.883471+00:00"
content_hash: "sha256:747fea0bcb3a1ea1a735106f4a9f6e0b38be19fd206934690af9aec93e898afa"
---

# CrowdStrike Announces Continuous Identity for AI Agents

Identity security has long been built around a simple premise: Authenticate a user, grant access, and trust that decision until their next login. While for many this model worked well enough when identities were primarily human and access patterns were predictable, that’s no longer the case for humans and definitely not the case for AI agents.


Modern identities span humans, service accounts, cloud workloads, SaaS applications, APIs, and increasingly, autonomous AI agents operating across cloud infrastructure, SaaS platforms, browsers, and unmanaged devices. These agents can access multiple systems, invoke APIs, interact with SaaS applications, and make autonomous decisions at machine speed.


This creates a challenge for traditional security models. The speed of these agents, combined with the varying privileges of the humans using them, means a trust decision that was valid at login may no longer be valid moments later. A compromised credential or change in business context can instantly alter risk. It’s not enough to grant access once and assume trust persists.


CrowdStrike is redefining identity security with Continuous Identity — delivered through CrowdStrike Falcon® Next-Gen Identity Security — which continuously evaluates identity, device, threat, and business context to determine whether access should be granted, adjusted, or revoked. Today, we are introducing three innovations that extend Continuous Identity across the modern identity attack surface:


- Continuous Identity for AI Agents, enabling real-time authorization for every agent action
- Expanded modern privileged access for AWS cloud infrastructure
- Unified ownership, visibility, and intelligence across non-human identities (NHIs)


Together, these capabilities help organizations continuously verify trust across human, non-human, and AI identities while reducing standing privileges and identity-driven risk.


## Introducing Continuous Identity for AI Agents


Continuous Identity for AI Agents introduces a model that eliminates standing privileges and immediately verifies trust for every agent action. This approach helps address emerging AI agent risks including excessive privileges, compromised credentials, unauthorized access, agent-to-agent delegation risks, and access that remains active after risk conditions change.


Using modern identity standards including SPIFFE and the Shared Signals Framework (SSF), every action is authorized in real time based on what the agent is, who the human behind it is, and what the security and business context demands at that moment. This proactive approach controls access before agents can act.


**How It Works:**


- Every agent should have a verifiable identity based on the SPIFFE standard.
- Every action is evaluated against the human's and agent's entitlements, in addition to security and business context
- An agent with read/write capability acting for a read-only user can only read; the same agent, with a different human, would produce a different outcome
- No standing privileges exist; authorization happens at the moment of action using live risk signals
- When agents delegate to sub-agents, human identity and permissions are preserved
- If context changes — a new vulnerability, an HR status change — access is immediately revoked


CrowdStrike provides defense in depth for AI agent security with Continuous Identity for AI Agents, delivered through Falcon Next-Gen Identity Security, as well as CrowdStrike Falcon® AI Detection and Response (AIDR). Falcon AIDR continuously inspects prompts and intent to detect permission misuse or attempts to manipulate an LLM beyond its authorized scope, triggering Continuous Identity to revoke access before damage is done.


## Expanded Modern Privileged Access for AWS


As organizations expand cloud operations, standing privileges create risk. When privileged access remains available after it is needed, adversaries can exploit compromised credentials or elevated permissions to move laterally and access critical cloud resources.


CrowdStrike is extending modern privileged access to AWS cloud infrastructure. Organizations can eliminate standing AWS privileges and give engineers only the access they need for the session, task, or approved workflow at hand.


**How It Works:**


- When identities log into AWS using single sign-on (SSO), CrowdStrike evaluates identity, device posture, Falcon Zero Trust Access (ZTA) score, group membership, and other security signals
- The Falcon platform dynamically assigns the correct AWS roles or tags for that session
- Access exists only for the session duration or until context changes; if risk changes, privileges can be adjusted or automatically revoked
- Workflows support self-elevation and approval-based access for higher-risk scenarios


This innovation extends Continuous Identity beyond identity providers and into cloud infrastructure by allowing organizations to eliminate standing AWS privileges and grant access only when it is required.


## Unified Visibility and Intelligence Across Machine Identities


In addition to AI agents, organizations have thousands of NHIs (service accounts, API keys, OAuth tokens, cloud service principals) across their environment. However, ownership, governance, and accountability for these identities are often unclear. Security and identity teams often have the same questions when investigating threats or reviewing access: Who owns this identity? Who do I contact? Can I disable it without breaking production?


Too often, that answer is buried across identity protection metadata, cloud tags, Git history, and ticketing systems. No single system has the complete picture.


Falcon Next-Gen Identity Security automatically maps NHIs to human owners using signals from across the Falcon platform, establishing a formal ownership graph that makes every NHI accountable to a person or team. Unowned NHIs surface as posture findings, which drives accountability without manual overhead.


**How It Works:**


- Falcon Next-Gen Identity Security uses metadata from the Falcon platform to assign owners to NHIs (e.g., who manages access, who uses the machine, who created the service account).
- NHIs missing an owner surface as posture findings. When an owner leaves, affected NHIs escalate to high severity so teams can reassign before coverage gaps become exploitable. This combines ownership context with permissions and threat activity to identify which NHIs pose the greatest risk.
- When an NHI is involved in a detection, teams immediately see who owns it, what it can access, and whether it's actively governed or orphaned.
- Falcon Next-Gen Identity Security automatically flags orphaned, stale, and overprivileged NHIs as employees leave the organization or change roles, or as permissions drift over time.


## The Future of Identity Is Continuous


AI agents demand a new approach to identity security. Organizations can’t rely on static access decisions, periodic reviews, or fragmented controls to secure autonomous systems operating at machine speed. Identity security must continuously evaluate trust, continuously validate access, and continuously enforce policy as conditions change.


CrowdStrike is redefining identity security with Continuous Identity, which transforms identity from a point-in-time decision into a real-time control system. Continuous Identity for AI Agents will extend these capabilities to the agents proliferating across business environments, and it’s backed by defense in depth across the Falcon platform.


Delivered through Falcon Next-Gen Identity Security, Continuous Identity will extend across identity providers, cloud infrastructure, SaaS applications, browser sessions, and remote access workflows — all from a single unified platform.


#### Forward-Looking Statements


*This blog includes capabilities available today, as well as capabilities expected to be delivered through the ongoing integration of SGNL technology into the CrowdStrike Falcon® platform.*


#### Additional Resources


- *Explore the[Falcon Next-Gen Identity Security](https://www.crowdstrike.com/en-us/platform/next-gen-identity-security/) product page.*
- *[Learn](https://www.crowdstrike.com/en-us/blog/crowdstrike-named-leader-in-identity-threat-detection-and-response/) what industry analysts are saying about CrowdStrike’s identity security solutions.*
- *Download the[Complete Guide to Next-Gen Identity Security](https://www.crowdstrike.com/en-us/resources/white-papers/complete-guide-to-next-gen-identity-security/) .*
- *Interested in learning more? Join us at[Fal.Con 2026](https://www.crowdstrike.com/en-us/events/fal-con/las-vegas/?utm_medium=evt&utm_source=blog&utm_campaign=fal-con-26&utm_term=crwdblogs&utm_language=en-us) , where these conversations take center stage.*
