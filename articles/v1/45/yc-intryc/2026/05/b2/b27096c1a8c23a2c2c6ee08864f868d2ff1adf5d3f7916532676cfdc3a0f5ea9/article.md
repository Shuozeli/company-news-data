---
schema_version: "1.0.0"
document_id: "b27096c1a8c23a2c2c6ee08864f868d2ff1adf5d3f7916532676cfdc3a0f5ea9"
company_key: "yc-intryc"
company: "Intryc"
source_id: "yc-intryc-news-import-17b79f653bb0"
canonical_url: "https://www.intryc.com/blog/ai-that-disappoints-customers-5-takeaways"
published_at: "2026-05-28T00:00:00+00:00"
first_seen_at: "2026-07-22T00:22:23.516240+00:00"
fetched_at: "2026-07-28T22:07:11.290939+00:00"
content_hash: "sha256:9ceb7fe7275128d82ed3a2a3b365d57d773d87c186c3e125fb8c4293a87ed014"
---

# AI That Disappoints Customers: 5 CX Takeaways

A 60% deflection rate can mean your AI is working. It can also mean your customers asked a question, got an incomplete answer, rephrased, got another incomplete answer, and stayed stuck in a loop they could not exit. The whole loop counts as a deflection. The dashboard calls it a win.


That is the gap Avner Firon has spent the last year closing. Avner is Director of Customer Experience at[AutoDS](https://www.autods.com/) , where he runs an 80-person CX department that handles AI-led support at volume. He joined Alex Marantelos on the first episode of[The Customer Experience Show](https://www.youtube.com/watch?v=3-WPbsJ1_30) to talk about what actually breaks when you deploy AI in support, and what separates the teams getting it right from the teams shipping disappointment at scale.


His core argument: AI deployment is not a technology rollout. It is an operational audit forced on you at speed. AI does not hide your process failures the way a trained human might. It executes them precisely, thousands of times a day. Here are the five takeaways from the conversation.


## 1. Stop reporting deflection. Start reporting resolution accuracy.


Avner does not soften this one. “Deflection rate is a vanity metric and the industry is celebrating the wrong number.”


Here is the mechanism he describes. A customer asks a question. The AI gives an incomplete answer. The customer rephrases. The AI responds with another inadequate variation. The customer stays in the loop. And the entire loop gets counted as a deflection, because the conversation never reached a human.


So the headline number goes up while the customer experience goes down. The old way measures whether a ticket avoided a human. The better question is whether the customer got a correct, complete resolution. Those are different numbers, and most dashboards are built to show you the first one.


For CX leaders being asked to report AI ROI upward, this is the conversation to have before someone else frames it for you. Deflection is the number your peers are still quoting.[Resolution accuracy](https://www.intryc.com/product/features/auto-qa) is the number that tells you the truth.


## 2. Treat a confident wrong answer as the most expensive failure you have.


Not every wrong answer costs the same. Avner draws a sharp line between a wrong answer and a confident wrong answer, and the second one is far more damaging.


“The most damaging failure is not a wrong answer. It is a confident wrong answer that creates that false expectation. Customers entered what felt like a real process, got what felt like a real confirmation and then hit a wall.”


Then he names why it lands harder than a human mistake: “Customers cannot rationalize it and they feel deceived by the brand itself, not by a person who had a bad day. That is a very different kind of damage to recover from.”


A customer can forgive an agent who had an off shift. They struggle to forgive a system that confidently told them they were eligible for something, let them act on it, and then walked it back. The blame attaches to the brand, not a person. That is why AI support needs[different quality standards than human support](https://www.intryc.com/blog/7-flavors-of-broken-qa) , not the same scorecard with a new logo on it.


## 3. Fix hallucinations at the source, not in the model.


The most vivid story in the episode is a loop with no exit. AutoDS runs an AI agent called Orin. Orin was telling customers to contact support. Orin is the support.


“The customer followed the instruction and landed right back in Orin. So it’s a loop you cannot exit. When we traced it back of course we found it in an article saying something like ‘if this happens contact support.’ Once we fixed it, the hallucination disappeared.”


The lesson is that the hallucination was not a model problem. It was a knowledge base problem. A human agent would have read “contact support,” understood the intent, and routed around it. The AI executed the instruction literally, at scale, until someone traced it back to the source article and corrected it there.


As Avner frames it: “The hallucination in a support conversation is a broken promise which might cost you a customer. If the AI tells the customer that they are eligible for something and then they act on it, that is your problem to solve, not the AI.” Correct the mistake at the source, and the symptom disappears everywhere it was showing up.


## 4. Design escalation as the premium tier, not the fallback.


Most teams treat a handoff to a human as the moment the AI failed. Avner argues that framing is backwards.


“The handoff between AI and humans is not a failure mode, it is a design feature. Companies getting this wrong treat escalations as a fallback. Companies getting it right treat it as a premium experience. I think that distinction matters more than any deflection rate.”


Where does he draw the line on what AI should handle alone? Outcomes with financial and account-level consequences. And even there, his answer is not to pull the AI out. It is to insert a quiet human checkpoint: “Insert maybe a silent human approval gate if needed. The customer sees the AI working in the background, a human reviews and approves the decision. The customer experiences continuity.”


This gives CX leaders language to push back when leadership asks them to minimize human involvement. Escalation is not the cost of AI getting it wrong. For the right conversations, it is the better product.


## 5. Sequence your rollout: tooling, then process, then mindset.


Avner is direct about the order of operations, and about which part is hardest.


“I would start with tooling because you cannot improve what you cannot measure, then the process because the tooling will expose gaps you didn’t know existed, then mindset and that’s the hardest part. You can buy tooling overnight, you cannot buy mindset.”


Tooling first, because measurement comes before improvement. Process second, because measurement surfaces the gaps you did not know you had. Mindset last, because it is the slowest to change and cannot be purchased.


The hinge point is your managers. “If your managers are not actively helping their teams learn and adapt, the mindset change stalls at the top and never reaches the floor. Managers are the bridge between AI strategy and human reality.”


He does not dodge the hardest part either. Some roles change, and some people leave. The agents who adapted, he says, “moved from transaction handlers to judgment specialists. That is a better job actually.” The same theme runs underneath his metric advice:[align leadership on a realistic year-one target](https://www.intryc.com/blog/ai-governance-for-contact-centers-from-pilot-to-production-qa) of roughly 40% resolution on your highest-volume topics. The trap is letting leadership chase 80% from day one. “Without the right framing, no number will ever feel like enough.”


## What ties these together


Five different failures, one root cause. Deflection that hides loops, confident wrong answers, hallucinations from bad articles, escalations treated as failures, rollouts that skip measurement. Each one is an operational gap that existed before AI and stayed invisible because a human quietly worked around it. AI removes the quiet workaround. It runs the gap at full speed and shows you exactly where you stand.


That is why Avner starts with tooling. You cannot improve what you cannot see, and AI makes the things you could not see impossible to ignore.
