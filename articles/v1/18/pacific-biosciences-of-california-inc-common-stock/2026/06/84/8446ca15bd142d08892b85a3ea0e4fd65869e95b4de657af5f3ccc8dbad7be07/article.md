---
schema_version: "1.0.0"
document_id: "8446ca15bd142d08892b85a3ea0e4fd65869e95b4de657af5f3ccc8dbad7be07"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/rapid-hifi-whole-genome-sequencing-for-time-critical-genomic-research/"
published_at: "2026-06-25T13:00:49+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T21:43:26.997349+00:00"
content_hash: "sha256:a5cf9936a6dc55a2f32a1f2189d9e289a62ed669cfc8e027495a1b88ad6369d0"
---

# Rapid HiFi whole genome sequencing for time-critical genomic research

In time-critical settings, like a neonatal intensive care unit, the pressure to find explanations is immediate. For example, an estimated 60% of level IV NICU infants in the US are likely eligible for rapid genome sequencing1, yet a large proportion remain untested. The stakes of this gap are difficult to overstate: In a recent interventional study, access to rapid genomic sequencing led to a finding that shaped a change in clinical management for nearly 97% of these infants1. For critically ill newborns and their families, earlier and more comprehensive insights can reshape the entire trajectory of care.


Researchers and clinicians have long recognized that the most comprehensive genomic data offers the greatest opportunity to reach a finding, particularly for[rare diseases](https://www.pacb.com/research-focus/human/rare-disease/) that require detection of complex variants.


Historically, the genomics community has faced a tradeoff between speed and comprehensiveness. That is beginning to change. While rapid sequencing workflows have largely been built around short-read technologies,[long-read sequencing](https://www.pacb.com/technology/long-read-sequencing/) has increasingly become the preferred approach for comprehensive whole genome analysis. Recent workflow innovations suggest that researchers may no longer need to choose between the two.


At the recent PacBio PRISM event in Barcelona, Emma Baple, Professor of Genomic Medicine at the University of Exeter,[spoke to the urgent need](https://programs.pacb.com/l/1652/2026-06-22/45kccs) for faster, more complete genomic testing for acutely unwell children and to the role long-read sequencing could play in that future. Her talk underscores the importance of the development of a PacBio rapid HiFi WGS workflow,[recently presented](https://www.pacb.com/wp-content/uploads/2026-ESHG-rapid-WGS.pdf) this month at ESHG in Gothenburg, Sweden.


[Watch Emma Baple’s PRISM talk](https://programs.pacb.com/l/1652/2026-06-22/45kccs)[View the ESHG poster](https://www.pacb.com/wp-content/uploads/2026-ESHG-rapid-WGS.pdf)


---


## Why speed matters in rare disease genomic research


For families of critically ill infants, the window in which a genomic finding can influence research decisions and help inform care pathways is often narrow, measured in days rather than weeks. Healthcare systems and national genomic medicine programs around the world have invested heavily in rapid sequencing to help accelerate findings in newborns suspected of a rare disease. Professor Baple described the process of England’s National Rapid Genome Sequencing Service, which is commissioned to sequence over 1,200 acutely unwell children per year using a gene-agnostic approach. Their team has worked to push turnaround time toward five days or less, a threshold where genomic findings can still intersect meaningfully with clinical decision-making.


The challenge is that current rapid WGS workflows are almost entirely built on short-read sequencing. While short reads can be delivered quickly, they systematically miss or incompletely resolve some of the variant classes most relevant to rare disease research, including structural variants, repeat expansions, and complex rearrangements that require phased, long-range genomic context to interpret. For situations where thoroughness and speed are both essential, this is a meaningful gap.


Long-read HiFi sequencing captures all of these variant classes in a single workflow, along with native methylation information, without the need for orthogonal assays. Where conventional rare disease workups often require multiple sequential tests to piece together a complete genomic picture, a single HiFi genome can help replace that patchwork from the outset, and now presents a clear path forward for time-critical genomic research.


## How the rapid HiFi WGS workflow achieves fast turnaround with comprehensive coverage


At the 2026 European Society of Human Genetics (ESHG) conference, PacBio researchers presented an accelerated HiFi WGS workflow designed for such time-critical genomic applications. The newly developed rapid HiFi WGS workflow reduces overall turnaround time from gDNA extraction to VCF generation from approximately 54 hours in the standard workflow to under 30 hours (Figure 1). The workflow is a modified version of the standard[HiFi prep kit 96](https://www.pacb.com/technology/library-prep/) workflow, with targeted optimizations at each stage of the pipeline (Figure 2).


**Figure 1** . Workflow timing estimates of standard HiFi WGS workflow vs accelerated protocol.


This modified workflow combines streamlined DNA extraction for blood, buccal, and saliva, faster library prep, reduced sequencing runtimes, and accelerated bioinformatics analysis. The rapid workflow leverages 12-hour movie times targeting 20x human genome coverage per SMRT Cell on the[Revio system with SPRQ-Nx chemistry](https://www.pacb.com/revio/) . Importantly, these improvements were achieved while preserving the comprehensive variant detection capabilities that make long-read sequencing valuable for rare disease research.


**Figure 2** . Workflow component accelerations. Overview of changes to rapid protocol to decrease overall workflow turnaround time.


Taken together, these results demonstrate that comprehensive long-read sequencing can be delivered within a timeframe relevant to urgent genomic research settings, with consistent human coverage maintained across diverse sample types, extraction methods, and multiple SMRT Cell uses with SPRQ-Nx chemistry.


## Long-read sequencing and the future of rapid genomic testing


Professor Baple’s talk at PRISM brought the human stakes of this work into focus. For families of critically ill infants, the arrival of a genomic finding is rarely just a data point. It can be the moment that informs clarity on a potential diagnosis, opens a treatment pathway, or finally gives parents an explanation after weeks of uncertainty. The ability to deliver that kind of comprehensive genomic insight quickly, without the gaps that short-read approaches leave behind, is what makes a rapid long-read workflow meaningful beyond its technical specifications.


As research groups and genomic medicine services work toward shorter turnaround times for acutely unwell children, the case for incorporating long-read sequencing into that effort continues to build. To hear more about the clinical research landscape driving this work, watch Professor Baple’s talk from PRISM in Barcelona, or explore the ESHG poster for a detailed look at what this workflow makes possible.
