---
schema_version: "1.0.0"
document_id: "c88ca7e4a9df5ae0c720cf41f203ccc30206dc5aff95a4a2270d659ece36206b"
company_key: "yc-zepto"
company: "Zepto"
source_id: "yc-zepto-rss-8182f1493a2f"
canonical_url: "https://blog.zepto.com/catching-secrets-before-they-leak-how-we-built-an-end-to-end-secret-detection-system-at-scale-7bf1541801c7"
published_at: "2026-04-20T10:28:50+00:00"
first_seen_at: "2026-07-20T23:24:50.197566+00:00"
fetched_at: "2026-07-28T21:46:35.260607+00:00"
content_hash: "sha256:38d568565b755e5c8ffb967666f1378b7fdd7a664762cdb2ed0d075901b50ba8"
---

# Catching Secrets Before They Leak: How We Built an End-to-End Secret Detection System at Scale

# Catching Secrets Before They Leak: How We Built an End-to-End Secret Detection System at Scale


[Zepto Tech](https://medium.com/@tech.culture?source=post_page---byline--7bf1541801c7---------------------------------------)


9 min read


·


Apr 20, 2026


--


Press enter or click to view image in full size


> At Zepto, we move fast — shipping hundreds of commits across multiple services every day — and our sensitive surface area is extensive: code repositories, documentation platforms like Confluence, issue trackers like Jira, countless messages on communication channels such as Slack, and even serverless functions running critical logic. With this scale, even a single leaked API key or credential can quickly escalate into a security incident or compliance issue. Simply telling people “don’t commit secrets” or relying on a single CI check was not enough. As our development moves rapidly and our tech stack evolves constantly, we needed secret detection everywhere, keeping pace with both our code and infrastructure changes. This led us to build an in-house, end-to-end secret detection system.


Here is how we did it: the problem we were up against, the layers we added, how the **data flow** fits together, and what actually worked.


## The problem: scale and surface area


Press enter or click to view image in full size


Secret leaks don’t occur only in application code they can appear across multiple parts of the development and operational lifecycle:


- **Source Code —** Secrets committed to repositories (main branches, feature branches, forks, or even deleted history).
- **CI/CD Systems —** Exposure through job configurations, pipeline scripts, environment variables, and build parameters (e.g. GitHub Actions).
- **Documentation —** Sensitive data shared in Confluence pages, runbooks, design documents, or Jira tickets often temporarily during debugging but left behind.
- **Collaboration Tools —** Secrets accidentally shared via Slack messages, pasted configurations, screenshots, or shared snippets.
- **API & Testing Tools —** Credentials stored in Postman collections, environment variables, or shared workspaces.


Relying on a single checkpoint (e.g. only PR checks) has clear gaps:


- **Bypasses —** Hotfixes, config-only changes, and legacy repos might not go through the same path.
- **Late feedback —** Finding a secret in CI or after merge means rework, reverted commits, and rotation overhead.
- **Blind spots —** Docs, Slack, and Postman are outside the git pipeline entirely.


We wanted **early feedback** for developers, **broad coverage** across every surface, and a **unified view** so we could respond quickly when something slipped through. That led us to a **defense-in-depth** model: multiple overlapping layers, with a clear **data flow** from event → scan → alert → remediation.


## Architecture overview: layers and responsibilities


Everything described in this post — including scanners, hooks, pipelines, and alerting — is built and run in-house at Zepto. We organize it into four layers:


**Layer 1: Dev Env & Pre-Push Checks**
What it scans: Local files and code changes before commit or push.
Trigger: Keystroke, file save, pre-push Git hook.


**Layer 2: SCM / Repository Scans**
What it scans: Branches, pull request diffs, and pushed commits.
Trigger: Code push, PR creation or update.


**Layer 3: Serverless & Cloud Functions Monitoring**
What it scans: Lambda code, build artifacts, pipeline configs, environment variables.
Trigger: Deployment events, scheduled runs.


**Layer 4: SaaS & Collaboration Monitoring**
What it scans: Confluence pages, Jira tickets, Slack messages, Postman collections.
Trigger: Scheduled scans, webhooks, or content changes.


## Layer 1: Dev Env & Pre-Push Checks


**Goal:** Give developers instant feedback so secrets are never committed or pushed in the first place.


## IDE-level detection


- We have **in-house IDE integration** that scans on file save and can also be run on-demand from the IDE.
- When a potential secret is detected, the developer sees an **inline warning** or sidebar alert. No need to wait for CI or a reviewer.


This runs entirely on the developer’s machine; no code or content is sent to a central scanner at this stage.


Press enter or click to view image in full size


**Why it matters:** Catching a secret in the IDE before commit or push gives instant feedback. Developers fix it right where they wrote it, with no wait for CI or reviewers. It’s the earliest and least disruptive place to catch a leak.


## Pre-push hook checks


- Before any` git push` , a **local pre-push hook** runs our secret scanner over the commits being pushed.
- If any commit introduces a pattern that looks like a secret, the push is **blocked** and the developer gets a clear message (e.g. file + line or commit range).
- Only after fixing or confirming (e.g. false positive) can the push succeed.


Press enter or click to view image in full size


- **Why it matters:** Fixing a leak before the first push is the cheapest and least embarrassing. Developers learn what “good” looks like and rarely see Layer 2 or 3 fire for their own changes.


## Layer 2: SCM / Repository Scans


**Goal:** Ensure every branch and every PR is scanned, regardless of whether pre-push or IDE was used.


## PR-level checks


- Every **pull request** triggers our scanning pipeline (e.g. GitHub Action or CI job that runs a secret scanner on the PR diff).
- The result is a **status check** on the PR: pass or fail. No merge until the check passes (or is explicitly overridden with approval).
- We scan the **diff** (added lines) to keep noise down and focus on new exposure.


Press enter or click to view image in full size


## Push-level checks


- We use **secret scanning on every push** .
- Pushes to the` master` branch trigger secret scans on the latest commits.
- Developers are notified immediately if any secrets are found.
- The full codebase is periodically scanned to catch any missed secrets.


This layer catches cases where pre-push was skipped, where someone used` **--no-verify**` to bypass the hook, where someone pushes from a different machine, or where config/repo rules differ. It's the **mandatory gate** before code lands on main.


**Goal:** Backstop for everything that might have slipped through, and coverage for places that don’t go through PRs including **deployed Lambda functions** (code + env vars) across AWS accounts, legacy repos, infra scripts,.


## Serverless & Cloud Functions Monitoring


**Goal:** Backstop for everything that might have slipped through, and coverage for deployed workloads that don’t go through PRs including **deployed Lambda functions** (code + env vars) across AWS accounts.


The **Lambda Secret Scanner** is a centralized, real-time security scanning system that automatically detects hardcoded secrets (API keys, passwords, tokens, credentials) in **AWS Lambda function code and configuration** across multiple AWS accounts.


**Why we needed it:** Deployments don’t only go through CI/CD they also happen via the AWS Console (“clickops”) or CLI/SDK, so pipeline-only checks miss a lot. Secrets can land in dozens of accounts, and they’re not just in code: they show up in **Lambda environment variables** too. Manual reviews don’t scale, and finding secrets only during a code review (if at all) means they may already have been exposed for days or weeks. We needed **real-time detection** and **central visibility** across all accounts.


## Get Zepto Tech’s stories in your inbox


Join Medium for free to get updates from this writer.


Remember me for faster sign in


**What it does:**


- **Real-time detection —** Scans Lambda functions right after deployment, so we catch secrets as soon as they’re deployed.
- **Multi-account support —** Hub-and-spoke architecture covering Dev, UAT, Prod (and any other) accounts from one place.
- **Code + configuration —** Scans both the function **code** (.zip) and **configuration** (e.g.` .json` environment variables), not just source.
- **Zero friction —** Asynchronous scanning doesn’t block deployments; we alert after the fact.
- **Automated alerting —** Instant Slack notifications when secrets are detected, plus optional ticketing.
- **Audit trail —** Full history of deployments and scan results stored in S3 for compliance and forensics.


We track state (new vs. known false positive vs. remediated) so we don’t spam on the same finding.


## Layer 4: SaaS & Collaboration Monitoring


**Goal:** Don’t leave the biggest collaboration and API surfaces unchecked.


## Confluence and Jira Secret Scanning


- We built an **in-house** automated scanner that **continuously monitors Jira and Confluence in real time** , detecting secrets as soon as content is created or updated so we catch credentials before they spread.
- **Real-time detection —** No batch or schedule delay; we scan on create/update via APIs and alert within seconds.
- **Fewer false positives —** Suspected secrets are **verified against relevant APIs** where possible, so we don’t flood the team with noise.
- **Fast alerting —** Security gets **Slack notifications within seconds** ; we can also map findings to page/ticket, auto-create a Jira security ticket, or notify page owners.


The goal is to stop credential leaks in docs and tickets from turning into incidents by finding them the moment they appear.


Press enter or click to view image in full size


## Slack Secret Scanning


- We built an **in-house Slack secret scanner** that scans messages for secret patterns across Slack.
- It can scan **public channels** and **private channels (on consent)** so we get coverage where we need it while respecting privacy and access.
- When a potential secret is detected, we **alert** the security channel and optionally notify the sender (with guidance to rotate and remove). Data handling follows our privacy and compliance policies.


Press enter or click to view image in full size


## Postman Monitor


- We built an in-house system at Zepto to monitor API collections and workspaces (including shared or external-facing) for exposed credentials, keys, or environment variables.
- The system periodically retrieves collection data and scans for potential secrets.
- Any findings are treated like standard secret alerts: notify users, rotate keys, and remove exposures.
- Both scheduled and manual scans are supported to catch accidental exposures promptly.


## End-to-end data flow: how it all fits together


Below is a **unified data flow** from “developer action” and “system events” through to “alert and remediation.” Everything flows toward a **central place** (dashboard, Slack, or ticketing) so we can see and act on findings at scale.


## Data flow by stage (what moves where)


Here’s the **minimal version without “Runs On”** :


Press enter or click to view image in full size


## Scaling considerations: what we had to get right


## 1. Pattern set and false positives


- We use a **common pattern set** (regex + format validators) across all layers so behavior is consistent and we tune once.
- We maintain an **allowlist / false-positive registry** (e.g. example keys, test values) so we don’t alert on the same known-safe value in every repo or doc.
- At scale, **reducing noise** was as important as coverage; otherwise alerts get ignored.


## 2. Performance and coverage


- **Lambda:** We scan repos in chunks, use shallow clones or API where possible, and fan-out with multiple invocations so we stay within time and memory limits.
- **PR/CI:** We only scan the **diff** and cache where possible so we don’t slow down every build.
- **Confluence/Jira/Slack:** We paginate and rate-limit API calls so we don’t hit limits or overload our own services.


## 3. Central visibility


- Every layer that can send findings **feeds the same store or channel** . That way we have one place to see “all secret exposure” and can dedupe, assign, and track remediation.
- For every secret we **post to a dedicated Slack channel and auto @mention the responsible user** (committer, PR author, or page owner) so they’re looped in immediately and the security team sees all activity in one place.
- We tag findings by **source** (IDE, PR, Lambda, Confluence, etc.) and **severity** so we can prioritize and report on where leaks happen most.


## 4. Privacy and compliance


- **IDE and pre-push** run locally; we don’t send code or pastes to a central server at that stage.
- For **Slack and docs** , we defined what we scan and who gets access to findings so we stay within privacy and compliance expectations.


## What we learned


1. **Shift left pays off —** The earlier we catch (IDE, pre-push), the less rework and the better developer experience. Most engineers now fix secrets before push without thinking about it.
2. **One pattern set, many layers —** Reusing the same rules everywhere made tuning and allowlisting manageable and kept behavior predictable.
3. **Coverage over perfection —** We’d rather scan “everything” (code, docs, chat, APIs) with good-enough rules than have one perfect scanner that only sees repos.
4. **Central aggregation is critical —** Without a single place for findings, we’d have alerts scattered across GitHub, Slack, email, and dashboards; dedupe and remediation would be much harder at scale.
5. **Data flow clarity —** Documenting exactly what triggers each layer, what data is read, and where results go made it easier to onboard new tools and explain the system to security and compliance.
6. **In-house from day one —** Building and running it ourselves gave us full control over patterns, integrations, and alerting no black box, no vendor lock-in.
