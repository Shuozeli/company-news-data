---
schema_version: "1.0.0"
document_id: "230a8965075dd9e57926d03e7518833e34318da59bf88d0e9f3fb3e00bfc38d6"
company_key: "arteris-inc-common-stock"
company: "Arteris Inc. Common Stock"
source_id: "arteris-inc-common-stock-news-import-b55a70a8b442"
canonical_url: "https://www.arteris.com/blog/model-your-ips-and-your-nocs-edn/"
published_at: "2026-06-17T11:40:36+00:00"
first_seen_at: "2026-07-23T02:24:35.785039+00:00"
fetched_at: "2026-07-28T21:43:28.836467+00:00"
content_hash: "sha256:24e7e8e98883428cc8eb7db90109dfaaeefbe56909b1ec1a7b0b8a65e2d8ca3d"
---

# EDN: Model your IPs and your NoCs

[Home](https://www.arteris.com/)


»[Newsroom](https://www.arteris.com/newsroom/)


»[Blog](https://www.arteris.com/newsroom/blog/)


» EDN: Model your IPs and your NoCs


# EDN: Model your IPs and your NoCs


- Jun 17, 2026


- Rocco Jonack


-


2


min read


When chip design and verification teams start a new project, they recognize the need for models that capture the design at a high level of abstraction. However, they tend to focus on acquiring or creating models of the IP blocks used to implement the device’s core functionality, while overlooking network-on-chip (NoC) interconnect IP until it’s too late.


## Modeling and simulation evolution


As chip designs grew from a handful of gates in the 1970s to hundreds of IP blocks connected by complex interconnect fabrics in the 2020s, modeling and simulation evolved to keep pace. Early approaches modeled everything at the gate level, providing complete visibility, but they quickly became impractical as complexity increased.


The industry’s first major step up in abstraction was the register transfer level (RTL). These models describe how data moves between registers on each clock cycle, maintaining bit-level and cycle-level accuracy. To this day, RTL simulation remains the gold standard for functional correctness and final sign-off. The trad-eoff is speed. Because the RTL models every signal transition, meaningful simulations can take hours or even days.


#####


*Figure 1. The integration of functional blocks and interconnects increased over time.*


To address this, engineers introduced cycle-accurate models. These preserve timing at the clock-cycle level but avoid modeling every individual signal. They capture events as they happen without describing every bit flip, thereby making them ideal for performance analysis. Designers can evaluate latency, bandwidth, and contention with high confidence while running simulations fast enough to explore architectural alternatives.


To read the full article on[EDN](https://www.edn.com/model-your-ips-and-your-nocs/) , click[here](https://www.edn.com/model-your-ips-and-your-nocs/) .


- [Network-on-Chip (NoC)](https://www.arteris.com/tag/network-on-chip-noc/)


Blogs


## **Latest** Blogs


[View All Blogs](https://www.arteris.com/newsroom/blogs/)


Blog


Semiconductor Engineering: Avoid The Hidden Bottleneck Of Integration At Scale


This Semiconductor Engineering article examines how SoC integration has become a major bottleneck as designs scale in complexity, with growing numbers of IP blocks, registers, and hardware/software interfaces.


[Learn more about this](https://www.arteris.com/blog/semiconductor-engineering-avoid-the-hidden-bottleneck-of-integration-at-scale/)


Blog


The AI Journal: Making chiplets work for AI requires more than connectivity


This article explains why building successful AI chiplet architectures requires more than high-speed die-to-die connectivity. It explores how efficient data movement, protocol selection, coherency, and intelligent NoC architecture are critical to maximizing performance, scalability, and energy efficiency in next-generation AI


[Learn more about this](https://www.arteris.com/blog/the-ai-journal-making-chiplets-work-for-ai-requires-more-than-connectivity/)


Blog


What the Cyber Resilience Act means for the future of chip design


The EU Cyber Resilience Act is reshaping semiconductor security, making cybersecurity, compliance, and lifecycle management core design priorities.


[Learn more about this](https://www.arteris.com/blog/what-the-cyber-resilience-act-means-for-the-future-of-chip-design/)


Blog


Semiconductor Engineering: Reducing Avoidable Memory Trips In HBM Systems


As AI and high-performance SoCs increasingly rely on HBM, memory bandwidth alone is no longer enough to maximize performance. This article discusses why the intelligent data movement and cache efficiency are critical to unlocking the full benefits of HBM-based architectures.


[Learn more about this](https://www.arteris.com/blog/semiconductor-engineering-reducing-avoidable-memory-trips-in-hbm-systems/)


Blog


Beyond Moore’s Law: Heterogeneous Computing and AI SoCs


As Moore’s Law slows, heterogeneous computing is driving AI, automotive, and data center innovation through specialized compute, chiplets, and advanced interconnects.


[Learn more about this](https://www.arteris.com/blog/beyond-moores-law-heterogeneous-computing-and-ai-socs/)


Blog


Cyber Defense Magazine: Securing The Unseen Why Data in Motion is the Next Cybersecurity Frontier


Securing the unseen: As AI drives massive data movement inside chips, organizations must secure and monitor data in motion to close hidden hardware attack surfaces.


[Learn more about this](https://www.arteris.com/blog/cyber-defense-magazine-securing-the-unseen-why-data-in-motion-is-the-next-cybersecurity-frontier/)


[View All Blogs](https://www.arteris.com/newsroom/blogs/)
