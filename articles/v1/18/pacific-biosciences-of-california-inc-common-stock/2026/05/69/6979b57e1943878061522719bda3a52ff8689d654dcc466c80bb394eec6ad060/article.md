---
schema_version: "1.0.0"
document_id: "6979b57e1943878061522719bda3a52ff8689d654dcc466c80bb394eec6ad060"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/long-read-sequencing-is-not-the-trade-off-it-used-to-be-these-are-the-5-questions-that-show-why/"
published_at: "2026-05-08T13:00:27+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T21:45:28.384377+00:00"
content_hash: "sha256:800ee244e87f69bbb777be68a34e998885d6cca63dfcdb72ad6a45c1c985aaa6"
---

# Long-read sequencing is not the trade-off it used to be: These are the 5 questions that show why

***By Samantha Kalla, Field Application Scientist, PacBio***


For years, five variables have defined the trade-offs in sequencing: read length, accuracy, methylation, cost, and sample input. Pick long reads, accept noisier data. Stick with short reads, lose structural variants and full-length isoforms. Want methylation? Run a separate assay, add cost, and wait longer while still only answering a subset of your research question.


That trade-off is no longer what it used to be and is worth revisiting to ensure you are not limiting what you can see with your data.


I spend most of my week in conversations with research labs, where I have an opportunity to understand what new ideas and questions are emerging, and where the scientific tides are pushing and flowing. In our recent Top 5 questions about HiFi video, I walked through what I get asked most often. On all five, HiFi[long-read sequencing](https://www.pacb.com/technology/long-read-sequencing/) has changed the answer, and I want to share what I tell people.


[Watch video](https://www.youtube.com/watch?v=zV8U8IYyZWY)[See how SPRQ-Nx compares](https://programs.pacb.com/l/1652/2026-05-07/45hwzp)


## Short reads vs long reads


When someone asks me why short reads are not enough for their question, I usually reach for a puzzle metaphor.


Short-read methods produce millions (or even in some cases billions) of 150 to 200 base snippets. But that’s the thing – they’re only fragments, shreds of the full genomic context. They’re great for base-level precision but simply cannot span the long or complex regions where much of the biology sits, including structural variants, repetitive elements, and GC-rich regions.


Your browser does not support the video tag.


No matter how many more tiny snippets you add, you end up missing the complete picture (or in my opinion, something worse: extrapolating context from a puzzle built from only the edges).


Your browser does not support the video tag.


“With HiFi sequencing, your DNA read length follows your DNA fragment size, from 500 to 20,000 bases, with 99.9% accuracy per read.”


And because you’re able to prep native DNA without PCR amplification, the same sequencing acquisition captures every nucleotide variant type plus DNA methylation.


While we don’t have the capability to sequence native RNA, HiFi still holds a specialty in transcriptomics. This edge comes from the ability to sequence full-length isoforms including their 5’ and 3’ UTR (untranslated regions of mRNA that are critical for post-transcriptional gene regulation, stability, localization, and translation efficiency), rather than those tiny base snippets mentioned earlier.


Anyone working in this field can imagine the feeling of opening a dataset with alternative splicing and gene expression already directly resolved and interpretable without weeks of bioinformatics labor.


---


## HiFi vs other long-read sequencing


When comparing long-read platforms, accuracy is the first hallmark I point to.[HiFi reads](https://www.pacb.com/technology/hifi-sequencing/) are highly accurate on their own, rather than relying on averaging noisy signals. This inherently leads to more consistent coverage across GC-rich and repetitive regions and fewer false positives in variant calling, just by the nature of the technology.


Your browser does not support the video tag.


HiFi data is so accurate that 20x coverage is sufficient depth for variant and methylation analysis (compared to ~40x required by other technologies). But the practical differences extend beyond just accuracy. A typical HiFi genome BAM file is around 30 to 60 gigabytes, ultimately leading to reduced analysis and storage costs.


Sample input requirements for library prep have also significantly dropped. A native whole-genome run on the


[Revio system](https://www.pacb.com/revio/) requires only 500 ng of gDNA to begin library prep. And for samples where DNA is scarcer and more precious, the


[Ampli-Fi protocol](https://www.pacb.com/blog/new-ampli-fi-ultra-low-input-protocol-will-support-hifi-sequencing-from-as-little-as-1-ng-of-dna/) allows library prep input as low as 1 ng.


---


## More data and less labor with simultaneous native methylation sequencing


The capability to observe methylation signatures within DNA (sometimes referred to as five-base or six-base sequencing) has introduced an entirely novel biological topography for us to discover through the field of epigenetics. And again, it is yet another spotlight where HiFi clearly stands out.


This methylation signature is linked to every native HiFi sequencing run through the observation of “polymerase kinetics,” where very subtle changes in the sequencing enzyme’s speed reveal base modifications like 5mC.


Your browser does not support the video tag.


“HiFi detects methylation in real time, directly from the native DNA. There is no chemical conversion, no extra prep, and no additional cost. It is built into every single run.”


This truly enables multiomic sequencing in a single assay, linking genetic variation automatically with methylation. Imagine no longer having to do a separate bisulfite treatment upfront or additional prep to collect methylation data, which adds cost and capture only part of the picture.


Your browser does not support the video tag.


With groundbreaking applications such as


[Fiber-seq](https://www.pacb.com/blog/how-pairing-epicyphers-fiber-seq-with-hifi-sequencing-delivers-an-all-in-one-multiomic-view/) , it is also possible to examine chromatin structure alongside methylation at single-molecule resolution.


---


## The bottom line: HiFi sequencing cost and input


Cost is usually where the conversation becomes practical. The gap has narrowed significantly, and HiFi sequencing is now within reach for most labs with the accessible


[Vega benchtop system](https://www.pacb.com/vega/) . With


[SPRQ-Nx chemistry](https://www.pacb.com/blog/how-sprq-nx-enables-affordable-long-read-whole-genome-sequencing-without-added-complexity/) , A 20x human whole genome runs around 300 dollars per genome at scale from 500 ng of input DNA. That is in line with short-read inputs, with the added benefit of more complete data.


Your browser does not support the video tag.


To be transparent about a trade-off to consider:


Transcriptomics on


[Kinnex](https://www.pacb.com/technology/kinnex/) costs more than basic short-read RNA-seq, but with the added value of a fundamentally richer dataset through full-length isoform information, including novel transcripts and fusion genes.


[Microbial sequencing](https://www.pacb.com/microbial-genomics/) runs in the same cost range as short reads, at tens of dollars per sample, while delivering closed genomes, plasmids, and methylation data. Full-length 16S and amplicons drop to just a few dollars per sample, with species and strain resolution that short reads cannot match.


Your browser does not support the video tag.


Across workflows, I often point to the hidden cost of incomplete data. Rework, missing variants, and bioinformatics workarounds can add time and expense that are not always obvious at the start.


Sample input is no longer a barrier for most labs. Extraction methods are designed to preserve long fragments, and workflows span from whole genomes to single-cell applications with low input requirements.


## Key takeaways


- HiFi sequencing resolves structural variants, repeats, and full-length isoforms in a single run with 99.9% per-read accuracy
- Capture 5mC, 5hmC, and 6mA methylation alongside every variant without extra prep or added cost
- Run a 20x human whole genome for ~$300 at scale
- Scale long-read sequencing to any lab with Vega and automation-ready workflows


Watch the full Top 5 HiFi video on the[PacBio YouTube channel](https://www.youtube.com/@PacificBiosciences) , then explore example[datasets](https://www.pacb.com/connect/datasets/) and connect with our team at[pacb.com](https://www.pacb.com/) .


[Watch video](https://www.youtube.com/watch?v=zV8U8IYyZWY)


---


## About the author


I’m Samantha Kalla, and I have been Field Application Scientist at PacBio for nearly five years. I support our customers in Northern California, which means I’m working directly with labs adopting HiFi sequencing. I’m fully committed to my part in teaching what our current tools in biology can do and enthusiastically observing what we will uncover next. In my free time, I assemble incomplete puzzles, write and read poetry, and spend time in nature with my daughter.
