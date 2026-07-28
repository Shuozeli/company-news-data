---
schema_version: "1.0.0"
document_id: "0801721a8bc9aa19c88d882260164984fbc8f863c6ed0f8844d07b495f64e27d"
company_key: "yc-nullstone"
company: "Nullstone"
source_id: "yc-nullstone-news-import-8892e125c773"
canonical_url: "https://nullstone.io/blog-posts/gitops-launch-week-day-3"
published_at: "2024-11-13T00:00:00+00:00"
first_seen_at: "2026-07-25T17:17:35.365256+00:00"
fetched_at: "2026-07-28T22:01:05.353137+00:00"
content_hash: "sha256:3f677cc9fa70455c9e3de7faa7d6499e0df4b353df4b0153e81613ca92abaef6"
---

# GitOps Launch Week, Day 3

## Overview


At Nullstone, we believe developers should be able to submit a single pull request that contains everything needed to deliver a feature or bug fix. No manual configuration in another system. No manual steps at deploy time. Instead, fully automated and identical across environments.


All week, we’re launching Nullstone GitOps to achieving this goal. Nullstone GitOps is not just an infrastructure management tool and is not a replacement for ArgoCD/FluxCD. Stay tuned all week to learn more.


## Test IaC locally


We noticed that our early adopters of GitOps struggled with the initial learning curve of IaC files. We saw the same symptoms of teams setting up their CI/CD pipelines; the git commit log is littered with “fix iac” or “try again” (and eventually an expletive).


That’s why we introduced a new CLI command \`nullstone iac test\`. This command performs validation and reports what will change on your local computer *before* you pushing your changes to Nullstone.


\[How to install the Nullstone CLI\](https://docs.nullstone.io/getting-started/cli/install-configure.html)


Read more about the command at \[\`nullstone iac test\`\](https://docs.nullstone.io/getting-started/cli/docs.html#iac-test).


## Export to IaC


We noticed another interesting trend among developers. The Nullstone portal serves as an excellent tool for discovery; however, developers want to stay in their code/repo to ship products. This came in a few areas: understanding Nullstone concepts, learning new cloud concepts, and learning the Nullstone IaC format.


As a result, we added a feature to alleviate migration (and translation) from the Nullstone UI to IaC files. Navigate to an app in any environment and switch to the “Overview” tab. There are buttons, “Full Configuration” and “Overrides”, that will emit yaml files that can be copied into your repository. This gives developers the ability to design infrastructure through a guided portal experience. Once in the desired state, the IaC can be exported to continue operating in a Git workflow.


We have also added this functionality to a CLI command \`nullstone iac generate\`. This command emits an IaC file containing the same configuration as the selected Nullstone workspace.


Read more about the command at \[\`nullstone iac generate\`\](https://docs.nullstone.io/getting-started/cli/docs.html#iac-generate).


‍
