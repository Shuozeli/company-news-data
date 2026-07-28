---
schema_version: "1.0.0"
document_id: "7e67cb3cc24bc283b4c6981ae6dcccb39410e50ff69952e4ce19098890f922e7"
company_key: "galaxy-digital-inc-class-a-common-stock"
company: "Galaxy Digital Inc. Class A Common Stock"
source_id: "galaxy-digital-inc-class-a-common-stock-news-import-fbc635ef0517"
canonical_url: "https://www.galaxy.com/insights/research/ostium-left-an-opening-for-exploiters-and-24m-went-out-the-door"
published_at: null
first_seen_at: "2026-07-25T06:07:02.932709+00:00"
fetched_at: "2026-07-28T21:35:55.789196+00:00"
content_hash: "sha256:b34070e8bd1fb6fc3116ee23742717ea6267b88aaf93b8e6ad7201c1da85003d"
---

# Ostium Left an Opening for Exploiters and $24m Went Out the Door

*This article originally appeared in Galaxy Research's weekly newsletter.*[Subscribe](https://www.galaxy.com/subscribe-to-research?utm_campaign=Weekly%20Research%20Brief%20-%20Email&utm_medium=email&utm_source=hs_email&_hsenc=p2ANqtz--YWOkviRZJsa_uYNPjl2N4ahqTpHeV86Rs9VQQeL9MWn1U09L_xNxjRhoRyGaaBrCPLXuX) *to get the most timely insights delivered to your inbox every Friday morning.*


