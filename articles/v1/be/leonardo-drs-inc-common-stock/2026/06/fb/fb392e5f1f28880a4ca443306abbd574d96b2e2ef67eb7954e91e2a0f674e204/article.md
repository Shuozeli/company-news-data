---
schema_version: "1.0.0"
document_id: "fb392e5f1f28880a4ca443306abbd574d96b2e2ef67eb7954e91e2a0f674e204"
company_key: "leonardo-drs-inc-common-stock"
company: "Leonardo DRS Inc. Common Stock"
source_id: "leonardo-drs-inc-common-stock-news-import-5f9388999390"
canonical_url: "https://www.leonardodrs.com/news/in-the-news/the-vehicle-is-the-computer-military-vetronics-enters-a-new-era/"
published_at: "2026-06-17T15:25:47+00:00"
first_seen_at: "2026-07-27T05:38:50.671866+00:00"
fetched_at: "2026-07-27T05:38:34.847150+00:00"
content_hash: "sha256:d8cadd38b1352b88dc37d37cbee653f0c69f91511da56a3fbf2558b29a80e5f7"
---

# The Vehicle is the Computer: Military Vetronics Enters a New Era

The Data Problem


**This shift happened over the years because the battlefield generates more data than any previous vetronics architecture was designed to handle.**


Today’s armored vehicles operate inside a sensor environment that previous generations couldn’t have imagined: Data is pouring in from optical and thermal sights, radar, acoustic detection, electronic warfare (EW) receivers, assured-PNT \[position, navigation, and timing\] inputs, and feeds from unmanned systems, all arriving simultaneously at the edge. In a contested environment, adversary jamming will target those very links at the worst possible moment.


“That data volume cannot be moved off-platform for processing in a contested environment and then moved back onto platform for instantaneous decisions; also this data cannot be handed to the crew in raw form without overwhelming them,” Niles says. “It has to be processed inside the vehicle, at the edge, in real time.”


This requirement has redefined vetronics. Where the discipline once centered on discrete subsystem controllers, it now encompasses the entire digital nervous system of the vehicle – sensor fusion, video distribution, vehicle survivability, artificial intelligence (AI) inference, networked communications, and crew/machine interfaces running concurrently, under armor, at temperatures and vibration levels that commercial data center designers don’t have to think about, he explains.


