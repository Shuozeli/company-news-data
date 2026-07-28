---
schema_version: "1.0.0"
document_id: "a88da79f11af84d766ee5cdb9d0eaf1594e1cf07b73f22d327f6303ebcdb3582"
company_key: "bitgo-holdings-inc-class-a-common-stock"
company: "BitGo Holdings Inc. Class A Common Stock"
source_id: "bitgo-holdings-inc-class-a-common-stock-news-import-43176398adc1"
canonical_url: "https://www.bitgo.com/resources/blog/bitgo-keyring-wallets-manage-every-evm-chain-from-one-account/"
published_at: "2026-07-14T00:00:00+00:00"
first_seen_at: "2026-07-24T21:07:41.088269+00:00"
fetched_at: "2026-07-28T21:22:05.726331+00:00"
content_hash: "sha256:26c4f6cf04e30f9ccf944d21630850b5a1f5d783bc42431b0521eb4df777170c"
---

# BitGo Keyring Wallets: Manage Every EVM Chain From One Account

## Key Takeaways


-


BitGo EVM Keyring connects all EVM-compatible chains to a single wallet setup. One account covers Ethereum, BSC, Polygon, Arbitrum, Optimism, and any supported chain you add later, without duplicate onboarding or separate credentials per network.


-


Gas management, wrong-chain recovery, and key ceremony overhead all benefit from the same consolidation. Each chain has its own gas tank under the same wallet address, so all gas tank balances can be monitored centrally within the Keyring wallet UI, and funds sent to the wrong EVM chain can be recovered without a separate access path for each network.


-


Adding a new EVM chain takes minutes, not an integration cycle. BitGo clients access EVM Keyring through the same security controls and governance workflows they rely on for standard custody operations.


The multi-chain EVM landscape has matured quickly. What started as a few teams experimenting with Polygon or Arbitrum alongside Ethereum has become standard practice for any serious digital asset operation. More chains means more market access, more clients to serve, and more transaction rails to offer. It also means more operational complexity.


For years, adding a chain meant adding a wallet. A separate setup, separate credentials, a separate deposit address your team had to track, reconcile, and maintain. Five EVM chains meant five independent wallets running in parallel, wallet sprawl, each with its own gas balance to fund and monitor. The math is simple: more chains, more overhead, more surface area for error.


[BitGo EVM Keyring](https://developers.bitgo.com/docs/wallets-evm-keyring) is a wallet that connects all your enabled EVM chains to a single wallet. Instead of treating each network as its own independent infrastructure decision, it surfaces them as linked contexts under one wallet, one view, and one security model.


## How EVM Keyring works


The core setup is straightforward. You create one wallet, and it covers every EVM chain you enable: Ethereum, BNB Smart Chain, Polygon, Arbitrum, Optimism, and any additional network BitGo supports going forward. BitGo manages chain-specific derived wallets behind the scenes; what you see and operate is one wallet. There’s no per-chain wallet creation, no separate credentials, and no additional onboarding work when you expand to new networks later.


Deposits, withdrawals, and balances across all enabled chains appear in a single wallet interface. Chain-specific activity is visible as its own context within that interface, so your team isn’t jumping between separate systems to get a complete picture of your multi-chain positions.


Gas management works the same way. Each enabled network has its own gas tank under the wallet, but you fund, monitor, and top up from one place. Gas covers address setup, balance syncing, and asset consolidation automatically. When something moves, it moves, without someone manually checking whether a particular chain has enough gas to process it.


The single-account model also simplifies two problems that come up more often than most teams expect. When funds are sent to the wrong EVM chain, recovery doesn't require navigating a separate wallet or credential set for each network. Because all chains share one wallet structure, the access path is the same regardless of which chain received the misdirected funds. For eligible wallets, EVM Keyring requires only one key ceremony to cover every enabled network; the cognitive overhead of key setup doesn't compound as you add chains. Multisig and older MPC version wallets cannot be converted and will continue to work as is. One ceremony, one set of procedures, one credential structure to manage and audit going forward.


## Adding chains without rebuilding your infrastructure


The more significant operational shift is what happens when you want to add a new network. With a traditional wallet setup, adding a chain is a project: new wallet creation, new integration work, new onboarding, and the decision of whether early-stage volume on that chain justifies the lift. Teams routinely delay chain expansion for exactly this reason.


With EVM Keyring, adding a new chain is a few clicks. No new wallet, no separate account setup, no integration cycle. As BitGo adds network support, clients extend their footprint without proportional overhead.


## Security and compliance that scales with your network


BitGo’s multi-party computation (MPC) security model applies across every chain within EVM Keyring. The same security controls and governance workflows that applies to your Ethereum operations extends to every additional network you turn on. Nothing changes about the security posture when you add a chain. The infrastructure scales; the risk profile stays consistent.


If you’d like to learn more about EVM Keyring[read more here](https://developers.bitgo.com/docs/wallets-evm-keyring) . To discuss how BitGo’s EVM Keyring fits your current multi-chain operations, get in touch.


## Frequently asked questions


### What is BitGo EVM Keyring?


EVM Keyring is a BitGo wallet that manages digital assets across multiple EVM-compatible blockchains from a single wallet. One wallet setup covers all your enabled networks, including Ethereum, BSC, Polygon, Arbitrum, and Optimism, with no separate credentials or onboarding required per chain.


### Which EVM chains does BitGo EVM Keyring support?


EVM Keyring currently supports Ethereum, BNB Smart Chain (BSC), Polygon, Arbitrum, and Optimism. BitGo continues to add network support, and clients can turn on new chains without creating a new wallet or completing a separate integration.


### Does adding a new chain require a new key ceremony?


For eligible wallets, no. EVM Keyring requires only one key ceremony to cover all enabled networks. When you add a new chain, you're extending an existing account structure, not creating a new one. That keeps the setup process consistent and the operational overhead of key management fixed regardless of how many chains you operate on. Note, multisig and older MPC-version wallets can’t be converted and will continue to work as is.


### Do I need to create a new wallet each time I add an EVM chain?


No. Adding a new EVM chain to EVM Keyring takes a few clicks. There’s no new wallet creation, no separate account setup, and no additional integration work required when you expand to a new network.


### What happens if funds are sent to the wrong EVM chain?


Because all enabled chains share the same account structure under EVM Keyring, recovery doesn't require a separate wallet or access path per network. The unified account model means your team can address a wrong-chain send through the same interface and credentials used for everything else.


### Does the same security and insurance coverage apply across all chains?


Yes. BitGo clients access EVM Keyring through the same security controls and governance workflows they rely on for standard custody operations. Adding a chain does not change your security posture or coverage.


## Table of Contents


- Key Takeaways
- How EVM Keyring works
- Adding chains without rebuilding your infrastructure
- Security and compliance that scales with your network
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
