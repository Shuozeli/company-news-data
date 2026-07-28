---
schema_version: "1.0.0"
document_id: "85c602edda5ff42d29424081c64e68247630fed890eb7a3100446f8a805e4e5b"
company_key: "synaptics-incorporated-common-stock-0-001-par-value"
company: "Synaptics Incorporated Common Stock $0.001 Par Value"
source_id: "synaptics-incorporated-common-stock-0-001-par-value-news-import-67901354d8df"
canonical_url: "https://www.synaptics.com/company/blog/synaptics-enables-real-time-connected-edge-intelligence-with-industrys-first-wi-fi-7-ai-mcu-syn765x-series"
published_at: "2025-01-31T00:00:00+00:00"
first_seen_at: "2026-07-26T02:29:20.825354+00:00"
fetched_at: "2026-07-28T21:32:04.842955+00:00"
content_hash: "sha256:f62e2c54aad25437716d0006b928a107d866e3ef12510e8c9758277bb28eaee1"
---

# Synaptics Enables Real-time Connected Edge Intelligence With Industry’s First Wi-Fi® 7 AI MCU SYN765x Series

[Home](https://www.synaptics.com/) /[Company](https://www.synaptics.com/company/overview) /[Blog](https://www.synaptics.com/company/blog) / Synaptics Enables Real-time Connected Edge Intelligence With Industry’s First Wi-Fi® 7 AI MCU SYN765x Series


# Synaptics Enables Real-time Connected Edge Intelligence With Industry’s First Wi-Fi® 7 AI MCU SYN765x Series


March 10, 2026[Mohit Agrawal Global Practice Head for Edge AI and IoT, Counterpoint Research](https://www.synaptics.com/company/blog?author=Mohit%20Agrawal) Share this article


### Intelligence Evolution from Cloud to Connected Edge


Over the past decade, most Internet of Things (IoT) devices focused on collecting data from sensors and devices at the Edge and then transferring it to the cloud for processing and analysis. This approach worked well when we were tracking the temperature or basic sensor logs, but this ‘send and wait’ model is hitting a wall.


We are moving into an era where ‘split-second’ is no longer a buzzword, but is a critical requirement. This shift toward local inference (processing and deciding right where the data is generated) is a game changer, but it is only half the battle. The device might have world-class on-chip AI acceleration, but if the wireless pipe is clogged or laggy, the system falls apart. True intelligence at the Edge requires a perfect marriage between local ‘brains’ and high-speed, low-latency connectivity.


That is why the integration of AI acceleration and[Wi-Fi 7](https://www.synaptics.com/products/wireless/wi-fi-7) on a single low-power platform is such a massive leap in AIoT design systems. By combining intelligence and connectivity at the hardware level, devices can respond instantly to changing conditions and share critical information quickly and reliably.


Consider how security cameras have evolved. Traditionally, cameras streamed video to a remote server 24/7 for processing and storage, placing intelligence primarily in the cloud. A unified AI-native MCU shifts inference to the device, enabling it to identify relevant faces or motion events locally, trigger alerts instantly, and limit cloud communication to meaningful activity. The result is a more responsive, bandwidth-efficient implementation of connected intelligence at the Edge.


### Introducing Synaptics SYN765x Series: Integrating AI MCU + Wi-Fi 7


At Embedded World 2026, Synaptics launched the world’s first Wi-Fi 7 AI-native MCU designed to run AI workloads natively. Powered by an Arm® Cortex®-M52 processor with Helium DSP and an Arm U55 NPU, the system delivers up to 50 GOPS at 200 MHz compute capability.


The[SYN765x](https://www.synaptics.com/assets/product-brief/syn765x-ai-native-connected-compute-soc) offers a broad range of connectivity options, including Wi-Fi 7 connectivity designed to support evolving network requirements, Bluetooth® 6.0 with channel sounding, and IEEE 802.15.4 (Thread and Zigbee) with Matter support for interoperability. The inclusion of Wi-Fi 7 ensures ultra-fast connectivity for smart home devices, while Matter support guarantees seamless interoperability across platforms.


The SYN765x can be used in a wide variety of devices, including smart appliances (such as dishwashers and vacuum robots), smart home devices (such as thermostats and security cameras), and industrial IoT applications (such as smart metering and EV charging front-end systems).


### Making Edge Intelligence and Wi-Fi 7 Accessible


We are reaching a tipping point where ‘instant’ has to mean instant. Whether in an EV charging station or smart security camera, reliance on cloud processing may create latency constraints in time-sensitive applications.


That is where an AI-native MCU comes in. Instead of clogging up bandwidth by shipping raw data to a remote server, these chips handle the heavy lifting (inference) right on the device, reducing delays, saving network bandwidth, and keeping sensitive data private.


When paired with Wi-Fi 7 connectivity, particularly in a 1x1 architecture, a balance between performance and power efficiency can be achieved. While this configuration prioritizes efficiency rather than maximum speed, by utilizing the 6 GHz band and Wi-Fi 7’s smarter channel management, we get a rock-solid connection that does not eat into the power budget or require a massive antenna array.


### Why the SYN765x Matters: Real-world Edge Intelligence


Most ‘smart’ homes are not really smart but are reactive. Synaptics SYN765x moves the system’s ‘brain’ to the Edge. Let us examine the key features of SYN765x from the lens of smart homes.


#### Wi-Fi Sensing for Smart Homes and More


The creep factor of indoor security cameras is real. Wi-Fi sensing offers a different approach by analyzing subtle changes in wireless signal reflections within a room to detect motion, presence, or environmental changes.


Imagine early in the morning when it is time to wake up; the kitchen comes alive without anyone touching a switch. The smart speaker in the living room detects the movement of the dog heading toward the door and gently cues soft music. The thermostat senses that someone is moving through the hallway and subtly adjusts the temperature to comfort the person walking in.


At night, a pair of Wi-Fi 7-enabled security cameras in the study and backyard track movement, not by streaming constant video but by sensing changes in the wireless signals bouncing around the rooms. In the middle of the night, when a teenager is trying to find his way down to the kitchen for midnight cravings, the devices quietly communicate with each other, turning on just enough light in the path and logging presence without recording faces.


Wi-Fi sensing can also be used for critical safety applications such as fall detection, which is one of the most significant use cases that can potentially alert caregivers or emergency services. This can be expanded into multiple scenarios from pre-fall detection, fall severity assessment, fall recovery monitoring, false alarm filtering, and instant alerts.


Another home use case is where each device, from the speaker to the camera to the smart display, works together over Wi-Fi 7, coordinating local intelligence with minimal latency, making the home feel aware, responsive, and safe. It is total privacy with no video feeds hitting the cloud, just raw signal data being processed locally.


#### Bluetooth Channel Sounding


Traditional Bluetooth ‘proximity’ is a guessing game based on signal strength, but Channel Sounding is different. It measures the Bluetooth signal to calculate distance with centimeter-level accuracy.


We have often misplaced the TV remote and searched through couch cushions trying to find it. In an MCU-based remote control design with Bluetooth Channel Sounding, a companion mobile app can trigger the remote to measure signal reflections and estimate its precise location within the room. The Synaptics MCU effectively transforms a conventional remote into a precision-tracked device.


#### Voice Commands: Sound Event Detection


The biggest hurdle for smart thermostats is not the HVAC control, but the ‘always-on’ microphone. Most people do not want a device streaming their private living room conversations to a server. The SYN765x addresses this concern by keeping the ‘ears’ local.


Consider the scenario of arriving home on a cold evening and simply saying, "Set the living room to 22°C,” and it happens instantly. There is no three-second processing lag because inference runs directly on the chip, not in a distant data center.


Beyond voice commands, the system is also trained to recognize unusual sounds such as window breaks or a baby’s cry. Distinguishing them from everyday background noise, the thermostat flags it immediately. Because this is Edge inference, the audio never leaves the four walls of the house, keeping privacy intact.


Furthermore, the real magic of Wi-Fi 7 is not just about raw speed but also concurrency. We are adding cameras, smart fridges, and wearables to our networks every day. Eventually, the airwaves get crowded, leading to congestion. Wi-Fi 7 is designed to manage that chaos, making sure the Wi-Fi remains responsive, leveraging newer capabilities such as Multi-Link Operation (MLO), better implementation of upgraded OFDMA technology and more.


#### Other Practical Applications Across Industries


- **EV Charging Stations:** Currently, many chargers rely heavily on cloud connectivity for power management and payment processing. With Edge intelligence, the station can manage load balancing and process transactions locally, maintaining operation even during temporary cloud interruptions.
- **Smart Home Security:** False motion alerts are a common frustration, often triggered by pets or moving tree branches. With an AI-native MCU, cameras can perform local inference to distinguish meaningful activity from background motion. The result is fewer unnecessary notifications and video data that does not need to be continuously transmitted to the cloud.
- **Healthcare Wearables:** If a heart monitor must rely on a round-trip to a server to detect an arrhythmia, the added delay can be critical. Local inference enables these devices to identify irregular patterns in real time and alert medical professionals within milliseconds, while keeping sensitive health data encrypted on device.
- **Industrial Automation and Physical AI:** In high-speed production environments, even minor latency can disrupt operations or damage equipment. Sensors with built-in AI can detect early signs of motor failure or production defects and respond immediately, without waiting for instructions from a remote system.


Overall, Wi-Fi 7 adoption is still in its early stages, particularly for access points or gateways. However, according to Counterpoint Research’s recent Broadband360 research report, Wi-Fi 7 is predicted to be the standard for over half of all new routers shipped by 2030. For OEMs designing hardware today with an 8- to 10-year lifecycle, long-term connectivity alignment is becoming an increasingly important consideration.


### The Bottom Line


For years, on-device AI and connectivity have been treated as separate design challenges. However, at the Edge, they are inherently linked. Integrating Wi-Fi 7 and AI acceleration into a single, cohesive MCU platform will finally move us past the clunky, fragmented architectures of the past decade.


The result is not just a spec-sheet upgrade, but hardware designed for real-time responsiveness and secure operation, bringing connected Edge intelligence closer to practical, scalable deployment.


#### Mohit Agrawal


Mohit Agrawal is the Global Practice Head for Edge AI and IoT at Counterpoint Research, leading research on AI silicon, embedded edge intelligence, and IoT connectivity. He has over 25 years of experience across Accenture, PwC, Nokia & Microsoft and previously co-founded a big data and AI-driven market intelligence startup. He is based in the Netherlands.


[Read more by Mohit Agrawal](https://www.synaptics.com/company/blog?author=Mohit%20Agrawal)


[AI](https://www.synaptics.com/company/blog?category=AI)[Edge Computing](https://www.synaptics.com/company/blog?category=Edge%20Computing)[Wireless](https://www.synaptics.com/company/blog?category=Wireless)
