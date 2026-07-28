---
schema_version: "1.0.0"
document_id: "2fbe9b848579a22e7dfa003530c50e24d2b274b75ffdd6af4dcdc681952b9326"
company_key: "nokia-corporation-sponsored-american-depositary-shares"
company: "Nokia Corporation Sponsored American Depositary Shares"
source_id: "nokia-corporation-sponsored-american-depositary-shares-news-import-bb650893ccf7"
canonical_url: "https://www.nokia.com/blog/how-optical-line-systems-are-evolving-for-the-ai-era-near-term-innovations/"
published_at: "2026-07-21T00:00:00+00:00"
first_seen_at: "2026-07-25T17:04:49.665774+00:00"
fetched_at: "2026-07-27T20:24:08.774797+00:00"
content_hash: "sha256:9317f303cf236169412dbbc3b610d5f91ddaa1d3f881a848341fcca7ee037e69"
---

# How optical line systems are evolving for the AI era: near-term innovations

Multiple factors are driving[optical line system (OLS) evolution](https://www.nokia.com/asset/215480/) :


> - Traffic growth is accelerating, amplified by[AI infrastructure buildouts](https://www.nokia.com/optical-networks/ai/) .
> - Spectral efficiency gains are increasingly incrementally as we approach the[Shannon](https://www.nokia.com/bell-labs/claude-shannon/) limit.
> - Coherent optical engines are evolving with[higher baud rates and pluggable form factors](https://www.nokia.com/blog/key-technology-trends-at-ecoc-2025/) .
> - Higher baud rates mean fewer wavelengths per band and per fiber.
> - Space and power constraints are becoming more critical.
> - Several large AI and cloud providers are adopting point-to-point long-haul architectures.
> - Applications and customer requirements are diversifying.


This is the first blog in a two-part series, looking at how these factors are driving[OLS evolution](https://www.nokia.com/asset/215480/) in the short-to-medium term. Part 2 will examine the longer-term outlook.


## Enhanced performance


As embedded coherent optical engines approach the[Shannon](https://www.nokia.com/bell-labs/claude-shannon/) limit, OLS have introduced multiple performance enhancements to best use the existing spectrum. Erbium-doped fiber amplifiers (EDFAs) have been developed with lower noise, especially at longer span losses/higher gains. In-line amplifiers (ILAs) have integrated dynamic gain equalizers (DGEs). Link-control algorithms that optimize wavelength power levels and amplifier gains have been enhanced to more optimally trade-off OSNR and nonlinear penalties on a per-wavelength basis.


## More spectrum: C+L, Super C, Super L


With spectral efficiency gains becoming more incremental, OLS have advanced to increase fiber capacity by expanding the available spectrum. This option is especially attractive when fiber availability is constrained and the cost of new fibers is prohibitive. Beyond the 4.8 THz of the extended C-band, the most widely deployed option is to light the[L-band](https://www.nokia.com/asset/210107/) , giving a total of 9.6 THz. A second option is[Super C](https://www.nokia.com/optical-networks/1830-global-express/) , which expands the C-band from 4.8 THz to 6.1 THz. This can increase capacity without the full cost (typically >2x) and complexity (e.g., SRS tilt) of C+L. It also offers a path to 11.6 THz with the addition of Super-L. Figure 1 illustrates the expansion of available spectrum.


*Figure 1 – Increased spectrum with L, Super C and Super L*


## Multi-rail


While these additional spectrum options can more than double fiber capacity, leading AI and cloud providers are demanding much greater scalability to meet AI-related capacity requirements. In response, OLS vendors such as Nokia are introducing[multi-rail in-line amplifiers (ILAs)](https://www.nokia.com/blog/when-ai-meets-line-systems-scaling-faster-with-multi-rail-ols/) that support bidirectional amplification for multiple fiber pairs in a single ~1RU card. Cost, power and footprint gains come from sharing components such as the optical channel monitor (OCM), optical supervisory channel (OSC) and dynamic gain equalizer (DGE), as well as from using low-power uncooled and/or multi-chip pump lasers. For example, the multi-rail ILA Nokia[announced at OFC 2026](https://www.nokia.com/newsroom/nokia-launches-suite-of-applicationoptimized-optical-solutions-for-ai-era-networks/) enables up to 160 C+L ILAs in a 40 RU (600 mm depth) rack with 4 ILAs per RU. This compares to current ILA technology, which typically requires 8 RU (300 mm depth) for four C+L ILAs. At the same time, power consumption per ILA is reduced by more than 60%.


## Direct-attach and low-port-count CDC


As baud rates increase and the number of wavelengths per fiber decreases, new ROADM add/drop architectures become attractive. For example, low-port-count[colorless directionless, contentionless (CDC)](https://www.nokia.com/asset/210819/) architectures that use unamplified multicast switch technology can provide a cost-effective option (Figure 2). Another newly attractive option is colorless direct attach, where the transponder is directly attached to the ROADM wavelength selective switch (WSS) port without an intermediate add/drop layer.


*Figure 2 – Low-port-count CDC examples*


## Reduced footprint


OLS footprint is reducing as key ROADM components, including WSSs and amplifiers, shrink and as functions such as OSC and optical time-domain reflectometry (OTDR) become available as compact pluggables. For example, around 2010, long-haul ROADMs typically required around 6 RU per degree, compared to 3 RU for metro ROADMs. Modern compact modular platforms can deliver two ROADM degrees in 1 RU. Another great example of footprint evolution is the[Nokia 1830 GX RD66](https://www.nokia.com/asset/214971/) (Figure 3), which provides C and L EDFA pre-amplifiers, C and L EDFA booster amplifiers, a twin C+L 1x66 WSS, integrated amplified spontaneous emission (ASE) noise, OSC, OCM and OTDR, all in the 2 RU 1830 GX G32E shelf, with two additional spare slots that could be used for Raman amplifiers or transponders.


*Figure 3 – Nokia 1830 GX RD66 with 66 C+L flexible grid, colorless direct-attach ports*


## Extended temperature range


Another vector for OLS evolution is extended temperature range (ETR), which has a number of benefits and applications. As OLS are increasingly deployed in metro access networks, including non-air-conditioned street cabinets, ETR is required to ensure reliable operation. A second application for ETR is reducing environmental controls in the ILA huts of long-haul networks. Higher availability is an additional benefit, as devices can still operate even if the cooling system fails. ETR is supported in the[Nokia 1830 XTM](https://www.nokia.com/optical-networks/1830-express-transport-metro/) , and in[Nokia 1830 PSS](https://www.nokia.com/optical-networks/1830-photonic-service-switch/) configurations, including new ILA and four-degree ROADM options.


## Operational enhancements


Several innovations reduce operational cost and enhance manageability. Zero-touch provisioning, cabling verification, auto-discovery of transponders and coherent pluggables in routers and switchable gain amplifiers have all contributed to simplify installation. High-performance link control no longer requires complex planning and configuration. OTDRs have become a standard feature, with use cases that include locating fiber cuts, detecting increased fiber loss and intrusion detection. OTDRs are now available as modules, compact pluggables or integrated into line system modules such as ROADM-on-a-blade or ILAs.


## Open optical networks


[OLS have become more open](https://www.nokia.com/optical-networks/open-optical-networking/) , with integrated OCMs and WSS- or DGE-based attenuation simplifying support for third-party wavelengths, while flexible-grid capabilities provide a path to spectrum services. Management interfaces such as TL1 and SNMP have evolved to open APIs (e.g., NETCONF and RESTCONF) with OpenConfig and OpenROADM YANG data models. Pull-based management protocols such as SNMP are evolving to push-based (e.g., gNMI, gRPC) with streaming telemetry.


## Meeting the short- to medium-term requirements of the AI era


Traffic growth is accelerating, amplified by AI infrastructure buildouts. At the same time, spectral efficiency gains are starting to run into the Shannon limit. In response, OLS are evolving to increase capacity, reduce cost, space and power, simplify operations and maximize availability. In the near term, OLS innovation is focused on scaling capacity by improving coherent performance, increasing spectrum and by enabling multi-rail architectures. Additional near-term innovations include direct-attach and low-port-count CDC add/drop, extended temperature ranges, operational enhancements and open optical.


To learn more about this important topic, download the new Nokia white paper:[Optical line system evolution for the AI era](https://www.nokia.com/asset/215480/) .
