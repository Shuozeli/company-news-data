---
schema_version: "1.0.0"
document_id: "02d52b6e95a0829b5056e4f091472d8383bdccc9d6b8ebf7fbed6e7af5fa595b"
company_key: "galaxy-digital-inc-class-a-common-stock"
company: "Galaxy Digital Inc. Class A Common Stock"
source_id: "galaxy-digital-inc-class-a-common-stock-news-import-fbc635ef0517"
canonical_url: "https://www.galaxy.com/insights/research/anthropic-fable-5-export-control-ai-regulation-last-model-problem"
published_at: null
first_seen_at: "2026-07-25T06:07:02.932709+00:00"
fetched_at: "2026-07-28T21:35:55.789196+00:00"
content_hash: "sha256:5c410131ec651974da642c76261ee450c961df2132b13824c277c65921684131"
---

# The Last Model Problem

*This alert was originally sent directly to clients of Galaxy Trading and Galaxy Asset Management on June 25, 2026. Trade or invest with Galaxy to receive the most timely research directly in your inbox.*


On Friday, June 12, at 5:21pm Eastern, Anthropic received an export-control directive from the Commerce Department ordering it to cut off Fable 5 and Mythos 5 to every foreign national on earth, including its own non-citizen employees. The government claimed someone had found a method to bypass Fable 5's safeguards and access the underlying Mythos model's cybersecurity capabilities. The artificial intelligence company could not segment users by nationality on the timeline the government demanded, so it disabled both models for everyone, worldwide, within hours. Every other Claude model stayed online. But two of the most capable large language models ever shipped disappeared due to a single, private letter from the government with no court order, no public filing, and no disclosed findings. Just on Wednesday of this week, Reddit users[posted](https://www.reddit.com/r/Anthropic/comments/1uejl4q/fable_5_coming_back/) that Fable 5 was added to a catalog on AWS Bedrock, so perhaps the cloud is lifting. But regardless, this episode creates substantial risk for AI, innovation, and American markets.


## Crossing the Rubicon


The U.S. government has effectively asserted that it can pull a commercial model off the market at will with an administrative action. While the mechanism was an export control, the market effect was a recall. The federal government has crossed the Rubicon on AI, moving from setting rules of the road to exercising a discretionary veto over which models reach the public and when. Once such power is established, it tends not to shrink on its own: if the government doesn’t reverse course, the next directive could be easier to issue than this one was.


The precedent is made even worse by the flimsiness of the trigger. The only outside expert who read the underlying research, Katie Moussouris of Luta Security,[described](https://www.lutasecurity.com/post/the-fable-5-export-controls-harm-us-cyber-defense) the supposed jailbreak in plain terms. Amazon researchers fed the models open-source code seeded with known and planted vulnerabilities and asked them to review it for security issues. The models refused. The researchers then asked them to fix the code, and the models complied.


Cybersecurity expert Katie Moussouris (Photo: Kristina D.C. Hoeppner/Wikimedia Commons)


Moussouris characterized this request as defensive prompting rather than a bypass, and[called it](https://fortune.com/2026/06/15/fix-this-code-three-words-behind-us-government-shut-down-anthropic-fable-mythos-ai-models-katie-moussouris-open-letter/) the most valuable thing an AI can do for a security team. The three words that took down the most powerful cyber-defense model on the market were, by the account of the one person who read the file, "fix this code."


The Department of Commerce did not publish its directive to Anthropic or the reasoning behind it. Nothing was published on Commerce’s website or in the Federal Register, or anywhere else that we can find. The directive instead came in the form of a private letter from Commerce’s Bureau of Industry and Security, which neither the department nor Anthropic has made public. The authority under which Commerce issued the directive is also not quite known. The Center for Strategic & International Studies (CSIS)[suggested](https://www.csis.org/analysis/department-commerce-restricted-access-anthropics-latest-models-what-comes-next) the department may be relying on the Export Control Reform Act of 2018 (“ECRA”), using what is called “is informed” authority, where Commerce privately tells a company that a license is now required. Such requirements are administered through the Export Administration Regulations (“EAR”). But there is no regulatory framework in the EAR for this statutory authority, which is why it was never used before as the basis for issuing a control, and Commerce has not developed a regulation implementing it.


## The Standard that Cannot Be Met


Anthropic's own[defense](https://www.anthropic.com/news/fable-mythos-access) contains the sentence that condemns the policy. The company stated that perfect jailbreak resistance is "not currently possible" for any provider, and that universal bypasses will likely be found eventually. Security researchers have[said this for years](https://arxiv.org/abs/2307.15043) : no deployed model is provably safe against a determined adversary. Closed API models can be[jailbroken at the prompt layer](https://github.com/llm-attacks/llm-attacks) .[Open-weight models](https://hai.stanford.edu/ai-definitions/what-is-an-open-weight-model) can be[abliterated](https://arxiv.org/abs/2406.11717) , a process which[strips the refusal behavior](https://github.com/andyrdt/refusal_direction) out of the weights themselves. If weights ever leak (and[they](https://tech.slashdot.org/story/23/03/07/1841256/facebooks-powerful-large-language-model-leaks-online)[have](https://venturebeat.com/ai/mistral-ceo-confirms-leak-of-new-open-source-ai-model-nearing-gpt-4-performance) ), a closed model will have the same vulnerabilities as the open one.


The government's implied standard cannot hold against that reality. If deployment requires that no method exist to elicit dangerous capability, the standard is unmeetable by construction. Anthropic cannot certify a negative its own engineers say is false, and neither can anyone else. By Anthropic's own[reasoning](https://fortune.com/2026/06/13/anthropic-fable-mythos-models-commerce-deparment-export-restrictions-jailbreak-defense-prompting/) , applying this test across the industry would halt[frontier AI model](https://www.nvidia.com/en-us/glossary/frontier-models/) deployment entirely. A bar no provider can clear is not a safety threshold. It is a discretionary veto in a lab coat.


## The Surveillance Option


Suppose Anthropic wanted to satisfy the letter of the directive, keeping foreign nationals out while serving Americans. Only full identity verification of every user could achieve that. Anthropic could implement full know-your-customer (KYC) onboarding, requiring citizenship and residency documents, the same friction of opening a brokerage account. With this, Anthropic could gate access by nationality (though its own employees could still be locked out). But without it, preventing “foreign” people from accessing Fable 5 would be impossible. Reporting already indicates Anthropic is[preparing](https://www.techzine.eu/news/security/142189/fix-this-code-three-words-behind-the-export-ban-on-claude-fable-5/) user identity verification to comply, and[leaked code](https://decrypt.co/372004/leaked-code-anthropic-preparing-fable-5-subscription) seems to confirm it. It’s building the surveillance option, but it should stop.


Surveillance infrastrcture is being built across the West. (Image: Blue Ākāśha/Wikimedia Commons)


The infrastructure for the surveillance option is already being built across the West. The U.K.'s Online Safety Act, in force since July 2025, requires what the government’s Office of Communications (Ofcom) calls[highly effective age assurance](https://en.wikipedia.org/wiki/Online_age_verification_in_the_United_Kingdom) . Accepted methods include photo ID, facial age estimation, and Open Banking checks (in which a bank confirms a user's age from account data without sharing the underlying financial details). Roughly 19 U.S. states have[passed](https://en.wikipedia.org/wiki/Social_media_age_verification_laws_in_the_United_States) comparable identity gates, several now in First Amendment litigation. The Electronic Frontier Foundation, which opposes all of this,[warns](https://www.eff.org/deeplinks/2025/12/age-verification-coming-internet-we-built-you-resource-hub-fight-back) that mandatory verification builds honeypots of the most sensitive data and ends online anonymity.


KYC for model access would import every one of those harms into the one technology most able to act on the data it hoards. No frontier lab should require it, and the government should not be the reason one does. The internet should remain open and free and access to the knowledge and power AI brings should be accessible to all.


## The Open-Source Problem


The export-control approach is also self-defeating, and the reason is the open-weight ecosystem. The frontier does not belong to a handful of U.S. companies. The[open letter](https://www.darkreading.com/vulnerabilities-threats/security-community-slams-us-ban-on-exporting-mythos-fable) signed by more than a hundred security leaders, organized by Alex Stamos and including Bruce Schneier, Casey Ellis, and Paul Vixie, makes the point flatly: Chinese open-weight models trail the best American systems by months, not years, and those are only the ones the public knows about.


If export-control vetoes keep the leading American labs from shipping their best work, development will not stop, it will just move to where the veto cannot reach: cleared government programs, foreign labs, and the open-weight ecosystem. Open models that trail by months today will close the gap once the thing they are chasing stops moving. Within a year or two of a sustained freeze, the most capable model an ordinary person or company can run could be an open-weight system from outside the United States, sitting on a laptop, with weaker guardrails than the model Washington just effectively recalled.


What will the government do then? It cannot recall a model already mirrored across a thousand hard drives and a hundred file-sharing networks. It can try to ban the publication of weights, but that is where the policy collides with the Constitution.


The United States fought this fight before and lost. In the 1990s, the U.S. government placed strong encryption on the U.S. Munitions List and controlled it as a weapon under the ITAR,[listing](https://www.loundy.com/Roadside_T-Shirt.html) cryptographic software alongside laser targeting systems and particle-beam weapons. The government then spent three years investigating[Phil Zimmermann](https://en.wikipedia.org/wiki/Phil_Zimmermann) over the global spread of his PGP (the humbly named “Pretty Good Privacy”) encryption software, on the theory that posting code to the internet made him an arms exporter. The feds[dropped](https://vice.com/en_us/article/jpgvy3/encryption-debate-the-end-of-end-to-end) the case in 1996 without charges.


Phil Zimmerman, creator of PGP encryption (Photo: Matt Crypto/Wikimedia Commons)


Zimmermann's answer became a landmark of the era. He[published](https://www.philzimmermann.com/EN/essays/BookPreface.html) PGP's complete source code as a hardcover book through MIT Press, on the logic that a printed book is plainly protected speech even when the same code in electronic form is deemed a controlled munition. Activists pressed the same point onto a T-shirt,[printing](http://www.cypherspace.org/adam/shirt/) cryptographer (and future Bitcoiner) Adam Back's compact[RSA](https://math.mit.edu/research/highschool/primes/circle/documents/2024/Honglin.pdf) cipher beneath a[warning](https://fortune.com/2026/06/15/fix-this-code-three-words-behind-us-government-shut-down-anthropic-fable-mythos-ai-models-katie-moussouris-open-letter/) that the shirt itself was a munition. The courts agreed on the principle. In the Bernstein and Junger litigation, federal judges held that[source code is speech](https://www.eff.org/deeplinks/2019/08/us-export-controls-and-published-encryption-source-code-explained)[protected](https://law.justia.com/cases/federal/district-courts/FSupp/974/1288/1451176/) by the First Amendment. And, in 1996, the government moved encryption off the munitions list to the Commerce Department,[dismantling](https://en.wikipedia.org/wiki/Crypto_Wars) the controls (and paving the way for the growth of the internet we have today). Moussouris, who later helped win defensive-security carve-outs in the[Wassenaar Arrangement](https://thehill.com/opinion/cybersecurity/365352-serious-progress-made-on-the-wassenaar-arrangement-for-global/) , reached for that same history in her[response](https://www.lutasecurity.com/post/the-fable-5-export-controls-harm-us-cyber-defense) : model weights are numbers; publishing them is expression. An attempt to suppress open models at scale would be a generational First Amendment fight, and the government would enter it from a weak position, having already conceded that the capability is widely available elsewhere.


So, the export-control approach fails twice over. It would not stop adversaries, which have their own systems and, given news site Semafor's reporting that the White House suspected a China-linked group had obtained access, may[already have this one](https://www.darkreading.com/vulnerabilities-threats/security-community-slams-us-ban-on-exporting-mythos-fable) . And it would surrender the public frontier to open and foreign models that Washington has no lawful way to control.


## Anthropic Punished for Candor


It’s worth noting that Anthropic told the truth. It acknowledged that perfect safeguards do not exist,[red-teamed](https://www.ibm.com/think/topics/red-teaming) Fable for thousands of hours with the U.S. and U.K. governments before launch, and disclosed the limits of its own defenses. That candor became the evidence used against it. A lab that tested less and admitted nothing would have presented a smaller target. When honesty about residual risk is the trigger for enforcement, the system trains every provider to say less, a perverse incentive.


The defenders see the same inversion from the other side. Moussouris and her co-signers argue the recall kneecaps the people who use these tools to find and fix bugs before attackers do, while leaving the attackers untouched. The capability the government fears and the capability defenders depend on are the same capability. You cannot strip out one without removing the other.


## The Case for the Ban


To be clear, some reporting suggests the government has reason to be worried. Senate testimony reported in late June, relayed by Sen. Mark Warner (D-VA) and[attributed](https://www.economist.com/briefing/2026/06/14/donald-trumps-blocking-of-anthropic-is-capricious-and-chaotic) to NSA Director General Joshua Rudd, described Mythos breaching nearly all of the agency's classified systems within hours during an authorized red-teaming exercise (though the Economist reporter who published the story[walked it back](https://x.com/shashj/status/2069078104941961293) mildly). Mythos was the[first](https://fortune.com/2026/06/15/fix-this-code-three-words-behind-us-government-shut-down-anthropic-fable-mythos-ai-models-katie-moussouris-open-letter/) model to clear both of the UK AI Security Institute's cyber test ranges. That is a serious capability and a serious data point. It argues for a serious process, not a Friday night letter with no findings attached.


Also, Mythos was always restricted to vetted partners. The model disabled for the entire planet was Fable, the consumer version, whose guardrails route sensitive cyber and bio requests to the older Opus 4.8. Recalling the guarded product worldwide over a defensive-prompting demo, while the genuinely dangerous version was never publicly available in the first place, is the response of a process that has confused capability with deployment.


## Opus 4.8: The Last Model?


Follow the logic to its conclusion and it doesn’t look good. If Fable cannot clear the bar, nothing more capable will, because every future model will be more capable, and therefore more dangerous, by exactly the metric the government is using. There is no Fable 5.1 or Fable 5.2 that is more jailbreak-proof against an unmeetable standard. Claude Opus 4.8, the most powerful model left alone by Commerce’s directive, has become the high-water mark for public frontier access in the United States. The lawful path to deploy the new technology closed while the unlawful and foreign paths stayed wide open.


This is the worst of every world at once: a domestic freeze, a surveillance apparatus built to administer it, and a frontier ceded to open-weight and foreign models beyond American reach and American safety standards. All of it is avoidable, and the fix is the process Anthropic itself[asked for](https://www.anthropic.com/news/fable-mythos-access) : the government should be able to block genuinely unsafe deployments through a statutory mechanism that is transparent, grounded in disclosed technical findings, and open to challenge. The threshold should be tied to demonstrated model-specific uplift (i.e., enhancement of dangerous capabilities) over what is already public, and not the fantasy of zero residual risk the government is calling for. Where a gate is genuinely needed, it should target[capability](https://www.techpolicy.press/did-the-us-government-just-set-an-ai-export-precedent-by-blocking-mythos/) rather than identity, because a regime that can only enforce its rules by fingerprinting every user has reached for the most dangerous instrument available to solve a narrow problem.


There is also a market argument for reversing this directive, and it is far larger than Anthropic. The Magnificent Seven now make up roughly a third of the S&P 500, and about 42 percent of the index's entire 2025 total return[came](https://www.investmentnews.com/equities/mag-7-for-tomorrow/264753) from those seven names. Nvidia alone crossed $4 trillion in July 2025 and $5 trillion by October, at one point worth[more than 7 percent](https://en.wikipedia.org/wiki/AI_bubble) of the whole index. The four largest hyperscalers are guiding to[roughly $725 billion of capital expenditure in 2026](https://www.tomshardware.com/tech-industry/big-tech/big-techs-ai-spending-plans-reach-725-billion) , up 77 percent from $410 billion the year before, and Goldman now[models](https://finance.yahoo.com/sectors/technology/article/meta-microsoft-amazon-and-alphabet-are-about-to-spend-a-shocking-amount-of-money-to-dominate-the-ai-era-115359575.html) $5.3 trillion of hyperscaler capex through 2030. That spending has literally become macroeconomic: estimates vary widely, from Goldman[pegging](https://www.investing.com/analysis/2026-another-year-of-ai-bubble-not-bursting-200672634) AI capex near 0.8 percent of GDP to more aggressive readings that credit it with the[majority](https://www.techi.com/ai-capex-carries-us-economy-token-factories/) of US output growth in early 2026.


All of this investment and prospects for growth rests on the assumption that frontier models keep improving and keep reaching customers, generating the revenue that eventually justifies the build. The assumption seems already stretched. OpenAI has[committed](https://techcrunch.com/2025/11/06/sam-altman-says-openai-has-20b-arr-and-about-1-4-trillion-in-data-center-commitments/) to roughly $1.4 trillion of spending over eight years against about[$13 billion](https://finance.yahoo.com/news/sam-altman-shuts-down-openai-180833310.html) in current revenue (Sam Altman[disputes](https://fortune.com/2025/11/01/sam-altman-openai-annual-revenue-13-billion-forecast-100-billion-2027/) the $13 billion number, saying OpenAI’s revenue is “well more than that”). The capex is being pulled forward against AI income that has not yet shown up in the macro data. Investors are paying for terminal value, for a future in which these systems are deployed at scale.


> ***With the stock market highly concentrated on the AI thesis, any slowing (let alone reversal) of the frontier could damage portfolios worldwide.***


The Fable directive introduces a significant variable to the mix: whether Washington will permit models to ship at all. If a deployment veto becomes routine, and the logic above suggests it could, then the growth that underwrites $725 billion of annual capex loses its anchor, and so could everything stacked on top of it: a memory supercycle that has sold out high-bandwidth memory through 2026 and driven DRAM prices[up more than 50 percent](https://www.cnbc.com/2026/01/10/micron-ai-memory-shortage-hbm-nvidia-samsung.html) in a single quarter, pushing SK Hynix[past a $1 trillion valuation](https://www.benzinga.com/markets/tech/26/06/53267631/nvidia-supplier-sk-hynix-ships-next-gen-hbm-samples-as-ai-demand-surges) ; a power buildout so large that hyperscalers are[signing](https://nextwavesinsight.com/hyperscaler-ai-capex-microsoft-google-amazon-meta-2026/) dedicated nuclear contracts to feed it; and a lattice of[circular financing](https://www.bloomberg.com/graphics/2026-ai-circular-deals/) that ties Nvidia, OpenAI, Oracle, CoreWeave, and Microsoft into one another. You cannot earn a return on a two-hundred-billion-dollar data center built to serve a model the government will not let you deploy. And with the stock market highly concentrated on the AI thesis, any slowing (let alone reversal) of the frontier could damage portfolios worldwide.


More than 100 of the country's leading cyber defenders have[signed](https://freefable.org/) their names asking Washington to[reverse course](https://fortune.com/2026/06/15/fix-this-code-three-words-behind-us-government-shut-down-anthropic-fable-mythos-ai-models-katie-moussouris-open-letter/) . Anthropic, which confidentially filed to go public this month at a reported[valuation](https://www.cnbc.com/2026/06/01/anthropic-ipo-s1-prospectus.html) near $965 billion, is now a company whose flagship can be switched off by one agency on one evening, with no finding it can contest. This approach to AI regulation should be undone before it hardens into the way American AI is governed. If this approach to AI regulation becomes the enduring framework for American AI governance, Anthropic, AI development generally, and American technological leadership will be substantially affected.


Legal Disclosure:


This document, and the information contained herein, has been provided to you by Galaxy Digital Inc. and its affiliates (“Galaxy Digital”) solely for informational purposes. This document may not be reproduced or redistributed in whole or in part, in any format, without the express written approval of Galaxy Digital. Neither the information, nor any opinion contained in this document, constitutes an offer to buy or sell, or a solicitation of an offer to buy or sell, any advisory services, securities, futures, options or other financial instruments or to participate in any advisory services or trading strategy. Nothing contained in this document constitutes investment, legal or tax advice or is an endorsement of any of the stablecoins mentioned herein. You should make your own investigations and evaluations of the information herein. Any decisions based on information contained in this document are the sole responsibility of the reader. Readers should consult with their own advisors and rely on their independent judgement when making financial or investment decisions.


Participants, along with Galaxy Digital, may hold financial interests in certain assets referenced in this content. Galaxy Digital regularly engages in buying and selling financial instruments, including through hedging transactions, for its own proprietary accounts and on behalf of its counterparties. Galaxy Digital also provides services to vehicles that invest in various asset classes. If the value of such assets increases, those vehicles may benefit, and Galaxy Digital’s service fees may increase accordingly. The information and analysis in this communication are based on technical, fundamental, and market considerations and do not represent a formal valuation. For more information, please refer to Galaxy’s public filings and statements. Certain asset classes discussed, including digital assets, may be volatile and involve risk, and actual market outcomes may differ materially from perspectives expressed here.


For additional risks related to digital assets, please refer to the risk factors contained in filings Galaxy Digital Inc. makes with the Securities and Exchange Commission (the “SEC”) from time to time, including in its Quarterly Report on Form 10-Q for the quarter ended September 30, 2025, filed with the SEC on November 10, 2025, available at www.sec.gov.


Certain statements in this document reflect Galaxy Digital’s views, estimates, opinions or predictions (which may be based on proprietary models and assumptions, including, in particular, Galaxy Digital’s views on the current and future market for certain digital assets), and there is no guarantee that these views, estimates, opinions or predictions are currently accurate or that they will be ultimately realized. To the extent these assumptions or models are not correct or circumstances change, the actual performance may vary substantially from, and be less than, the estimates included herein. None of Galaxy Digital nor any of its affiliates, shareholders, partners, members, directors, officers, management, employees or representatives makes any representation or warranty, express or implied, as to the accuracy or completeness of any of the information or any other information (whether communicated in written or oral form) transmitted or made available to you. Each of the aforementioned parties expressly disclaims any and all liability relating to or resulting from the use of this information. Certain information contained herein (including financial information) has been obtained from published and non-published sources. Such information has not been independently verified by Galaxy Digital and, Galaxy Digital, does not assume responsibility for the accuracy of such information. Affiliates of Galaxy Digital may have owned, hedged and sold or may own, hedge and sell investments in some of the digital assets, protocols, equities, or other financial instruments discussed in this document. Affiliates of Galaxy Digital may also lend to some of the protocols discussed in this document, the underlying collateral of which could be the native token subject to liquidation in the event of a margin call or closeout. The economic result of closing out the protocol loan could directly conflict with other Galaxy affiliates that hold investments in, and support, such token. Except where otherwise indicated, the information in this document is based on matters as they exist as of the date of preparation and not as of any future date, and will not be updated or otherwise revised to reflect information that subsequently becomes available, or circumstances existing or changes occurring after the date hereof. This document provides links to other Websites that we think might be of interest to you. Please note that when you click on one of these links, you may be moving to a provider’s website that is not associated with Galaxy Digital. These linked sites and their providers are not controlled by us, and we are not responsible for the contents or the proper operation of any linked site. The inclusion of any link does not imply our endorsement or our adoption of the statements therein. We encourage you to read the terms of use and privacy statements of these linked sites as their policies may differ from ours. The foregoing does not constitute a “research report” as defined by FINRA Rule 2241 or a “debt research report” as defined by FINRA Rule 2242 and was not prepared by Galaxy Digital Partners LLC. Similarly, the foregoing does not constitute a “research report” as defined by CFTC Regulation 23.605(a)(9) and was not prepared by Galaxy Derivatives LLC. For all inquiries, please email[\[email protected\]](https://www.galaxy.com/cdn-cgi/l/email-protection) .


©Copyright Galaxy Digital Inc. 2026. All rights reserved.
