---
schema_version: "1.0.0"
document_id: "cb7eb173db6958baf2795a260aa9eaacee7d4b07d9640c3154b9c0f0edd07c31"
company_key: "qorvo-inc-common-stock"
company: "Qorvo Inc. Common Stock"
source_id: "qorvo-inc-common-stock-news-import-e3018e454ae6"
canonical_url: "https://www.qorvo.com/design-hub/blog/smarter-power-for-smarter-doorbells-enabling-the-next-wave-of-home-security"
published_at: "2026-03-19T00:00:00+00:00"
first_seen_at: "2026-07-24T13:14:16.870814+00:00"
fetched_at: "2026-07-28T22:00:18.082649+00:00"
content_hash: "sha256:4533a834b491deb4f2756545353d7d885d723a0d8465d2c6f65fc6585084e199"
---

# Smarter Power for Smarter Doorbells: Enabling the Next Wave of Home Security

Porch pirates stole over USD $12 billion in packages from more than 58 million Americans last year. Home security is no longer an item of luxury but a necessity in this era of smart homes, of which the centerpiece is the doorbell camera.[According to Grand View Research](https://www.grandviewresearch.com/industry-analysis/doorbell-camera-market) , the U.S. doorbell camera market was estimated to be USD $418 million in 2023 and is projected to reach USD $1048 million by 2030. Continued innovation of the doorbell camera is vital to providing convenient, accessible home security to consumers.


Seventy-eight percent of consumers report that convenience is their biggest motivator when purchasing smart home technology. Installation time and ease have the most immediate impact on convenience and must seek to be non-intrusive i.e. renter friendly. More demanding peripherals and increased thermal loads have put severe strain on battery performance, so modern power management integrated circuits (PMIC) in video doorbells must include fault protections and monitoring to allow the user to perform timely preventative maintenance.


Lastly, under- or oversensitive motion detection will make or break a video doorbell’s performance. False alerts from passing vehicles or wild animals must be filtered out to not distract the user from actual security alerts—this is also predicated on seamless connectivity to a user’s mobile device. The doorbell camera thus presents unique engineering design challenges: how can one fit a camera, processor, Wi-Fi module, audio, sensors and memory all within a palm-size enclosure that may run on batteries, must endure potentially harsh temperatures and remain “always on”? PMICs adequately address these evolving demands of video doorbell devices.


### Key Features of the Modern Doorbell Camera


The basic video doorbell operates in three key modes: always-on standby monitoring, event-triggered recording and real-time two-way audio communication. This requires several voltage rails for all the peripherals; the supply must remain stable for always-on functions and for peak loads during video recording and two-way audio. Most video doorbells are powered with a 12VAC or 24VAC line directly from the home electrical system, via battery or via a combination of both. Battery-powered and wireless systems now account for over 55% of the market, mainly because they’re renter friendly and easier to install. In tandem with higher thermal and processing loads because of the incorporation of AI, the need for more efficient power solutions is vital.


Video processing has undergone the most consistent innovation in recent years. Machine vision has robustly improved the consumer experience by reducing false or redundant alerts. Competitive products can now identify individuals with facial recognition, distinguish pets from wild animals, track when packages are delivered and removed from the doorstep and recognize vehicles and delivery trucks. Improved motion detection is enabled by technology such as mmWave radar, ambient light, ultrasonic and infrared sensors. Improvements to audio capture and communication also necessitate more peripherals. For consumers in noisier environments such as urban or metropolitan areas, audio-direction sensing requires more microphones to improve noise cancellation.


Event-triggered video capture presents a key power requirement: the PMIC must be able to provide a stable supply in light load conditions and then curb operational transients once the event is triggered. It is worth noting here that multiphase power solutions are advantageous because they significantly reduce transients and ripple by interleaving the switching phases and they have better thermal performance. Event-triggered actions also call for lower quiescent current ratings for both peripherals and their control system to maximize battery life. Many modern PMICs have low power modes (LPM) to target quiescent currents of less than 50µA.


As previously mentioned, doorbell cameras must contend with potentially harsh environmental conditions from scorching heat to extreme colds; this is particularly relevant because Canada is projected to be the next-fastest-growing regional market. As such, PMIC and processor control architectures have adopted better fault protection and monitoring to prolong device usage. Seamless integration with mobile applications allows for a user to continuously track the health of their device—essentially remote diagnostics and maintenance as it relates to thermal performance, battery issues, anti-theft protection, etc.


The last and perhaps most constraining power requirement for doorbell cameras is the small form factor. The PMIC cannot become a size-limiting factor of the peripherals it’s meant to power, not to mention the thermal shielding and thermal management the power solution may require for itself. Space inside the enclosure is as precious as the packages the doorbell camera is meant to protect.


Advancements in cloud computing have opened up some space in the doorbell enclosure because some processing and much of the data collection and storage can be offloaded and viewed directly on one’s mobile device. Additionally, the ability to perform over-the-air updates eliminates the need to disassemble or replace the doorbell camera. However, this does require consistent internet access, be it Ethernet or Wi-Fi. The placement of routers in most homes is not idealized to the front door space, so Wi-Fi modules must operate with good receiver sensitivity and low-phase noise. Since Ethernet lines are not commonly placed in doorways, wireless doorbell cameras must be able to operate efficiently and securely in areas with poor reception.


Qorvo’s newly released ACT88760 can help design engineers attain the efficiency, reliability and connectivity needed in today’s doorbell camera products.


### About the ACT88760


Qorvo is excited to introduce the[ACT88760](https://www.qorvo.com/products/p/ACT88760) , a next-generation, highly integrated PMIC designed to meet the evolving demands of video doorbell devices and other space-constrained IoT devices, further enabling more integrated, smarter homes. Below is the block diagram followed by its key features:


The ACT88760 delivers comprehensive rail support with 13 total configurable outputs designed to support the major peripherals of a modern doorbell camera or similar IoT device. It includes seven high-efficiency buck converters—three rated at 4 A, two at 3 A and two at 2 A—providing robust support for high-current components like AI processors and wireless modules. These are joined by six low dropout regulators (LDOs), including two high-PSRR 800 mA LDOs ideal for noise-sensitive analog and RF circuits and four general-purpose 400mA LDOs. Two of the LDOs can be reconfigured as 1.2 A load switches (LSWs) with low RDS(on), making them versatile enough for switching auxiliary loads. This comprehensive rail support allows designers to eliminate the need for multiple discrete regulators, significantly simplifying board layout and conserving valuable PCB real estate.


The ACT88760 also excels in power efficiency and scalability, particularly for designs where battery life and thermal management are critical. The 4 A and 3 A buck converters can be paralleled to support total output currents of up to 8 A and 6 A, respectively—ideal for components with burst-mode or high-load activity such as event-triggered video processors or microphone arrays with directional sensing. With a quiescent current as low as 10 µA in low-power mode, the device helps extend battery life in standby and monitoring states, while the high PSRR of its LDOs ensures clean, ripple-free supply voltages for sensitive analog blocks.


For seamless integration into increasingly intelligent and connected systems, the ACT88760 offers advanced telemetry features. An I²C interface enables real-time voltage configuration, sequencing and system monitoring. Eleven multifunction GPIOs provide system-level signaling and control for a variety of use cases, including interrupt requests, power-good indications, wake/sleep transitions, dynamic voltage scaling (DVS) and LED driver control. Built-in programmable sequencing logic ensures peripherals power up in a controlled fashion, preventing inrush currents that could otherwise damage sensitive components.


The device includes robust fault protection mechanisms across all power rails. These include over-voltage, over-current and short-circuit protections, as well as thermal shutdown and early warning features to ensure safe operation under extreme temperature swings. Integrated diagnostic and fault reporting functionality also allows for remote health monitoring and predictive maintenance, helping reduce field failures and extending device lifespan.


Despite its rich feature set, the ACT88760 is packaged in an ultra-compact 3.78 mm x 3.78 mm WLCSP, making it one of the smallest 13-rail PMICs with this level of integration. Minimal external component requirements further reduce the bill of materials (BoM) and simplify overall layout to help speed up the time-to-market. In comparing a discrete versus an integrated solution, the ACT88760 reduces board space by at least 60%. In sum, the ACT88760 is an ideal choice for highly integrated, space-constrained designs like next-generation video doorbells.


### Conclusion


Doorbell cameras have evolved from simple motion detectors into AI-powered, cloud-connected security hubs. These devices must fit more and more features into ultra-compact enclosures without compromising on performance, requiring more integrated and power dense PMICs. Power architectures must contain several voltage rails to satisfy the diverse needs of several peripherals such as cameras, machine vision processors, wireless modules, microphones and several types of internal and environmental sensors. Thermal management must not only account for potentially harsh environmental conditions but also be robust enough to handle the bursts of high current for event-triggered functions. Always-on connectivity and AI processing loads demand better power efficiency and low quiescent current to minimize recharge cycles and extend operational life. Any modern PMIC used in doorbell cameras must holistically address all these challenges—and that’s exactly what the ACT88760 delivers.


As the demands and processing loads of peripherals increase, so too must the capacity of power solutions for IoT devices. Qorvo’s new ACT88911 PMIC is poised to meet the needs of more power-hungry applications—it’s equipped with 19 total rails: 5 bucks, 2 buck-boosts, 2 boosts and 10 LDO/LSWs. See Smarter Power for Smarter Vision: Powering SoCs and AI Processors for more details on the power architecture and features of the ACT88911.


### Learn More


Visit[qorvo.com](https://www.qorvo.com/) to explore the[ACT88760](https://www.qorvo.com/products/p/ACT88760) or[ACT88911](https://www.qorvo.com/products/p/ACT88911) product pages and request samples or access technical resources for your next design.


**About the Authors**


Our authors bring a wealth of technical expertise in developing and optimizing power solutions. With a deep understanding of customer needs and industry trends, they collaborate closely with our design teams to drive innovation and deliver cutting-edge solutions that support industry-leading products.


Thank you to our main contributors of this article; Jon Alejandro (Analog Products Marketing Manager), David Schnaufer (Corporate, Technical Marketing Manager) and Michael Day (Sr. Manager Applications Engineering) for their contributions to this blog post, ensuring our readers stay informed with expert knowledge and industry trends.