For these applications, Leonardo DRS engineers developed the[THOR](https://www.leonardodrs.com/what-we-do/products-and-services/thor-edge-computing/) chassis to help solve the problem of too many mission functions, too little space. Rather than fielding a separate box for AI processing, another for sensor fusion, another for electronic warfare, and another for communications, THOR is designed to host all of them in a single 3U VPX chassis built to military environmental standards. Internal data rates run as fast as 100 Gbps. The chassis is also aligned to the Sensor Open Systems Architecture, or SOSA, Technical Standard, meaning new processing cards and payloads can be swapped in as technology advances without redesigning the underlying infrastructure.


Describing the scope in similar terms, Jake Braegelmann, vice president of business development at New Wave Design (Eden Prairie, Minnesota), says: “Today’s vetronics environment includes EO/IR \[electro-optical/infrared\] sensing, sensor fusion, autonomy support, integrated moving maps, EW and communications coordination, assured-PNT functions, and countermeasure management.


“These capabilities are no longer isolated subsystems,” he says. “They are interconnected and increasingly expected to operate collaboratively across the platform and with external battle-management networks.”


The proliferation of unmanned systems adds still another layer. Uncrewed ground vehicles and aerial drones on the battlefield generate additional sensor data that has to be consumed and acted on in near-real time. The vehicle crew is no longer just managing what it can see from the hatch but is in fact managing a network.


Integration the Breaking Point


**When everything on the vehicle is connected, integration stops being a matter of plugging in boxes and starts being a systems architecture problem. The challenges compound in ways that aren’t linear.**


“Doubling the number of sensors does not double the architectural complexity, it multiplies it,” Niles says.


Every new capability draws power, generates heat, demands bandwidth, and competes for finite space inside an armored hull. The traditional answer – a dedicated box for each mission function – no longer scales; there are simply too many functions, and the vehicle can’t carry the weight, volume, or power draw that the old mission model demands.


Mark Littlefield, director of system products at Elma Electronic (Fremont, California), describes the change in design philosophy: “We’re shifting from a stovepipe solution model of systems to a multifunction platform model. Computing, networking, and communications resources are shared among various functions, meaning functions performed by the electronics shift, as needs evolve. No more bespoke systems shoved into a corner of the vehicle to do some specialized task – suppliers need to bring interoperability and flexibility to the platform or risk limiting their value.”


Braegelmann points to size, weight, and power (SWaP) as a constraint that has arrived in vetronics with a force previously felt mainly in airborne systems.


“The addition of more sensors, self-protection capabilities, counter-UAS \[uncrewed aerial system\], AI, directed-energy systems, and improved navigation and mobility capability has pushed weight and power demand into the modern ground vehicle fleet,” he says. “Smaller, lighter, and more power-efficient computing solutions are being sought to support the mission and continuously improve survivability.”


Open Architecture: from Policy to Engineering Reality


Because of these realities, open standards are becoming the order of the day. The U.S. Department of Defense (DoD) has made it clear that it expects the industry to focus on open architecture systems rather than on closed boxes. What’s changed is the pace at which that policy is translating into actual hardware – fielded systems, prototypes, and program offices standing up around CMOSS Mounted Form Factor (CMFF) and Next Generation Command and Control (NGC2).


For the defense industry, the significance of open architecture goes beyond compliance and has become the mechanism by which a vehicle’s electronics can keep pace with threats that evolve faster than any traditional acquisition cycle can accommodate.


“A vetronics system designed around proprietary interfaces is obsolete the moment it is fielded,” Niles says, “because every capability upgrade requires chassis redesign, software rework, and full system requalification – a process measured in years, a luxury that the force does not have.”


Standards like CMOSS, VICTORY, MORA, NGVA, and the SOSA Technical Standard change that equation by establishing common electrical, mechanical, and software interfaces that enable new processors, AI accelerators, and mission payloads to be inserted as they mature but without redesigning the chassis or rewriting the integration layer. Niles says the result is “a sustainment model in which the architecture absorbs emerging capability rather than aging against it.”


Littlefield uses an analogy that translates the concept for anyone who has ever upgraded a laptop: “Think of your laptop or desktop: Do you run a single application on each, or does each have many applications? You add or upgrade capabilities by adding peripherals or specialized hardware – USB devices, graphics cards – that get shared by the different applications you run. The same goes for vehicle electronic systems.”


Braegelmann points to concrete examples of what that flexibility looks like in practice. When threats evolve rapidly, a software-defined radio (SDR) in a shared mission processor can be swapped out to counter the risks far more quickly than a traditional integration cycle would allow.


“New software ‘skills’ can be quickly introduced via new 3U VPX processors into an existing computer chassis infrastructure,” he says. “These types of upgrades used to require a significant development and integration effort, which now can be turned in a much shorter timeline through industry-acknowledged slot profiles and other open system approaches at the module and chassis level in embedded computing.”


The Cybersecurity Challenge


**Open interfaces create cybersecurity challenges: That is, the more capable the vehicle’s digital architecture, the more consequential a successful intrusion becomes – and the more entry points an adversary has to try.**


“Every networked compute node on the vehicle is a potential attack surface; high-performance edge processing cannot come at the cost of platform vulnerability,” Niles says. “That requires cyber­security built into the architecture from the silicon up – secure boot, encrypted data paths, hardware roots of trust, and continuous monitoring – rather than added on at integration.”


Supply-chain assurance has emerged as its own parallel challenge. The commercial demand surge in AI compute power has created sustained pressure on the availability of advanced processors, accelerators, and memory – pressure that echoes the disruptions the industry experienced during the COVID-19-era semiconductor shortage.


“Lead times have extended and unit costs have risen,” Niles acknowledges. “Responsible vetronics suppliers are responding with deeper supplier qualification, strategic inventory positioning, multi-source design where the architecture allows, and contract structures that protect program schedules against component-level volatility.”


Littlefield frames the cybersecurity and supply-chain challenge as fundamentally perpetual. “We want and need an open market with many suppliers, so that there’s a constant pace of innovation and robust competition to keep prices reasonable,” he says. “But the sensitive nature of cybersecurity and the relentless problem of securing the supply chain means that suppliers always have to be on top of their game and provide the integration community with the best tools and assurance that their supply chain is sound.


“It’s not an ‘OK, I’ve developed that, now I can move on to other things’ – it’s perpetual”


Power and Thermal Constraints


**No matter how capable a new sensor or AI accelerator might be, it won’t reach the field if it can’t fit within the vehicle’s power budget and thermal envelope. SWaP constraints have always been a challenge in airborne systems – now they are arriving in ground-vehicle programs with comparable force.**


“Performance that cannot fit in the vehi-cle is not performance – and processing capacity that the crew cannot exploit is not capability,” Niles says.


The SWaP arithmetic is unforgiving: Every additional sensor, every new networked feed, every step up in AI inference demands more power and generates more heat. Armored vehicles have fixed power budgets, finite cooling capacity, confined crew compartments, and no tolerance for additional weight that compromises mobility or survivability. Nile says the answer is not less capability, but rather capability that solves the SWaP problem at the architecture level, before the hardware goes in.


Littlefield notes that the emergence of robust standards-based, out-of-band system management is helping address power and thermal challenges in ways that weren’t previously available. “Like cybersecurity, system management is not a central part of the mission, but it helps to keep the electronics healthy and a part of the fight, and is thus critical to the success of the platform and system,” he says.


The platforms that will succeed operationally, Niles asserts, will be those that consolidate multiple mission functions into a single compute chassis, design for power efficiency from the silicon up, and push AI-enabled automation as the mechanism that turns raw sensor volume into a manageable operational picture.


What’s Coming


The Army’s CMFF program became a formal acquisition effort in 2025, with rapid-­prototype OTAs awarded to General Dynamics Mission Systems and Pacific Defense. The NGC2 program office stood up the same year, followed by a major prototype Other Transactional Authority (OTA) to Team Anduril, creating what the Army describes as an ecosystem for transport, infrastructure, data, and applications. MAPS Gen II received its full-rate production decision in March 2025 and was already fielding by September of that year. The M1E3 Abrams battle tank – justified in part as an upgradable digital platform built around open architecture and government-owned technical data – unveiled its first early prototype in early 2026.


For suppliers, the message from these programs is consistent: The Army is buying architecture, not just bolting on boxes. The chassis is preplumbed and its interfaces are defined, while the capabilities arrive on cards and in software updates. What the Army is purchasing, increasingly, is the ability to insert new capabilities quickly – and the vetronics suppliers best positioned for the future are the ones that have internalized that logic at every level of their design.


“The transition from a platform-centric model to a data-centric and network-centric operational approach requires more computing at the edge,” Braegelmann says.


The vehicle’s electronics are no longer supporting the fight but are – in a real sense – central to the fight.
