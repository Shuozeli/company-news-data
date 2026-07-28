---
schema_version: "1.0.0"
document_id: "75125639601439446d5b8e7d914bd20474b542ad8ef5d4808e68d4e9de7ee9e2"
company_key: "yc-nullstone"
company: "Nullstone"
source_id: "yc-nullstone-news-import-8892e125c773"
canonical_url: "https://nullstone.io/blog-posts/gitops-launch-week-day-4"
published_at: "2024-11-14T00:00:00+00:00"
first_seen_at: "2026-07-25T17:17:35.365256+00:00"
fetched_at: "2026-07-28T22:01:05.353137+00:00"
content_hash: "sha256:c38d3b91791021b4b62e2a8f4c69567f3db994e6a708a7a8283ab2550fa6de57"
---

# GitOps Launch Week, Day 4

## Overview


At Nullstone, we believe developers should be able to submit a single pull request that contains everything needed to deliver a feature or bug fix. No manual configuration in another system. No manual steps at deploy time. Instead, fully automated and identical across environments.


All week, we’re launching Nullstone GitOps to achieving this goal. Nullstone GitOps is not just an infrastructure management tool and is not a replacement for ArgoCD/FluxCD. Stay tuned all week to learn more.


## IaC Auto-completion/Validation


Yesterday, we launched CLI commands to generate and test your IaC files. This helps developers tremendously, but sometimes changing a variable or connection leads to confusion for the developer. Instead of bouncing back and forth between the terminal, it would be better to see immediate feedback in the editor. Today, we released auto-complete and validation for Nullstone IaC files that is built-in to your favorite editor. If you’re using a supported editor, invalid syntax or invalid input will add visuals to indicate errors or warnings accordingly. Also, as you’re typing, your editor will reveal a set of valid choices.


The following editors are supported:
- Android Studio
- CLion
- Emacs via \[eglot\](https://github.com/joaotavora/eglot)
- IntelliJ IDEA
- JSONBuddy
- Neovim via \[SchemaStore.nvim\](https://github.com/b0o/SchemaStore.nvim)
- PhpStorm
- PyCharm
- ReSharper
- Rider
- RubyMine
- SublimeText via \[LSP-json\](https://packagecontrol.io/packages/LSP-json),\[LSP-yaml\](https://packagecontrol.io/packages/LSP-yaml)
- Visual Studio
- Visual Studio Code (\[YAML\](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml),\[TOML\](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml),\[JSON\](https://marketplace.visualstudio.com/items?itemName=remcohaszing.schemastore))
- Visual Studio for Mac
- WebStorm


## GitOps/IaC Docs


If you’re a fan of classic reference material or need to read more about GitOps or IaC format/attributes, we have launched a resource for you. We published a new section to the Nullstone docs site, “GitOps”. In this section, we detail the ins and out of GitOps workflows, examples, how it works, and best practices. Also in this new section, we detail examples, attributes, and reference for IaC files.


Check it out at \[GitOps\](https://docs.nullstone.io/gitops/overview.html).


‍
