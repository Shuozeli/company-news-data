---
schema_version: "1.0.0"
document_id: "c86b0631e5914a0698dfe08492ae973dea2fd319b457f7891c46fdd9b05d79cf"
company_key: "btq-technologies-corp-common-stock"
company: "BTQ Technologies Corp. Common Stock"
source_id: "btq-technologies-corp-common-stock-news-import-4b4199d8e235"
canonical_url: "https://www.btq.tech/blog/is-quantum-computing-killing-blockchains"
published_at: "2023-11-22T00:00:00+00:00"
first_seen_at: "2026-07-21T11:47:25.232763+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:d6f0ca9b16e76bbe4845ae05d5987b3b453242c731ebca77353ff8b63c0d3b05"
---

# Is Quantum Computing Killing Blockchains?

Blockchain technology has changed the way we think about digital transactions and added a new level of security and transparency in the digital world that no bank has been able to compete with. One of the key features that make blockchains so secure is their immutability—once data is put on the blockchain, changing it would require changing all the new blocks and getting the network consensus. However, as we move closer to quantum computing becoming a reality, this very feature of immutability could make it much harder for blockchains to adapt to the post-quantum era.


How can quantum computers threaten blockchains? Shor's algorithm is a quantum algorithm that can efficiently factor large numbers and discrete logarithms, which are the core of our modern encryption. Bitcoin and many cryptocurrencies use the same modern cryptography, elliptic curve cryptography (ECC), to authorize transactions. For a more in-depth discussion of the quantum threat, you can find[more information here](https://www.btq.tech/blog/how-far-away-is-the-quantum-threat) .


That means we will need to figure out how to replace ECC, and other vulnerable cryptography, in blockchains. Special consideration is needed for blockchain technology to stay secure against quantum computing attacks. But it’s not the end.


## The Importance of Immutability


Blockchain immutability is a property of blockchain that ensures that once data is recorded to the blockchain, it cannot be altered, changed, or deleted by someone. This property is core to blockchain's promise to be a trustless, verified, digital ledger.


Immutability is built through several properties:


Hash Functions: Each block in a blockchain contains a list of transactions, and each block is represented by a hash. If any data within the block changes, the block's hash also changes.


Chaining Blocks: Each block also uses the hash of the previous block, creating a chain of blocks. This chaining means that if any information in a previous block is changed, it will change the hash of every subsequent block, disrupting the entire chain.


Consensus Mechanism: Consensus is where multiple nodes (computers) in the network have to agree on the validity of the transactions and blocks. Getting consensus means bad actors making changes is almost impossible because changing any block would require the consensus of most of the network. It’s not like changing a number on an Excel spreadsheet. If someone tries to submit a fraudulent change, the rest of the nodes reject the transaction.


Immutability builds trust among users, as they can be sure that once a transaction is recorded, it cannot be changed or deleted. This is crucial for secure financial transactions, contracts, and data records, reducing the risk of fraud and data tampering. This feature also allows for Bitcoin to operate as a currency on top of the blockchain. Everyone with access to the blockchain can view the entire transaction history, creating transparency and accountability, and allowing for easy verification of transactions. This led to further innovations, like smart contracts and tokenization.


So, this immutability sounds great. It allows us to have a public, verified ledger. However, that also means that all that data is exposed, including public keys, when a transaction is made. That’s not a problem right now, because it’s pretty impossible to extract a private key, the key that’s needed for someone to prove they own this Bitcoin, from a public key. But a quantum computer could do that. So we need to mitigate the threat by upgrading the cryptography. But because of these properties of blockchains, that also means upgrading the blockchain is harder than a traditional web app.


## Mitigation Strategies


What would mitigation strategies look like for blockchain? For those using ECC, like Bitcoin, the immediate strategy would involve transitioning to cryptographic methods that are resistant to quantum attacks.


### Post-Quantum Cryptography


