---
schema_version: "1.0.0"
document_id: "d14a7dded090bcb60c3ea22eacc31d055ae9f1f99502f7548c21c6186db2c4e2"
company_key: "btq-technologies-corp-common-stock"
company: "BTQ Technologies Corp. Common Stock"
source_id: "btq-technologies-corp-common-stock-news-import-4b4199d8e235"
canonical_url: "https://www.btq.tech/blog/how-does-the-nist-standardization-process-work"
published_at: "2023-11-07T00:00:00+00:00"
first_seen_at: "2026-07-21T11:47:25.232763+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:261fe5b92d53e5d0702e1df30ff6d41619a2bf703b0c1edc369d9ec0a3114028"
---

# How does the NIST Standardization Process Work?

The arrival of quantum computing is thrilling for the value it can provide worldwide, with near-term impacts on materials, chemistry, and fundamental physics. But with great power does come great responsibility. Quantum computers can also break down our safeguards in our digital world using Shor’s Algorithm to break RSA and ECC cryptography, which protects most of our digital communication. With the latest progress with increasing quantum bit (qubit) counts and reduction of the number of qubits needed to run encryption-breaking quantum algorithms, it seems like a daunting task to stop the quantum threat.


But innovation can’t be stopped. This threat created the need for Post-Quantum Cryptography (PQC). PQC uses classical mathematical methods (meaning, running on non-quantum hardware, just on a regular computer) that remain secure even against large-scale quantum computers. To protect against quantum computers, we need to find new algorithms to replace RSA and ECC cryptography.


The National Institute of Standards and Technology (NIST) plays a leading role in standardizing various technologies and methodologies used within the United States and internationally. The first step in NIST’s PQC call for proposals was launched in 2016 to find new cryptography standards for a post-quantum world.


## Understanding the NIST Standardization Process


NIST's standardization process is characterized by its systematic, open, and rigorous approach to make sure the algorithms selected are scrutinized fully before being recommended as standards worldwide.


Here's a step-by-step breakdown of the process:


1.


Problem Identification: NIST identifies a specific problem or need in the industry. This can arise from technological advancements, new security threats, or shifts in industry demands. Around 2015, a shift in funding began moving quantum computing out of the lab and into the industry, though players like DWave, IBM, and Northrop Grumman had been around for many years.


2.


Call for Proposals: Once a problem is identified, NIST makes a public announcement outlining the specific criteria and requirements. The institute invites experts, researchers, and organizations worldwide to submit their proposals or algorithms that can address the identified problem.


3.


Evaluation: Submitted proposals go through rigorous evaluation. This phase involves testing, security assessments, and performance analysis, to confirm the proposed solutions are robust, efficient, and effective.


4.


Public Review and Feedback: For transparency, proposals under consideration are published and opened up for public review. This allows the broader community – from academia to industry stakeholders – to provide feedback, point out potential issues, or support particular solutions. Trust in cryptography can only be built with an open process.


5.


Testing and Refinement: Based on feedback, proposals may be refined, improved, or thrown out. It’s an iterative process where only the best solutions reach the final stages.


6.


Final Selection: After exhaustive evaluations and refinements, NIST selects the best-suited algorithms for standardization.


7.


Publication: The chosen algorithms are then published as Federal Information Processing Standards (FIPS) or as NIST Special Publications (SP), providing detailed specifications and guidelines for implementation.


## Timeline of the Post-Quantum Cryptography Standardization Process:


Though the PQC Standardization process began in 2016, it’s not yet complete.


Recognizing the gravity of this quantum challenge, the National Institute of Standards and Technology (NIST) initiated a process to standardize post-quantum cryptographic algorithms.


Here's a glimpse of the journey so far:


**2016-2017: Call for Proposals**


NIST kickstarted the PQC standardization process by releasing a public call for proposals in 2016. They invited the global community of cryptographers to submit quantum-resistant cryptographic algorithms. The focus was primarily on public-key encryption, public-key digital signatures, and key-establishment protocols.


**2017-2019: Initial Screening and Round 1**


From the submissions, NIST selected 69 algorithms to move to the first round of evaluation. This phase primarily involved vetting and eliminating algorithms with evident flaws or vulnerabilities.


**2019-2020: Round 2**


Based on the evaluations and feedback from the first round, NIST shortlisted 26 algorithms for the second round. This phase entailed a deeper analysis involving performance testing, security assessments, and scrutiny under various deployment scenarios.


**2020-2022: Round 3**


From the second round, NIST refined the list to a handful of candidate algorithms that entered the third round. This phase is even more rigorous, with a broader community of experts dissecting each algorithm for potential weaknesses, implementation challenges, and other parameters.


