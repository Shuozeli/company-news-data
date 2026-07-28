---
schema_version: "1.0.0"
document_id: "2c5cf331859d987ff2b77f24ab830a295e1026ae1c1c9240a28fe98ae496f78a"
company_key: "nokia-corporation-sponsored-american-depositary-shares"
company: "Nokia Corporation Sponsored American Depositary Shares"
source_id: "nokia-corporation-sponsored-american-depositary-shares-news-import-bb650893ccf7"
canonical_url: "https://www.nokia.com/blog/co-creating-ai-native-wireless-networks-to-deliver-next-level-reliability/"
published_at: "2026-02-23T00:00:00+00:00"
first_seen_at: "2026-07-25T17:04:49.665774+00:00"
fetched_at: "2026-07-27T20:24:08.774797+00:00"
content_hash: "sha256:b786aef4ca20626761a7cff7a89127e80433271b254943b912b3e4e5facb663a"
---

# Co-creating AI-native wireless networks to deliver next-level reliability

As wireless networks evolve toward AI-native design and lay[the foundations for 6G](https://www.nokia.com/6g/) , innovation is extending deeper into the physical layer. In a wireless network, not all signals are created equal: some carry user data such as video, voice, and messages, while others quietly keep the system reliable. Hybrid Automatic Repeat Request (HARQ) feedback belongs to the latter category. It consists of just a few bits sent from the user equipment (UE) to the network, yet those bits determine whether data is retransmitted, discarded, or successfully delivered.


Most transmissions succeed, and the UE responds with an acknowledgment (ACK). Occasionally, a packet arrives with error and the UE sends a negative acknowledgment (NACK), triggering a critical recovery action. If that NACK is incorrectly decoded, the consequences can ripple through the system, leading to missed retransmissions, wasted radio resources, or even service outages. An incorrect ACK is inefficient; an incorrect NACK can be far more damaging.


This asymmetry is reflected in system design targets. HARQ combines forward error correction with fast retransmissions to drive data block error rates (BLER) to very low levels, but its effectiveness depends on the reliability of the feedback loop. In practice, networks target ACK error rates below 1% and NACK error rates below 0.1% at the signal-to-noise ratios where they are expected to operate. While ACKs dominate feedback traffic under most channel conditions, the rare NACKs carry disproportionate operational importance.


In[5G New Radio (NR)](https://www.nokia.com/radio-access/) , however, HARQ feedback coding treats all feedback sequences equally, without accounting for the highly imbalanced probabilities and asymmetric reliability requirements of ACK and NACK bits. This one-size-fits-all approach limits efficiency and robustness, particularly under challenging radio conditions.


This is where[AI-native wireless networks](https://www.nokia.com/6g/unlocking-the-full-potential-of-ai-native-6g-through-standards/) make a difference. By integrating AI directly into network design, the system can learn real-world ACK and NACK distributions, channel characteristics, and reliability objectives, and use that insight to protect feedback where it matters most.


To explore this,[Nokia Bell Labs](https://www.nokia.com/bell-labs/research/6g-networks/) and Qualcomm Technology have teamed up on an AI-based Joint Source-Channel Coding (JSCC) approach for HARQ feedback. A neural network is trained to generate optimized codewords and map them to waveforms with unequal protection, reflecting both traffic statistics and reliability priorities. Once trained, the solution can be implemented using a simple lookup table for real-time encoding, making it both intelligent and practical.


This work demonstrates how AI-native design can transform even long-established mechanisms in wireless systems. By combining Nokia’s expertise in radio systems and base-station design with Qualcomm’s leadership in device platforms, a proof-of-concept was developed to evaluate traditional and AI-native approaches under identical conditions. The result is a more robust and efficient HARQ feedback loop, better aligned with operational needs.


At Nokia, we are advancing connectivity for the AI era to help our customers stay ahead in the AI supercycle by delivering secure, reliable, and high-performance network infrastructure. AI-native wireless networks represent more than a technical upgrade; they mark a shift in how networks are designed and built. Through co-creation, partners can develop smarter, more adaptive systems that not only correct errors but anticipate them, paving the way for the continued evolution of 5G and the foundations of[future 6G networks](https://www.nokia.com/6g/) .
