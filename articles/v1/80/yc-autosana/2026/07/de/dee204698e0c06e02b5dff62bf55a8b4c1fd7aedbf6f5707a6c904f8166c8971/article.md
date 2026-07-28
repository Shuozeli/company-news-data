---
schema_version: "1.0.0"
document_id: "dee204698e0c06e02b5dff62bf55a8b4c1fd7aedbf6f5707a6c904f8166c8971"
company_key: "yc-autosana"
company: "Autosana"
source_id: "yc-autosana-news-import-ffdc10c70484"
canonical_url: "https://autosana.ai/blogs/gobi-case-study"
published_at: "2026-07-08T00:00:00+00:00"
first_seen_at: "2026-07-24T08:47:45.975311+00:00"
fetched_at: "2026-07-28T21:22:09.082656+00:00"
content_hash: "sha256:1ffc844a619d37017aedf35e3d966f5034ed3c5d4a0b73a3da5a54a855486aea"
---

# 'It's Like a Human Is Using Your App': How Gobi Replaced Maestro with Agentic Testing

*By Jason Steinberg · July 2026 · 10 min read*


Tyler Becks, CTO and co-founder of Gobi, got pulled onto the main stage at App.js Conf 2026 in Poland five days before the talk. The conference asked him on Monday. His slides were not finished until Friday morning. The makeup person was asking him to put his laptop down five minutes before he went on.


The talk was called "Why Your End-to-End Tests Are Lying to You." He told a room full of React Native engineers to stop using Maestro and switch to Autosana. Maestro was a conference sponsor.


This is the story of how he got there.


## What Gobi Does


Gobi is a social maps app that puts places, events, and friends in one place. It uses LLMs to enrich listings so users can see what to order at a restaurant, what is interesting about an event, and get curated weekend plans.


Tyler and his co-founder Shri built it after traveling the world and trying a million apps to solve this problem. Nobody was nailing it, so they built it themselves. Their tech stack started as a Next.js app, moved to Capacitor, then React Native, and is now migrating to native.


## The Maestro Era


When the Gobi team decided to invest in end-to-end testing, they did what most React Native teams do. They checked the Expo docs. Expo recommended Maestro. So they used Maestro.


The initial setup was painful, but that was expected. Any company has to go through some pain setting up account provisioning and making sure an environment can support end-to-end tests. Tyler was excited. He told the team it was easy to write Maestro tests and that anyone could do it.


Then he hosted an all-hands test-writing session. Two hours, the whole team writing tests. They went from six tests to thirteen. That was it.


> It wasn't that easy to write.


The problems compounded. Gobi's copy and UI changed constantly, so the team had to adopt test IDs on every single element in the app. Tyler described that decision simply:


> Which made me wanna die inside.


He tried to advocate for the React Testing Library principle: test the app as a user would use it. But Maestro could not deliver on that. Tests were point-and-click assertions tied to element IDs and labels. Tyler built a review-step workflow that tried to detect when a PR would break a test before it merged.


> The whole thing was jank and didn't work.


> At some point we caught one bug, or maybe it was like three bugs, in four months of using Maestro. And we spent hours maintaining these tests.


After all of this, the app still was not tested.


## The Breaking Point


> We were coming from a point of desperation. We needed tests and we needed something that wasn't gonna be an absolute nightmare.


A mutual friend connected Shri with Yuvan Sundrani, Autosana's CEO. Yuvan showed him a demo and they immediately set up a Slack channel to try it out.


Tyler saw "Autosana" appear in Slack and had no idea what it was. But Shri's assessment was direct:


> I think these guys are cracked. You gotta check it out.


A recommendation from Shri goes a long way. Tyler had this task assigned to another engineer. He could not wait.


## The Hesitancy


Tyler's biggest concern was simple. Introducing an LLM into testing sounded like adding more randomness to something that was already fragile.


> If you were to use an LLM in the Maestro test, I actually think it would have made things worse, not better.


The concern was rational. Most teams hear "AI testing" and picture an LLM injected into each step of a script, making an already brittle process more unpredictable. Tyler assumed the same thing.


## The Moment It Clicked


Tyler got on a call with Jason, Autosana's CTO, at 9 or 10 PM. By midnight, the entire setup was live.


> The moment that I understood how you guys were doing it, and it wasn't just injecting AI into each step, it was actually using an LLM the whole way with vision... it just clicked.


Then he watched an Autosana test encounter an element that was not visible on screen. It was inside a bottom sheet, below the fold. The agent scrolled down on its own, found the element, and completed the interaction.


> That took us almost a full day to try to write in Maestro. We never actually did it.


A full day of engineering time spent trying to get a test to scroll a bottom sheet. They never shipped it. The Autosana agent handled it without being told to scroll. It saw that the element was not visible, reasoned that scrolling would reveal it, and did it.


