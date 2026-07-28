---
schema_version: "1.0.0"
document_id: "4d8898e7ac874c7438e36b11ee10367f7e4d4dd20dfec895f41e0a8a0e665479"
company_key: "crowdstrike-holdings-inc-class-a-common-stock"
company: "CrowdStrike Holdings Inc. Class A Common Stock"
source_id: "crowdstrike-holdings-inc-class-a-common-stock-news-import-26dc963e5592"
canonical_url: "https://www.crowdstrike.com/en-us/blog/crowdstrike-zscaler-bring-continuous-identity-security-to-zero-trust-access/"
published_at: null
first_seen_at: "2026-07-25T01:07:09.054440+00:00"
fetched_at: "2026-07-28T21:36:14.883471+00:00"
content_hash: "sha256:be32a104d4ca42103f8b689acab29e08ec086ff97c01fada23a5d17f2b248b07"
---

# CrowdStrike and Zscaler Bring Continuous Identity to Zero Trust Access

Modern adversaries are accelerating attacks across identities, endpoints, cloud environments, and SaaS applications, often moving faster than security teams can respond. Identity has become a primary attack vector as attackers leverage credential abuse to evade detection and expand their foothold. Stopping today’s threats requires visibility and context across every domain to accurately assess risk before adversaries can move laterally.


Without comprehensive visibility, rich threat context, and coordinated response, security teams are left managing disconnected tools and manually correlating signals. This leads to slower response — and gives adversaries a larger window to act.


That's why CrowdStrike and Zscaler continue to deepen their strategic partnership. Together, the two platforms bring together AI-native cybersecurity and Zero Trust to help organizations stop cross-domain attacks, reduce complexity, and strengthen security across the enterprise.


Today, we're previewing a new integration coming soon between CrowdStrike Falcon® Next-Gen Identity Security and Zscaler that helps organizations adapt access based on real-time identity risk. Powered by CrowdStrike’s Continuous Identity approach, the CrowdStrike Falcon® platform continuously evaluates user risk and shares that context with Zscaler's Adaptive Access Engine (AAE) to enable real-time, risk-based access decisions across the Zero Trust Exchange.


Unlike traditional identity solutions that rely primarily on authentication events, CrowdStrike's Continuous Identity approach evaluates risk using signals across identity, endpoint, cloud, SaaS, and threat intelligence domains. This richer context enables organizations to make more informed access decisions and respond to emerging threats in real time.


## Stop Identity-Driven Attacks Before They Spread


Detecting risk is only half the battle. Security teams must act on that risk before attackers can access critical applications or move laterally across the environment.


The new Falcon Next-Gen Identity Security integration continuously shares real-time risk signals from the CrowdStrike Falcon® platform with Zscaler using open standards, including the[OpenID Shared Signals Framework](https://openid.net/specs/openid-sharedsignals-framework-1_0-final.html) (SSF) and[Continuous Access Evaluation Profile](https://www.crowdstrike.com/en-us/cybersecurity-101/identity-protection/continuous-access-evaluation-profile-caep/) (CAEP). When Falcon Next-Gen Identity Security identifies high-risk activity, such as a malicious script execution or suspicious user behavior, Zscaler can automatically adjust access policies based on the user's current risk posture — no manual intervention required.


See it in action:


Here's how it works in practice:


1.


A user activity triggers a detection in Falcon Next-Gen Identity Security; for example, due to suspicious credential activity, a brute-force attempt, impossible travel, or malicious execution on a device.


2.


Falcon Next-Gen Identity Security continuously evaluates user risk by correlating identity, endpoint, and threat signals to determine when access policies should adapt to changing risk conditions.


3.


A rule configured in Falcon Next-Gen Identity Security's CAEP Hub triggers a risk level change event, which is sent to Zscaler in real time.


4.


Zscaler AAE receives the elevated risk signal and reevaluates the AAE profile to take appropriate actions, such as automatically blocking the user's access to sensitive resources, like a code repository or requiring step-up authentication.


5.


When the incident is resolved and risk decreases, the Falcon platform sends an updated signal to Zscaler, and access is automatically restored.


With this integration, organizations can dynamically restrict access to sensitive resources, prevent lateral movement, and automatically restore access in real time once risk has been mitigated without manual intervention.


## Turn Security Signals into Security Outcomes


Modern attacks don't stay in one place. A compromised endpoint can quickly escalate into identity abuse, unauthorized access, and broad organizational compromise. The longer it takes to respond, the greater the business risk.


Together, CrowdStrike and Zscaler give security leaders a unified defense that detects threats earlier across endpoint, identity, network, and additional domains, and automatically shares risk context in real time to enforce access decisions the moment circumstances change. The result is seamless interoperability, stronger cross-domain visibility, and the ability to stop attacks before they become breaches.


As adversaries grow faster and more sophisticated, the ability to act on risk across every domain, without manual intervention, is a business imperative. The upcoming Falcon Next-Gen Identity Security integration extends CrowdStrike and Zscaler's shared vision of unified defense by bringing CrowdStrike’s Continuous Identity approach to Zero Trust access, which will help organizations continuously adapt access as risk changes, automatically and at scale.


**Disclaimer**


*This content includes discussion of unreleased services or features. Any references to unreleased features reflect our current plans only and do not constitute a promise or commitment to deliver such features. These items may change or may not be made available in all regions. Customers should make purchase decisions based on features currently available.*


#### Additional Resources


- *Be part of[Fal.Con 2026](https://www.crowdstrike.com/en-us/events/fal-con/las-vegas/?utm_medium=evt&utm_source=blog&utm_campaign=fal-con-26&utm_term=crwdblogs&utm_language=en-us) and connect with 10,000+ cybersecurity professionals shaping the future of the industry.*
- *Explore the[Falcon Next-Gen Identity Security](https://www.crowdstrike.com/en-us/platform/next-gen-identity-security/) product page.*
- *Download the[Complete Guide to Next-Gen Identity Security](https://www.crowdstrike.com/en-us/resources/white-papers/complete-guide-to-next-gen-identity-security/) .*
