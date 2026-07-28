---
schema_version: "1.0.0"
document_id: "d355f30f4e65558a92fbb50ce7a9532cdab676f2aaef8223dc504df5fb147123"
company_key: "avepoint-inc-class-a-common-stock"
company: "AvePoint Inc. Class A Common Stock"
source_id: "avepoint-inc-class-a-common-stock-rss-485a4e1b5f08"
canonical_url: "https://www.avepoint.com/blog/backup/3-2-1-backup-rule"
published_at: "2026-04-30T13:00:00+00:00"
first_seen_at: "2026-07-20T23:21:42.943226+00:00"
fetched_at: "2026-07-28T21:45:24.644708+00:00"
content_hash: "sha256:062f12ea29a342ca8e38c31f1aaa561151c6efdc515144c0e7978a1ddc685561"
---

# What Is the 3-2-1 Backup Rule? A Complete 2026 Guide

The 3-2-1 backup rule is a data protection strategy: keep three copies of your data on two different storage types, with one copy stored off-site. It reduces the risk of total data loss from hardware failure, ransomware, or disaster. The rule applies to all data environments, including Microsoft 365, which Microsoft does not comprehensively back up on your behalf, making 3-2-1 a foundational control for IT, security, and compliance teams responsible for data resilience.


## Key Takeaways


- **3-2-1 defined.** This backup rule refers to maintaining three copies of data on two storage types, with one copy off-site. It eliminates single points of failure across hardware, media, and location.
Ransomware changes the calculus. Ransomware will target backup copies on the network as well as production data. At least one copy must be immutable or offline to be ransomware resistant.
- **SaaS Apps and cloud vendors don’t provide comprehensive, customer-controlled backups.** Microsoft, Salesforce, Amazon, Google, and other SaaS vendors’ shared responsibility models mean tenant data protection is largely managed by the customer.
- **3-2-1 applies to SaaS apps and cloud Infrastructure.** Your production copy is with the vendor. A third-party backup provides you with your second copy. By using cloud backup to store immutable off-site copies, you can easily meet the 3-2-1 best practices, but it might not be enough today.
- **Modern standards recommend 3-2-1-1-0.** This adds an immutable or air-gapped copy and requires zero unverified restores, widely referenced as a modern enterprise best practice.
- **Zero errors; test your restores.** A backup that has never been tested is not a backup. The “0 errors” requirement in 3-2-1-1-0 means automated verification is a best practice.


## What Is the 3-2-1 Backup Rule?


The 3-2-1 backup rule is a data protection guideline that states you should keep three total copies of your data, stored across two different media or storage types, with one copy located off-site. The rule was originally formulated by photographer Peter Krogh in the mid-2000s and has since become the standard framework for enterprise and SMB backup strategy.


The logic behind the rule is straightforward: It eliminates single points of failure. If one storage device fails, you have two other copies. If a local disaster destroys both on-premises copies, you have the off-site copy. If ransomware encrypts your primary environment, your off-site backup remains intact, provided it's isolated from the network.


Each number maps to a specific protection goal:


- **Three copies.** Your original data plus two backup copies. Having three copies ensures that even if two fail simultaneously, your data survives.
- **Two storage types.** Different storage media protect against type-specific failures. A redundant array of independent disks (RAID) failure that destroys your network-attached storage (NAS) won't affect a cloud-based copy.
- **One off-site copy.** A copy in a separate physical or logical location, typically cloud storage, protects against site-level events: fire, flood, theft, or a ransomware strain that spreads across local infrastructure.


## **Why Does the 3-2-1 Rule Still Matter in 2026?**


****


The 3-2-1 backup rule remains relevant in 2026 because the threats it was designed to address, hardware failure, accidental deletion, ransomware, and site-level disasters, have only intensified. Ransomware attacks


