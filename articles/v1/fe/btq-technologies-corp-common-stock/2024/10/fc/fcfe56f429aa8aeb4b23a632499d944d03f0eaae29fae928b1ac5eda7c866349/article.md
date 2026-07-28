---
schema_version: "1.0.0"
document_id: "fcfe56f429aa8aeb4b23a632499d944d03f0eaae29fae928b1ac5eda7c866349"
company_key: "btq-technologies-corp-common-stock"
company: "BTQ Technologies Corp. Common Stock"
source_id: "btq-technologies-corp-common-stock-news-import-4b4199d8e235"
canonical_url: "https://www.btq.tech/blog/ethereums-roadmap-post-quantum-cryptography"
published_at: "2024-10-21T00:00:00+00:00"
first_seen_at: "2026-07-21T11:47:25.232763+00:00"
fetched_at: "2026-07-28T21:33:00.470256+00:00"
content_hash: "sha256:6955b2b58d98d62d6805eed6c1ee23536bc59cff6b60f7b1d24b3c1c97070816"
---

# Ethereum’s Roadmap for Post-Quantum Cryptography

Ethereum, a decentralized public blockchain platform created by Vitalik Buterin in 2015, enables developers to build decentralized applications (DApps) and deploy smart contracts using its native cryptocurrency, Ether (ETH). Ethereum has played a crucial role in the development of non-fungible tokens (NFTs), decentralized finance (DeFi), decentralized autonomous organizations (DAOs), and the Metaverse. Often described as "the world's most programmable blockchain," Ethereum facilitates digital asset transactions and supports a wide range of decentralized applications.