For Tyler, this was the full-circle moment. The thing he had been advocating for since the beginning, testing the app the way a user would actually use it, was finally happening.


> It's like a human is using your app.


> This is the closest that you can get to a human using it without a human actually using it.


The implication hit immediately. Writing tests no longer required writing code. It required describing what you wanted to verify, the same way you would describe a task to someone in a usability test.


> I can write instructions like I would tell someone in a usability test. I don't have to write code to do that.


## The Feedback Loop


Tyler's comparison between working with Maestro and working with Autosana is blunt.


With Maestro, the team had a couple of meetings. One bug got fixed as a result of an hour-long call. Maestro didn't seem to keep up with how fast they ship. Gobi was not really their target.


With Autosana, Tyler posts feedback in a shared Slack channel. Issues get resolved quickly. He estimates about 50 things have been fixed as a direct result of that feedback loop.


> Guys that are hungry and hustling making shit happen.


Every few days, Tyler notices a new updates and improvements messaged in the channel (new team members too!).


The cycle is tight: feedback, fix, ship. For a startup moving as fast as Gobi, that responsiveness is the difference between a testing tool that works and one that collects dust.


## Product People Writing Tests


One of the less obvious shifts is who writes tests now.


John, Gobi's head of product, built a spreadsheet with roughly 250 rows listing every user flow in the app. Each flow is rated low, medium, or high importance from a product perspective, not an engineering perspective. Tyler added a column: tested or not. He worked through the list to make sure every critical flow was covered.


The key insight: once engineers build the testing infrastructure (account provisioning, CI/CD integration), the actual test authoring does not require engineering knowledge. Product people can write tests directly because the tests are natural language descriptions of user flows, which is exactly what product people already think in.


> You can really have the product people writing these tests.


This changes the economics of test coverage. Instead of test authorship bottlenecked on engineering time, the people closest to the user define what matters. Engineers build features. Product defines what needs to be verified. The testing tool handles execution.


## Testing the App Like a User Would


Tyler frames the shift from traditional test scripts to agentic testing as generational. In his App.js talk, he called it the move from gen three to gen four.


> You wanna test the app as your user would use it. You don't wanna write code to try to manufacture that. You wanna actually do it.


The argument is not that AI is a nice addition to testing. The argument is that vision-based, agentic testing is the first approach that actually delivers on a principle the industry has talked about for years: test the application the way a real user experiences it.


> This is the first time that we've gotten close to the ability, if not close, but actually there. We can actually have something that picks up nuance and actually sees an app and understands.


Tyler now runs Autosana as part of his local development workflow too. He leaves a coding agent running overnight with a Linear ticket and Autosana handling end-to-end validation. He wakes up and the feature is roughly 90% complete, tested against real user flows.


## From Side Speaker to Main Stage


Tyler originally submitted a couple of random talk ideas to App.js Conf. One was about a CLI they built. The other was about using the Maestro CLI to automate feedback loops with Claude, which he never actually implemented.


Then someone dropped out, and the conference asked Tyler to take a main stage slot. On Monday. For a Friday talk.


Patrick, one of Gobi's engineers, suggested the topic:


> Talk about Autosana. It's probably the thing that would be the most valuable for people to hear and also the thing that people probably haven't heard of yet.


Tyler's instinct was to talk about something they built. Then he reconsidered. The most valuable thing he could put on people's radar was not a CLI or a workflow hack. It was the fact that an entirely new generation of testing exists and most teams do not know about it yet.


So he gave the talk. Slides finished Friday morning. Makeup person asking him to close his laptop. Maestro, a conference sponsor, in the audience.


> It was awkward.


## Current Workflow


Gobi runs nightly builds off main via GitHub Actions. As of June 2026, they are fully migrated to Autosana for testing.


Tests run against staging every night. Staging is the same codebase as production, pointed at a different API endpoint. The team cuts releases roughly every three days, so the nightly test run aligns closely with each production cut.


Test count grew fast. Tyler went from 12 tests to 25 or 30. He has added another 10+ since. The suite is approaching stability, with about three bugs left to fix before the full suite passes clean.


Tyler's triage workflow is straightforward. He reviews the Slack channel where test results post. For each failure, he checks to see if it's an actual bug in the app or an environment issue. In recent runs, he found six real bugs in five days. These are bugs that would have shipped to production without the nightly suite catching them.


From thirteen Maestro tests that kept breaking, to 30+ Autosana flows written on a plane, to a main stage talk telling the industry to rethink how they test. Gobi's testing journey is what happens when a skeptical CTO finds a tool that finally does what testing was always supposed to do.


---


## Test your app the way your users actually use it


Get set up at[autosana.ai](https://autosana.ai/signup) .


Prefer a walkthrough first?[Book a demo](https://autosana.ai/book-a-demo?source=blog_gobi-case-study) .
