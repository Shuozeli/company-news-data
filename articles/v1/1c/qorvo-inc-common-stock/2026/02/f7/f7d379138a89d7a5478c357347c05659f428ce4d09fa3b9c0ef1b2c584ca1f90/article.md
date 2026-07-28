---
schema_version: "1.0.0"
document_id: "f7d379138a89d7a5478c357347c05659f428ce4d09fa3b9c0ef1b2c584ca1f90"
company_key: "qorvo-inc-common-stock"
company: "Qorvo Inc. Common Stock"
source_id: "qorvo-inc-common-stock-news-import-e3018e454ae6"
canonical_url: "https://www.qorvo.com/design-hub/blog/lessons-learned-from-a-used-lawnmower"
published_at: "2026-02-19T00:00:00+00:00"
first_seen_at: "2026-07-24T13:14:16.870814+00:00"
fetched_at: "2026-07-28T22:19:38.682305+00:00"
content_hash: "sha256:fcf112d997d82adfe043f10e4977f82eb4fe6ec70b1bce5ebc87fa5b31daf523"
---

# Lessons Learned from a Used Lawnmower

I was in the market for a battery powered lawnmower when I saw one at a yard sale. “It has only been used twice,” the seller said, as I noticed another one just like it. It was half the price of a new one, so I bought it and happily pushed it to my house. It worked great: quiet, plenty of power, neatly cut grass. After mowing the lawn, I popped out the battery and slid it into the charger, which flashed a red light and refused to charge it. “Now I know why it was for sale. It was dumb of me to risk buying it,” I thought to myself.


At this point, I faced a decision: I could buy a new battery, but what if it is also defective? Then I would spend almost as much as for a new lawnmower, but I would have no warranty. I disliked the thought of going back to gasoline power, especially after experiencing the quietness and convenience of a battery powered lawnmower. No, I would not go back. I chose another alternative.


I have been working with power electronics for many years, so I felt confident enough to disassemble the battery case and slide out the neatly bundled lithium-based cells. Using my multimeter, I quickly discovered that one cell had lower voltage than all the other cells. “How could this be?” I wondered. “This battery is practically new.” I thought perhaps this cell was defective, and the battery pack was junk. With nothing to lose, I connected my programmable power supply across the weak cell and carefully, slowly charged it to the same voltages as the other cells. (Remember, I have many years of experience working with high power, high voltage power converters, so I am accustomed to this sort of task. Please, do not attempt to work on lithium-based battery packs if you lack the expertise and the equipment.)


After reassembling the battery, the charger accepted it and recharged it. After uneventfully mowing the lawn, I disassembled the battery again to see if there was a persistently weak cell. To my surprise, all cells had nearly identical voltages. I repeated this process a few times with the same result. The battery is fine, and there are no weak cells. “Gee, am I smart for buying that lawnmower!” I thought, followed by “There must be no cell balancing by the battery management system. If the manufacturer were to use a Qorvo BMS, its battery warranty return rate would probably drop like a rock.”


Here is how it works. Each PAC2xxxx BMS can balance cell voltages by alternately partially discharging energy in higher voltage cells, with heat dissipated in power transistors and resistors. This is a very simple, cost-effective approach, even if not the most technically sophisticated.


Figure 1. Portion of a PAC2xxxx cell balancing circuit with external transistors and load resistors


Internal 25 Ω MOSFETs support up to 50 mA, limited by internal heating. However, outdoor tools usually require higher balance current, so the internal MOSFETs control external transistors allowing much higher current through the load resistors. This partially discharges a higher voltage cell, which could be anywhere in the battery pack. Typically, there are multiple cells with higher voltage, as was the situation with my battery. The PAC2xxxx BMS then alternates from cell to cell, taking a nibble of energy from each until the cell voltages are closely balanced. This balancing process usually happens while recharging the battery, although the PAC2xxxx can be programmed to balance cells anytime.


Of course, the PAC2xxxx family of battery management systems do much more than balance cell voltages. Each PAC2xxxx BMS is highly integrated and performs the following functions:


- Precisely measures all cell voltages and current
- Measures temperatures
- Automatically interrupts battery current in emergency conditions
-


Battery disconnect when not in use
- Includes power management for all internal circuitry


Balancing cell voltages requires highly precise voltage measurements, and for this reason, each PAC2xxxx BMS includes a 16-bit analog-to-digital converter (ADC) dedicated to cell voltage measurement and safety checks. Battery current measurement also requires high precision to enable Coulomb counting for battery gauge and service life calculations. A second 16-bit ADC driven by a precision, programmable gain differential amplifier serves this purpose.


Figure 2. Portion of a PAC2xxxx showing battery disconnect/breaker MOSFETs and internal drivers, and self control fuse driver


Each PAC2xxxx includes extensive protection features. For example, integrated within each PAC2xxxx are protection circuitry and drivers for external MOSFETs, working together to function as battery disconnect and circuit breaker. Two MOSFETs can separately block current in either direction, automatically interrupt any fault current, and disconnect the battery from the power terminals when not in use. These can be[connected to the charger and load separately](https://www.qorvo.com/products/d/da009026) to economize the charger-blocking MOSFET. A third MOSFET can optionally activate a self control fuse.


Finally, power management is very simple. An integrated high-voltage buck converter requires only an inductor, diode and a couple capacitors. Recommended components are listed in the[datasheet](https://www.qorvo.com/products/d/da009151) or[evaluation kit](https://www.qorvo.com/products/d/da008617) .


Figure 3.PAC2xxxx power management buck converter with bootstrap gate driver supply


In summary, this real-life tale about salvaging a defective lawnmower battery illustrates the importance of effective battery management systems. Imbalance in lithium-based cells can lead to extremely short service life of an otherwise serviceable battery. Qorvo’s PAC2xxxx BMS family addresses this with cell balancing, precise voltage and current measurements, and integrated protection features, resulting in robust solutions for outdoor power equipment with maximum run-time and service life.


More information is available in the following application notes:


[Application Note: PAC2xxxx External Cell Balancing](https://www.qorvo.com/products/d/da009029)


[Outdoor Power Equipment Design Guide](https://www.qorvo.com/products/d/da009838)


[PAC Battery Management System Guide](https://www.qorvo.com/products/d/da009836)


About the Author


Jonathan Dodge, P.E. is a technical contributor for Qorvo. He has mowed around the barn many times, working with several types of power converters ranging in power output from 1.5 to 500 kW, and almost every type of power transistor. Recently, he developed online calculator and simulator tools for switch-mode and circuit breaker applications. He received BSEE and MSEE degrees from Oregon State University and The University of Idaho respectively. He is a licensed professional engineer in the state of Oregon.
