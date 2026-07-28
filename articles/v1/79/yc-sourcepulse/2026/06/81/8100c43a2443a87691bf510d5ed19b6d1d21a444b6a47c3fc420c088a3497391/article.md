---
schema_version: "1.0.0"
document_id: "8100c43a2443a87691bf510d5ed19b6d1d21a444b6a47c3fc420c088a3497391"
company_key: "yc-sourcepulse"
company: "Sourcepulse"
source_id: "yc-sourcepulse-news-import-906fe2d84e52"
canonical_url: "https://medium.com/@quackai/q402-free-trial-with-agent-wallet-getting-started-guide-6de072013e01"
published_at: "2026-06-01T13:46:34.915+00:00"
first_seen_at: "2026-07-24T01:48:42.654756+00:00"
fetched_at: "2026-07-28T20:47:49.978466+00:00"
content_hash: "sha256:62bb09ad3c6c7360c2a504a2a25c94a87425881d3dfa48b3daf17346092f1a33"
---

# Q402 Free Trial with Agent Wallet — Getting Started Guide

# **Q402 Free Trial with Agent Wallet — Getting Started Guide**


[Quack AI](https://medium.com/@quackai?source=post_page---byline--6de072013e01---------------------------------------)


2 min read


·


Jun 1, 2026


--


**Q402 Free Trial is underway** — and now it’s time to build.


In this 5-minute tutorial, we’ll walk you through how to set up your Free Trial API key, Agent Wallet, and Q402 MCP, then complete your first gasless stablecoin payment through an AI client.


## 1. Get Your Free Trial API Key


Visit the Q402 Free Trial page and sign in with Google, email, or wallet:
👉[https://q402.quackai.ai/event](https://q402.quackai.ai/event)


Open the Developer page and grab your two keys:


- ***Trial API Key — q402_live_…***
Used for real on-chain transfers. Includes 2,000 gasless transactions, valid for 30 days.
- ***Sandbox Key — q402_test_…***
Used for sandbox testing only. Returns mock results and does not burn credits.


*Tip: start in sandbox while you wire things up, then switch to your live key when you’re ready to send real funds.*


## 2. Set Up Your Agent Wallet


Inside the Q402 dashboard, create a new Agent Wallet — this is the wallet your AI will sign and pay from.


Then fund it: send USDC or USDT on BNB Chain to your Agent Wallet address. No native BNB is required for gas — Q402’s facilitator sponsors gas on your behalf.


## 3. Install the Q402 MCP


Install the Q402 MCP server in your AI client (Claude, Codex, or any MCP-compatible host):


***npx -y @quackai/q402-mcp***


That’s it — the MCP exposes Q402’s payment tools directly to your AI.


## 4. Hand Your Trial API Key to the AI


In your AI chat, paste:


***Q402_TRIAL_API_KEY=q402_live_xxxx***


***Please set up the payment via my agent wallet.***


Your AI is now wired into Q402 and can act through your Agent Wallet.


## 5. Check Status Before You Send


Always verify the wallet before moving funds. Ask:


***Show me my agent wallet address and balance.***


Confirm the address matches the one you funded, and that the balance is what you expect.


## 6. Send a Gasless Transfer


## Single Transfer


Ask: ***Send 1 USDC on BNB Chain to 0x32…***


Your AI will summarize the transfer and ask for final confirmation. Approve it, and Q402 submits the transaction gaslessly — no BNB required, no pre-approval transaction needed.


## Batch Payments


Ask: ***Send 1 USDC on BNB Chain to 0xA, 0xB, 0xC***


One signature, multiple recipients, one transaction.


*Free Trial supports BNB Chain only. Batch size limits may apply depending on your key type.*


The first 2,000 transactions are on us. Go ship something.


Start here 👉[https://q402.quackai.ai/event](https://q402.quackai.ai/event)
