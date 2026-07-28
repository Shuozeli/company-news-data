---
schema_version: "1.0.0"
document_id: "88dfe5744d461bf81c2398f4bafdc80d1afd04c45bdf8747ebfb8e4df0f28799"
company_key: "bitgo-holdings-inc-class-a-common-stock"
company: "BitGo Holdings Inc. Class A Common Stock"
source_id: "bitgo-holdings-inc-class-a-common-stock-news-import-43176398adc1"
canonical_url: "https://www.bitgo.com/resources/blog/regulated-otc-institutional-otc-desks-and-crypto-block-trades/"
published_at: "2026-07-23T00:00:00+00:00"
first_seen_at: "2026-07-24T21:07:41.088269+00:00"
fetched_at: "2026-07-28T21:20:10.944044+00:00"
content_hash: "sha256:113fc35c59772a3e03b7d171a2c68c12002532a1212ed21a606ffbeb1030361b"
---

# Regulated OTC: Institutional OTC Desks and Crypto Block Trades

Crypto OTC trading lets institutions execute large digital asset orders without showing the full trade on a public order book. The reason is to maximize execution quality.


A large exchange order can sweep available liquidity, worsen the average fill price, and signal intent before execution is complete. An institutional OTC desk addresses this by arranging a private crypto block trade, quoting a price for a specific asset, size, and pair, and settling the transaction through an agreed workflow.