**July 5th, 2022: Selected Algorithms**


Four algorithms were selected in 2022. For public-key encryption and key-establishment algorithms, CRYSTALS-Kyber was selected. Additionally, three digital signature schemes, CRYSTALS-Dilithium, FALCON, and SPHINCS+ were selected.


**2022 - present: Round 4**


A new round was announced in July 2022. Through this extended round process, BTQ’s Preon was announced as a finalist. It’s expected that more algorithms in this round will be added to selected algorithms, and eventually standardization.


**Expected 2024: Standardization**


NIST’s recommendations for the Post-Quantum Cryptography Standard[will likely be released in 2024](https://csrc.nist.gov/Projects/post-quantum-cryptography/workshops-and-timeline?ref=btq-publication.ghost.io) .


## What Do We Expect in the PQC Standardization Process


Likely, NIST will opt to standardize multiple algorithms in the PQC process to ensure a broader security net, due to the uncertain landscape of emerging quantum technology and threats.


The SIKE cryptographic algorithm, a fourth-round candidate for the PQC standard,[was cracked using a single-core Xeon processor by Belgian researchers](https://cacm.acm.org/news/269080-nist-post-quantum-cryptography-candidate-cracked/fulltext?ref=btq-publication.ghost.io#:~:text=NIST%20intends%20its%20PQC%20standard,have%20confirmed%20the%20researchers'%20findings.) . While none of the algorithms currently selected for standardization have faced this fate, this situation showed the need for multiple layers of security and backup options.


In this context, the concept of crypto-agility becomes important for industries. Crypto-agility is the ability of a system to easily switch between different cryptographic algorithms without requiring massive overhauls. If one algorithm is compromised, systems designed with crypto-agility can swiftly switch to another standardized algorithm and maintain their security.


This becomes particularly significant in a landscape where multiple algorithms have been vetted and standardized by NIST, offering a range of options to adapt to. Thus, NIST’s approach of selecting multiple algorithms serves as both a risk mitigation strategy and a catalyst for encouraging crypto-agility within the industry.


## BTQ's Preon Selected as Candidate for the Post-Quantum Cryptography Standardization Process


BTQ Technologies Corp.'s[Preon](http://preon.btq.com/?ref=btq-publication.ghost.io) has been selected for consideration in the fourth round of the NIST PQC standardization process. Developed in collaboration with Hon Hai Research Institute, the research arm of Foxconn, Preon is designed to be a robust and efficient post-quantum signature scheme. It’s compact, with a key size that requires only tens of bytes, has rapid key generation processes supported by one or two AES encryptions, and minimal assumptions, by only requiring a collision-resistant hash function for its security model, which, so far, has stood up to quantum attacks.


The details on Preon are published online at[preon.btq.com](http://preon.btq.com/?ref=btq-publication.ghost.io) and, alongside all the algorithms, will continue to be scrutinized through the NIST PQC Standardization process.


## What Happens Once an Algorithm is Chosen?


Once NIST selects an algorithm for standardization, the next steps for use are open:


1.


Widespread Adoption: The algorithm often becomes widely adopted within U.S. federal agencies, since NIST standards are mandated. The first orders are already in place to require government vendors to evaluate threats against quantum computing by government vendors. Because of NIST's international reputation, many other countries and organizations outside the U.S. adopt these standards.


2.


Integration into Products and Services: Manufacturers and service providers, especially those catering to the U.S. federal market, add the standardized algorithms into their products and solutions. This ensures compatibility and security compliance. NIST offers continued support and guidance on standardized algorithms, helping organizations with correct use and implementation.


3.


Continuous Oversight and Review: The lifecycle of a standard doesn’t end with its publication. NIST continues to monitor the chosen algorithms, making sure they remain secure and effective against evolving threats and changing technological landscapes.


4.


Potential Updates or Deprecation: If vulnerabilities are found or if there’s a need for improved efficiency, NIST might revise the standard. In some cases, if an algorithm is deemed insecure due to new discoveries, NIST might deprecate it, advising against its use, as it did with ECC when quantum computing growth began to accelerate.


One of the expectations is a phased transition from classical to post-quantum algorithms. This won't be an overnight shift but a gradual process where systems initially deploy hybrid models (combining classical and quantum-safe algorithms) to ensure backward compatibility and phased migration.


Even after the PQC standards are finalized, the cryptographic community will continually assess them. The dynamic nature of technological advancements means that today's secure algorithm could be vulnerable tomorrow. Not only do new algorithms need to be found, but the industry needs to start thinking about how to upgrade their systems, when, and what the action plan will be if these algorithms become vulnerable to classical or quantum computers.
