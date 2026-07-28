---
schema_version: "1.0.0"
document_id: "fd1548bb1e1eccac892a3c1d00af56e59abe6a6cc6fb17d1d9707f9c6c1f05f3"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/exploring-the-epigenome-of-earths-biodiversity-from-chg-and-chh-methylation-to-fiber-seq/"
published_at: "2026-06-16T13:00:44+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T21:43:30.232286+00:00"
content_hash: "sha256:c5d0a1e8aaf816a44da23654afc88db1ae2f2c150246e7c5d80615f0f4535493"
---

# Exploring the epigenome of Earth’s biodiversity: From CHG and CHH methylation to Fiber-seq

Sequencing has transformed our ability to study genetic variation across the tree of life, but DNA sequence alone does not explain how biological traits emerge. The same genome can produce different outcomes depending on how genes are regulated, when they are expressed, and how DNA is organized within the cell. These layers of regulation, collectively known as the epigenome, play critical roles in development, environmental response, genome stability, and cell identity across plants and animals.


Understanding the epigenome is increasingly essential for connecting genotype to phenotype. This blog explores how DNA methylation and chromatin architecture shape genome function, and how advances in HiFi sequencing now make it possible to measure these regulatory layers with unprecedented completeness. For a deeper dive into experimental design and how HiFi based approaches compare to methods like ATAC-seq and bisulfite sequencing, the Fiber-seq 101 guide has everything you need before your first experiment.


