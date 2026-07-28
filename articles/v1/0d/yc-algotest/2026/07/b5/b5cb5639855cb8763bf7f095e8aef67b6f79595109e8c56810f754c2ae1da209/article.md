---
schema_version: "1.0.0"
document_id: "b5cb5639855cb8763bf7f095e8aef67b6f79595109e8c56810f754c2ae1da209"
company_key: "yc-algotest"
company: "AlgoTest"
source_id: "yc-algotest-news-import-7cc502b412f0"
canonical_url: "https://algotest.in/blog/how-to-backtest-algo-trading-strategies/"
published_at: "2026-07-13T10:37:45+00:00"
first_seen_at: "2026-07-25T00:56:57.418756+00:00"
fetched_at: "2026-07-28T21:38:32.326002+00:00"
content_hash: "sha256:2d210dc4d1776620a8dc1bc79e8ba7adffff97d83b5cae28ee843b7661d46dee"
---

# How to Backtest Algo Trading Strategies: Intraday, BTST, Positional & More (Step-by-Step)

# How to Backtest Algo Trading Strategies: Intraday, BTST, Positional & More (Step-by-Step)


[AlgoTest](https://algotest.in/blog/author/algotest/)


Jul 13, 2026


•


8 min read


•


[General](https://algotest.in/blog/category/general/)


- [Twitter / X](https://twitter.com/intent/tweet?url=https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F&text=How%20to%20Backtest%20Algo%20Trading%20Strategies%3A%20Intraday%2C%20BTST%2C%20Positional%20%26%20More%20%28Step%2Dby%2DStep%29)
- [Facebook](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F)
- [LinkedIn](https://www.linkedin.com/shareArticle?mini=true&url=https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F&title=How%20to%20Backtest%20Algo%20Trading%20Strategies%3A%20Intraday%2C%20BTST%2C%20Positional%20%26%20More%20%28Step%2Dby%2DStep%29)
- [WhatsApp](https://api.whatsapp.com/send?text=How%20to%20Backtest%20Algo%20Trading%20Strategies%3A%20Intraday%2C%20BTST%2C%20Positional%20%26%20More%20%28Step%2Dby%2DStep%29%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F)
- [Ask ChatGPT](https://chatgpt.com/?hints=search&q=Summarize%20this%20article:%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F)
- [Ask Claude](https://claude.ai/new?q=Summarize%20this%20article:%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F)
- [Ask Grok](https://grok.com/?q=Summarize%20this%20article:%20https%3A%2F%2Falgotest%2Ein%2Fblog%2Fhow%2Dto%2Dbacktest%2Dalgo%2Dtrading%2Dstrategies%2F)
- Copy link


Every profitable-looking strategy has a backstory. Most of the time, that backstory is a backtest.


Before you risk a single rupee of margin,[backtesting](https://algotest.in/feature/backtest?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=feature&utm_term=backtest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=backtest&utm_content=feature&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=backtest&utm_content=feature) lets you replay a strategy against years of real market data and see, honestly, whether it holds up. It's the step between "I have an idea" and "I have evidence."


This guide covers two things:


-


What actually makes a backtest reliable — principles that apply no matter which platform you use


-


How to run each type of backtest on[AlgoTest](https://algotest.in/?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=main-page&utm_term=algotest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=algotest&utm_content=main-page) , step by step


## What a Backtest Actually Tells You


A good backtest isn't just a profit number. It's a report card across several dimensions:


-


**Win rate** — how often the strategy makes money, not just whether it's profitable overall


-


**Maximum drawdown** — the worst peak-to-trough loss you'd have had to sit through


-


**Consistency** — whether returns hold up across different months, or depend on one lucky quarter


-


**Cost sensitivity** — whether the edge survives once brokerage, slippage, and taxes are subtracted


-


**Regime dependence** — whether the strategy only works in trending markets, or sideways ones, or both


-


**Risk-adjusted return (Sharpe ratio)** — whether the returns justify the risk taken, not just the raw profit number


If you only look at the total P&L, you're missing most of what a backtest is actually for.


Popular read:[5 Mistakes Traders Make in Algo Trading](https://algotest.in/blog/5-mistakes-traders-make-in-algo-trading/)


## 5 Things That Make a Backtest Trustworthy


Backtesting is easy to do badly. These five checks apply whether you're using[AlgoTest,](https://algotest.in/?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=main-page&utm_term=algotest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=algotest&utm_content=main-page) a spreadsheet, or a Python script.


### 1. Realistic Costs


Brokerage, STT, exchange charges, and slippage all eat into returns. A backtest that ignores them will always look better than real trading does.


### 2. Enough History, Across Regimes


A strategy tested only on the last three bullish months tells you almost nothing about how it behaves in a volatile or sideways market. Aim for multiple years and multiple market conditions.


### 3. Mechanical Rules, Not Vibes


"Sell when it feels toppy" can't be backtested. Every entry, exit, and adjustment needs a rule specific enough that a computer — or a stranger — could execute it without asking you a follow-up question.


### 4. Out-of-Sample Validation


If you tweak a strategy until it looks perfect on your test data, you've probably just fit the past, not found an edge. Hold back a chunk of data you don't touch until the strategy is finalised, then check it there.


### 5. Enough Trades to Mean Something


Ten trades over one expiry can look great by luck alone. Look for a large enough sample — ideally 100+ trades across a couple of years — before trusting the numbers.


*Check out the*[10 Best Algo trading Softwares in India (Free & Paid)](https://algotest.in/blog/10-best-algo-trading-software-in-india-2025/)


## The Main Types of Algo Strategies You Can Backtest


Most retail algo strategies in India fall into a few structural buckets:


-


**Intraday** — entered and exited within the same trading day, with no overnight exposure


-


**BTST (Buy Today, Sell Tomorrow)** — positions held overnight and squared off the next session


-


**Positional** — held across multiple days, often tied to how many trading days remain before expiry


-


**Indicator/signal-based** — entries and exits driven by technical conditions (EMA crossovers, RSI, SuperTrend) rather than a fixed clock time


-


**Crypto** — the same structures, applied to BTCUSD or ETHUSD instead of NSE indices


Each of these needs slightly different settings once you actually sit down to backtest it — which is where a purpose-built platform saves a lot of manual setup.


## How to Backtest Algo Trading Strategies on AlgoTest


[AlgoTest](https://algotest.in/?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=main-page&utm_term=algotest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=algotest&utm_content=main-page) is built specifically for Indian options and futures traders, with a no-code strategy builder and 7.5+ years of historical NSE data behind every backtest.[You get 25 free backtests every week to start](https://algotest.in/register?utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo) .


The core workflow stays the same regardless of strategy type:


1.


Create a strategy from the AlgoTest dashboard


2.


Set your Strategy Type — Intraday, BTST, or Positional


3.


Choose your index or stock, and whether strikes are based on Cash or Futures price


4.


Build your legs (option type, position, strike selection, expiry) using the leg builder


5.


Add stop-loss, target, and re-entry rules


6.


Save the strategy, pick your date range, and click[Backtest](https://algotest.in/feature/backtest?utm_source=blog&utm_medium=organic&utm_campaign=seo)


Here's how the settings shift depending on what you're testing.


### Backtesting an Intraday Strategy


Intraday strategies enter and exit within the same session, so the settings you'll configure are:


-


**Entry Time and Exit Time** — when the strategy activates and when it force-closes for the day


-


**Restrict Re-entry Time** — an optional cutoff after which the strategy won't take a fresh entry


-


**Partial or complete square-off** — whether a stop-loss or target closes the whole position or just part of it


Once your legs and stop-loss rules are in place, save the strategy, pick a backtest window, and run it.


### Backtesting a BTST Strategy


BTST strategies carry a position overnight, which introduces gap risk that intraday strategies don't have. AlgoTest's BTST backtest includes one setting worth knowing about:


-


**Delayed Restart** — by default, overnight positions are marked to the 9:15 AM price. Turning this on exits at 9:16 AM (or a time you choose) instead, which is a fairer real-world number, since gap-ups and gap-downs at the open can move prices sharply before you'd realistically be able to react.


Beyond that, the same square-off and leg-builder settings from intraday carry over.


### Backtesting a Positional Strategy


Positional strategies hold across several days and are usually built around how far out the expiry is, rather than a fixed calendar date. The settings that matter most here:


-


**Trading days before expiry (DTE)** — instead of picking a fixed date, you set entry/exit relative to expiry (for example, "5 trading days before expiry"), so the same logic applies automatically to every future expiry cycle


-


**Weekly vs. monthly expiry** — positional strategies can behave differently depending on which expiry cycle you're targeting, so it's worth testing both if your strategy could apply to either


-


**SEBI expiry-change toggle** — a toggle lets you include or exclude backtest data from before the latest SEBI expiry-day changes, since market behaviour shifted meaningfully around that change


### Backtesting the 920 Straddle


The 920 Straddle is one of the most widely used intraday strategies in India — selling an ATM call and an ATM put around 9:20 AM to capture premium decay once the opening volatility settles. It's worth knowing how to set up, since the same leg-builder logic applies to most other straddle and strangle variants:


-


Set Strategy Type to Intraday, Entry Time to 9:20, and Exit Time to your chosen square-off (commonly 3:10 PM)


-


Add a Sell ATM Call leg — Options segment, 1 lot, Sell, Call, Weekly expiry, ATM strike


-


Add a Sell ATM Put leg with the same settings, swapping Call for Put


-


Set a stop-loss (a common starting point is 25% per leg, or a combined-premium stop)


-


Save and backtest across a few years to see how it holds up across different volatility regimes


### Backtesting Crypto Strategies (Delta Exchange)


If you trade BTCUSD or ETHUSD,[AlgoTest](https://algotest.in/?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=main-page&utm_term=algotest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=algotest&utm_content=main-page) lets you backtest crypto strategies through the same interface used for indices and stocks, powered by Delta Exchange data:


-


Select BTCUSD or ETHUSD from the Index dropdown


-


Choose Cash or Futures as your underlying


-


Pick Intraday, BTST, or Positional as the strategy type, same as you would for NSE indices


-


Build Options or Futures legs the same way — lot size, position, strike selection, expiry


For more details, read the '[How to Master Backtesting on AlgoTest' doc](https://docs.algotest.in/Time-Based-Algo-Trading/How-to-Master-Backtesting-on-AlgoTest/)


## Comparing and Combining Backtests


Once you've run a few backtests, two features help you move from "I have a strategy" to "I have a system":


-


**Backtest Comparison** lets you line up to 15 recent backtests side by side — useful when you're tweaking one variable at a time, like stop-loss percentage or entry timing, and want to see exactly what moved the needle.[Read the full guide to Backtest Comparison on AlgoTest](https://algotest.in/blog/backtest-comparison-algo-trading/) .


-


**Portfolio Backtesting** lets you combine multiple strategies and backtest them together, with a correlation matrix showing how they move relative to each other — important if you're relying on diversification to smooth out your equity curve.[See how to backtest multiple strategies together using the Portfolio feature](https://algotest.in/blog/backtest-multiple-strategies-together-using-the-portfolio-feature/) .


## Common Backtesting Mistakes to Avoid


-


**Testing only recent, bullish data** — a strategy that only survives calm uptrends isn't tested; it's untested with extra steps


-


**Ignoring slippage and brokerage** — this is usually the single biggest gap between backtested and live returns


-


**Over-optimising strike distance or stop-loss %** until the backtest looks perfect — this often means you've fit noise, not found an edge


-


**Skipping forward testing** — a backtest validates the logic; forward testing (paper trading) validates the execution, including delays and fills a backtest can't fully model


-


**Confusing correlation with diversification** — two strategies that look uncorrelated over one year can move together the moment markets get volatile


For worked examples across straddles, strangles, and iron condors, AlgoTest's[detailed guide on backtesting options strategies](https://algotest.in/blog/how-to-backtest-options-trading-strategies-with-examples/) walks through entry rules, strike selection, and what to look for in the results.


Still comparing platforms before committing to one? These two roundups are worth a look:[the best free backtesting and trading tools in India](https://algotest.in/blog/best-backtesting-trading-tools-in-india/) , and a closer[comparison of backtesting software built specifically for options trading](https://algotest.in/blog/best-backtesting-software-for-options-trading-in-india/) .


## Join Us as We Simplify Algo Trading in India


Backtesting is what separates a strategy you believe in from one you've actually proven. Skip it, and you end up paying tuition in live capital for lessons a free backtest could have taught you in seconds.


Sign up for free and get the full AlgoTest toolkit built for Indian options traders:


→[Backtesting](https://algotest.in/feature/backtest?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=feature&utm_term=backtest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=backtest&utm_content=feature&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=backtest&utm_content=feature) tests your strategy against years of historical data before you risk real money.


→[Forward testing](https://algotest.in/feature/forward-test?utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo) validates the strategy on live market data without putting any capital at risk.


→ The[strategy builder](https://algotest.in/feature/strategy-builder?utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo) lets you build and customize strategies with a no-code interface.


→ The[simulator](https://algotest.in/feature/simulator?utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo&utm_source=blog&utm_medium=organic&utm_campaign=seo) lets you practice execution in real market conditions using virtual capital.


From pricing a single option to running a full strategy,[AlgoTest](https://algotest.in/?utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_content=main-page&utm_term=algotest&utm_source=blog&utm_medium=internal&utm_campaign=seo&utm_term=algotest&utm_content=main-page) gives you the tools to trade with more confidence and less guesswork.


Run your first backtest today.
