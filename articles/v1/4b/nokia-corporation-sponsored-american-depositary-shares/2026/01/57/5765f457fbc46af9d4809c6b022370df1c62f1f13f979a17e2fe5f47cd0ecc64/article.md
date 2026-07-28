---
schema_version: "1.0.0"
document_id: "5765f457fbc46af9d4809c6b022370df1c62f1f13f979a17e2fe5f47cd0ecc64"
company_key: "nokia-corporation-sponsored-american-depositary-shares"
company: "Nokia Corporation Sponsored American Depositary Shares"
source_id: "nokia-corporation-sponsored-american-depositary-shares-news-import-bb650893ccf7"
canonical_url: "https://www.nokia.com/blog/can-ai-for-networks-be-sustainable/"
published_at: "2026-01-09T00:00:00+00:00"
first_seen_at: "2026-07-25T17:04:49.665774+00:00"
fetched_at: "2026-07-27T20:24:08.774797+00:00"
content_hash: "sha256:cd6586796dfe05a6d319a587858e94b546c0ff37de2cc33eaa940db3811af676"
---

# Can AI for networks be sustainable?

The amount of energy consumed by AI is a growing concern. Dr. Alexandra Sasha Luccioni, a research scientist at Hugging Face and a prominent voice on the environmental footprint of AI, has led efforts to create tools like the[AI Energy Score Leaderboard](https://huggingface.co/blog/sasha/announcing-ai-energy-score) to measure and compare energy consumption of different models. She has stated that "Measuring AI's environmental impact isn't just a responsibility—it's the compass that ensures innovation that guides us toward a more sustainable future."


To quantify the scale of the problem, in Q2 2025, ChatGPT 4.0 received ~2.5 billion queries[every day](https://techcrunch.com/2025/07/21/chatgpt-users-send-2-5-billion-prompts-a-day/) with an energy cost of at least[0.34 Wh](https://blog.samaltman.com/the-gentle-singularity) per query, according to CEO Sam Altman. That works out to about 275 GWh of electricity per year, which is equivalent to the energy usage of an average American household over 120 years. More recent estimates put ChatGPT 5.0 at 18 Wh per[query](https://www.tomshardware.com/tech-industry/artificial-intelligence/chatgpt-5-power-consumption-could-be-as-much-as-eight-times-higher-than-gpt-4-research-institute-estimates-medium-sized-gpt-5-response-can-consume-up-to-40-watt-hours-of-electricity) .


This year, Gartner forecasts electricity demand for data centers to double by[2030](https://www.gartner.com/en/newsroom/press-releases/2025-11-17-gartner-says-electricity-demand-for-data-centers-to-grow-16-percent-in-2025-and-double-by-2030) . Given these kinds of numbers, it doesn’t seem overly cautious to question the sustainability of our current AI trajectory. Beyond electricity demand and the resources needed to produce it, there is also water for cooling, rare earth shortages and the opportunity costs—i.e., even if all the energy required was provided by renewables, we would have to ask whether those generation sources wouldn’t be more usefully employed powering transportation, heating homes and generally helping us to electrify our societies.


## AI for networks


Along with energy consumption, AI is also driving a rapid expansion in network capacity, both inside and outside of the data center. Hyper-connectivity is one of the critical conditions for supporting AI and expanding its impact in real-world applications. From model training to the inferencing of AI agents, networks will be critical for connecting cloud, edge and endpoint devices (the ‘cloud continuum’) to provide end users (human and machine) with the AI capabilities they need, wherever they are.


Somewhat ironically, in order to support the AI-cloud continuum , networks will have to also embrace AI, becoming autonomous in many parts of their operations. 3GPP sees AI-nativeness as foundational in future networks, which is reflected in current discussions around the design of 6G.


## Designing sustainability


The sustainability issues associated with AI, thus, will also impact network operations. Network operators are already conscious of energy costs for running servers, along with cooling and space requirements. Embracing AI can make network operations more energy efficient; this is one of its key use cases in 6G. But, as Jevons’ paradox predicts, these energy gains may simply go to scaling AI training and inferencing, with the total energy use only growing as a result.


So, the question begging to be answered is, can we design AI for networks to use less energy? As it turns out, yes, there are several things we can do. These strategies include using smaller, purpose-built models, training models more efficiently, reducing the training set to only relevant data, and employing sparse, event-driven computation that mimics the functioning of the human brain. There are, in fact, several brain-inspired AI architectures being researched in an attempt to reduce energy use: spiking neural networks (SNN), liquid neural nets (LNN) and tiny hierarchical reasoning models (HRM) are some of the more well-known.


Hardware architectures are also being looked at to improve power performance. IBM has been researching the use of analog chips that have shown a 14x improvement in energy use. Researchers at Tsinghua University have reported that their analog photonic chips, called ACCELs, are achieving energy efficiencies that are millions of times[higher](https://www.tsinghua.edu.cn/en/info/1569/12965.htm#:~:text=In%20a%20laboratory%20test%2C%20the,times%20less%20energy%2C%20researchers%20found.) than today’s digital GPUs.


## Energy-efficient AI for networks


We’ve recently published a[paper](https://onestore.nokia.com/asset/215230) discussing many of the approaches to energy saving s currently being explored by the broader industry. We propose a three-step guide to pursuing more sustainable approaches to AI use in networks.


1. Don’t apply AI indiscriminately to network functions. Determine if there is a real need. This will help you decide on the trade-off between energy required vs. benefit received.
2. Once you’ve decided AI is worthwhile, do a thorough analysis of which techniques to use and optimize your design using compression techniques, optimized training approaches, specialized hardware (where available), and optimal software architecture approaches.
3. Measure and monitor the performance of energy consumption as well as other metrics (we discuss several benchmarks that can be used). The results of these metrics should give you the necessary feedback to iterate on your technical choices and achieve greater energy optimization.


##


##


## Looking ahead


Our network vision for AI systems is that they be energy-efficient while at the same time capable of scalable continual learning.


If you are interested in reading more about our research, start with our recently published paper, “[Advancing AI: Sustainable AI for networks](https://onestore.nokia.com/asset/215230) .”
