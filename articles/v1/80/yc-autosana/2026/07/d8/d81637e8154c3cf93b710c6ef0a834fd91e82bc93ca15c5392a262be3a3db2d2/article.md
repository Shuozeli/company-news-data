---
schema_version: "1.0.0"
document_id: "d81637e8154c3cf93b710c6ef0a834fd91e82bc93ca15c5392a262be3a3db2d2"
company_key: "yc-autosana"
company: "Autosana"
source_id: "yc-autosana-news-import-ffdc10c70484"
canonical_url: "https://autosana.ai/blogs/launching-the-ui-ux-agent"
published_at: "2026-07-14T00:00:00+00:00"
first_seen_at: "2026-07-21T08:42:48.440297+00:00"
fetched_at: "2026-07-28T21:22:05.726331+00:00"
content_hash: "sha256:3b94b188c3f293a643ce231cf0221d462ad07a61bb7cd522983895e945f5cf03"
---

# Launching the UI/UX Agent

*By Yuvan Sundrani · July 2026 · 4 min read*


## The problem


E2E testing answers the most important question in software quality: does it work?


Your tests verify that the auth flow completes, the checkout processes a payment, and the settings page saves changes. If all steps pass, the build is green. Ship it.


But there's a category of problems that functional testing was never designed to catch. Teams stop noticing these because they look at their app every day. You built the screen, you know where everything is, and on your device it looks fine. A user opening your app for the first time sees something different.


Today we're launching the UI/UX agent. Every E2E test you run on Autosana now evaluates whether your app's experience actually holds up, not just whether it functions.


## What the UI/UX agent does


While the E2E agent verifies that your app works, the UI/UX agent watches the same run like a senior QA engineer. It looks at the screenshots, the actions, and your instructions, and flags anything that looks wrong from an experience standpoint.


Every finding is tagged with a type and a severity. The three types:


**Functional issues are real bugs:**


- Buttons that don't respond to taps
- Flows that dead-end or redirect to the wrong screen
- Explicitly-asserted elements that are missing or wrong
- Regressions where something that worked before no longer does


**UI issues are visual problems:**


- Text overflowing its container
- Misaligned or overlapping elements
- Truncated labels or clipped content
- Layout shifts on specific screen sizes or devices


**UX issues are experience problems:**


- A feedback prompt that fires at a "weird" state and partially covers the home screen
- Flows where the next step isn't obvious
- Screens that open when they shouldn't
- Confusing state transitions that leave the user unsure if their action went through


Each finding also gets a severity: critical, major, or minor. Critical issues should block a release. Major and minor issues need tickets.


## The Issues dashboard


Findings don't just appear in individual test runs. They land on a new Issues board, organized into three columns: Critical, UI/UX, and Instruction.


The same problem often shows up across dozens of runs. A broken checkout button fails the same way on iOS and Android, across three flows, over a week of nightly runs. Listing all of those separately would bury you. Instead, Autosana groups findings that describe the same underlying problem into a single issue, even when the wording, flow, app, or device differs.


The grouping is semantic. We compare the meaning of findings, not just their text. As new runs come in, matching findings join the right group automatically. Near-duplicate groups get merged. Groups that have grown too broad get split apart. You don't manage any of this. The board just stays clean.


Each issue tracks:


- **Occurrences:** how many times this problem has been seen
- **Affected flows, apps, devices, and builds:** the full blast radius
- **Severity breakdown:** how many critical, major, and minor findings rolled into the group
- **First seen and last seen:** whether it's brand new, recurring, or gone quiet
- **Branches:** which build and branch the failing runs came from


Click any issue to open its detail page with a plain-English summary, an evidence table with screenshots from the exact action that triggered the finding, every affected flow and device, and one-click ticket creation.


## How it connects to E2E testing


This is not a replacement for E2E testing. It's what becomes possible once your functional foundation is solid.


E2E testing tells you the bridge is structurally sound. The UI/UX agent tells you whether the guardrails are confusing to drivers. You always need the bridge to be sound first.


---


## Get started


The UI/UX agent is live now for all Autosana customers.


Get started at[autosana.ai](https://autosana.ai/signup) .


Prefer a walkthrough first?[Book a demo](https://autosana.ai/book-a-demo?source=blog_launching-the-ui-ux-agent) .
