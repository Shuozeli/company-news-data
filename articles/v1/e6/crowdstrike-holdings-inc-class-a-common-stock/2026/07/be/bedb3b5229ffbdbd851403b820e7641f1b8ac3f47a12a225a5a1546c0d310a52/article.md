---
schema_version: "1.0.0"
document_id: "bedb3b5229ffbdbd851403b820e7641f1b8ac3f47a12a225a5a1546c0d310a52"
company_key: "crowdstrike-holdings-inc-class-a-common-stock"
company: "CrowdStrike Holdings Inc. Class A Common Stock"
source_id: "crowdstrike-holdings-inc-class-a-common-stock-news-import-26dc963e5592"
canonical_url: "https://www.crowdstrike.com/en-us/blog/crowdstrike-technical-risk-assessments-reveal-common-exposure-patterns/"
published_at: null
first_seen_at: "2026-07-25T01:07:09.054440+00:00"
fetched_at: "2026-07-28T21:36:14.883471+00:00"
content_hash: "sha256:4f0901352d0fb2930b30a874f4663d4b5e0add052c01679ba173fe61d1fb4ef4"
---

# CrowdStrike Technical Risk Assessments Reveal Common Exposure Patterns

Every year, CrowdStrike Professional Services performs hundreds of Technical Risk Assessments (TRAs) across myriad industries, geographies, and business environments. These deep, hands-on reviews look at how security controls behave in production to evaluate the threats they see and block — and crucially, the threats they miss.


Exposure is constantly changing as organizations adopt new technologies and adversaries accelerate and explore new tactics. Because our team sees so many different environments up close, we have a lens into the patterns that put businesses at risk: the same misconfigurations, visibility gaps, and temporary exceptions continue to appear, and they map to the techniques modern adversaries use to move quickly and bypass detection. By analyzing these real-world findings, we’ve identified that the highest risk often resides in "silent" spaces — unmanaged assets and overlooked credential paths — where adversaries now operate with machine speed.


Addressing these systemic issues requires moving beyond tool acquisition and toward operational discipline. Our assessments reveal that securing the enterprise isn't just about having the right technology, but about gaining clarity into where risk lives. By closing the visibility gaps across critical areas, organizations can shift from a reactive posture to a proactive approach that disrupts the adversary’s path.


