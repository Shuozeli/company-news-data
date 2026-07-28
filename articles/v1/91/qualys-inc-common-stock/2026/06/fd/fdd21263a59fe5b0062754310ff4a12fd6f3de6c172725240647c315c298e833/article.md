---
schema_version: "1.0.0"
document_id: "fdd21263a59fe5b0062754310ff4a12fd6f3de6c172725240647c315c298e833"
company_key: "qualys-inc-common-stock"
company: "Qualys Inc. Common Stock"
source_id: "qualys-inc-common-stock-news-import-04a5e6e88fc1"
canonical_url: "https://blog.qualys.com/qualys-insights/2026/06/15/what-changed-in-owasp-top-10-2025-and-recommendations-for-each-category"
published_at: "2026-06-15T16:00:00+00:00"
first_seen_at: "2026-07-22T10:38:12.541071+00:00"
fetched_at: "2026-07-28T21:23:21.398471+00:00"
content_hash: "sha256:9d254d2e488500e2274e059a1c0a508040c0b160c41e37302dae211bc7de4659"
---

# What Changed in OWASP Top 10 2025 and Recommendations for Each Category

#### Table of Contents


- OWASP Top 10 2025 VS. 2021 Category Mapping
- OWASP Top 10 2021 vs 2025 at a Glance
- The Full Breakdown of What Changed in OWASP Top 10 2025
- Reading OWASPs Recommendations is the Easy Part
- Qualys TotalAppSec Helps Address These Operational Challenges
- What Your Program Does Next Matters
- Frequently Asked Questions


### **Key Takeaways**


1. The 2025 list introduces two new categories – Software Supply Chain Failures (A03) and Mishandling of Exceptional Conditions (A10) – reflecting attacks already happening in production.
2. Security Misconfiguration jumping from #5 to #2 signals that continuous deployment without continuous scanning creates active exposure windows.
3. Broken Access Control (A01) now explicitly covers BOLA and BFLA API authorization failures – the most exploited patterns in modern API-heavy applications.
4. OWASP recommendations are sound, but assume unified tooling, continuous coverage, and mature SDLC discipline that most AppSec programs still lack.
5. A03 (Software Supply Chain Failures) has the highest incidence rate (5.19%), but very low CVE coverage – attacks are happening while scanners lack signatures.
6. Programs that close operational gaps category-by-category will enter the next audit cycle with a defensible posture.


