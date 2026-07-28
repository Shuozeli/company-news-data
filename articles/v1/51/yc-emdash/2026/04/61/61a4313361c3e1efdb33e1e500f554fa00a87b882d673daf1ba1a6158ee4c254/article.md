---
schema_version: "1.0.0"
document_id: "61a4313361c3e1efdb33e1e500f554fa00a87b882d673daf1ba1a6158ee4c254"
company_key: "yc-emdash"
company: "Emdash"
source_id: "yc-emdash-news-import-f97630886411"
canonical_url: "https://emdash.ai/blog/emdash-v1-stable"
published_at: "2026-04-24T00:00:00+00:00"
first_seen_at: "2026-07-21T17:59:11.363639+00:00"
fetched_at: "2026-07-28T21:25:35.830406+00:00"
content_hash: "sha256:1ebc2844fc895329183a2120e5aa7628ad8ebe2f5ec5da1f55254b6b29fd54b1"
---

# Emdash v1

Emdash v1 is now stable and the default download for macOS, Windows, and Linux.[Download it here](https://emdash.ai/download) .


Emdash is an open-source desktop app for running coding agents in parallel. Start a few tasks, give each agent its own Git worktree or remote environment, and keep control over what lands in your repo.


The focus of v1 was to make Emdash fast, calm, and reliable.


We opened the public beta last week. Since then, many of you tried it and sent feedback. Thank you!


## What changed since v0.4


The biggest difference is in the overall performance of the app.


Tasks load faster and task switching no longer flickers. Terminals stay where you expect them to. Archive, delete, and restore flows feel immediate thanks to our fully rebuilt 'worktree engine'.


Emdash now has a very reliable 'pull request engine'. When an agent commits, pushes, opens a PR, or changes files locally, Emdash catches this immediately. We put additional effort into the changes panel and diff viewer too; it has never been easier to understand what changed before you merge it.


## Small things


v1 also includes a long (!) list of smaller improvements. For the full list, see the[changelog](https://emdash.ai/changelog) :


- Terminal search with Cmd/Ctrl+F
- Better hotkeys, including clearable shortcuts
- Clearer task names, especially for tasks created from issues
- More “Open in” targets, including Xcode, Windsurf, and Antigravity
- Better settings feedback and fewer layout jumps
- More consistent theming across Monaco and the diff viewer
- Fixes for restore, archive, lifecycle scripts, MCP state, and selected-agent state


## Remote development


We are spending a lot of time with teams that run coding agents on remote servers.


Emdash was the first agentic development environment that supported remote projects over SSH. v1 gives us a cleaner base for remote development and for the next phase of Emdash Cloud.


If your team wants to run coding agents on your own infrastructure instead of developer laptops,[reach out](https://emdash.ai/cloud) .


## Upgrade


v1 uses a new data model. During onboarding, you can import tasks from v0.4.x.


You can download Emdash v1[here](https://emdash.ai/download) .


Or read the[v1 changelog](https://emdash.ai/changelog) for the full list of changes.
