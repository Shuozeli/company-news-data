---
schema_version: "1.0.0"
document_id: "5b67e097fafcbc0a5f874c4a546caab3d460270b2ed6c999630c4d60f531d6c3"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/the-practical-questions-clinical-research-labs-consider-when-adopting-hifi-sequencing/"
published_at: "2026-06-11T15:10:04+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T21:46:31.447870+00:00"
content_hash: "sha256:a27f43cafde230ec987cff2d21898c6c7229f093a54ff08b46ffdbf849273498"
---

# The practical questions clinical research labs consider when adopting HiFi sequencing

For clinical laboratories evaluating long-read sequencing, the central question has changed. A substantial and growing body of research now demonstrates that HiFi sequencing can deliver the accuracy, comprehensiveness, and reproducibility that clinical research demands. The harder question today is what adoption actually looks like.


What does validation require? Where do HiFi whole genome sequencing and PureTarget fit within an existing menu? How does a lab build the operational case for consolidating multiple assays into one workflow? These are the questions that live between the published literature and the decision to move forward, and they tend to be best answered by people who have already navigated them.


An on-demand expert panel featuring laboratory leaders from Myriad Genetics, GeneDx, Karolinska University Hospital, and Radboudumc covers exactly this ground, offering practical perspective on where long-read sequencing fits and what teams should consider when planning for validation and scale.


[Watch the panel](https://programs.pacb.com/l/1652/2026-06-08/45jwtq)


## Real-world evidence for HiFi sequencing in clinical research


The research record on HiFi sequencing has expanded rapidly in recent years. A large prospective[study from Radboud University Medical Center](https://www.pacb.com/blog/radboud-umc-research-highlights-promise-of-hifi-long-read-sequencing-to-match-standards-of-care-in-rare-disease-genomics/) designed to reflect how testing is actually ordered in practice evaluated HiFi whole genome sequencing against standard-of-care testing across more than 1,000 samples, finding 96.4% concordance across variant types. When modeled across an annual subject population, HiFi WGS showed the potential to improve or refine diagnostic findings in an estimated 3.4% of cases, potentially translating to clearer explanations for hundreds of additional families per year through a single comprehensive assay.


Work at GeneDx put this into operational terms. A[recent study](https://www.pacb.com/blog/the-power-of-one-how-assay-consolidation-and-menu-expansion-reshape-sequencing-economics/) of 191 subjects enriched for difficult-to-detect variants found that HiFi whole genome sequencing identified 99.6% of 481 known pathogenic variants from a single workflow, variants that would traditionally require a combination of short-read sequencing, microarrays, MLPA, and targeted panels. Where standard workflows had required more than one test and nearly a month to reach a resolution on average, the research context estimated results within five to seven days from a single HiFi run.


Research at Children’s Mercy Kansas City examined that same question in a pediatric rare disease research context. A comparative study published in[JAMA Pediatrics](https://jamanetwork.com/journals/jamapediatrics/fullarticle/2838675) followed 235 subjects evaluated with HiFi WGS against 513 matched controls receiving standard-of-care genetic testing, including expedited exome sequencing, karyotype, FISH, chromosomal microarray, and targeted panels. HiFi WGS showed a roughly 10% increase in solve yield compared to standard of care, a 37-day improvement in time to result, and an average of 2.7 assays per solve versus 6.1 with standard workflows. Of the cases where HiFi made the difference, the majority benefited from capabilities that are difficult or impossible to access with other technologies, including structural variant resolution, repeat expansion detection, methylation profiling, and variant phasing.


## Planning for HiFi sequencing analytical validation


For labs ready to move from the evidence to the next step, analytical validation of a long-read sequencing assay follows a framework similar to other NGS assays, covering accuracy, precision, analytical sensitivity and specificity, and reportable range. There are a few considerations specific to long reads worth understanding early in planning.


One thing worth knowing upfront is that HiFi data can surface true genetic variation that existing truth sets do not fully capture, since many were built using technologies with lower resolution. Discrepancies between HiFi calls and legacy truth calls are not always errors; sometimes they reflect real genetic diversity that prior technologies missed, and understanding where those differences arise is a useful part of validation design. Beyond that, the considerations that most commonly require more planning than expected are operational rather than scientific. Compute requirements, data storage, network configuration, and LIMS integration all involve decisions that are substantially easier to address before a validation study begins than after. The pre-clinical playbook covers these infrastructure requirements in practical detail alongside the full validation framework, and is designed to be consulted section by section as labs work through different stages of planning.


## How HiFi WGS and PureTarget panels fit laboratory workflows


The central question for many teams is where HiFi whole genome sequencing (WGS) and PureTarget fit within a laboratory’s existing menu. The two approaches address different needs and often serve as complementary entry points.


[HiFi WGS](https://www.pacb.com/products-and-services/applications/whole-genome-sequencing/) delivers a comprehensive view from a single run, capturing SNVs, structural variants, copy number variants, repeat expansions, phasing, and methylation without additional library preparation. This makes it well suited for rare disease research contexts where the value of completeness is highest. The[Radboud UMC study](https://www.medrxiv.org/content/10.64898/2026.01.13.26343759v1) showed that this broader view can surface findings that sequential testing misses while also providing haplotype-resolved data that reduces the need for parental samples in some cases.


[PureTarget](https://www.pacb.com/technology/puretarget/) panels offer a focused, high-throughput path for applications where the research question is more defined but the genes are difficult to sequence. In carrier screening research, genes with tandem repeat expansions, high-homology regions, and complex structural variants have long required a patchwork of specialized assays. A single targeted HiFi workflow can consolidate that testing without sacrificing the depth needed to characterize these regions reliably.


This consolidation argument has grown stronger with the commercial launch of[SPRQ-Nx chemistry](https://www.pacb.com/revio/) for the Revio system, which brings the cost of HiFi whole human genome sequencing to approximately $345 per genome and less than $300 at scale, a roughly 30% reduction that makes long-read sequencing an increasingly practical option to evaluate across a wider range of laboratory settings and volumes.


## Perspectives from labs adopting long-read sequencing


The on-demand panel brings together laboratory leaders from across the clinical landscape to share how they are thinking through adoption in practice. The session covers where HiFi WGS and PureTarget fit within different laboratory contexts, what evaluation and validation planning realistically involves, how assay consolidation affects operational complexity and turnaround time, and what laboratory teams should weigh when thinking about scale. Speakers from Radboud UMC and Karolinska University Hospital speak to rare disease research workflows and what first-tier sequencing adoption looks like in European clinical settings, while GeneDx and Myriad Genetics bring perspective on how large-scale commercial laboratories think about analytical validation design, workflow integration, and the practical tradeoffs involved in expanding a test menu with long-read sequencing.


Together, the panel and playbook offer a way to move from the evidence to the practical: understanding where HiFi sequencing fits, what evaluation involves, and what the path toward implementation can realistically look like.


[Watch the panel](https://programs.pacb.com/l/1652/2026-06-08/45jwtq)[Download the pre-clinical playbook](https://programs.pacb.com/l/1652/2026-06-08/45jwym)
