---
schema_version: "1.0.0"
document_id: "3e6a608f57064e1e2f5a24ad5656c3bdbff7db1bb6a25c60750f7ddb22251c6a"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/hifi-multiomics-reveals-how-biology-shapes-life-on-earth/"
published_at: "2026-04-22T13:00:30+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T21:45:30.754431+00:00"
content_hash: "sha256:a08c9b52ee0c924261152350683fbc660bbcef1fdc4e34f8b48f79d5b70a5926"
---

# HiFi multiomics reveals how biology shapes life on Earth

Earth Day is a reminder that life on this planet is as intricate as it is interconnected. From coral reefs to crop fields, every ecosystem tells a story written in DNA. For a long time, that story has been incomplete, shaped by the limits of the tools we use to read it.


Now, with multiomic approaches, we are beginning to reveal not just what genomes contain, but how they function, adapt, and interact with their environments. Recent studies are bringing together insights on sequence, structure, and regulation to reveal how the genome operates as a dynamic, interconnected system. This broader view makes the diversity of life on Earth feel even more extraordinary and worth taking a moment to celebrate.


## Exploring somatic and germline mutation across the tree of life’s genomes with HiFi


As an example of looking beyond any single species to patterns across the entire tree of life, in a[new study](https://www.biorxiv.org/content/10.64898/2025.12.28.691837v1.abstract) , researchers at the Wellcome Sanger Institute examined mutational processes of hundreds of organisms. Using highly accurate long reads, they were able to detect somatic and germline mutations across plants, animals, and fungi. This study is part of the wider[Darwin Tree of Life project](https://www.darwintreeoflife.org/) , an ambitious initiative to sequence and catalog the genomes of 70,000 eukaryotic species in Britain and Ireland, with HiFi long-read sequencing as a core enabling technology. By capturing the genetic diversity of an entire region, this project opens new possibilities for understanding evolution, guiding conservation, and monitoring ecosystem health at an unprecedented scale.


The results revealed just how diverse these processes are. Mutational patterns varied widely between species and environments, with some signatures shared across broad lineages and others tied to specific ecological niches. This work pushes mutation research beyond traditional model organisms and into a much broader biological context.


This kind of analysis depends on accuracy. Detecting rare somatic mutations requires confidence at the single-molecule level, which powers the 99.9% read accuracy of HiFi sequencing. With that foundation, researchers can begin to compare mutation biology across the full diversity of life.


As the authors put it:


> ### “Leveraging high-fidelity long-read sequencing, we have glimpsed the heterogeneity of mutational processes operative across a large cross-section of the tree of life, revealing a much richer landscape than that previously studied in humans. If this represents the diversity present in species resident on a few temperate rocky islands on the northwestern fringes of Europe, we can only wonder at what might await discovery planet-wide.”


## How HiFi and CiFi work together to generate chromosome-scale assemblies


If mutation studies tell us how genomes evolve, assemblies tell us what elements make up their genomes in the first place.


To investigate how structural variation shapes biology, researchers at UC Davis[recently](https://www.biorxiv.org/content/10.64898/2026.03.13.711624v1.abstract) used[the CiFi method](https://www.nature.com/articles/s41467-025-66918-y) alongside HiFi sequencing to generate chromosome-scale, haplotype-resolved assemblies of vole genomes from a single library.


By capturing long-range chromatin interactions together with accurate sequence data and combined with the[Ampli-Fi method](https://www.pacb.com/blog/new-ampli-fi-ultra-low-input-protocol-will-support-hifi-sequencing-from-as-little-as-1-ng-of-dna/) to improve sequencing yield and read length, CiFi enables more complete genome reconstruction, especially in complex or repetitive regions. In this study, it allowed researchers to resolve structural features that were missing from earlier references, including a species-specific duplication in a gene linked to pair bonding.


*Workflow and assembly data for prairie and meadow voles using CiFi with HiFi sequencing to generate chromosome-scale, haplotype-resolved genome assemblies. To learn more about the CiFi workflow with HiFi sequencing and its advantages, read the[Application note](https://www.pacb.com/wp-content/uploads/Application-note-CiFi-Long-read-multi-contact-3C-for-chromosome-scale-assemblies-using-PacBio-HiFi-reads.pdf) .*


For biodiversity genomics, this kind of approach is key. It brings chromosome-scale assemblies within reach for more species, including those that are difficult to study, and provides a clearer view of the structural variation that underpins diversity. This method replaces complex, multi-technology workflows with a single HiFi approach, making high-quality genome assembly more accessible across far more species.


## Mapping the maize methylome and epigenome with HiFi Fiber-seq


While approaches like CiFi capture chromatin structure to help assemble genomes, other methods such as[Fiber-seq](https://www.pacb.com/blog/how-pairing-epicyphers-fiber-seq-with-hifi-sequencing-delivers-an-all-in-one-multiomic-view/) examine that same chromatin architecture to understand how genomes are regulated. In a[study](https://www.nature.com/articles/s41477-025-02002-z) from researchers at the University of Washington presented at this year’s[PAG conference](https://www.youtube.com/watch?v=krjyaSL5_tg) , this method was used to map chromatin accessibility and DNA methylation across the maize genome at single-molecule resolution.


Because it relies on long reads, Fiber-seq can resolve regulatory elements even within highly repetitive regions. In maize, this uncovered accessible chromatin regions within transposable elements and showed how these elements can act as promoters or enhancers, shaping gene expression and genome evolution.


*Chromatin architecture organizes DNA into nucleosomes that shift between open, active states and closed, repressed states, with DNA methylation and histone modifications regulating gene expression, all of which can be resolved at single-molecule resolution using Fiber-seq.*


This kind of insight is especially important for plant genomes, where repetitive content often obscures regulatory signals. By pairing sequence with chromatin context, researchers can begin to understand not just what genes exist, but how they are controlled.


## Resolving the zebrafish transcriptome with HiFi long-read RNA sequencing


Beyond DNA and chromatin, understanding how genomes function also depends on accurately capturing the transcripts they produce. In a[recent study](https://link.springer.com/article/10.1186/s12915-025-02271-2) from researchers at the Chinese Academy of Sciences, HiFi sequencing was used to generate a more complete view of the zebrafish transcriptome across embryonic development using[long-read RNA sequencing](https://www.pacb.com/products-and-services/applications/rna-sequencing/) .


*Workflow for profiling the zebrafish embryonic transcriptome using HiFi long-read RNA sequencing across developmental stages, revealing novel isoforms and previously unannotated genes. Figure 1A from[Bo et al. (2025)](https://link.springer.com/article/10.1186/s12915-025-02271-2) .*


By sequencing full-length RNA molecules, the team was able to resolve complex isoforms, refine gene models, and improve genome annotation in ways that are difficult with short-read approaches alone, uncovering 2,113 previously unannotated genes and 33,018 novel isoforms of previously annotated genes. This provided a clearer picture of transcript diversity, including previously unannotated transcripts and alternative splicing events.


For widely used model organisms like zebrafish, these improvements have broad impact. More accurate transcriptomes support everything from developmental biology to disease research, ensuring that downstream analyses are built on a more complete and reliable reference.


Together with genome and epigenome data, transcript-level insight adds another critical layer to multiomic studies of plants and animals, helping connect sequence and structure to function.


## Capturing microbial diversity with HiFi sequencing


While much of biodiversity research focuses on plants and animals, a vast portion of life on Earth exists at the microbial level. In a recent[soil microbiome study](https://www.frontiersin.org/journals/microbiology/articles/10.3389/fmicb.2025.1633360/full) , researchers compared sequencing platforms to better understand how microbial communities shape ecosystems. Using full-length 16S rRNA sequencing, they showed that long-read approaches can more accurately capture bacterial diversity, with HiFi sequencing offering strong sensitivity for detecting even low-abundance species.


Initiatives like the[Trillion Gene Atlas](https://www.pacb.com/blog/how-hifi-metagenomic-sequencing-is-powering-ai-driven-discovery-with-basecamp-research/) are expanding the reach of microbial sequencing even further by combining large-scale metagenomics with HiFi sequencing to generate deeply sequenced datasets from diverse environments. While targeted microbiome profiling identifies which organisms are present, metagenomics provides insight into the genes within those communities and how they function in context.


Microbial sequencing approaches offer complementary ways of exploring life at its smallest scales, helping illuminate a vast, largely unseen layer of biodiversity that sustains ecosystems across our planet.


## A living planet, seen more clearly


Taken together, these studies point toward a more connected view of biodiversity genomics.


From mutation patterns across hundreds of species to chromosome-scale assemblies and single-molecule maps of gene regulation, multiomic approaches are expanding what we can learn from the genomes of plants and animals. They are also scaling across applications, from[low-pass sequencing strategies](https://www.pacb.com/blog/publication-spotlight-advancing-plant-breeding-with-long-read-low-pass-sequencing/) that support crop improvement to advances in[sex chromosome assembly](https://www.pacb.com/blog/celebrating-fathers-day-with-new-discoveries-of-the-y-chromosome-achieved-with-hifi-sequencing/) and[soil metagenomics](https://www.frontiersin.org/journals/microbiology/articles/10.3389/fmicb.2025.1633360/full) .


The common thread is clarity. With more complete data and integrated approaches, multiomics weaves together sequence, structure, and function into a single, coherent view that captures the richness and wonder of life across our planet.


---


When it comes to understanding life on Earth, there is always more to uncover. If you are curious where this is all heading, read through our[plant & animal research brochure](https://www.pacb.com/wp-content/uploads/Plant-animal-research-brochure102-193-668.pdf) and explore our[biodiversity page](https://www.pacb.com/plant-animal-sciences/biodiversity/) to get a look into the growing body of work exploring biodiversity through long-read sequencing and multiomics.


[Join our webinar](https://programs.pacb.com/l/1652/2026-03-26/45gh5c) and see how gene editing and HiFi sequencing are unlocking new ways to grow resilient crops and protect the planet’s biodiversity.