**Thieves made off with an**[estimated](https://arkm.com/explorer/entity/456a2624-9f5f-40da-a124-9552894443ed) **$23.75 million worth of the USDC stablecoin Wednesday after**[exploiting](https://x.com/kaledora/status/2077525044733837736) **Ostium, a platform for synthetic trading of stocks, commodities, forex, and crypto onchain.**


The exploit was carried out over a sequence of eight transactions in which funds left Ostium’s[OLP vault](https://arbiscan.io/address/0x20d419a8e12c45f88fda7c5760bb6923cee27f98) :


-


[Transaction 1](https://arbiscan.io/tx/0x4b7ff5de823dd7af29cf1a6602a84d7b6eee354edcbaf0427fd5e691d3d80951) totaling 898 USDC


-


[Transaction 2](https://arbiscan.io/tx/0x359f8c05b86a4409d60cfba02084334313fd94b19f74a294fb7fc4ea7d4870e0) totaling 11.86 million USDC


-


[Transaction 3](https://arbiscan.io/tx/0x56e4139a2f51e99933479becee21812dd2ec656128f6f3593a7fa225e2f24adc) totaling 13,480 USDC


-


[Transaction 4](https://arbiscan.io/tx/0x397daa6c23c87670f949a970961b1014e966cc40301a99b55c3c1908dd61418e) totaling 13,480 USDC


-


[Transaction 5](https://arbiscan.io/tx/0xd9f91cc3eaec695f45bffad3a068fa52e1625ed44bfcc47d6ac3938f78d9061d) totaling 4.49 million USDC


-


[Transaction 6](https://arbiscan.io/tx/0x3b04639ab9b40760b2138e7bfa7eccc9657f3a767a5c414dbb1b3632ed71f3bf) totaling 3.59 million USDC


-


[Transaction 7](https://arbiscan.io/tx/0x6c254483fa47a14622662e792bc3728ab3c408a33d3cbb5712434ba96f5ecdc2) totaling 2.7 million USDC


-


[Transaction 8](https://arbiscan.io/tx/0xfaf6d3d4d7f1a75bfc11fb4d36d0525791546267fda1cdd371703ce03ae8ba8c) totaling 1.08 million USDC


All eight transactions paid out to the same wallet,[0x321Df1...8bfD9](https://arbiscan.io/token/0xaf88d065e77c8cc2239327c5edb3a432268e5831?a=0x321df194646029e7a6193ea05573d4b9c398bfd9#transactions) . The largest single payout transaction was executed in a single atomic batch that looped through open-and-close cycles. Every transaction routed through the same contract pair (Ostium: Trading → Ostium: Private PriceUpKeep).


Ostium, which runs on Arbitrum, lets users trade leveraged synthetic positions on forex, commodities, indices, stocks, and crypto. All activity is settled onchain in USDC. Users trade synthetic perpetual contracts that track the prices of underlying assets, and there is no delivery of the underlying or fixed expiries on user trades. The Ostium Liquidity Pool (OLP) is the vault side of all this. Liquidity providers deposit USDC and receive[OLP tokens](https://ostium-labs.gitbook.io/ostium-docs/vault/olp-token) representing their pro-rata share of the pool, which is used to back perpetual positions and to provide liquidity for trader profit and loss (PnL) settlement.


The issue arises from how Ostium's oracle system authorizes price data. The verifier takes a price report, derives the signer from the signature, and checks that the signer is on an authorized list. It simply validates the signer's identity, not whether the price itself is accurate. An attacker who held both an authorized oracle-signer key and a registered[PriceUpKeep](https://arbiscan.io/address/0xb71ec9ebd8145dacacf6724363143cb5667a3d36#code) forwarder (the keeper role responsible for fulfilling pending orders) used that combination to submit a future-dated, correctly signed price report and then repeatedly opened and closed positions against it. This allowed them to appear to generate trading profits from the view of the system without any real market exposure. Both the signer and forwarder roles are meant to be[granted](https://x.com/tempst0/status/2077449926544433395) only by Ostium governance/timelock and are not supposed to be self-assignable; the exploit worked because the attacker obtained legitimate credentials for each, not because of a flaw in Ostium’s trading logic itself.


#### **OUR TAKE**


The Ostium incident is one of a number of major application exploits that have happened this year, including at[Drift](https://www.galaxy.com/insights/research/weekly-top-stories-04-17-26) and[KelpDAO’s](https://www.galaxy.com/insights/research/kelpdao-layerzero-exploit-defi)[rsETH](https://www.galaxy.com/insights/research/weekly-top-stories-04-24-26) . A common theme has been that smart contracts and the logic they contain have held up, and the main targets for exploiters have been operational infrastructure and human trust (the compromised signer credentials in Ostium's case, the socially engineered pre-signed admin takeover in Drift's case, and the poisoned RPC infrastructure behind KelpDAO's rsETH bridge).


After each of these high-profile exploits, some have called for safeguards around user funds on applications, such as throttled withdrawals, to disincentivize nefarious actors and limit the loss of funds in the event an exploit occurs. These proposals should be resisted.


Throttling withdrawals introduces censorship risk directly at the application layer. The moment a protocol can unilaterally delay or cap what a user can deposit or withdraw, self-custody becomes conditional instead of absolute. In this case, the app, not the user, decides when funds are accessible and how they can be used. It also collapses the distinction between the exploiter and the average user in the sense that a safeguard designed to slow down an attacker necessarily applies to everyone using the app at that moment. By design, apps would start treating ordinary users as suspects, with no way to distinguish intent in real time.


The slippery slope risk compounds this. Once a protocol builds in the technical capability to throttle or freeze deposits and withdrawals, that capability becomes precedent. Regulators can point to it as evidence that these applications already have the tool to comply with freeze orders, KYC gating, or other requirements and should therefore be required too. A safeguard built to stop attackers can become a hook that pulls a protocol toward obligations they would otherwise be incapable of meeting.


Moreover, innocent market actors will become incentivized to route around the frictions introduced by such measures. In this case, risk can become displaced rather than contained. Users locked behind a throttle will look for a way to exit their economic exposure anyway, which typically means a tradeable claim on the delayed deposit emerges to fill the gap (such as a receipt token, an IOU, a wrapped stand-in for "your funds, pending release"). That claim becomes a new dependency with its own risk surface at both the market level (a peg that can break, a discount that widens under panic) and the technical level (a new contract, a new oracle, a new thing that can be exploited independently of the application it's supposed to represent). The safeguard meant to contain one point of failure ends up compounding the very fragility it was built to prevent.


None of this means protocols shouldn’t harden the parts of the stack that actually failed here (e.g. signer key management, verifier redundancy, admin timelocks, social-engineering awareness). But the fix for weaknesses in operational infrastructure and human trust is hardening those things, not adding new discretionary controls over user funds that undermine the core value proposition of the thing being protected.


Legal Disclosure:


This document, and the information contained herein, has been provided to you by Galaxy Digital Inc. and its affiliates (“Galaxy Digital”) solely for informational purposes. This document may not be reproduced or redistributed in whole or in part, in any format, without the express written approval of Galaxy Digital. Neither the information, nor any opinion contained in this document, constitutes an offer to buy or sell, or a solicitation of an offer to buy or sell, any advisory services, securities, futures, options or other financial instruments or to participate in any advisory services or trading strategy. Nothing contained in this document constitutes investment, legal or tax advice or is an endorsement of any of the stablecoins mentioned herein. You should make your own investigations and evaluations of the information herein. Any decisions based on information contained in this document are the sole responsibility of the reader. Readers should consult with their own advisors and rely on their independent judgement when making financial or investment decisions.


Participants, along with Galaxy Digital, may hold financial interests in certain assets referenced in this content. Galaxy Digital regularly engages in buying and selling financial instruments, including through hedging transactions, for its own proprietary accounts and on behalf of its counterparties. Galaxy Digital also provides services to vehicles that invest in various asset classes. If the value of such assets increases, those vehicles may benefit, and Galaxy Digital’s service fees may increase accordingly. The information and analysis in this communication are based on technical, fundamental, and market considerations and do not represent a formal valuation. For more information, please refer to Galaxy’s public filings and statements. Certain asset classes discussed, including digital assets, may be volatile and involve risk, and actual market outcomes may differ materially from perspectives expressed here.


For additional risks related to digital assets, please refer to the risk factors contained in filings Galaxy Digital Inc. makes with the Securities and Exchange Commission (the “SEC”) from time to time, including in its Quarterly Report on Form 10-Q for the quarter ended September 30, 2025, filed with the SEC on November 10, 2025, available at www.sec.gov.


Certain statements in this document reflect Galaxy Digital’s views, estimates, opinions or predictions (which may be based on proprietary models and assumptions, including, in particular, Galaxy Digital’s views on the current and future market for certain digital assets), and there is no guarantee that these views, estimates, opinions or predictions are currently accurate or that they will be ultimately realized. To the extent these assumptions or models are not correct or circumstances change, the actual performance may vary substantially from, and be less than, the estimates included herein. None of Galaxy Digital nor any of its affiliates, shareholders, partners, members, directors, officers, management, employees or representatives makes any representation or warranty, express or implied, as to the accuracy or completeness of any of the information or any other information (whether communicated in written or oral form) transmitted or made available to you. Each of the aforementioned parties expressly disclaims any and all liability relating to or resulting from the use of this information. Certain information contained herein (including financial information) has been obtained from published and non-published sources. Such information has not been independently verified by Galaxy Digital and, Galaxy Digital, does not assume responsibility for the accuracy of such information. Affiliates of Galaxy Digital may have owned, hedged and sold or may own, hedge and sell investments in some of the digital assets, protocols, equities, or other financial instruments discussed in this document. Affiliates of Galaxy Digital may also lend to some of the protocols discussed in this document, the underlying collateral of which could be the native token subject to liquidation in the event of a margin call or closeout. The economic result of closing out the protocol loan could directly conflict with other Galaxy affiliates that hold investments in, and support, such token. Except where otherwise indicated, the information in this document is based on matters as they exist as of the date of preparation and not as of any future date, and will not be updated or otherwise revised to reflect information that subsequently becomes available, or circumstances existing or changes occurring after the date hereof. This document provides links to other Websites that we think might be of interest to you. Please note that when you click on one of these links, you may be moving to a provider’s website that is not associated with Galaxy Digital. These linked sites and their providers are not controlled by us, and we are not responsible for the contents or the proper operation of any linked site. The inclusion of any link does not imply our endorsement or our adoption of the statements therein. We encourage you to read the terms of use and privacy statements of these linked sites as their policies may differ from ours. The foregoing does not constitute a “research report” as defined by FINRA Rule 2241 or a “debt research report” as defined by FINRA Rule 2242 and was not prepared by Galaxy Digital Partners LLC. Similarly, the foregoing does not constitute a “research report” as defined by CFTC Regulation 23.605(a)(9) and was not prepared by Galaxy Derivatives LLC. For all inquiries, please email[\[email protected\]](https://www.galaxy.com/cdn-cgi/l/email-protection) .


©Copyright Galaxy Digital Inc. 2026. All rights reserved.
