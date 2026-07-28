---
schema_version: "1.0.0"
document_id: "413276ba9e57f4952990b5191c21594bb6316cc43d0604cad67186a0736d5f01"
company_key: "yc-algotest"
company: "AlgoTest"
source_id: "yc-algotest-news-import-7cc502b412f0"
canonical_url: "https://algotest.in/blog/nifty-lot-size/"
published_at: "2026-07-21T08:26:56+00:00"
first_seen_at: "2026-07-25T00:56:57.418756+00:00"
fetched_at: "2026-07-28T21:21:00.620727+00:00"
content_hash: "sha256:30dd99a6248db394da9ba29992b5d643c0aaf3a1e8278228f2c564d2516445c2"
---

# Nifty Lot Size Explained: Nifty, Bank Nifty, FINNIFTY & Midcap Nifty Lot Sizes

# Nifty Lot Size Explained: Nifty, Bank Nifty, FINNIFTY & Midcap Nifty Lot Sizes


[AlgoTest](https://algotest.in/blog/author/algotest/)


Jul 21, 2026


•


6 min read


•


[General](https://algotest.in/blog/category/general/)


- [Twitter / X](https://twitter.com/intent/tweet?url=https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F&text=Nifty%20Lot%20Size%20Explained%3A%20Nifty%2C%20Bank%20Nifty%2C%20FINNIFTY%20%26%20Midcap%20Nifty%20Lot%20Sizes)
- [Facebook](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F)
- [LinkedIn](https://www.linkedin.com/shareArticle?mini=true&url=https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F&title=Nifty%20Lot%20Size%20Explained%3A%20Nifty%2C%20Bank%20Nifty%2C%20FINNIFTY%20%26%20Midcap%20Nifty%20Lot%20Sizes)
- [WhatsApp](https://api.whatsapp.com/send?text=Nifty%20Lot%20Size%20Explained%3A%20Nifty%2C%20Bank%20Nifty%2C%20FINNIFTY%20%26%20Midcap%20Nifty%20Lot%20Sizes%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F)
- [Ask ChatGPT](https://chatgpt.com/?hints=search&q=Summarize%20this%20article:%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F)
- [Ask Claude](https://claude.ai/new?q=Summarize%20this%20article:%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F)
- [Ask Grok](https://grok.com/?q=Summarize%20this%20article:%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fnifty%2Dlot%2Dsize%2F)
- Copy link


A lot size is the fixed number of units you trade in one Nifty futures or options contract. You don't buy "1 unit" of Nifty the way you'd buy 1 share of Reliance, every trade happens in multiples of this number.


Get it wrong, and your risk calculation is off, sometimes by lakhs. We cover the latest Nifty, Bank Nifty, FINNIFTY and Midcap Nifty lot sizes, why NSE keeps revising them, and how to use this number correctly when you're trading or backtesting.


## What Is Nifty Lot Size?


An index itself isn't something you can deliver. Nifty 50 is just a number calculated from 50 stocks, it doesn't exist as a physical asset you can hand over.


To let people trade a view on that number, NSE created a standardized contract. One lot equals the index value multiplied by a fixed quantity, currently 65 units for Nifty 50.


So when someone asks about the Nifty 1 lot size, this is the number they're asking about. It only changes when NSE issues a new circular, which we'll cover later in this guide.


## Latest Nifty Lot Size


Here's where things stand right now, based on NSE's most recent revision:


Instrument


Current Lot Size


Applicable Since


Nifty 50


65


January 2026 series


Bank Nifty


30


January 2026 series


FINNIFTY (Nifty Financial Services)


60


January 2026 series


Midcap Nifty (Nifty Midcap Select)


120


January 2026 series


NSE reviews these numbers periodically, roughly every six months, under a SEBI-mandated framework. Don't treat these as permanent.


Always confirm the lot size on your trading terminal before placing an order. A mental note from even a year ago can already be outdated.


Related:[Nifty Expiry Day Explained](https://algotest.in/blog/nifty-expiry-day)


## Why Does NSE Change Lot Sizes?


SEBI wants every index derivative contract to represent a broadly similar amount of money, no matter which index you trade. When an index rallies hard, the value of one lot balloons, pricing out smaller traders and concentrating risk in fewer, larger positions.


If lot sizes stay too small while prices climb, contracts become cheap enough to encourage excess speculative churn. That's the balance NSE is managing.


Under SEBI's current rule, every index derivative contract needs a minimum value of around ₹15 lakh. Every six months or so, NSE looks at each index's recent average price and resets the lot size to fit that band.


This is also why Nifty, Bank Nifty, FINNIFTY and Midcap Nifty don't share one lot size. Each trades at a different price level, so each needs its own lot to land in a similar value range.


## How Lot Size Affects Your Trading


The lot size multiplies everything, not just your entry cost.


-


A bigger lot size means a bigger position for the same 1-lot trade, which raises both your margin requirement and your potential profit or loss.


-


If you trade with a fixed capital budget, a lot size increase can quietly change how much capital a single lot demands. Bank Nifty's lot size, for example, has moved between 15 and 35 units over the past two years.


-


Comparing risk across indices only makes sense once you look at contract value, not just the lot size number, since a 120-unit Midcap Nifty lot and a 30-unit Bank Nifty lot carry very different exposure depending on each index's price level.


Here's a simple example. You sell 1 lot of Bank Nifty options at a premium of ₹150. Since 1 lot equals 30 units, you receive ₹150 × 30, which is ₹4,500, not ₹150.


If the trade moves against you by ₹50 in premium, your loss is ₹50 × 30, or ₹1,500. This is the part new traders miss most often: every point of[premium](https://algotest.in/blog/black-scholes-option-pricing-model) movement gets multiplied by the full lot, not counted per unit.


## How to Calculate Nifty Contract Value


The formula is straightforward:


### Contract Value = Index Price × Lot Size


Say Nifty 50 is trading at 24,500. One lot's contract value is 24,500 × 65, which works out to ₹15,92,500. That's the notional value you're controlling, not what you pay upfront.


As an options buyer, you pay only the premium on those 65 units, a small fraction of the total. As a futures trader, or as an options seller, you hold margin against a much larger share of that notional value instead, typically 10 to 15%, though the exact figure depends on volatility and your broker.


On a contract worth close to ₹16 lakh, that's roughly ₹1.6 lakh to ₹2.4 lakh in margin. It's worth checking the[AlgoTest Margin Calculator](https://algotest.in/margin-calculator) before placing a trade instead of estimating.


## Nifty Futures vs Nifty Options Lot Size


Nifty futures and Nifty options share the same lot size. NSE's rule is simple: the lot size for[futures and options](https://algotest.in/blog/futures-and-options-trading) on the same underlying has to match. If Nifty 50's lot size is 65, that applies whether you're buying a call option or taking a futures position.


What differs is how much of that contract value you pay upfront. As an options buyer, you pay only the premium, a small fraction of the total. As a futures trader, or as an options seller, you hold margin against the full notional value instead, a much larger number.


That's why futures positions and short options need far more capital than buying a single option, even though the lot size behind them is identical.


## Nifty Lot Size Changes Over the Years


Lot sizes aren't fixed forever. Here's how they've moved for the major indices over the last two years:


Date


Nifty 50


Bank Nifty


FINNIFTY


Midcap Nifty


What Changed


Before April 2024


50


15


40


75


Baseline


April 2024


25


15 (no change)


25


50


Periodic review as index levels had risen


November 2024


75


30


65


120


SEBI's new rule raising minimum contract value to around ₹15 lakh


April 2025


75 (no change)


35


65 (no change)


140


Periodic review as Bank Nifty and Midcap Nifty prices had moved


January 2026 (current)


65


30


60


120


Periodic review as index levels shifted again


The pattern is clear: lot sizes aren't a one-way street. They go up when an index price falls or a regulatory floor is introduced.


They come down when the index price climbs and NSE wants to keep contract values from getting too large. Expect this cycle to continue roughly twice a year.


Related:[Nifty Midcap 150: Complete Stocks List, Weightage, and Trading Guide (2026)](https://algotest.in/blog/nifty-midcap-150)


## Common Mistakes Traders Make


-


Traders often confuse 1 lot with 1 unit of the index, which leads them to underestimate how much capital or risk a single trade actually involves.


-


Many focus only on the option premium and forget to account for the full contract value when judging whether a trade is worth the risk.


-


Some calculate potential profit or loss per unit instead of multiplying by the lot size, which throws off every number in their plan.


-


It's easy to forget that lot sizes change every few months, so a number you memorized a year ago may already be wrong.


-


Assuming every index shares the same lot size is a common error, since Nifty, Bank Nifty,[FINNIFTY](https://algotest.in/blog/guide-to-finnifty-financial-services-index-trading) and Midcap Nifty are each set independently.


## Why Lot Size Matters When Backtesting Strategies


A backtest is only as accurate as the contract specifications behind it. If your backtesting tool is still running an old lot size, every margin estimate, position size, and profit or loss figure it shows you will be off, sometimes by a wide margin.


A strategy that looks profitable on paper with stale numbers can turn out to need far more capital than you actually have. That only becomes clear once you check it against the current lot size.


This is where a platform like[AlgoTest](https://algotest.in/options-trading) helps. Its[backtesting engine](https://algotest.in/blog/how-to-backtest-options-trading-strategies-with-examples/) and[Option Simulator](https://algotest.in/feature/simulator) run on updated contract specifications.


When you test a strategy on Nifty, Bank Nifty, FINNIFTY or Midcap Nifty, the margin and position size numbers reflect what you'd actually need today, not what you needed two lot-size revisions ago.


## Trade With the Right Numbers, Every Time


Understanding the latest Nifty lot size is a small detail that can have a big impact on your trading. It influences your capital requirement, position sizing, margin, and overall risk.


Since NSE revises lot sizes from time to time, it's worth checking the latest contract specifications before placing your next trade.


By democratizing algorithmic trading,[AlgoTest](https://algotest.in/?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=main-page&utm_term=algotest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=algotest&utm_content=main-page) is transforming the Indian financial landscape. As the market evolves, AlgoTest stands poised to equip Indian traders with the tools they need to thrive in the competitive world of algorithmic trading.


*Read More:*[8 Best Algo Trading Platforms in India in 2026](https://algotest.in/blog/10-best-algo-trading-software-in-india-2025)


[Best Brokers for Algo Trading in India in 2026: API, Speed & Compliance](https://algotest.in/blog/best-brokers-for-algo-trading-in-india/)


### Additional Resources


📚[Product Documentation](https://docs.algotest.in/?utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo)


🛠️ Trading Tools


-


[Margin Calculator](https://algotest.in/margin-calculator)


-


[IVR & IVP](https://algotest.in/feature/ivr-ivp)


-


[VRP Analysis](https://algotest.in/feature/vrp-analysis)


-


[OpenBroker](https://openbroker.in/)