[increased by 37% year-on-year in 2025](https://www.verizon.com/business/resources/reports/2025-dbir-data-breach-investigations-report.pdf) , and the average cost of a data breach


[reached $4.44 million globally](https://www.ibm.com/reports/data-breach) . A well-implemented 3-2-1 strategy is one of the most cost-effective mitigations available.


When the rule was first formulated, the most common threats were hardware failure and accidental deletion. Today's threat landscape is more complex:


- Ransomware attacks can encrypt an entire environment within minutes, including connected backup targets.
- SaaS platforms like Microsoft 365 operate on a shared responsibility model: The vendor ensures platform availability, but data recovery is largely the customer's responsibility.
- Multicloud and hybrid environments create new data sprawl, making it easier to have gaps in backup coverage.


None of these threats requires abandoning the 3-2-1


framework,


they require extending it.


## **What Do the 3 Numbers Actually Mean?**


****


In the 3-2-1 backup rule, “3” means three total copies of your data (original plus two backups), “2” means those copies are stored on at least two different types of storage media or devices, and “1” means at least one copy is kept in an off-site or geographically separate location. Each number targets a distinct category of failure.


Here is how each component maps to a real-world failure scenario:


**Component** **What It Means** **Failure It Prevents**


**3 Copies** Original data + 2 backup copies


Single-device or single-copy loss


**2 Storage Types**


E.g., local NAS + cloud object storage


Media-type failure (e.g., RAID failure, tape degradation)


**1 Off-site Copy**


Cloud backup or a physically separate facility


Site-level events: fire, flood, ransomware spread


In modern implementations, "two different storage types" most commonly means a combination of:


- A local backup on NAS, storage-area network (SAN), or external drive
- A cloud backup in object storage (Azure Blob, AWS S3, or a managed backup service)


For SaaS workloads like Microsoft 365, Google Workspace, and


Salesforce


"local" and "cloud"


take


on a different meaning — covered in more detail in the SaaS applications sections below.


## How Does Ransomware Change the 3-2-1 Backup Rule?


Ransomware changes the 3-2-1 rule by exposing the weakness of any backup copy that remains network-accessible. Many modern ransomware strains are designed to identify and encrypt backup targets before attacking primary data. A 3-2-1 strategy that stores all three copies on internet-connected systems is significantly more vulnerable to modern ransomware attacks. The response is adding offline or immutable backup copies to the strategy.


Several well-documented ransomware variants, including Conti, LockBit, and BlackCat, specifically target backup software and connected storage before initiating the primary encryption phase. This means:


- A cloud backup that uses standard credentials, without immutability enabled, can be encrypted or deleted.


- A NAS-connected backup on the same network as the primary environment is at risk.


- Even SaaS backup tools that write to cloud storage are vulnerable if the cloud account is compromised.


The practical response: At least one of your backup copies should use immutable storage, where data cannot be altered or deleted during a defined retention window, even by an administrator with valid credentials.


## **What Are Immutable Backups and Why Do They Belong in a 3-2-1 Strategy?**


****


Immutable backups are backup copies that cannot be modified, encrypted, or deleted for a specified retention period, regardless of who tries to change them, including ransomware and administrators with full credentials. Immutability is typically enforced at the storage layer using write once, read many (WORM) policies in cloud object storage or purpose-built backup repositories. They are increasingly viewed as a baseline requirement in enterprise backup design.


Immutability is enforced differently depending on the backup platform:


- **Cloud object storage (Azure Blob, AWS S3).** Object lock policies prevent deletion or modification for a set period. Even a compromised admin account cannot override a locked object.
- **Purpose-built backup appliances.** Certain vendors offer repository-level immutability baked into their architecture.
- **SaaS backup platforms.** Third-party backup tools for Microsoft 365, Salesforce, and Google Workspace increasingly offer immutable storage tiers as a retention option.


## **What Is the 3-2-1-1-0 Rule?**


The 3-2-1-1-0 rule is a modern extension of the original framework, adding two critical requirements: 1 offline or air-gapped copy (to withstand ransomware that targets connected backup systems) and 0 errors (meaning all backups are verified and tested before they are needed). This variant has is commonly recommended for enterprise environments facing persistent ransomware threats.


The two additions address specific gaps the original rule doesn't cover:


- **+1 air-gapped or immutable copy.** An offline or logically isolated copy that ransomware cannot reach. This could be tape, a cold storage vault, or an immutable cloud backup where data cannot be overwritten or deleted for a defined retention period.
- **+0 errors.** Backup jobs that run successfully but fail during restore testing provide a false sense of security and increase recovery risk. The zero-error requirement means automated backup verification plays a critical role in the strategy


**Version** **Components** **Best For**


**3-2-1 (Classic)**


3 copies / 2 media / 1 off-site


SMBs, consumer data protection, low-threat environments


**3-2-1-1-0 (Modern)**


Above + 1 immutable/air-gapped + 0 unverified restores


Enterprise, regulated industries, high-ransomware-risk environments


## Does My Vendor Back Up My Data?


Microsoft, Google, Amazon, Salesforce, Atlassian, and other SaaS vendors do not perform full backup of customer data on your behalf by default. The vendor is responsible for the availability and infrastructure of the Microsoft 365 platform, but data recovery from user error, ransomware, or accidental deletion is the customer's responsibility. Microsoft's own documentation recommends that customers use third-party backup solutions to meet their data retention and recovery requirements.


This is the shared responsibility model, and it catches many organizations off guard. Here is a breakdown:


**What Vendors Provide** **What Vendors Do** ***Not*** **Provide**


**Platform uptime and availability SLAs (e.g. 99.9%)**


Granular item level recovery (versions, settings, configurations, security, permissions, views, metadata, labels, etc.)


**Network, storage, power, and other infrastructure redundancy for service continuity**


Recovery from accidental or malicious bulk deletion (scripts, file sync and share conflicts, etc.)


**Basic recycle bin and version history (limited retention for 30, 60, 90, etc. days)**


Independent and immutable backup copies isolated from the primary network and the vendors security trust boundary


**Litigation holds and record declarations for compliance (**


**often requires**


**additional licensing**


**)**


Self-service data recovery of individual e-mails, conversations, attachments, documents, etc. to reduce IT overhead


The practical implication: Outside of service-level disruptions the cloud vendor is not responsible for providing additional immutable data copies, protecting data hosted in other cloud vendors and providing granular cloud app-aware recovery.


## Example: Applying the 3-2-1 Rule to Microsoft 365


Applying the 3-2-1 backup rule to Microsoft 365 means treating your Microsoft 365 tenant data, Exchange Online, SharePoint, OneDrive, and Teams, as a distinct dataset that needs three copies: the live Microsoft 365 environment counts as the original, a third-party cloud backup provides the second copy, and a geographically separate or immutable storage tier provides the third. Microsoft's native retention features can support the strategy but should not be the only protection layer.


Here is how the 3-2-1 framework maps onto a typical Microsoft 365 environment:


1. **Copy 1: Your live Microsoft 365 tenant.** Exchange Online mailboxes, SharePoint sites, OneDrive data, and Teams chats. This is your "original" data.
2. **Copy 2: Third-party cloud backup.** A dedicated Microsoft 365 backup solution that snapshots your tenant data at regular intervals (daily or more frequently) and stores it in a separate cloud environment. This provides point-in-time recovery that Microsoft's native tools cannot.
3. **Copy 3: Off-site / immutable tier.** A second cloud storage location with immutability enabled, or a separate regional data store. This is the ransomware-resistant copy — physically or logically isolated from both your live tenant and the primary backup.


### Key workloads to ensure are covered:


- **Exchange Online:** Mailboxes, shared mailboxes, archive mailboxes
- **SharePoint Online:** All site collections, including classic and modern sites
- **OneDrive for Business:** Individual user drives, including versioned files
- **Microsoft Teams:** Channel messages, private chat history, meeting recordings
- **Microsoft 365 Groups and Planner data**


A third-party Microsoft 365 backup platform, such as[AvePoint Cloud Backup](https://www.avepoint.com/products/cloud-backup) , handles the collection and retention of this data at scale, provides granular item-level recovery, and supports immutable storage configurations to satisfy the ransomware-resistant copy requirement.


## **What Are the Best Practices for Implementing 3-2-1 Today?**


****


The most important 3-2-1 implementation practices in 2026 include enabling immutability on at least one backup copy, testing restores regularly and automatically, ensuring SaaS workloads like Microsoft 365 are explicitly in scope, and documenting your


[recovery time objective (RTO) and recovery point objective (RPO)](https://www.avepoint.com/blog/backup/what-are-rto-and-rpo-cloud) before selecting backup cadence and retention settings. A backup strategy that has never been tested carries significant recovery risk.


**Practice** **Why It Matters** **Tier Priority**


**Enable immutability on off-site copy** Prevents ransomware from deleting or encrypting backups All tiers


**Test restores on a scheduled cadence** Unverified backups may fail silently; only tested restores confirm recoverability All tiers


**Set RPO ≤ 24 hours for critical workloads** Determines how much data you can afford to lose; drives backup frequency Tier 1


**Cover Microsoft 365 workloads explicitly** Microsoft does not back up tenant data; native retention has hard limits All tiers


**Separate backup credentials from production** Prevents credential reuse attacks from compromising backup access All tiers


**Define and document retention periods** Different data types have different regulatory retention requirements Regulated workloads


**Automate backup verification** Manual testing is too infrequent; automated verification catches issues before incidents All tiers


## Frequently Asked Questions


### What is the 3-2-1 backup rule in simple terms?


The 3-2-1 backup rule means keeping three copies of your data, on two different types of storage, with one copy off-site. The rule exists to ensure no single failure, hardware crash, ransomware, or physical disaster, can destroy all copies of your data. It is the one of the most widely adopted baseline frameworks in enterprise and SMB data protection.


### What counts as "two different storage media" in a modern 3-2-1 strategy?


In a modern 3-2-1 strategy, 'two different storage media' most commonly means a combination of local or network storage (NAS, SAN, or on-premises backup server) and cloud object storage (Azure Blob or AWS S3). For SaaS-only environments with no on-premises infrastructure, it can mean two logically separate cloud storage accounts or services, ideally in different geographic regions.


### How often should backups run to satisfy the 3-2-1 rule?


Backup frequency is not defined by the 3-2-1 rule itself — it is determined by your RPO. For most business-critical workloads, daily backups are the minimum; for high-value environments like financial data or Microsoft 365 production tenants, hourly or continuous backups are more appropriate. The 3-2-1 rule defines how many copies exist, not how frequently they are created.


### Are immutable backups the same as air-gapped backups?


Immutable backups and air-gapped backups are different, though both serve similar purposes. Immutable backups use storage policies to prevent data from being modified or deleted for a retention period — they may still be network-accessible. Air-gapped backups are physically or logically disconnected from any network, making them unreachable by ransomware. Both add layers of resilience beyond a standard 3-2-1 strategy.


### How does ransomware specifically defeat a 3-2-1 backup strategy?


Ransomware defeats a 3-2-1 strategy by targeting backup copies that remain network-accessible. Modern ransomware strains identify and encrypt backup repositories, connected NAS devices, and cloud backup accounts before attacking production data. A 3-2-1 strategy without at least one immutable or offline copy may result in all three copies encrypted in a single attack. Adding immutability to the off-site copy is the primary defense.


### What workloads are most at risk without a 3-2-1 backup?


Collaboration workloads where there is a high rate of change and interaction between lots of users like Microsoft 365 and Google workspace are particularly at risk due to the potential of accidental deletion or corruption of data which often can go unnoticed beyond native recycle bins and retention windows.


Workloads that are exposed to the risk of ransomware or lack high availability options.


## Related Questions


- [What is a recovery point objective (RPO)?](https://www.avepoint.com/blog/backup/what-are-rto-and-rpo-cloud)
- [What is a recovery time objective (RTO)?](https://www.avepoint.com/blog/backup/rto-rpo-recovery-time-and-recovery-point-objectives-explained)


[AvePoint Cloud Backup](https://www.avepoint.com/products/cloud-backup) helps organizations operationalize the 3-


2-1-1


-0 framework across


[Microsoft, Google, Salesforce, Atlassian, Amazon](https://www.avepoint.com/products/cloud-backup) and


[many more,](https://www.avepoint.com/solutions/saas) with automated backups, granular recovery, immutable storage options, and built-in verification for teams responsible for resilience, compliance, and recovery confidence, helping close the gap left by native retention tools.
