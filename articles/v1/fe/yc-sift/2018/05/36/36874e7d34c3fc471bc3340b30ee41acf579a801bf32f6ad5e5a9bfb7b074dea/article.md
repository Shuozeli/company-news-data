---
schema_version: "1.0.0"
document_id: "36874e7d34c3fc471bc3340b30ee41acf579a801bf32f6ad5e5a9bfb7b074dea"
company_key: "yc-sift"
company: "Sift"
source_id: "yc-sift-news-import-56a09e055dd6"
canonical_url: "https://engineering.sift.com/engineeing-management-effective-design-reviews/"
published_at: "2018-05-31T21:34:58+00:00"
first_seen_at: "2026-07-24T13:26:21.656972+00:00"
fetched_at: "2026-07-28T21:33:49.818370+00:00"
content_hash: "sha256:7f5ca8acd30573bbe91b2e208504a8153b61cbf15725ca9da930e1813257dbf9"
---

# Engineering Management – Effective Design Reviews

Post category:


[Articles](https://engineering.sift.com/articles/)


# [Engineering Management – Effective Design Reviews](https://engineering.sift.com/engineeing-management-effective-design-reviews/)


Sam Talaie


• May 31, 2018


# Engineering Management Series


The past few years have been a time of incredible growth at Sift and there is


[no sign that we are slowing down](https://blog.siftscience.com/2018/sift-science-series-d/) . To continue


[delighting](https://engineering.siftscience.com/2017-sift-engineering-review/)[our ever growing list of customers](https://siftscience.com/case-studies) , we’ll be scaling our engineering team in San Francisco and across


[multiple other offices](https://www.geekwire.com/2017/san-franciscos-sift-science-opens-new-seattle-engineering-center-led-amazon-vet/) at a faster pace than ever. To do this successfully, we find ourselves continuously revisiting processes, organizational structures, and communication protocols and adjusting them to meet the needs of the ever growing teams.


In the following series of engineering management posts, we’ll share some of our learnings while growing our engineering team from a handful to 40+ engineers across 8 teams in San Francisco and Seattle. Please note that the processes and learnings we highlight are snapshots of what has worked for us at a specific point in our history and will likely continue to evolve as we grow.


We’ll start the series with a summary of how we go about planning for and running effective design reviews.


# **1. Effective Design Reviews**


Design reviews are a powerful tool for delivering high quality software products by drawing upon the valuable collective knowledge and experience of the team. The goal of a review is to uncover hidden assumptions and rationale behind key design choices and to ensure that these choices adequately address the objectives of the project. In the following section, we share a concise version of our field-guide for engineers, tech leads, and managers performing design reviews.


## **Foundation:**


Evaluating designs without context is like trying to pick between a pair of sandals and snow boots without knowing the travel destination. To ensure your reviewers have the right context while reviewing your design, you’ll want to set the stage and speak to the items highlighted below. We’ve found it helpful to document and share this info ahead of the meeting and speak to it during the meeting before getting into the actual review.


- Clearly identify the **key objectives** and **product requirements** that the design is going to address and set the context for product and business needs. The product may be customer-facing or internal, e.g. an API to be consumed by other services.


- *Objective: Need a system to store user generated content*
- *Product Requirement: Any content older than 3 months may be purged from the system (GDPR anyone?)*


- Clearly identify **assumptions** and **engineering constraints** for addressing the objectives


- *Assumption: Backups won’t be larger than 200GB and will occur at most once a day*
- *Engineering Constraint: We can only support tarballs without massive overhaul of the system*


- Establish **common understanding** of the current state of the solution of system


- Offline documentation alone is often not sufficient.
- Plan to spend some time during the design review whiteboarding the architecture and answering questions.


##


## **Design Review Meeting**


- Establish the **foundation** for the discussion:


-


- Key objectives and product constraints
- Assumptions and engineering constraints
- System’s current state


- This step is not to be glanced over. Often times a majority of questions and issues are due to misunderstandings of the key objectives and assumptions


- **Present the proposed design** and highlight how it differs from the current system
- Clearly **present tradeoffs**


- Design choices are a result of carefully balancing product and engineering constraints, implementation complexity, risk, maintenance burden, fault tolerance, etc.
- Ensure that you clearly identify your design tradeoffs, and work with the reviewers to uncover theirs. The goal is to **challenge assumptions** and come to an understanding of root concerns together.
- The main goal here is to elicit feedback and document the various options, not to make a decision


- Work patiently to uncover concerns of the team. Try to determine the root cause of the concerns rather than debating them endlessly:


- *Engineer: We need a car*
- *Reviewer: You’ll definitely need an SUV*
- *Engineer:* ***Why*** *specifically do we need an SUV?*
- *Reviewer: Since we need to drive through the snow, you’ll likely need an SUV*
- *Engineer: We considered this scenario and decided chains might be sufficient – any other reasons why we’d still need an SUV?*
- **Reviewer: 👍**


## **For a successful design review**


- **Schedule meetings at the earliest reasonable stage:**


- The goal of design review is to uncover problems in time to make necessary changes. This may include having to completely consider a new design. Late stage review meetings are not going to be terribly effective. Plan accordingly and be comfortable with the idea of parting completely with the existing design.


- **Allow enough time per meeting(s) to really get to the core issues.** Large systems / designs may require more meetings, and meetings that are longer than 1 hour
- **Avoid bikeshedding / out-of-scope discussions**


- Avoid spending too much time on similar designs, stylistic choices, cosmetic issues, and ensure you set the scope of the design review prior to discussions.


- **Reviewers: come prepared.** Read all documentation and ask clarifying questions before the meeting. We found it useful to directly do by adding comments to the design documents in Dropbox Paper or Google Docs.
- **Presenters:** static, lengthy documentation is not always the most ideal way to present complex systems and lacks interactivity. If needed, schedule a separate meeting just to establish **the foundation interactively in person.** The goal here is to *complement* the written documentation with in person discussion to fill in any gaps.


## **Basic Meeting Etiquette / Tips**


- Document **open questions and suggestions on the board**


- Folks who feel their feedback hasn’t been heard may continue repeating the same question or go on lengthly monologues until it’s been acknowledged.
- Actively documenting helps move the discussion along and also serves as a great shared model of what’s been discussed (in addition to allowing visual clustering of similar topics)


- Reviewer: ask questions or present concerns with an understanding that lots of thought and discussion has gone into the design by the presenters
- Presenter: be humble, patient, open to feedback. The reviewers clearly haven’t spent as much time thinking about the issues, but likely have very real and valuable feedback which should be elicited
- Reviewers and presenters are **on the same team** , working together against faulty designs and future bugs
- Consider **tone and voice**


- “Why haven’t you considered cost?” is accusatory and may elicit a much more defensive response vs. “Have you considered cost / budget constraints?” which assumes costs may have been considered but not presented or documented properly.


- **Reiterate questions** to ensure you have the right context
- “Be tough on ideas but excellent to each other” (This is one of our company values)


- Be courteous, avoid interrupting others, avoid long monologues


## **On Decisions:**


- At Sift, engineers are **empowered** to make important decisions rather than go through lots of formal processes and committees
- The final call for a design ultimately lies with the engineers
- However, in this model, such level of freedom comes with an **immense responsibility** for the ultimate success of deliverables


- Engineers should thoroughly consider team feedback in addition to any other available resources to make their decisions
- Engineers are expected to speak to their decisions and helps others understand the rationale


- During the code review stage, reviewers are expected to review not only the code but also the overall system design and how it fits within the current ecosystem. Hence, if there are structural design issues called out and not addressed early during the design phase, they will ultimately have to be explained, or addressed prior to rollout. Engineers are encouraged to handle design feedback early in order to avoid making drastic changes or having the conversation for the first time during the code review.


In summary, we find that coming to the meetings prepared with the right context, then having constructive discussions to tease out assumptions and potential blindspots leads to much better outcomes.


## Author


-


[Sam Talaie](https://engineering.sift.com/author/saam/)
