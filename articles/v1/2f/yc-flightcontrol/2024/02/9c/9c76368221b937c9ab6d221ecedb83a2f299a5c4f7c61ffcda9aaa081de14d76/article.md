---
schema_version: "1.0.0"
document_id: "9c76368221b937c9ab6d221ecedb83a2f299a5c4f7c61ffcda9aaa081de14d76"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/reduced-github-actions-bill-by-63"
published_at: "2024-02-16T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:757febbb10918b4083fe05d590f053a3cd38382a89e2c2a0ddc71f8c418816e9"
---

# Reduced GitHub Actions bill by 63%

We reduced our monthly GitHub Actions usage **from 46,144 minutes to 19,155 minutes** .


This reduced our bill by 63%, and most importantly, **sped up pull requests with less time waiting on CI checks.**


We have a modestly sized monorepo with eight main packages. Two of these packages are shared by multiple other packages. Each package has a number of CI checks, including linting, type checking, compiling, and tests.


Each of these checks would run for each PR, regardless of whether the code in that package changed or not. Over time, this became more frustrating. Often, you were stuck waiting on an irrelevant check. And we were pointlessly paying for this server time.


We were using 46,144 minutes, which is **32 full days** of CI time per month! That’s like paying for a permanently running server.


## GitHub Actions doesn’t natively support file path filters


Finally, we got around to trying to optimize this. You’d think GitHub Actions would have a config for this, because they have a config for almost everything.


But nope, the[built-in path filters](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#onpushpull_requestpull_request_targetpathspaths-ignore) only work on at the top workflow level. To use this, each job would have to be in a separate workflow file.


## Open-source to the rescue


Thankfully, we found[paths-filter](https://github.com/dorny/paths-filter) , an open-source Action that makes it easy to skip jobs or steps based on changed files.


You can use the action multiple ways, but we defined a new job just for change detection like this:


```text
jobs:
changes:
name: Detect files changes
runs-on: ubuntu-latest
timeout-minutes: 3
outputs:
tower: ${{ steps.filter.outputs.tower }}
only-tower: ${{ steps.filter.outputs.only-tower }}
shared: ${{ steps.filter.outputs.shared }}
website: ${{ steps.filter.outputs.website }}
ui: ${{ steps.filter.outputs.ui }}
docs: ${{ steps.filter.outputs.docs }}
flightdeck: ${{ steps.filter.outputs.flightdeck }}
api: ${{ steps.filter.outputs.api }}
steps:
- uses: actions/checkout@v2
- uses: dorny/paths-filter@v2.2.1
id: filter
with:
filters: |
tower:
- 'package.json'
- 'pnpm-lock.yaml'
- 'packages/tower/**'
- 'packages/shared/**'
only-tower:
- 'packages/tower/**'
api:
- 'package.json'
- 'packages/api/**'
shared:
- 'package.json'
- 'pnpm-lock.yaml'
- 'packages/shared/**'
ui:
- 'package.json'
- 'pnpm-lock.yaml'
- 'packages/ui/**'
website:
- 'packages/website-next/**'
flightdeck:
- 'package.json'
- 'pnpm-lock.yaml'
- 'packages/flightdeck-next/**'
- 'packages/ui/**'
- 'packages/shared/**'
docs:
- 'package.json'
- 'pnpm-lock.yaml'
- 'packages/docs/**'
```


Then every other job imports those results with the` needs: changes` config and conditionally runs with a config like` if: ${{needs.changes.outputs.shared == 'true'}}` .


```text
shared:
name: Shared
runs-on: ubuntu-22.04
needs: changes
if: ${{needs.changes.outputs.shared == 'true'}}
steps:
- uses: actions/checkout@v2
- name: Set up pnpm
uses: pnpm/action-setup@v2
with:
version: 8.6.7
- name: Set up Node
uses: actions/setup-node@v4
with:
node-version: 20.x
cache: "pnpm"
cache-dependency-path: pnpm-lock.yaml
- run: pnpm -v
- name: Install
run: pnpm install --no-optional
- name: Lint
env:
NODE_OPTIONS: "--max_old_space_size=8192"
run: pnpm eslint packages/shared
- name: Set up pnpm
uses: shogo82148/actions-setup-mysql@v1
with:
mysql-version: "8.0"
- name: Test
run: cd packages/shared && pnpm test:setup && pnpm test
```


## Results and what’s next


This reduced our usage to 19,155 minutes and our bill by 63%. And most importantly, it reduced CI waiting time by eliminating irrelevant checks.


Thanks to Camila Rondinini for making this improvement for our team!


The next improvement is to **use a custom runner** . Because the default runners are ridiculously expensive.


You have two default Ubuntu size options:


-


2 CPU, 7 GB RAM is $346/month


-


4 CPU, 14 GB RAM is $691/month


That’s over four times as expensive as AWS EC2. Depending on the instance type, 4 CPU with 16 GB RAM is around $150/month.


**For the same price as GitHub’s 4 CPU + 16 GB RAM, you can get 32 CPU + 128 GB RAM!**


Granted, it’s not that trivial to set up your own EC2 runner. An easier option is a drop-in service called[Warpbuild](https://www.warpbuild.com/) . And at Flightcontrol we’re soon going to make a replacement for AWS CodeBuild for blazing fast builds. A secondary goal with this project is to easily use the build system as GitHub Action runners.


Let me know on[Twitter](https://twitter.com/flybayer) or[LinkedIn](https://www.linkedin.com/in/brandonbayer1/) if you’ve found this helpful!