In this blog, we draw on a large sample of[CrowdStrike Technical Risk Assessments](https://www.crowdstrike.com/en-gb/services/fortify/technical-risk-assessment/) to examine those patterns and highlight the most common issues quietly driving cyber risk. For security teams seeking to lower their risk profile, these are the areas to focus on to strengthen security posture.


## Most Common Risk Patterns


### Shadow AI: The Governance Gap Organizations Can't Ignore


Employees, developers, and SaaS platforms are deploying AI tools faster than security and policy teams can respond. From LLM-powered browser extensions to unapproved AI agents running in production, AI is proliferating outside sanctioned channels — and security teams often have no visibility into it. Unlike traditional shadow IT, shadow AI requires no installation, hides inside existing tools, and can silently route sensitive data to external models. In one recent CrowdStrike Services assessment, the client had zero approved agentic AI use but had agents running in production. In another, the approved inventory was off by 400. The risks are significant: uncontrolled data exposure, broken access permissions, unmonitored autonomous agent behavior, and no clear accountability.


#### Recommendations


- Form a cross-functional AI committee to align business needs with security requirements
- Deploy CrowdStrike Falcon® AI Detection and Response (AIDR) to surface shadow AI adoption and CrowdStrike Falcon® Exposure Management to inventory LLMs, agents, IDE extensions, and MCP servers
- Use CrowdStrike Falcon® Cloud Security (AI-SPM), CrowdStrike Falcon® Shield, and Falcon AIDR to identify AI activity across productivity and communication platforms
- Publish clear rules and a sanctioned list of approved models and interfaces
- Define who can build and deploy AI agents, what they can access, and how their behavior is logged and terminated
- Ensure staff understand the data exposure, compliance, and integration risks of unauthorized AI tools


### External Attack Surface


The external attack surface refers to everything an adversary can see and access from the internet before they enter the target network. This includes:


- Public-facing websites and applications
- Domains and subdomains (including old or “test” ones)
- Internet-exposed IP addresses and services
- VPN gateways, remote access portals, and management interfaces
- Cloud and SaaS services that can be reached directly from the internet


In our Technical Risk Assessments, we consistently find that this external footprint is larger and more exposed than security teams realize. Shadow IT, forgotten projects, third-party integrations, and misconfigured cloud services all expand the attack surface in ways that rarely show up in internal inventories.


Common issues we uncover include:


- Unknown or “orphaned” assets that no one owns but are still live on the internet
- Outdated software and configurations on public-facing systems
- Overly permissive access to admin portals, APIs, and management interfaces
- Inconsistent controls between on-premises and cloud, or between different business units


Each one of these gaps represents an opportunity for an adversary to gain initial access with minimal effort.


#### How Falcon Exposure Management Uncovers Risk


CrowdStrike Professional Services uses Falcon Exposure Management to uncover and validate these risks as part of the Technical Risk Assessment.


Falcon Exposure Management continuously discovers and maps internet-facing assets — domains, IP ranges, cloud services, and more — and correlates them with vulnerabilities, misconfigurations, and threat intelligence. This gives us a view of the external attack surface.


During a Technical Risk Assessment, our consultants:


1. Enumerate the organization’s external footprint using Falcon Exposure Management to identify known and unknown assets.
2. Prioritize exposures based on exploitability and adversary behavior, focusing on the paths real attackers are most likely to use.
3. Validate risk with hands-on analysis, confirming what an attacker could see and do from the outside.
4. Deliver clear recommendations outlining which issues to fix first and how to close high-risk internet-facing gaps.


The result is an evidence-based view of the external attack surface and a prioritized roadmap to reduce the risk of a breach starting from an exposed asset on the public internet.


### Applications and Vulnerabilities


When we review applications and vulnerabilities during a Technical Risk Assessment, we rarely find a lack of tools. Most organizations have endpoint detection and response (EDR), vulnerability scanners, and patch management platforms. The challenge they most often face is the gap between finding issues and fixing them within a defined window.


The most common pattern we see is critical vulnerabilities on “managed” assets. Even on systems covered by endpoint sensors and vulnerability scanners, we routinely find critical-severity CVEs that have been open for weeks or months. These are often on business-critical servers and externally reachable systems.


Patching is often treated as best-effort instead of a measured commitment. Technical Risk Assessments frequently find organizations lacking clear, risk-based SLAs for remediation, or SLAs that exist on paper but aren’t tracked and enforced in practice.


Our recommendation is straightforward:


- Establish explicit SLAs for vulnerability remediation based on severity, exploitability, and exposure — for example, internet-facing and business-critical assets are held to the tightest timelines.
- Continuously measure against those SLAs so security and IT teams can see where patch debt is accumulating.


In a Technical Risk Assessment, our team uses Falcon Exposure Management to surface these high-risk CVEs on managed assets, show where SLA breaches are concentrated, and give you a prioritized, evidence-based plan to close the most dangerous gaps.


### Accounts, Identity, and Configuration Hygiene


In almost every Technical Risk Assessment, we find identity hygiene issues create easy, high-impact paths for attackers. A few patterns repeatedly surface:


#### Noisy Remote Accounts on Home Networks


With today’s remote and hybrid workforce, many employees are accessing corporate resources from home networks that don’t have enterprise-grade security controls. In our assessments, we often see a small number of systems associated with remote workers generating a very high volume of login attempts.


These endpoints become magnets for credential stuffing and brute-force activity. Attackers repeatedly try username/password combinations against internet-reachable services, and nothing on the home Wi-Fi stops this activity at the perimeter. Without good monitoring and controls, this “background noise” can hide real compromise attempts and make it harder for defenders to spot malicious logins in time.


#### Kerberos Misconfigurations that Make Kerberoasting Trivial


Kerberos is foundational to how many organizations authenticate users and services — and there are many ways it can be misconfigured. In many environments, we see service accounts with weak passwords, legacy encryption settings, and excessive privileges.


Kerberoasting remains a go-to technique: Attackers request service tickets, take them offline, and try to crack them. When passwords are weak or never rotated, this becomes a reliable way to quickly turn a standard domain account into powerful access. Misconfigured Kerberos and weak service account passwords is a combination that dramatically lowers the bar for a successful compromise.


#### Active Directory as a Critical and Accessible Target


Most enterprises still rely on Active Directory (AD) as the backbone of their identity infrastructure. This makes AD a primary target for modern attackers. Once an adversary can control or abuse AD, they can move laterally, escalate privileges, and persist with relative ease.


In Technical Risk Assessments, we frequently uncover:


- Stale or orphaned accounts that still have access they no longer need
- Over-privileged service and admin accounts
- Weak or inconsistent password policies


Legacy configurations that were “good enough” years ago are dangerous today. Cleaning up AD, tightening identity configurations, and enforcing strong authentication and password hygiene are some of the most direct ways to reduce cyber risk.


## Patterns of Strong Security


Across hundreds of Technical Risk Assessments, the organizations in the strongest position tend to have a few things in common:


**A mapped and owned external attack surface:** They know which domains, IP ranges, cloud services, and internet-facing applications belong to them, and who owns each one. Falcon Exposure Management is used to continuously discover new assets and flag drift. It helps confirm nothing lives on the public internet without clear ownership, baseline controls, and a plan to remediate issues.


**Risk-based vulnerability management with real SLAs:** Vulnerability data is prioritized by exposure and adversary behavior. High-risk CVEs on critical and internet-facing systems have tight, enforced SLAs. Falcon Exposure Management helps correlate vulnerabilities with real-world context so teams can focus on what reduces breach likelihood.


**Clean, well-governed identities and directories:** Remote endpoints are monitored for unusual login activity, and policies account for the realities of home networks. Kerberos is configured securely, service account passwords are strong and rotated, and Kerberoasting-resistant configurations are in place. Active Directory is well-maintained: Stale accounts are removed, privileges are minimized, and configuration hygiene is continuously improved.


**Integrated visibility and a habit of continuous validation:** Security and IT teams work from a shared, current view of assets, vulnerabilities, and identities. Technical Risk Assessments are used as a recurring health check to validate that controls are behaving as expected, SLAs are met, and newly introduced technologies don’t silently expand risk.


## How We Help: CrowdStrike Technical Risk Assessment


The Technical Risk Assessment provides a unified view of exposure across the external attack surface, applications, vulnerabilities, accounts, identity, and configuration hygiene — powered by the CrowdStrike Falcon® platform.


**What the assessment delivers:**


- An executive‑ready report that summarizes exposure, business impact, and accountable owners
- Remediation details for each finding, mapped to real‑world adversary techniques
- A prioritized plan that scores every action by criticality and level of effort, so teams know what to fix first and how much work is required


**Platform capabilities behind the assessment:**


- Falcon Exposure Management to discover, assess, and act on risk across assets and the external attack surface
- CrowdStrike Falcon® Next-Gen Identity Security to reveal and close risky identity paths and Active Directory weaknesses
- CrowdStrike Falcon® for IT to query, manage, and remediate at scale across the environment


***Contact your CrowdStrike representative or complete this[form](https://www.crowdstrike.com/en-gb/services/request-information/) to schedule your Technical Risk Assessment.***


#### Additional Resources


- *Dive deeper into topics like this at[Fal.Con 2026](https://www.crowdstrike.com/en-us/events/fal-con/las-vegas/?utm_medium=evt&utm_source=blog&utm_campaign=fal-con-26&utm_term=crwdblogs&utm_language=en-us) with expert-led sessions, hands-on training, and real-world insights.*
- *Learn more about the[CrowdStrike Technical Risk Assessment Service](https://www.crowdstrike.com/en-gb/services/fortify/technical-risk-assessment/) ,[Falcon Exposure Management](https://www.crowdstrike.com/en-us/platform/exposure-management/) ,[Falcon Next-Gen Identity Security](https://www.crowdstrike.com/en-us/platform/next-gen-identity-security/) , and[Falcon for IT](https://www.crowdstrike.com/en-us/platform/falcon-for-it/) .*