[Download the Fiber-seq 101 guide](https://programs.pacb.com/l/1652/2026-06-11/45k18q)


## What DNA methylation reveals about animal development and diversity


Two categories of epigenetic information are particularly important for plant and animal researchers.


The first is DNA methylation. In[animals](https://www.frontiersin.org/journals/cell-and-developmental-biology/articles/10.3389/fcell.2018.00027/full) , methylation of cytosines at CpG dinucleotides, 5mC, regulates gene silencing, genomic imprinting, and transposon suppression, and plays a central role in how cell identity is established and maintained during development. A related mark, 5-hydroxymethylcytosine, 5hmC, is produced when TET enzymes oxidize 5mC, and it turns out to have a distinct biological identity of its own.


While 5mC tends to be associated with silencing,[5hmC](https://www.nature.com/articles/nrm3589) is enriched at active gene bodies and enhancers and has been tied to cell differentiation, neuronal function, and developmental transitions. The brain accumulates particularly high levels of 5hmC, especially in neurons, and the mark has been found in a range of vertebrates and even some invertebrates. In bees,[5hmC is detectable in brain tissue](https://www.frontiersin.org/journals/genetics/articles/10.3389/fgene.2015.00008/full) and[methylation can differ between behavioral castes](https://www.nature.com/articles/nn.3218) , hinting at roles in the complex behaviors and social organization that make social insects such a fascinating research system. Notably, how these marks are distributed is not uniform across vertebrate evolution:[research in zebrafish and chickens](https://www.tandfonline.com/doi/abs/10.4161/epi.19375) has shown that 5hmC is nearly absent in early embryos until organogenesis begins, quite unlike the enrichment seen in mammalian stem cells. This variation makes both 5mC and 5hmC valuable lenses for studying how epigenetic regulation has diverged across animal lineages.


## How DNA methylation governs plant genomes


In plants, the methylation landscape is richer still.[Plant methylation occurs in three sequence contexts](https://www.nature.com/articles/s41580-018-0016-z) : CpG, CHG, and CHH. Each is maintained by a distinct enzymatic pathway and carries different biological meaning. CHG methylation operates through a reinforcing feedback loop with histone modifications and is important for sustained silencing of transposable elements. CHH methylation is driven by the RNA-directed DNA methylation pathway, which plants use to recognize and silence newly active TEs *de novo* , giving plants a kind of adaptive epigenetic immune system against genomic disruption. Together, these three contexts help govern genome stability, stress memory, and developmental transitions in ways that make plant methylation one of the most active areas of epigenomics research.


## How chromatin architecture shapes gene regulation across Earth’s biodiversity


The second category is chromatin architecture. DNA in eukaryotic cells is wound around histone proteins into nucleosomes, and whether a region of the genome is open or closed determines whether transcription factors can bind, whether enhancers can communicate with their target genes, and ultimately whether genes are expressed. Because regulatory elements often act over long distances, understanding chromatin architecture requires reading long stretches of DNA in context, something short-read methods struggle with, especially in the repeat-dense genomes that characterize most crop and model plant species.


## Expanded methylation calling with HiFi sequencing


HiFi sequencing has long detected CpG methylation natively, but the ability to call methylation across all three plant contexts from HiFi data is new and genuinely expands what is possible for plant epigenomics research.[HiFiMeth](https://github.com/xiaochuanle/hifimeth) now brings all three plant methylation contexts, CpG, CHG, and CHH, into the HiFi sequencing workflow. Validated across 11 plant species including *Arabidopsis* and rice, HiFiMeth achieves genome-wide Pearson correlations with bisulfite sequencing of 0.900 to 0.973 for CHG and 0.755 to 0.800 for CHH, creating a new standard for non-CpG methylation detection from long-read data.


Made possible by the release of new[SPRQ-Nx chemistry on the Revio system](https://www.pacb.com/revio/) , HiFi sequencing can now also detect 5hmC, alongside[improved performance of 5mC methylation detection](https://www.pacb.com/blog/what-a-clearer-view-of-epigenetics-can-mean-for-cancer-research/) . These capabilities are delivered through updated chemistry rather than any changes to library preparation or workflow, so labs adopting SPRQ-Nx gain access to a substantially expanded epigenetic view without operational disruption. For researchers working in plants, this means more sensitive detection across all three methylation contexts within the same sequencing run. For animal researchers, it opens the door to studying 5hmC distribution in development, neuronal biology, and comparative epigenomics without any workflow additions beyond genome sequencing.


## Fiber-seq for chromatin accessibility in plants and animals


[Fiber-seq](https://www.pacb.com/wp-content/uploads/Application-note-Fiber-seq-high-resolution-long-read-chromatin-fiber-sequencing-in-a-single-multiomic-assay.pdf) maps chromatin accessibility, nucleosome positioning, transcription factor occupancy, and CpG methylation from the same HiFi sequencing run used for whole genome sequencing. The method works by treating nuclei with a non-specific adenine methyltransferase,[EpiCypher’s CUTANA Hia5](https://www.pacb.com/blog/how-pairing-epicyphers-fiber-seq-with-hifi-sequencing-delivers-an-all-in-one-multiomic-view/) , that marks accessible adenines within open chromatin. Those marks are detected alongside endogenous 5mC during HiFi sequencing, and because 6mA is not naturally present in most eukaryotic genomes, the signal is clean and interpretable.


A landmark study in maize by[Bubb et al. (2025)](https://www.nature.com/articles/s41477-025-02002-z) illustrates what Fiber-seq makes possible in plant genomes. Because short reads rarely map uniquely within transposable elements, and TEs make up roughly 80% of the maize genome, prior chromatin profiling methods left most of that genome dark. Fiber-seq identified more than twice as many accessible chromatin regions as paired ATAC-seq and revealed how accessibility within retrotransposon long terminal repeats degrades with evolutionary age, how some LTRs are co-opted as gene promoters, and how a specific epigenetic signature marks preferred insertion sites for hAT transposable elements. These are exactly the kinds of findings that require single-molecule, long-range resolution to see.


## The epigenome of life’s diversity, more fully in view


Between HiFiMeth’s expanded methylation calling, SPRQ-Nx-enabled 5hmC detection, and Fiber-seq’s multiomic view of chromatin state, the epigenetic picture accessible through HiFi sequencing has grown considerably. Researchers can now gather chromatin accessibility, DNA methylation across relevant contexts for both plants and animals, and haplotype-resolved genetic variation on a single Revio SMRT Cell. Layers of the epigenome that once required multiple separate assays, each with its own sample requirements and limitations, are now within reach in one streamlined workflow. To get started, the Fiber-seq 101 guide walks through what you need to know.