For institutions, price is only the first question. The rest is custody, counterparty exposure, reporting, settlement timing, and whether assets must leave controlled custody before execution. For baseline mechanics, see[BitGo’s guide to crypto OTC trading](https://www.bitgo.com/resources/blog/what-is-crypto-otc-trading/) .


OTC is not automatically better than exchange execution, but it is more relevant when trade size, settlement risk, asset coverage, or information leakage creates a problem the public order book is not built to solve.


## Key Takeaways


-


Crypto block trades help institutions move size without displaying the full order on a public market.


-


RFQ crypto trading creates a defined process for requesting, accepting, and executing a quote for a specific trade size.


-


Institutional OTC workflows should combine liquidity access with controlled OTC settlement, custody segregation, and clear counterparty terms.


-


A regulated OTC model matters because execution quality depends on more than the quoted spread. It also depends on asset location, settlement controls, counterparty exposure, and post-trade reporting.


## Why Institutions Use OTC for Crypto Block Trades


Public order books work well when the order size is small relative to available liquidity. They become less efficient when a fund, corporation, or family office needs to move meaningful size.


The larger the order, the more likely it is to move through multiple price levels before it is filled. This issue is called “slippage” and it happens in large crypto orders: the displayed price may not survive contact with the full order size. A trade that works at the top-of-book price can fail once the average fill reflects market impact. This is especially relevant in assets where visible liquidity is thinner than historical trading volumes suggest.


Privacy is the second reason institutions use OTC. A large visible order can invite adverse positioning, copycat trading, or attempts to trade ahead of the flow. In transparent blockchain markets, counterparties may also monitor wallet movement, venue flows, and settlement behavior. OTC execution limits how much trade intent must be exposed before the transaction is arranged.


A block trade does not completely remove the risk from signaling trade intent on a public orderbook—information about a large order could still be inferred by some market participants. However, it can improve how the institution accesses liquidity. Depending on the desk model, liquidity may come from counterparties, internal inventory, market makers, and trading venues. The institution receives a quote for size, evaluates the terms, and decides whether to execute.


The trade-off is that desk selection matters. Poor liquidity access, weak settlement controls, or unclear counterparty terms can offset the benefits of private execution.


## How RFQ Crypto Trading and OTC Settlement Work


An OTC block trade usually begins with a request for quote or RFQ. The client identifies the asset, side, amount, pair, and any timing or settlement constraints. The desk prices the trade using available liquidity, inventory, market conditions, and risk limits.


The quote is typically valid for a defined window. If the client accepts within the quote window, the trade is locked at the quoted terms. If the client does not accept, the quote expires and the desk reprices based on current market conditions.


The settlement workflow is where institutional OTC differs most from standard exchange execution. In a prefunded model, the client may need to move assets to an exchange, desk, or counterparty before execution. That introduces exposure to the venue or trading counterparty while the assets are outside the client’s preferred custody framework.


A post-trade settlement model can reduce that exposure by allowing the client to agree to the trade before moving assets. Where available, delivery-vs-payment settlement goes further by coordinating the asset and payment legs so neither side is expected to deliver first. BitGo’s Delivery-vs-Payment provides a way for institutions to exchange digital assets and payments while assets remain in regulated qualified custody until settlement.


Stablecoins are often used in OTC settlement because they allow digital asset transactions to settle across crypto-native rails. Fiat may also be used depending on the desk, client, jurisdiction, and counterparty setup.


## How to Evaluate an Institutional OTC Desk


An institutional OTC desk should be evaluated on liquidity, pricing discipline, settlement design, custody model, controls, and support. A narrow spread is useful only if the desk can fill the requested size under real market conditions.


Liquidity depth matters because institutional orders often need access to more than one venue or liquidity provider. A desk that can source liquidity across multiple counterparties may provide more reliable execution than a desk dependent on one venue.


The next feature to consider is coverage. Major assets (BTC and ETH), stablecoins, long-tail assets, and locked tokens each require different pricing and risk processes.


The settlement model is just as important. If assets must be prefunded to a trading venue, the institution takes on exposure before the trade is complete. If assets can remain in regulated custody until settlement, the workflow may better align with fiduciary, risk, and operational requirements.


Custody structure should be reviewed directly. Institutions need to know where assets are held, how accounts are segregated, which entity controls the assets, and what happens if the desk, venue, or counterparty faces stress.[Qualified custody](https://www.bitgo.com/products/qualified-custody/) ought to be regulated, insured, and secured via private keys held offline in cold storage.


Finally, operational controls are essential. The desk should support clear approval flows, post-trade reporting, exception handling, and escalation paths. Institutions also need to understand coverage hours, weekend processes, margin procedures for derivatives, and how failed settlement instructions are handled.


An OTC desk is part of an institution’s risk and trading infrastructure.


## OTC Crypto Derivatives and Locked Token Trading


Institutional OTC demand increasingly extends beyond spot execution. Some clients need hedging, yield, or financing against existing positions. Others need to manage concentrated token exposure, pre-unlock positions, or large treasury flows.


OTC derivatives crypto workflows can support objectives such as hedging downside risk, generating income, or expressing a directional view with leverage. These products may include options, swaps, forwards, baskets, or structured transactions. They can be useful when matched to a clear mandate, but they require more diligence than spot trades because of the greater complexity.


For OTC derivatives crypto workflows, the custody and collateral question is central. Institutions should understand margin, collateral, liquidation, and escalation details. The trade structure may


be economically attractive, but the operating model determines whether it can be managed safely.


The same logic applies to locked token trading. Venture funds, foundations, and early investors may hold assets that are locked, vesting, or subject to transfer restrictions. A desk that supports specialized liquidity can help institutions manage that exposure, but only if the trade terms, custody controls, transfer restrictions, legal review, and settlement mechanics are clear before the trade is executed.


Finally, a lot of product fragmentation can create operational risk. A fund might custody assets with one provider, trade spot with another, hedge with a third, borrow from a fourth, and settle through a separate network. Each additional relationship adds documentation, controls, reporting, collateral movement, and counterparty review.


A consolidated model—like[BitGo’s OTC derivatives](https://www.bitgo.com/resources/blog/bitgo-expands-institutional-otc-platform-enhanced-derivatives-trading/) —can simplify the model by providing all these features within a single counterparty.


## BitGo OTC Desk: OTC Execution Inside Qualified Custody


The[BitGo OTC desk launched publicly](https://www.bitgo.com/resources/blog/bitgo-unveils-secure-all-in-one-otc-trading-desk/) in February 2025 after operating in stealth mode since early 2024. The desk is a global, 24/7/365 institutional product covering spot trading, derivatives, lending, and yield products within its regulated, insured qualified custody framework.


The BitGo OTC desk allows clients to execute across spot, derivatives, and lending while assets remain in qualified custody until settlement. This design addresses a core institutional concern with OTC execution: the need to access liquidity without transferring assets to an execution venue before the trade is complete. Client assets also remain in regulated custody while trading. BitGo Bank & Trust, National Association maintains a $250M insurance policy on digital assets where BitGo Bank & Trust, National Association maintains all of the keys, subject to specific policy coverage. Clients seeking additional protection can also work with BitGo's insurance broker to purchase excess coverage. Full policy details and coverage terms are outlined in[BitGo's insurance FAQs.](https://www.bitgo.com/insurance-faqs/)


BitGo’s desk sources liquidity from dozens of exchanges and liquidity providers. It supports dynamic order types, including risk bid or offer, limit or stop, TWAP, VWAP, pegged orders, and percentage-of-volume execution. Institutions have many more execution paths than a single block trade.


For institutions, BitGo’s OTC desk launch places execution, custody, settlement, and lending inside one provider relationship, which may reduce the number of counterparties an institution has to manage.


## Conclusion


Regulated OTC is becoming a core part of institutional crypto market structure because large trades need more than exchange access. They need privacy, liquidity depth, quote discipline, custody controls, and reliable settlement.


OTC is not better than exchange trading in every case. The question is whether the trade size, asset, timing, and risk model justify a private execution workflow. For small orders, public markets may be sufficient. For block trades, OTC can provide a more controlled execution path.


## FAQs


### What Is Crypto OTC Trading?


Crypto OTC trading is the execution of large digital asset transactions outside public exchange order books. Institutions use OTC desks to negotiate pricing, source liquidity, and settle trades through a more private and controlled workflow.


### Why Do Institutions Use OTC Instead Of Exchanges?


Institutions use OTC when order size, privacy, settlement needs, or asset coverage make public exchange execution less suitable. OTC can reduce market impact, limit information leakage, and provide a negotiated price for a defined size.


### How Does RFQ Crypto Trading Work?


RFQ crypto trading starts with a client requesting a quote for a specific asset, size, side, and pair. The desk returns a quote based on liquidity and market conditions. If the client accepts within the quote window, the trade proceeds under the agreed terms.


### What Is OTC Settlement?


OTC settlement is the process of delivering assets and payment after an OTC trade is agreed. For institutions, settlement design matters because prefunding assets to a venue or desk can create counterparty exposure before the trade is complete.


### Why Does Qualified Custody Matter In OTC Trading?


Qualified custody matters because institutions need asset protection, governance, auditability, and regulatory alignment while trading. A custody-integrated OTC model can reduce the need to move assets out of custody before execution or settlement.


### Does OTC Trading Include Derivatives?


Yes. Some institutional OTC desks support spot trading as well as derivatives such as options, swaps, baskets, and structured products. These products can support hedging, income generation, and directional exposure, but they require careful collateral, liquidity, and governance controls.


## Table of Contents


- Key Takeaways
- Why Institutions Use OTC for Crypto Block Trades
- How RFQ Crypto Trading and OTC Settlement Work
- How to Evaluate an Institutional OTC Desk
- OTC Crypto Derivatives and Locked Token Trading
- BitGo OTC Desk: OTC Execution Inside Qualified Custody
- Conclusion
- FAQs


*The* digital asset infrastructure company.


## The latest


[All News](https://www.bitgo.com/resources/blog)


- [Gate US Joins BitGo's Go Network, Expanding Secure Access to Exchange Liquidity](https://www.bitgo.com/resources/blog/gate-us-joins-bitgos-go-network-expanding-secure-access-to-exchange-liquidity/)


- [Institutional Crypto Custody: A Guide for Asset Managers](https://www.bitgo.com/resources/blog/what-to-look-for-in-an-institutional-crypto-custody-provider/)


- [Regulated OTC: Institutional OTC Desks and Crypto Block Trades](https://www.bitgo.com/resources/blog/regulated-otc-institutional-otc-desks-and-crypto-block-trades/)


- [BitGo Prime: Connecting Institutions to Global Digital Asset Markets](https://www.bitgo.com/resources/blog/connecting-institutions-to-global-digital-asset-markets/)


**About BitGo**


BitGo is the digital asset infrastructure company, delivering custody, wallets, staking, trading, financing, and settlement services from regulated cold storage. Since our founding in 2013, we have been focused on accelerating the transition of the financial system to a digital asset economy. With a global presence and multiple regulated entities, BitGo serves thousands of institutions, including many of the industry's top brands, exchanges, and platforms, and millions of retail investors worldwide.
