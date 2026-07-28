---
schema_version: "1.0.0"
document_id: "84816b1a0cdb36bb70f8641fe9f03777a50744d983876c7dbcfa248e9deaf364"
company_key: "nokia-corporation-sponsored-american-depositary-shares"
company: "Nokia Corporation Sponsored American Depositary Shares"
source_id: "nokia-corporation-sponsored-american-depositary-shares-news-import-bb650893ccf7"
canonical_url: "https://www.nokia.com/blog/one-year-later-the-residential-proxy-botnet-problem-got-bigger-not-smaller/"
published_at: "2026-06-23T00:00:00+00:00"
first_seen_at: "2026-07-25T17:04:49.665774+00:00"
fetched_at: "2026-07-27T20:24:08.774797+00:00"
content_hash: "sha256:a49b1fc89ab771b276bb716a850ac25ded05bce49879d488f292557374a1c95b"
---

# One year later: the residential proxy botnet problem got bigger, not smaller

*Adapted from NANOG97 talk, June 2026, done jointly by Comcast Threat Research Lab (CTRL) and Nokia Deepfield Emergency Response Team. The figures below reflect a fast-moving, adversarial environment, so treat them as point-in-time estimates.*


## A year later, what changed?


A year ago, at NANOG94, I warned about a strange new kind of DDoS traffic originating from within consumer networks. This DDoS infrastructure, later named Kimwolf, exploited a trivial flaw in residential proxy devices to become the largest botnet in history. Nokia helped take down Kimwolf DDoS command-and-control, and that part worked: Kimwolf is no longer active, and the record-breaking attacks that defined its peak have slowed. But the threat did not die so much as metastasize. Kimwolf fragmented into more than 20 competing botnets, and the number of DDoS active daily endpoints climbed from roughly 1 million to 8–9 million over the last year. This is a story of AI’s[multi-billion-dollar appetite for residential bandwidth](https://www.forbes.com/sites/josipamajic/2025/11/20/inside-the-209-billion-battle-powering-ais-web-data-infrastructure-future/) indirectly fueling an entirely new scale and type of critical internet infrastructure threat.


## A boring problem that stopped being boring


I’ll start with a confession: for most of my career, DDoS was boring. That’s not a knock on the people defending against attacks -- it’s just that for twenty years the attacks barely changed. Almost all DDoS originated in a handful of bulletproof hosts in Eastern Europe that used the same decades-old amplification and spoofing tricks. A multi-terabit attack was rare enough to make headlines. Residential proxies (overlay networks that route traffic through ordinary people’s home IP addresses) existed, but they were a niche part of the internet ecosystem. I did not pay much attention to residential proxy until last summer when everything I knew about DDoS attacks began to change…


*Two decades of largely flat DDoS, and then the residential proxy surge.*
*The Y axis shows the peak volume of DDoS attacks.*
*Each circle is a discrete attack above 600 Gbps. Data obtained from collaborating ISPs and hosting companies.*


## The botnet I didn’t see coming


The first crack was Eleven11bot (some call it RapperBot): roughly 100,000 compromised DVRs stitched into a botnet that threw a record ~6 Tbps attack in late 2024. I thought Eleven11 would remain the DDoS record holder for months or even years.


I was wrong.


Immediately before last year’s NANOG94, Nokia customers began to face new attacks at the record-breaking levels of tens of Tbps. These DDoS attacks were categorically different. The attacks did not come from bulletproof hosting or far-off countries – they poured out of Comcast, Verizon, BT and dozens of other major US and European providers. And not a few thousand devices, but the new DDoS came from hundreds of thousands of residential endpoints. We estimated the aggregate capacity (if all compromised residential IoT devices were used simultaneously) in the hundreds of terabits!


## How do your devices end up working for someone else?


Residential proxies can be installed on home devices in two ways. The first is SDKs: a dozen or so vendors pay app developers to embed a small library in games, calendars, and utilities, which are mostly downloaded from the Android app store. A few apps notify users of the embedded proxy; as far as we can tell, most do not. The second is cheap Android streaming boxes and digital picture frames that ship from the factory with a backdoor already installed. You plug in your $30 streaming box, and it quietly joins a proxy network straight out of the box. The Wall Street Journal put up a[video](https://youtu.be/apEPPKYgLL0) that explains this well.


## Why the U.S., and why now? Of course, it’s the money


Surprisingly, the U.S. dominated as the primary source of residential proxy DDoS traffic – responsible for 75% of attack volume and number of compromised endpoints in 2025. Residential proxies are everywhere, so why did proxy DDoS attacks mostly come from the U.S.? The answer is money. If you are committing fraud or circumventing content restrictions, a Russian IP address gets geo-blocked instantly. A fresh U.S. residential IP address (especially one behind carrier-grade NAT and harder to block individually) is “gold.” Customers pay up to $95 to lease a single U.S. residential IP address for 2 weeks (versus $0.30 for an Eastern European IP). Compare that to your own ARPU per subscriber and sit with it for a second. When an individual IP is worth more than the customer relationship behind it, you don’t have a technical problem. You have a *market* problem.


## The trick that solved the mystery


For months, we had a mystery: Why would a proxy operator allow the use of their residential endpoints in highly visible DDoS attacks (and risk losing that endpoint)? Historically, residential proxies were far more valuable for avoiding crawling restrictions or cybercrime than DDoS.


The answer, surfaced by outside researchers, was a surprising flaw in most residential proxy software: you could route a proxy request back to the exit node itself and gain unauthenticated Android Debug Bridge (ADB) shell. An attacker who bought proxy access could make each device scan and own itself. The person who industrialized this ADB flaw and built what became the largest botnet ever observed[has since been arrested](https://www.justice.gov/usao-ak/pr/canadian-man-arrested-international-authorities-charged-administrating-kimwolf-ddos) . But the bug remains unpatched across many proxy endpoints; the technique is public, and more than two dozen other groups are now exploiting the flaw.


*Resolving the residential proxy DDoS mystery: a suprising flaw: a proxy request to the proxy endpoint itself reaches the device’s unauthenticated ADB and enables third-party access and abuse of residential proxy infrastructure.*


## Did we win? Yes and no


By January 2026, we understood the attacks, the infrastructure, and the relationships well enough to act. Nokia joined a global collaboration of ISPs, cloud providers and law enforcement that resulted in action on March 19 against four of the largest DDoS botnets, including Kimwolf. That work is reflected in the[U.S. Department of Justice](https://www.justice.gov/usao-ak/pr/authorities-disrupt-worlds-largest-iot-ddos-botnets-responsible-record-breaking-attacks) takedown of the command-and-control infrastructure. Did it work? Yes and no. The U.S. share of residential proxy traffic dropped sharply and durably, but Brazil promptly replaced a significant portion of the disrupted U.S. residential proxy DDoS. Generally, the size of residential proxy networks remains unchanged – the disrupted proxy command-and-control servers migrated to other infrastructure and were back to pre-takedown levels within weeks.


*The IPIDEA disruption hit the U.S. hard: a sharp, durable decline in residential proxy traffic. Brazil and the rest of Latin America rose to fill the gap.*


## The hydra problem


Cutting off Kimwolf’s head produced a hydra as the threat metastasized into more than 20 smaller botnet families. These smaller residential proxy botnets generate the same or a greater number of daily DDoS attacks (up to 10,000). But the disruption did real damage. Kimwolf is no longer active, and the botnet families that have replaced it now compete fiercely for the same pool of vulnerable devices, so individual herds are smaller: median attack sizes have fallen from hundreds of thousands of nodes to roughly 20,000–30,000 nodes.


The largest issue is that the residential proxy problem is not going away. While some proxy providers patched the ADB bug, most of the compromised home endpoints remain compromised, with third-party attackers having installed their own backdoors. Nokia and other research groups continue to track new proxy networks, as seen in last week’s[Qurium press release](https://www.qurium.org/press-releases/qurium-traced-the-global-scraping-campaign-to-popa-a-residential-proxy-network-hidden-inside-consumer-devices/) .


In general, the number of proxy endpoints is growing rapidly, and (as discussed next) there remain multi-billion dollar incentives to add new proxy endpoints.


## Who’s funding this?


Why does the proxy endpoint population keep growing? Analysts estimated that the residential proxy market has grown from a sub-$100 million industry five years ago to a $2–$3 billion business today, driven largely by AI companies that need residential IPs to crawl and harvest training data while circumventing controls imposed by major content platforms. That investment funds the compromise of nodes inside your network.


And the telecom industry handed proxy DDoS a tailwind: the race to roll out symmetric gigabit (or multi-gigabit) connectivity to homes. Most ISP planners assumed that no home application would ever use a full gigabit of upstream bandwidth. They were *nearly right* . The one application that could and does use a full upstream is residential proxy DDoS. More endpoints, each with far more upstream. That’s the ground for a perfect (DDoS) storm.


## The war of two infrastructures


If you take just one thing from this, it’s this: residential proxy infrastructure now rivals the world’s largest transit and content networks in aggregate upstream capacity. Proxies are not a sidecar, but a significant new, long-term component of internet infrastructure.


**There is no panacea.** Long-term, we need policy changes, market disincentives, and consumer education to slow the inflow of cheap, pre-compromised hardware and mobile apps.


**But you can act today:** disrupt botnet C2 communication inside your own network. One of our customers recently deployed roughly 200 C2-filtering ACLs on a border router, blocking about a terabit of outbound malicious traffic. A Latin American ISP enabled C2 filtering for the first time on May 7 and saw an immediate, terabit-scale drop in outbound DDoS traffic.


*“Shield ON”: the moment a LATAM ISP enabled C2 filtering on its border routers, an immediate, terabit-scale drop in outbound DDoS.*


The devices stay infected but starved of commands, go quiet. We encourage network operators to participate in ongoing global efforts to disrupt residential botnets. Operators can use their own tools and threat intelligence shared within the global security community or deploy Nokia's recently announced Deepfield Genome Shield to disrupt proxy botnets within their own networks.


For the full story, watch the NANOG97 talk, delivered jointly by the Comcast Threat Research Lab (CTRL) and the Nokia Deepfield Emergency Response Team. The video[recording is available on YouTube](https://www.youtube.com/watch?v=eOmeQcwSK3o) , and the slides are[available on the NANOG97 website](https://nanog.org/events/nanog-97/content/5771/) .


For more information about how Nokia addresses the residential proxy problem, please visit our webpage on[Deepfield Genome Shield](https://www.nokia.com/ip-networks/deepfield/genome-shield/) . We[announced Genome Shield on June 9](https://www.nokia.com/newsroom/nokia-launches-deepfield-genome-shield-security-automation-system-to-deliver-proactive-network-wide-ddos-protection-for-the-ai-era/) .