The OWASP Foundation has released the[eighth edition of its Top 10](https://owasp.org/Top10/2025/) Web Application Security Risks. This is the first major update since 2021, and was built on analysis of more than 175,000 CVE records and 589 Common Weakness Enumerations.


Two entirely new OWASP Top 10 2025 categories entered the list, and several rankings shifted significantly. One category was consolidated into another. The complete breakdown of OWASP Top 10 changes 2025 follows below, category by category. But the more important aspect is what those changes say about where attacks are happening right now, and what your AppSec program should do about each one.


This post breaks down every category in the 2025 list, what OWASP recommends for addressing each, and the operational realities that make those recommendations harder to apply than they look.


## OWASP Top 10 2025 VS. 2021 Category Mapping


## OWASP Top 10 2021 vs 2025 at a Glance


### Key shifts include:


- A02 Security Misconfiguration surged from #5 to #2
- A03 Software Supply Chain Failures — new category at #3 with highest incidence rate
- A10 Mishandling of Exceptional Conditions — new category
- A01 Broken Access Control remains #1 and now explicitly includes BOLA and BFLA


## The Full Breakdown of What Changed in OWASP Top 10 2025


### A01: Broken Access Control – Remains #1, Now Explicitly Covers BOLA and BFLA


Broken Access Control retains the top spot, with a significantly expanded scope. It now includes Server-Side Request Forgery (SSRF), privilege escalation, account takeover, and unauthorized data access across API endpoints. Two authorization failure patterns now fall squarely within this category: Broken Object Level Authorization (BOLA), which lets attackers access another user’s data by manipulating object references in API calls, and Broken Function Level Authorization (BFLA), where lower-privileged users invoke admin-level API functions by calling endpoints directly. These aren’t edge cases. They’re among the most exploited patterns in API-heavy applications, and exactly the surface most traditional DAST tools weren’t built to test.


Open banking mandates ([PSD2 in the EU](https://www.eba.europa.eu/regulation-and-policy/payment-services-and-electronic-money) , the[UK’s FCA-governed Open Banking Standard](https://www.openbanking.org.uk/) , and[RBI’s Account Aggregator framework in India](https://sahamati.org.in/) ) have multiplied API endpoints across financial services without proportional testing coverage. That’s exactly the surface this category exploits. In healthcare, patient portal APIs that weren’t threat-modeled at design grant unauthorized access through endpoints periodic web scans never reach. Any detection scope, compliance report, or audit documentation still treating SSRF as a separate category is now out of date.


**OWASP Recommends:** Run access control checks in server-side code that an attacker can’t tamper with, never in the browser or client. Deny by default, with exceptions only for resources meant to be public. Build a single, reusable access control layer rather than scattering checks across the codebase and keep cross-origin sharing tightly scoped. Your access control model should enforce that users can only act on records they own, instead of allowing actions on any record they can reference. Log every access control failure and trigger alerts when failures cluster on a single account or endpoint. Rate-limit your APIs and controllers. After logging out, invalidate session identifiers on the server; for stateless JWTs, keep token lifetimes short. Treat functional access control as a first-class test case in your unit and integration suites.


### A02: Security Misconfiguration – Surges from #5 to #2


Security Misconfiguration is the OWASP 2025 category with the most striking data point: 100% of tested applications showed some form of misconfiguration, with an average incidence rate of 3.00%. The category covers insecure default settings, open cloud storage buckets, misconfigured HTTP headers, and verbose error responses exposing stack traces, environment variables, and internal architecture.


The jump reflects deployment reality more than developer behavior. In retail and e-commerce, misconfigured cloud storage buckets have exposed millions of customer records without a single line of malicious code written. In SaaS and technology companies, every CI/CD-provisioned service is a potential misconfiguration surface, and most teams scan intermittently while continuously deploying. The gap between scans isn’t a compliance footnote. It’s an active exposure window.


**OWASP Recommends:** Build a hardening process that is repeatable, scripted, and identical across development, QA, and production. Only the credentials should differ. Ship a minimal platform: strip out unused features, components, sample apps, and documentation. Fold configuration review into your patch management cycle, including cloud storage permissions. Use network segmentation, containerization, or cloud security groups to keep components and tenants isolated. Enforce security through HTTP headers. For credentials, lean on identity federation, short-lived tokens, or platform-native role-based access rather than embedding static keys or secrets inside code, config files, or pipelines.


### A03: Software Supply Chain Failures – New, Highest Incidence Rate, Lowest CVE Coverage


**Software Supply Chain Failures** is OWASP’s new A03 category, addressing the full software supply chain: third-party dependencies, build systems, CI/CD pipelines, and update and delivery mechanisms. It carries the highest average incidence rate of any category at 5.19%, but only 11 CVEs map to related CWEs. That gap (attacks happening in production, while scanners lack the signatures to flag them) is what makes it dangerous.


The 2020 SolarWinds breach reached thousands of downstream organizations through a compromised build update, arriving via a legitimate, signed software update that bypassed signature-based detection. Magecart-style attacks inject malicious JavaScript into checkout pages through compromised third-party scripts. A03 entering the list with the highest incidence rate isn’t a warning about future risk; it’s a finding about current exposure.


**OWASP Recommends:** Centrally generate and manage an SBOM, tracking direct and transitive dependencies. Remove unused dependencies. Continuously monitor CVE, NVD, and OSV sources for component vulnerabilities. Only obtain components from official, trusted sources; prefer signed packages. Monitor unmaintained libraries; consider migration or virtual patching where patches aren’t available. Use staged rollouts or canary deployments to limit blast radius. Harden code repositories, developer workstations, build servers, and artifact repositories. Enable MFA, sign artifacts, and ensure immutable builds.


### A04: Cryptographic Failures – Drops from #2 to #4


Covers weak or absent encryption for data in transit and at rest, broken algorithms, inadequate key management, and unencrypted sensitive fields. The drop reflects better industry adoption of baseline encryption, not reduced consequences when failures occur. For regulated industries, this remains a direct path to PCI DSS, HIPAA, and GDPR exposure.


**OWASP Recommends:** Inventory the data your application handles and classify it by sensitivity, regulation, and business value. Keep your most sensitive keys in a hardware or cloud HSM. The less sensitive data you retain, the less you can lose, so discard, tokenize, or truncate aggressively. Encrypt sensitive data at rest and use TLS 1.2 or higher with forward-secrecy ciphers in transit, with HSTS enforced for HTTPS. Hash passwords with adaptive, salted algorithms like Argon2, scrypt, or PBKDF2, not MD5 or SHA1. Avoid CBC mode and other deprecated primitives. Use authenticated encryption rather than encryption alone. OWASP also advises beginning post-quantum cryptography preparation now, with high-risk systems PQC-safe no later than the end of 2030.


### A05: Injection – Drops from #3 to #5


SQL injection, NoSQL injection, and Cross-Site Scripting (XSS) remain among the most actively exploited vulnerabilities in production. The lower ranking reflects better tooling coverage, not reduced attacker interest. The persistent gap is API parameter coverage. DAST tests web front-end forms while leaving the API endpoints behind them untouched. In most enterprise applications today, the API layer is where most user input actually enters, which is exactly the surface that goes untested.


**OWASP Recommends:** Use safe APIs that avoid the interpreter entirely or provide a parameterized interface, including ORMs. Note that even parameterized stored procedures can introduce SQL injection if they concatenate queries with data. Use positive server-side input validation. For residual dynamic queries, escape special characters using interpreter-specific escape syntax. Note that SQL structure names (tables, columns) can’t be escaped, so user-supplied structure names remain dangerous.


### A06: Insecure Design – Drops from #4 to #6


Architectural security failures: missing threat modeling, inadequate security requirements in the SDLC, systems designed without security-by-default principles. Detection tools can’t retroactively redesign architecture or surface flaws baked in during requirements and design. Teams that integrate threat modeling into design reviews before code is written are the ones that don’t spend the next quarter in remediation. They catch authorization logic failures, trust boundary errors, and missing requirements at the point where fixing costs days, not months.


**OWASP Recommends:** Run a secure development lifecycle with AppSec professionals involved in evaluating security and privacy controls. Build an internal library of vetted, pre-approved “paved road” components: secure-by-default building blocks that teams can pick up without reinventing controls. Use threat modeling for the parts of the application that matter most: authentication, access control, business logic, and key data flows. Treat threat modeling as an educational tool, not just a checklist. Bake security requirements into user stories. Add validation checks at every tier of the application. Write tests that cover both intended use-cases and misuse-cases. Use system and network segregation to enforce tier and tenant boundaries.


### A07: Authentication Failures – Holds at #7


Credential stuffing, brute-force attacks, and session hijacking remain consistently exploitable. The exploited failure often isn’t the login page. It’s an API endpoint handling token validation, or a machine-to-machine authentication path outside the testing scope. For API-heavy applications, authentication testing needs to go well beyond web login flows.


**OWASP Recommends:** Enforce multi-factor authentication wherever you can. Don’t ship products with default credentials in place. Check new and changed passwords against known-breached credential lists. Align password policies with NIST 800-63b, and don’t force users to rotate passwords on a schedule unless you suspect a breach. Make sure registration, password reset, and other auth-related endpoints return identical responses for valid and invalid users, so attackers can’t enumerate accounts. Throttle or progressively delay failed login attempts. Use a server-side session manager that issues high-entropy session IDs after logging in. Where possible, transfer authentication risk by using a hardened, well-tested third-party identity system. For JWTs, validate the aud, iss claims and scopes. Don’t trust unverified token payloads.


### A08: Software or Data Integrity Failures – Holds at #8


Covers failures to verify application trust at runtime and delivery: unsigned updates, insecure deserialization, CI/CD pipelines that don’t verify artifact integrity before deployment. Frequently confused with A03, but the operational distinction matters. A03 is dependency-level supply chain failures. A08 is whether your application and delivery mechanism verify integrity at runtime. Addressing one without the other leaves a gap that attackers exploit simultaneously across both vectors.


**OWASP Recommends:** Use digital signatures or similar mechanisms to verify that software and data are from the expected source and unaltered. Ensure libraries and dependencies consume only from trusted repositories; host an internal vetted repository for higher-risk profiles. Implement a review process for code and configuration changes. Ensure the CI/CD pipeline has proper segregation, configuration, and access control. Don’t accept unsigned or unencrypted serialized data from untrusted clients without integrity checks.


### A09: Security Logging and Alerting Failures – Holds at #9


The 2025 update renamed this from “Monitoring” to “Alerting”, and the word change signals intent. Logs that sit in a bucket without triggering a response aren’t a detection capability. They’re evidence collection for the post-mortem. If your MTTD and MTTR are getting asked about up the chain, this is the category that moves them.


**OWASP Recommends:** Log all login, access control, and server-side input validation failures with enough context to identify suspicious accounts. Log every part of the application containing a security control, success or failure. Generate logs in a format log management solutions can consume. Maintain audit trails with integrity controls for all transactions. Roll back and restart transactions that throw errors. Always fail closed. Issue alerts on suspicious behavior. Establish monitoring and alerting use cases with playbooks. Add honeytokens: any access generates near-zero-false-positive alerts. Adopt an incident response plan, such as NIST 800-61r2.


### A10: Mishandling of Exceptional Conditions – New


The most practitioner-driven addition to the 2025 list. Covers improper error handling, fail-open logic, and systems that expose sensitive data, or grant unintended access, under abnormal conditions. Added through community vote: security engineers are seeing these exploits in production before automated tools have signatures. Applications that fall back to permissive defaults when an authentication service is unreachable. Error responses that include full stack traces, database schemas, or internal IP ranges, exactly the reconnaissance data an attacker needs. Systems should be designed to fail closed. Scanning needs behavioral coverage that goes beyond known vulnerability signatures.


**OWASP Recommends:** Plan for exceptional conditions. Catch every possible error at the point where it occurs, and handle it meaningfully (recover, log, alert if justified). Maintain a global exception handler as a backup. Roll back transactions completely if interrupted partway through (fail closed). Add rate limiting, resource quotas, and throttling to prevent exceptional conditions in the first place. Implement centralized error handling: one application shouldn’t have multiple ways of handling exceptional conditions. Perform threat modeling in design, plus code review, static analysis, stress testing, and penetration testing.


---


#### Qualys Webinar


### Watch how TotalAppSec addresses the discovery blind spots, scan cadence gaps, and authentication coverage failures the 2025 categories expose.


Watch Now


---


## Reading OWASP’s Recommendations is the Easy Part


The OWASP Top 10 2025 recommendations assume things most programs don’t have: continuous scanning that keeps pace with daily deployments, detection that works without a prior signature, authentication testing that follows OAuth2 and JWT into the endpoints that get attacked, unified coverage across web and API surfaces, and a secure-design foundation already in place.


### Fragmented tooling


A typical AppSec stack includes a DAST scanner, separate API testing, SAST, SCA, a SIEM, GRC, and ticket-routing through Jira or ServiceNow. They often don’t work together, and the gaps between them are where high-impact findings stay open longer than they should, and where OWASP’s “log, alert, route to response” guidance for A09 quietly breaks down.


### Accelerated release cycles


A02’s jump to #2 is the structural proof. Most AppSec teams scan weekly while engineering deploys multiple times a day. Every gap between scans is an exposure window. OWASP recommends automated configuration verification across all environments, but continuous scanning is operationally hard when scans take hours.


### Modern auth and crypto outpace standard DAST


A07 calls for MFA enforcement, JWT claim validation, breached-credential checks, and account enumeration prevention. A04 calls for TLS 1.2+ with forward secrecy, modern password hashing, deprecated-primitive avoidance, and post-quantum cryptography preparation. Most DAST tools weren’t built to test the full set, and audit cycles surface the gaps after the fact, not before.


### Behavioral and supply chain detection


A03 and A10 both require detection beyond known signatures. OWASP recommends SBOM generation, dependency monitoring, behavioral coverage for error handling, and runtime integrity verification, but most AppSec programs don’t have unified tooling for any of them.


### “Shift left” doesn’t help if the foundation isn’t there


A06 and the design-phase guidance threaded through A01, A07, and A08 all assume threat modeling, secure SDLC discipline, and paved-road components are already in place. For most teams, they aren’t. The recommendations are sound; the organizational maturity to act on them is the gap. Each challenge has a tactical answer. The harder question is whether your tooling and processes are unified enough to address them together, before the next breach or audit cycle forces the issue.


## Qualys TotalAppSec Helps Address These Operational Challenges


[Qualys TotalAppSec](https://www.qualys.com/apps/totalappsec) is built to address all 10 OWASP 2025 categories from a single platform: AI-powered DAST and dedicated API security testing for the application-layer categories, deep learning–based Web Malware Detection for supply chain and runtime integrity, continuous discovery for assets and APIs that periodic scans miss, and TruRisk prioritization to focus remediation on findings that actually threaten the business.


For teams running multiple AST tools,[Enterprise TruRisk Management (ETM)](https://www.qualys.com/apps/enterprise-trurisk-management) ingests TotalAppSec findings alongside DAST results from Checkmarx One and Veracode in one risk view, without a rip-and-replace decision. The full category-by-category mapping is covered in the next blog.


## What Your Program Does Next Matters


The 2025 list is built on four years of real-world breach data. The new categories, reshuffled rankings, and expanded CWE coverage reflect what is already being exploited in production. Programs that walk through each category and close operational gaps will enter the next audit cycle with a defensible posture.


Each challenge has a tactical answer. The harder question is whether your tooling and processes are unified enough to address them together, before the next breach or audit cycle forces the issue.


The follow-up to this blog, ***Is Your AppSec Program Built to Close the OWASP Top 10 2025 Coverage Gap?*** maps every OWASP Top 10 2025 category to TotalAppSec’s coverage capabilities — detection method, what gets tested, and where scanner-based programs typically fall short.


---


#### Qualys Blog


### Read how TotalAppSec closes the discovery, authentication, and detection gaps the OWASP Top 10 2025 categories expose.


Read Now


---


## Frequently Asked Questions


### What is new in OWASP Top 10 2025?


Two new categories were added – Software Supply Chain Failures (A03) and Mishandling of Exceptional Conditions (A10). Several rankings shifted significantly, and Broken Access Control now explicitly covers BOLA and BFLA API authorization failures.


### Why did Security Misconfiguration jump from #5 to #2 in OWASP 2025?


Because teams deploy continuously, but scan intermittently. Every gap between scans is an active exposure window – and OWASP found 100% of tested applications showed some form of misconfiguration.


### What is the difference between A03 and A08 in OWASP 2025?


A03 is dependency and supply chain failures. A08 is runtime and delivery integrity verification. Both need to be addressed – fixing one without the other leaves a gap attackers exploit across both vectors simultaneously.


### Why is Injection ranked lower in 2025, despite still being actively exploited?


Better front-end tooling coverage moved the ranking down – but API parameter inputs remain largely untested, which is where injection risk actually lives in most modern applications.


### What does OWASP 2025 recommend for post-quantum cryptography?


Begin preparation now. High-risk systems should be post-quantum safe no later than the end of 2030.


### What is the biggest operational challenge with OWASP 2025 recommendations?


The recommendations assume unified tooling, continuous scanning, and mature SDLC discipline. Most AppSec programs have fragmented stacks and periodic scans – which is exactly the gap the 2025 list was built on real breach data to expose.
