---
schema_version: "1.0.0"
document_id: "ccec85a3f0e81ed6e8870697f408443c26992ad3c4fb5e7136abd29a78ee7a04"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/argo-workflows-3-6"
published_at: "2024-09-24T18:37:08+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:01:06.812214+00:00"
content_hash: "sha256:73dd23f52f09fbadd07f6836316d3cb53d11cce1c25de3d9e9a9eca50429d0e9"
---

# Argo Workflows 3.6

*Argo workflows 3.6 is currently available as a*[release candidate](https://github.com/argoproj/argo-workflows/releases/tag/v3.6.0-rc1) *. Please test and report any issues.*


*Some quick statistics about this release — there have been:*


- 49 new features
- 216 fixes
- 150 documentation updates
- 121 people have contributed to this release of which
- 80 are new contributors to the project


A big thank you to everyone who’s helped out in building this release of Argo Workflows.


# Cron Workflows


[Eduardo Rodrigues](https://github.com/eduardodbr) has made some improvements to Cron Workflows. You can now specify multiple cron schedules on a single Cron Workflow (in[#12616](https://github.com/argoproj/argo-workflows/pull/12616) )


You can also use a stop strategy on Cron Workflows to stop them running any more workflows after a set of conditions occur such as too many errors (in[#12305](https://github.com/argoproj/argo-workflows/pull/12305) )


Cron jobs also now have a when expression to further tune which occurrences of the workflow will run and which may be skipped, thanks to[Isitha Subasinghe](https://github.com/isubasinghe/) in[#13474](https://github.com/argoproj/argo-workflows/pull/13474)


# UI


**The full name of the workflow is now visible in the list details of a workflow. Thanks to**[@polarbear567](https://github.com/polarbear567) **in**[#13519](https://github.com/argoproj/argo-workflows/pull/13519) **.**


**The UI will now show the directory used for input artifacts thanks to**[Shuangkun Tian](https://github.com/shuangkun) **in**[#12350](https://github.com/argoproj/argo-workflows/pull/12350)


**You can also now see line numbers in the object view thanks to**[Mahdi Alizadeh](https://github.com/alizmhdi) **in**[#12873](https://github.com/argoproj/argo-workflows/pull/12873)


WorkflowTemplate and ClusterWorkflowTemplate will show you their execution history like you can see for CronWorkflows thanks to[@panicboat](https://github.com/panicboat) in[#13452](https://github.com/argoproj/argo-workflows/pull/13452)


- You will be able to see live logs from pods if retrieval of logs from archived workflows fails and the pod logs are available thanks to[Yuan Tang](https://github.com/terrytangyuan) in[#12024](https://github.com/argoproj/argo-workflows/pull/12024)
- Cron Workflows and Workflow Templates now display their title and descriptions in the list view thanks to[@panicboat](https://github.com/panicboat) in[#12674](https://github.com/argoproj/argo-workflows/pull/12674)
- You can specify HTTP headers used to detect IP addresses using the` IP_KEY_FUNC_HEADERS` environment variable. This is used in the rate limiter. Thanks to[Yuan Tang](https://github.com/terrytangyuan) in[#12199](https://github.com/argoproj/argo-workflows/pull/12199)


# Metrics


The workflow controller can now emit metrics over OpenTelemetry GRPC protocol[#13265](https://github.com/argoproj/argo-workflows/pull/13265) with selectable temporality[#13267](https://github.com/argoproj/argo-workflows/pull/13267) and more configuration of what is emitted[#13268](https://github.com/argoproj/argo-workflows/pull/13268) . Many of the metrics have been updated and there are some new ones, all by[Alan Clucas](https://github.com/Joibel) :


- Version information in the controller[#13269](https://github.com/argoproj/argo-workflows/pull/13269)
- Is this controller the leader[#13270](https://github.com/argoproj/argo-workflows/pull/13270)
- Kubernetes API calls duration[#13271](https://github.com/argoproj/argo-workflows/pull/13271)
- Pod phase monitoring[#13272](https://github.com/argoproj/argo-workflows/pull/13272) and pod pending problem metrics[#13273](https://github.com/argoproj/argo-workflows/pull/13273)
- Cron Workflow[#13274](https://github.com/argoproj/argo-workflows/pull/13274) and[#13497](https://github.com/argoproj/argo-workflows/pull/13497) and Workflow Template[#13275](https://github.com/argoproj/argo-workflows/pull/13275) counters


There are a couple of other new features:


- There is a new` retries` variable available in metrics describing the number of retries thanks to[@moonyoungCHAE](https://github.com/moonyoungCHAE) in[#11927](https://github.com/argoproj/argo-workflows/pull/11927)
- Pod missing metrics will be emitted before pods are created thanks to[@moonyoungCHAE](https://github.com/moonyoungCHAE) in[#11857](https://github.com/argoproj/argo-workflows/pull/11857)


# Controller


- The controller uses a queue when archiving workflows to improve memory management when archiving a large number of workflows at once[#13419](https://github.com/argoproj/argo-workflows/pull/13419) thanks to[@ChenRussell](https://github.com/ChenRussell)
- Plugins can now be stopped, so that a stopped workflow will shutdown its plugin nodes thanks to[@GhangZh](https://github.com/GhangZh) in[#12441](https://github.com/argoproj/argo-workflows/pull/12441)
- The OSS artifact driver can now work with directories thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12188](https://github.com/argoproj/argo-workflows/pull/12188) and it supports deletion ([#12907](https://github.com/argoproj/argo-workflows/pull/12907) ) and streaming ([#12908](https://github.com/argoproj/argo-workflows/pull/12908) ) now both thanks to[@AlbeeSo](https://github.com/AlbeeSo)
- Pod deletion will now happen in parallel to speed it up, also thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12419](https://github.com/argoproj/argo-workflows/pull/12419)
- You can use Shared Access Signatures to access artifacts stored in Azure now thanks to[Kavish Dahekar](https://github.com/kavishdahekar-sap) in[#13360](https://github.com/argoproj/argo-workflows/pull/13360)
- Workflow pods now have a kubernetes finalizer to try to prevent them being deleted prematurely in[#12413](https://github.com/argoproj/argo-workflows/pull/12413) thanks to[@sakai-ast](https://github.com/sakai-ast) and[Rohan Kumar](https://github.com/rohankmr414)
- Large environment variables will be offloaded to Config Maps thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12325](https://github.com/argoproj/argo-workflows/pull/12325)
- Large and flat workflows where there are many steps that need resolving at the same time could time out during template referencing. This is now much faster, also thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12328](https://github.com/argoproj/argo-workflows/pull/12328)
- Kubernetes scheduling constraints such as node selectors and tolerations will now be honored where they are specified in a WorkflowTemplate. These will be applied to the task and step pods, also thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12568](https://github.com/argoproj/argo-workflows/pull/12568)
- The pods created by workflows will have a` seccompProfile` of` RuntimeDefault` by default now thanks to[@lukashankeln](https://github.com/lukashankeln) in[#12984](https://github.com/argoproj/argo-workflows/pull/12984)
- You can now template the` name` and` template` in a` templateRef` . This allows for fully data driven workflow DAGs, so try it out. Thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12842](https://github.com/argoproj/argo-workflows/pull/12842) .
- The expr library has been upgraded providing some new functions in expressions thanks to[Jiacheng Xu](https://github.com/jiachengxu) in[#13194](https://github.com/argoproj/argo-workflows/pull/13194)


# CLI


- You can now update Cron Workflows, Workflow Templates and Cluster Workflow Templates with the` update` command via the CLI thanks to thanks to[Shuangkun Tian](https://github.com/shuangkun) in[#12803](https://github.com/argoproj/argo-workflows/pull/12803)
- You can selectively list workflow templates using a` -l` label selector thanks to[名白](https://github.com/qingfeng777) in[#13364](https://github.com/argoproj/argo-workflows/pull/13364)
- The CLI will now generate shell completions for the[fish shell](https://fishshell.com/) thanks to[@Sn0rt](https://github.com/Sn0rt) in[#13128](https://github.com/argoproj/argo-workflows/pull/13128)
- We also build and ship the CLI complied for[Risc-V](https://riscv.org/) thanks to[Meng Zhuo](https://github.com/mengzhuo) in[#12977](https://github.com/argoproj/argo-workflows/pull/12977)
- The lint command supports a` --no-color` flag thanks to[Miltiadis Alexis](https://github.com/miltalex) in[#12953](https://github.com/argoproj/argo-workflows/pull/12953)


# Build and Development


- There is now an awesome` /retest` command for retesting PRs in Github that occasionally fail in a flakey test thanks to[Miltiadis Alexis](https://github.com/miltalex) in[#13000](https://github.com/argoproj/argo-workflows/pull/13000)
- You can supply your own http client when using the go API client, allowing for proxying thanks to[Will Wang](https://github.com/williamburgson) in[#12867](https://github.com/argoproj/argo-workflows/pull/12867)
