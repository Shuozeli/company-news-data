---
schema_version: "1.0.0"
document_id: "d5987fe67339972a893e33476d846e7ddf8713056d8ae7786c8fa69bab80494d"
company_key: "btq-technologies-corp-common-stock"
company: "BTQ Technologies Corp. Common Stock"
source_id: "btq-technologies-corp-common-stock-news-import-4b4199d8e235"
canonical_url: "https://www.btq.tech/blog/what-does-a-transition-to-post-quantum-cryptography-look-like"
published_at: "2023-10-11T00:00:00+00:00"
first_seen_at: "2026-07-21T11:47:25.232763+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:94c8b614c7d42e50564bccb6eb9af64a34a71f97ef0de42fd886cf45584ddfde"
---

# What Does a Transition to Post-Quantum Cryptography Look Like?

Cryptography is the cornerstone of digital security, enabling everything from secure communications to online banking. In the other resources in this series, we have covered the[rise of quantum computing](https://www.btq.tech/blog/how-far-away-is-the-quantum-threat) and how it threatens current cryptographic systems.


Quantum computing is not theoretical. Real strides are being made towards building scalable quantum computers. However, there's still debate about when quantum machines will become powerful enough to break contemporary cryptographic algorithms. Estimates range from a few years to a few decades, but the general consensus is that it's a matter of "when," not "if."[BTQ’s QByte Quantum Risk Calculator](https://qbyte.btq.com/?ref=btq-publication.ghost.io) tracks two important milestones for quantum advantage: qubit counts and quantum infidelity. Even the most pessimistic estimates on the BTQ Risk Calculator place that threshold in the 2030s, without any breakthroughs or improvements in error correction. Given the foundational role of cryptography in modern digital life, preparing for this inevitability is critical.


Through the NIST Standardization Process for Post-Quantum Cryptography (PQC), new cryptographic standards are being released in 2024. But this is not just an academic exercise, it's an urgent goal for organizations to upgrade. If you wait, you’ll be left behind!


## Preparing for the Quantum Age


The National Institute of Standards and Technology (NIST) in the United States has been a key resource in preparing for the post-quantum age. NIST has organized the PQC Standardization Process to identify robust post-quantum cryptographic algorithms for digital signatures and general encryption. Though this process is ongoing, the urgency to identify candidates is increasing as the timeline for scalable quantum computing becomes clearer.


Post-quantum cryptography refers to cryptographic algorithms that are secure against the capabilities of quantum computers. The objective is to provide the same level of security and functionality as existing cryptographic algorithms but stand against attacks from scalable quantum computers. And, not only do we need to protect against quantum computers, but we also don’t want the new cryptographic standards to be[cracked by a Xeon processor](https://www.computing.co.uk/news/4054253/post-quantum-cryptography-candidate-cracked-hours-simple-cpu?ref=btq-publication.ghost.io) .


To guard against future quantum threats, the Cybersecurity and Infrastructure Security Agency (CISA), the National Security Agency (NSA), and the National Institute of Standards and Technology (NIST) have jointly[created a factsheet](https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/3498776/post-quantum-cryptography-cisa-nist-and-nsa-recommend-how-to-prepare-now/?ref=btq-publication.ghost.io) to help organizations create quantum-readiness roadmaps before the post-quantum cryptographic standards release in 2024.


Technology vendors are urged to start planning and evaluations for integrating post-quantum cryptographic algorithms with these action steps:


### Establish a Quantum-Readiness Roadmap


First, organizations must create a team to create a quantum-readiness roadmap. To begin this journey, organizations should establish a dedicated project management team. This team will explore and identify the usage of quantum-vulnerable cryptography and inventory quantum-vulnerable systems and assets. This inventory is a roadmap for organizations to start quantum risk assessment processes and identify the more critical systems for migration to PQC.


### Prepare a Cryptographic Inventory


A well-structured cryptographic inventory is key in aiding organizations to become quantum-ready. Organizations should regularly audit their systems to identify hard-coded cryptographic algorithms that can become potential points of failure and release new internal processes to make sure any new software packages, technology vendors, and systems have a plan and timeline to move to PQC. This will help identify vulnerabilities, particularly in sensitive datasets, network protocols, end-user systems, and identity services.


### Evaluate Technology Vendors and Supply Chain Quantum-Readiness


Companies are recommended to start engaging with technology vendors regarding their quantum-readiness roadmaps. Conversations should focus on vendors’ plans, timelines, and commitment to migrating to PQC. This involves commercial-off-the-shelf and cloud-based products, as well as creating backup plans and vendors. Organizations must prioritize high-impact systems and those with long-term confidentiality needs. Conversations with vendors should include discussions about updates, upgrades, expected costs associated with migration to PQC, and ensuring that future products are delivered with built-in hybrid and PQC options.


## PQC Implementation


Transitioning to post-quantum cryptography is a huge task. Beyond just selecting an algorithm, challenges include re-engineering software and hardware, training staff, and ensuring backward compatibility, crypto-agility, and fallback plans. There are logistical issues, like updating devices remotely or across regions that may be part of critical infrastructure or embedded systems. Financially, the transition will require significant investment, but the cost of inaction—compromised global digital security—is higher. A business that is not ready will already experience financial losses from government clients today.


### Crypto-agility


Crypto-agility is the ability of a system to effortlessly switch out cryptographic algorithms and methods without requiring huge re-engineering efforts of the underlying infrastructure. In the past, it took 10 years to upgrade from RSA to ECC cryptography. The idea is gaining traction in today's rapidly evolving digital landscape where algorithms can become obsolete overnight due to new vulnerabilities or technological advancements, like quantum computing.


Corporations should implement crypto-agility as a foundational principle in their security architecture. The first step is to centralize the management of cryptographic libraries and keys, ensuring they can be updated or replaced without requiring a complete system overhaul. Components that use cryptography—whether hardware or software—should be modular to allow for straightforward replacements or upgrades. APIs should be designed to be algorithm-agnostic, permitting an easier switch between algorithms.


Essentially, crypto-agility is a form of future-proofing. It allows organizations to swiftly adapt to new cryptographic standards, thereby maintaining the integrity and security of their data and systems.


### Hybrid systems


The next step in the transition to post-quantum cryptography is using hybrid systems. These are systems that deploy both classical and post-quantum cryptographic methods in parallel. This way organizations can maintain compatibility with existing systems while integrating stronger, quantum-resistant algorithms. For example, TLS 1.2 and 1.3, a security protocol for information exchange between web clients and servers, has been experimenting with a[hybrid mode that uses both ECC and PQC](https://www.microsoft.com/en-us/research/project/post-quantum-tls/?ref=btq-publication.ghost.io) . These hybrid systems act as a bridge, helping organizations become crypto-agile and transition smoothly, without sacrificing current operational capability.


## A Challenge and Opportunity Ahead


While the transition to post-quantum cryptography is still early, some tech corporations are modeling crypto-agility. For example, Google initiated PQC experiments in 2016 and as of[August 2023, added support in Chrome 116](https://blog.chromium.org/2023/08/protecting-chrome-traffic-with-hybrid.html?ref=btq-publication.ghost.io) for establishing symmetric secrets in TLS for[X25519Kyber768](https://www.ietf.org/archive/id/draft-tls-westerbaan-xyber768d00-02.html?ref=btq-publication.ghost.io) , a NIST PQC finalist.


The transition to post-quantum cryptography is not an option, it’s necessary. Whether one believes the quantum threat is around the corner or is still a decade away, the regulations require plans to support upgrades to align with PQC standards now. This is a big opportunity for players in the cybersecurity space where quantum knowledge is critical.


Organizations must act swiftly, developing quantum-readiness roadmaps and engaging proactively with technology vendors to ensure a transition to a new era of quantum-resistant cryptographic standards and practices. The guidance provided by CISA, NSA, and NIST helps organizations navigate the quantum future securely and efficiently.


While there are many interconnected systems – databases, servers, web traffic, blockchain, and more – to think about, the challenges of a transition are not insurmountable. Through collaborations from governmental bodies like NIST, industry players creating new products, and academic researchers and organizations finding new algorithms, we see a roadmap to a secure digital future that withstands quantum computing’s threat to encryption.


‍
