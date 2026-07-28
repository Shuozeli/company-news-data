---
schema_version: "1.0.0"
document_id: "5b0f042f3212ccf01b983b52e9098a0b0e3ed940814ea18b3666930be959ddf8"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-workflows-3-7"
published_at: "2025-07-28T15:35:20+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T21:59:46.813241+00:00"
content_hash: "sha256:b0e45401b18b891693850ffe7a3e987f4d4054ea78420cf3148354af44102f41"
---

# Argo Workflows 3.7

We’re excited to announce the release of **Argo Workflows v3.7.0** ! This release brings a host of new features and fixes to help you automate your workflows with even more power, flexibility, and security.


Whether you’re running machine learning pipelines, managing CI/CD at scale, or automating complex workflows across namespaces, this release delivers the performance, flexibility, and control you need.


# Release Statistics


- 🚀 **24 new features**
- 🐞 **83 fixes**
- 👥 70 **contributors total (including 39 new contributors)**


# What’s New in v3.7.0?


## Highlights


- Smarter caching & memoization — Save compute time and make reuse more transparent.
- Multi-controller locking (semaphores + mutexes) — Scale with confidence across clusters.
- Dynamic namespace parallelism — Tune resource usage per namespace.
- Non-root execution for argoexec — Tighten your security posture.
- React Testing Library & UI polish — Better test coverage and a cleaner UI.
- Preview workflows before submission — Catch issues earlier.
- Filter workflows by timestamps via API — More efficient filtering for large numbers of workflows for API users.
- Scroll to read more… 👇


# Retry Improvements