The security of online communications and digital assets relies on two popular cryptographic standards: RSA and elliptic curve cryptography (ECC), both of which assume that conventional computers cannot easily solve certain complex mathematical problems. Cryptocurrencies like[Bitcoin](https://btq-publication.ghost.io/blog/will-quantum-computers-break-bitcoin/) and Ethereum are built on ECC. These standards currently use public key encryption (PKE) algorithms that are considered secure because classical computers struggle to factor very large numbers or compute elliptic curve discrete logarithms.


However, the development of quantum computers has introduced the "[quantum threat.](https://btq-publication.ghost.io/blog/how-far-away-is-the-quantum-threat/) " When large-scale quantum computers are developed, they could solve these problems and break current public-key cryptosystems, undermining the security, confidentiality, and integrity of digital communications and data on the internet.


Currently, Ethereum is safe from quantum attacks because quantum computers are not yet powerful enough to break its underlying cryptographic security. However, as quantum computing advances, it could eventually compromise Ethereum's cryptographic algorithms, which protect assets and value stored on the ledger.


## Understanding Post-Quantum Cryptography (PQC)


In 1992, Peter Shor demonstrated that large-scale quantum computers could break current cryptographic systems using Shor’s algorithm. This discovery prompted cryptographers and researchers worldwide to explore post-quantum cryptography (PQC) implementation.


Post-quantum cryptography, also known as quantum-proof or quantum-resistant encryption, refers to cryptographic schemes designed to protect classical computers from quantum computer attacks. PQC prepares for the quantum computing era by revising the mathematical algorithms underlying current cryptography. Importantly, PQC can be implemented on today's classical computers to safeguard them from future quantum attacks.


PQC is critical to the future of digital security because data that is safe today, based on current cryptography, will become vulnerable in the quantum computing era. Implementing PQC techniques is necessary to keep data secure, both for blockchain systems and the internet as a whole.


## The Quantum Threat to Ethereum


Ethereum uses common cryptographic methods to secure transactions and maintain the integrity of its distributed ledger. However, these methods may become ineffective due to potential advances in quantum computing. Ethereum's reliance on ECDSA, BLS, and KZG makes it vulnerable to quantum attacks, which could enable malicious actors to decrypt private keys, compromise smart contract integrity, and forge digital signatures—potentially giving them control over associated funds.


The BLS signature scheme, which uses bilinear pairings and elliptic curve operations (BLS12-381), differs from ECDSA (secp256k1) but is still vulnerable to quantum attacks. A sufficiently powerful quantum computer running Shor's algorithm could break these elliptic curve-based cryptographic systems and expose sensitive user data on the Ethereum blockchain.


Similarly, KZG (Kate-Zaverucha-Goldberg) commitment schemes, used in various parts of Ethereum for generating cryptographic secrets based on polynomial commitments, are also vulnerable to quantum computers. Trusted setups, which involve generating randomness that quantum computers cannot reverse-engineer, are currently used to mitigate this risk. However, the optimal solution is to replace these schemes with quantum-safe cryptography.


## Proposed Quantum-Resistant Solutions


To prepare Ethereum for the quantum computing era, several quantum-resistant solutions have been proposed, including hash-based cryptography, lattice-based cryptography, code-based cryptography, multivariate polynomial cryptography, and[STARK-based solutions](https://btq-publication.ghost.io/blog/completing-the-first-falcon-signature-verification-in-starkware-initiating-the-transition-to-a-quantum-safe-ethereum/) . Two have gained particular attention:


**STARK-based solutions**
zk-STARKs (Zero-Knowledge Scalable Transparent Arguments of Knowledge) use a zero-knowledge proof system to enable the verification of encrypted data without revealing any underlying information. STARKs offer improvements over zk-SNARKs by relying on collision-resistant hash functions rather than elliptic curves and trusted setups. This makes them more secure and quantum-resistant. Additionally, STARKs eliminate the need for trusted setups in a blockchain network like Ethereum. To support the planned adoption of zk-STARKs in Ethereum 3.0, the Ethereum Foundation has awarded a $12 million grant to STARKware, a company focused on developing zk-STARK scaling solutions.


**Lattice-based cryptography**
Lattice-based cryptography, a post-quantum technique, is based on the computational difficulty of the nearest or shortest vector problem in lattices. Public keys are generated by encrypting an arbitrary lattice point, while private keys are derived from evaluating the shortest vector in the lattice. Many cryptographers view lattice-based algorithms as the most promising solution for securing data and providing quantum-resistant encryption due to their reliance on the hardness of solving lattice problems.


However, these post-quantum cryptography methods present new challenges, including efficiency issues and compatibility with existing blockchain operations. Securing Ethereum from quantum attacks while balancing efficiency, compatibility, scalability, and performance will be crucial.


## Ethereum's Proactive Approach to Quantum Threats


Ethereum recognizes the quantum threat and has taken proactive steps to integrate quantum resistance into its roadmap. Current research and development efforts, especially regarding post-quantum cryptography, include the implementation of an opcode that allows users to submit zk-STARK proofs. These proofs validate a user's knowledge of a private preimage and a public key generated via approved hash functions, enabling the replacement of the user's account code with a quantum-resistant validation mechanism.


Ethereum 2.0, fully launched in late 2022, replaced the Proof of Work (PoW) consensus mechanism with the Proof of Stake (PoS) system, which is believed to be more quantum-resistant. Ethereum 2.0 also offers the option to switch to quantum-resistant signature schemes like Lamport, XMSS, and SPHINCS+.


Looking ahead, Ethereum 3.0, expected to launch in 2027, will introduce more robust quantum-resistant protocols such as Winternitz signatures and zk-STARKs, further protecting transactions from quantum attacks by preventing the exposure of private keys.


## Conclusion


While quantum computers powerful enough to break cryptographic systems are not yet here, the ongoing development of quantum technology threatens Ethereum's security. The Ethereum community has been proactive in its efforts to safeguard the network from quantum threats by integrating quantum-resistant solutions into future upgrades. As quantum computing advances, continued innovation in blockchain security will be essential to protect Ethereum and the multi-billion-dollar assets it secures.


To explore Ethereum's official roadmap documentation, see[here](https://ethereum.org/en/roadmap/?ref=btq-publication.ghost.io) and[here](https://ethereum.org/en/roadmap/future-proofing/?ref=btq-publication.ghost.io) .
