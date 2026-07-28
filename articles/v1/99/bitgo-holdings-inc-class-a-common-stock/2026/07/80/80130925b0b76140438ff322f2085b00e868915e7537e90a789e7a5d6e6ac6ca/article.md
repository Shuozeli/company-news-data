---
schema_version: "1.0.0"
document_id: "80130925b0b76140438ff322f2085b00e868915e7537e90a789e7a5d6e6ac6ca"
company_key: "bitgo-holdings-inc-class-a-common-stock"
company: "BitGo Holdings Inc. Class A Common Stock"
source_id: "bitgo-holdings-inc-class-a-common-stock-news-import-43176398adc1"
canonical_url: "https://www.bitgo.com/resources/blog/bitgo-adds-new-quantum-risk-management-capabilities-for-bitcoin-wallets/"
published_at: "2026-07-22T00:00:00+00:00"
first_seen_at: "2026-07-24T21:07:41.088269+00:00"
fetched_at: "2026-07-28T21:20:58.380206+00:00"
content_hash: "sha256:e5aa5df043a7cc89d1adf1124b60471ae1ea957f3909b515889b9b58b761400a"
---

# BitGo Adds New Quantum-Risk Management Capabilities for Bitcoin Wallets

## Key Takeaways


-


BitGo has launched quantum-risk management capabilities for Bitcoin wallets, giving institutions a way to assess, manage, and reduce quantum-related exposure across BTC-based multi-signature custody.


-


The release adds four institutional controls: a novel UTXO selection method that groups and prioritizes coins by address, a Quantum Risk Score that shows how exposed your BTC wallets are, a Fix Exposed Addresses workflow that moves funds into addresses whose public keys have never been exposed onchain, and new default settings that automatically set up wallets more resistant to quantum threats.


-


The capabilities extend the visibility and workflows institutions need to reduce address and transaction-level exposure at scale.


## The safest key is one a public network has never seen


Every time you spend from a BTC address, the public key is revealed onchain. For most of the asset's history, that detail carried no practical cost. It is the kind of exposure that sits quietly in the background of custody operations, rarely measured and rarely managed.


That calculus is starting to shift as institutions think harder about how quantum computing could affect the addresses they hold. The risk concentrates in one place: addresses whose public keys have already been revealed on the network. An address that has never exposed its public key onchain is far harder to reason about as a target, which is why the practice of holding assets in addresses whose public keys have never been exposed onchain has become a foundation of careful custody.


BitGo built its wallet architecture around that principle long before the industry started using the word "quantum" in earnest. The new capabilities give institutions the tooling to see that exposure clearly, measure it, and act on it.


## What the capabilities do


The release extends BitGo's multi-signature security model with operational controls for managing wallet-key exposure and improving how UTXOs are handled. There are four parts.


The UTXO Selection Method is a new coin selection approach: when any UTXO from an address is selected, all UTXOs associated with that address are included in the transaction where possible. This ensures that, in most cases, a spend empties the address completely, minimizing the risk of leaving funds behind once the key is exposed. Funds already held in address types that expose a public key from creation, such as Taproot or Pay-to-Public-Key, require separate remediation.


The Quantum Risk Score is an in-platform scoring system that helps clients understand potential quantum-related exposure across supported Bitcoin wallets. Instead of treating exposure as an abstract concern, institutions get a concrete measure they can track and report against.


The Fix Exposed Addresses Workflow is a guided remediation flow. It helps clients move funds away from addresses with elevated exposure and into newly generated addresses, returning to the practice of holding assets in addresses whose public keys have never been exposed onchain.


Default Address-Type Controls update the default wallet behavior to reduce reliance on Bitcoin address types and transaction patterns that may introduce additional quantum-related considerations. The safer path becomes the default one, rather than something an operator has to configure by hand.


## Why institutions are acting now


BitGo pioneered multi-signature wallets for Bitcoin and has long argued for security models that reduce single points of failure. Its architecture, strict address handling, and use of new addresses for transactions already aims to reduce unnecessary key exposure. These capabilities give institutions more visibility, more controls, and clearer workflows to manage quantum-related risk across large balances.


BitGo's view is that institutions do not need to wait for a quantum event to begin managing quantum risk. The safest key is one whose public key has never been revealed on the network. The practical path is to reduce exposure now, harden wallet operations, and prepare for the eventual migration from today's security models to future post-quantum standards, all while continuing to rely on the proven security of multi-signature.


The new capabilities apply to BTC wallets.


If you would like to learn more about managing quantum risk across your Bitcoin custody, get in touch.


## Frequently asked questions


### What is quantum risk for a Bitcoin wallet?


Quantum risk refers to the possibility that future advances in quantum computing could affect the security of addresses whose public keys have already been revealed on the Bitcoin network. Addresses that have never exposed their public key onchain are much harder to reason about as a target. BitGo's capabilities help institutions measure and reduce this exposure.


### How does the Quantum Risk Score work?


It is an in-platform scoring system that assesses potential quantum-related exposure across your supported Bitcoin wallets. It gives you a concrete measure of exposure so you can track it over time and prioritize which addresses to remediate first.


### What does the Fix Exposed Addresses workflow actually do?


It is a guided flow that moves funds out of addresses with elevated exposure and into newly generated addresses. The result is a return to the practice of holding assets in addresses whose public keys have never been exposed onchain, without your operations team having to manage the process manually.


### Do I need to change how my wallets work today?


The updated default address-type controls adjust wallet behavior to reduce reliance on address types and transaction patterns that carry additional quantum-related considerations, so safer behavior becomes the default. You can use the Quantum Risk Score and the Fix Exposed Addresses workflow to review and remediate existing balances at your own pace.


## Table of Contents


- Key Takeaways
- The safest key is one a public network has never seen
- What the capabilities do
- Why institutions are acting now
- Frequently asked questions


*The* digital asset infrastructure company.


## The latest


[All News](https://www.bitgo.com/resources/blog)


- [Gate US Joins BitGo's Go Network, Expanding Secure Access to Exchange Liquidity](https://www.bitgo.com/resources/blog/gate-us-joins-bitgos-go-network-expanding-secure-access-to-exchange-liquidity/)


- [Institutional Crypto Custody: A Guide for Asset Managers](https://www.bitgo.com/resources/blog/what-to-look-for-in-an-institutional-crypto-custody-provider/)


- [Regulated OTC: Institutional OTC Desks and Crypto Block Trades](https://www.bitgo.com/resources/blog/regulated-otc-institutional-otc-desks-and-crypto-block-trades/)


- [BitGo Prime: Connecting Institutions to Global Digital Asset Markets](https://www.bitgo.com/resources/blog/connecting-institutions-to-global-digital-asset-markets/)


**About BitGo**


BitGo is the digital asset infrastructure company, delivering custody, wallets, staking, trading, financing, and settlement services from regulated cold storage. Since our founding in 2013, we have been focused on accelerating the transition of the financial system to a digital asset economy. With a global presence and multiple regulated entities, BitGo serves thousands of institutions, including many of the industry's top brands, exchanges, and platforms, and millions of retail investors worldwide.