- **Support retry strategy on daemon containers** ([#13738](https://github.com/argoproj/argo-workflows/pull/13738) ) **thanks to**[@MenD32](https://github.com/MenD32) Retry strategies can now be applied to daemon containers, allowing for better fault tolerance.
- **Support cap on retryStrategy backoff** ([#13782](https://github.com/argoproj/argo-workflows/pull/13782) ) **thanks to**[@chengjoey](https://github.com/chengjoey) You can now cap the maximum backoff duration in retry strategies to avoid excessively long waits.
- **Allow last retry variables in expressions** ([#14450](https://github.com/argoproj/argo-workflows/pull/14450) ) **thanks to**[Isitha Subasinghe](https://github.com/isubasinghe) Expressions can now reference variables from the last retry, enhancing workflow logic flexibility.


# Parallelism Improvements


- **Multi-controller locks (semaphores and mutexes)** ([#14309](https://github.com/argoproj/argo-workflows/pull/14309) ) **thanks to**[Alan Clucas](https://github.com/Joibel) Support for distributed locks across multiple controllers to improve synchronization and concurrency handling.
- **Dynamic namespace parallelism** ([#14188](https://github.com/argoproj/argo-workflows/pull/14188) ) **thanks to**[Isitha Subasinghe](https://github.com/isubasinghe) Set parallelism limits dynamically per namespace to better control resource usage.


# Enhanced Caching


- **More granular caching options for the argo kubernetes informer** ([#14304](https://github.com/argoproj/argo-workflows/pull/14304) ) **thanks to**[Jakub Buczak](https://github.com/jakkubu)
Gain finer control over informer cache behavior, enabling better performance tuning for your Kubernetes client interactions.
- **Cache semaphore limit lookup** ([#14205](https://github.com/argoproj/argo-workflows/pull/14205) ) **thanks to**[Dmitri Rabinowitz](https://github.com/drabinowitz) Semaphore limit lookups can now be cached to reduce overhead during workflow execution.


# UI Enhancements


Workflows can now be visualized before submission


- **Visualize workflows before submitting** ([#14034](https://github.com/argoproj/argo-workflows/pull/14034) ) **thanks to**[@Unperceivable](https://github.com/Unperceivable) Added the ability to preview workflow visualizations before submission.


Filtering being performed based on \`Finished before\`


- **Filter workflows by “Finished before” and “Created since” via API** ([#13962](https://github.com/argoproj/argo-workflows/pull/13962) ) **thanks to**[Adrien Delannoy](https://github.com/Adrien-D)
API users can now filter workflows based on creation and finish timestamps, improving search and management capabilities.


Markdown based description being rendered


- **Allow markdown titles and descriptions** ([#13935](https://github.com/argoproj/argo-workflows/pull/13935) ,[#12697](https://github.com/argoproj/argo-workflows/pull/12697) ) **thanks to**[@panicboat](https://github.com/panicboat) Markdown formatting is now supported in titles and descriptions across various editors including KeyValueEditor, CronWorkflows, WorkflowTemplates, and ClusterWorkflowTemplates.


Memoized nodes are now clearly visible from the UI


- **Mark memoized nodes as cached** ([#13883](https://github.com/argoproj/argo-workflows/pull/13883) ) **thanks to**[@MenD32](https://github.com/MenD32) Workflow nodes that use memoization are now clearly marked as cached, improving observability and debugging.


Parameters can now be pre-filled using query parameters


- **Prefill parameters for workflow submit form** ([#13922](https://github.com/argoproj/argo-workflows/pull/13922) ) **thanks to**[Sairam Arunachalam](https://github.com/sairam91) The UI now pre-fills workflow submit forms with parameters for faster and less error-prone submission.


Display name customization allows for human readable names


- **Set template display name in YAML** ([#14077](https://github.com/argoproj/argo-workflows/pull/14077) ) **thanks to**[@MenD32](https://github.com/MenD32) You can now specify a human-readable display name for templates directly in workflow YAML.


# User Experience


- **Label actor action when making changes to workflows/templates** ([#14104](https://github.com/argoproj/argo-workflows/pull/14104) ) **thanks to**[Tianchu Zhao](https://github.com/tczhao) Workflow/template changes are now labeled with actor actions for improved auditability.
- **Support archive logs in resource templates** ([#13933](https://github.com/argoproj/argo-workflows/pull/13933) ) **thanks to**[Shuangkun Tian](https://github.com/shuangkun)
Resource templates now support archiving logs for better log retention and auditing.
- **Include container name in error messages** ([#13790](https://github.com/argoproj/argo-workflows/pull/13790) ) **thanks to**[@tooptoop4](https://github.com/tooptoop4) Error messages now include the container name for easier troubleshooting.


# Cron Workflow Enhancement


- **Support backfill for cron workflows** ([#13999](https://github.com/argoproj/argo-workflows/pull/13999) ) **thanks to**[Shuangkun Tian](https://github.com/shuangkun) The CLI now supports backfilling Cron Workflows, enabling retroactive workflow execution for missed schedules.


# Security Improvements


- **Non-root` argoexec`** ([#14477](https://github.com/argoproj/argo-workflows/pull/14477) ) **thanks to**[Alan Clucas](https://github.com/Joibel)
` argoexec` now has an image allowing it to run as a non-root user, enhancing security for environments with stricter policies.


# Developer Experience


- **Add React Testing Library and initial component coverage** ([#14412](https://github.com/argoproj/argo-workflows/pull/14412) ) **thanks to**[Eric S](https://github.com/ericsengineer)
We improved frontend test coverage using React Testing Library to increase reliability and maintainability.
- **Move contextless log messages to debug level** ([#13920](https://github.com/argoproj/argo-workflows/pull/13920) ) **thanks to**[Kat](https://github.com/kizzie) Improved logging hygiene by moving contextless log messages to debug level, reducing noise.
- **Enable cherry-pick bot** ([#14151](https://github.com/argoproj/argo-workflows/pull/14151) ) **thanks to**[Alan Clucas](https://github.com/Joibel) Automated cherry-pick bot now enabled to help streamline backporting fixes and features across branches.
- **Add support for databases enforcing strict data integrity through primary keys** ([#14103](https://github.com/argoproj/argo-workflows/pull/14103) ) **thanks to**[Radu Sora](https://github.com/radusora) Argo now supports database backends with strict PK enforcement for more robust metadata management.


# Get Started


Upgrade to the latest version by following our[installation guide](https://argoproj.github.io/argo-workflows/installation/) .


Try out the new features and improvements, and as always, please provide feedback or report issues on our[GitHub repo](https://github.com/argoproj/argo-workflows) .


Happy workflowing! 🚀


*The Argo Workflows Team*