To counter this threat, post-quantum cryptography research aims to develop new cryptographic methods resistant to quantum attacks. These new cryptographic schemes include lattice-based cryptography, code-based cryptography, hash-based cryptography, and multivariate cryptography. For a more detailed discussion of these methods, you can find more information[at this link](https://www.btq.com/blog/difference-between-cryptography-post-quantum-cryptography?ref=btq-publication.ghost.io) .


By incorporating these into the blockchain's architecture, we can make these digital assets secure against quantum computers. But, once we choose the new encryption scheme to use, how do we upgrade with the issues that immutability brings?


### Crypto-Agile Blockchains


First, a blockchain needs to develop crypto-agility. Crypto-agility refers to the ability of a system to easily swap out cryptographic algorithms without disrupting functionality. With blockchain, this means being able to change the cryptographic methods used for securing transactions and data without compromising the blockchain's integrity, speed, and coin ownership.


However, doesn't immutability make blockchains harder to be crypto-agile? Yes, the immutability of blockchains does pose a unique challenge to crypto-agility. Since blockchains are designed to be unchangeable, updating the cryptographic algorithms used can be a complex process that requires network consensus. To upgrade to a post-quantum-resistant algorithm, we have to fork it.


### Forking: Hard and Soft


Forks in a blockchain can serve as a process for radical change. This can allow the implementation of new, quantum-resistant cryptographic algorithms. Forking involves creating an alternate version of the blockchain, starting from a specific block.


There are two types of forks: hard forks and soft forks. A hard fork is a radical change to the protocol that makes previously invalid blocks or transactions valid, or vice-versa. A soft fork, on the other hand, is a change to the protocol that tightens the rules, making previously valid blocks invalid.


Hard forks, in particular, can be used to make previously invalid blocks or transactions valid, requiring all users or nodes to upgrade to the latest version of the protocol software. This is likely what will need to be done for a big change like an encryption overhaul.


The forking process is often carefully managed and requires extensive communication within the blockchain community. However, there are a lot of human elements that need to come together to make this process happen. Forking requires network consensus. If a fork is proposed but doesn't gain enough support, it can result in the blockchain splitting into two separate chains. Differences in ideology, technical direction, or pure human ego can cause this. This can lead to confusion and potentially devalue the cryptocurrency if it faces a decline in user adoption and support because of the loss of trust.


## Ethereum's Approach to Quantum Resistance and Future-Proofing


Ethereum, one of the leading blockchain platforms, is not just looking at the immediate future but is planning for long-term stability and reliability. Quantum computing is one of the threats they’re looking ahead to, as seen in the[September 2023 update on the Ethereum Roadmap](https://ethereum.org/en/roadmap/future-proofing/?ref=btq-publication.ghost.io#quantum-resistance) .


One big challenge is that Ethereum's current proof-of-stake protocol relies on a very efficient signature scheme known as BLS (Boneh-Lynn-Shacham) to aggregate votes on valid blocks. However, BLS is vulnerable to quantum attacks. Ethereum also uses "KZG" schemes to generate cryptographic secrets, which are known to be quantum-vulnerable.


The ideal solution would be to replace these vulnerable schemes with quantum-safe cryptography. Two approaches are being considered as potential replacements for the BLS scheme: STARK-based and lattice-based signing. Both of these are still in the research and prototyping phase, and no decision has been made yet on what will be implemented.


Ethereum aims to be secure for centuries, making the platform quantum-resistant as soon as possible, given that estimates for breaking cryptography land in the 2030s. Etherum taking the quantum threat seriously is a good model for other blockchains.


## Opportunities for Innovation


This transitional phase in blockchain technology should not be viewed as a crisis, or the end of a technology that has changed lives, but as an opportunity for innovation. Blockchain projects that proactively address these quantum vulnerabilities from the initial inception, sometimes called “quantum-first”, are attracting users and investors concerned about long-term security.


While the beginnings of quantum computing have created some big challenges for the cryptographic foundations of blockchains and security in general, it doesn’t render blockchain obsolete. Through innovation and integration of quantum-resistant cryptographic methods, blockchains can become even more resilient and secure in the quantum age.


‍
