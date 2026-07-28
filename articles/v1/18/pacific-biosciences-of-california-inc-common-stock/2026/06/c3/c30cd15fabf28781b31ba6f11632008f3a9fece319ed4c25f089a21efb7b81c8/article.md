---
schema_version: "1.0.0"
document_id: "c30cd15fabf28781b31ba6f11632008f3a9fece319ed4c25f089a21efb7b81c8"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/the-microbial-world-is-everywhere-long-read-sequencing-is-finally-allowing-us-to-see-it-clearly/"
published_at: "2026-06-04T13:07:00+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T21:54:56.147054+00:00"
content_hash: "sha256:1af5268a99bd7fe740addce66c46ed96ae896e74002385e68ad172a5f3bc8c2d"
---

# The microbial world is everywhere. Long-read sequencing is finally allowing us to see it clearly.

Microbes account for most of the diversity of life on our planet, yet fewer than 1% have been identified. They drive human health and disease, shape agriculture, cycle nutrients through ecosystems, and hold enormous potential for therapeutic and industrial discovery. Researchers are working to understand microbes across these varied contexts and yet, for much of the field’s history, the tools available to study these organisms have offered only a narrow slice of what’s actually there.


That tension between the scope of what microbes do and the limits of what sequencing could reveal is what much of the innovation in microbial genomics has been working to resolve.[ASM Microbe](https://programs.pacb.com/l/1652/2026-06-02/45js1h) brings that conversation into focus, with researchers from across the field gathering to share discoveries and compare approaches. For those working in human microbiome research specifically, that conversation continues with a[special webinar rebroadcast and live Q&A](https://programs.pacb.com/l/1652/2026-06-02/45js1l) led by PacBio microbial genomics expert Jeremy Wilkinson, PhD. This expert panel explores how HiFi sequencing addresses the resolution challenges at the core of microbiome research, covering full-length 16S rRNA sequencing and shotgun metagenomics workflows.


[Join us at ASM 2026](https://programs.pacb.com/l/1652/2026-06-02/45js1h)[Attend the webinar](https://programs.pacb.com/l/1652/2026-06-02/45js1l)


## Why partial 16S sequencing, short-read metagenomics, and draft assemblies fall short


The limitations of conventional microbial sequencing show up differently depending on the application, but the underlying problem is consistent: the data does not fully reflect the biology.


The 16S rRNA gene contains several variable regions, and conventional short-read sequencing targets only one or two of them. Which region is sequenced determines which organisms can be identified, and no single partial region captures the full picture. For complex environments like the human gut, that means entire lineages stay invisible or get lumped together under genus-level approximations. Full-length sequencing spanning V1 through V9 provides more complete and unbiased resolution across clades than any partial-region approach can offer.


In shotgun metagenomics, short reads struggle to distinguish closely related strains, and metagenome-assembled genomes (MAGs) tend to stay fragmented rather than closing into complete sequences. That fragmentation limits what can be learned about community function. Roughly[only one-third of short reads](https://www.pacb.com/wp-content/uploads/BugSeq-Taxonomic-and-functional-profiling-with-HiFi-metagenomics-Application-brief.pdf) carry enough information to be functionally annotated even once, compared to 80 to 90% of[HiFi long reads](https://www.pacb.com/technology/long-read-sequencing/) , which typically average four annotations each.


For bacterial whole genome sequencing, draft-quality assemblies miss plasmids, misrepresent repeat-dense regions, and leave the genomic context of AMR genes ambiguous.[Research from the University Hospital Münster](https://www.pacb.com/wp-content/uploads/Solutions-Guide-Public-Health-Brochure.pdf) has shown that plasmid-mediated resistance transmissions account for a substantial share of AMR spread in hospital settings, and detecting them requires closed, complete genomes that draft assemblies cannot reliably produce.


## HiFi long-read sequencing achieves strain-level resolution, closed microbial genomes, and complete MAGs


PacBio HiFi sequencing addresses these gaps through a combination of read length and accuracy that other approaches have not been able to offer simultaneously.


In community profiling, full-length 16S sequencing with HiFi reads spans the entire 16S rRNA gene, delivering species- and strain-level taxonomic resolution that partial-region approaches cannot match. A[2023 study](https://www.mdpi.com/2073-4425/14/8/1567) found full-length 16S sequencing with HiFi reads showed the highest discriminating power among approaches compared, outperforming short-read methods. PacBio[Kinnex 16S technology](https://www.pacb.com/technology/kinnex/) extends this capability by enabling highly multiplexed runs with read counts and costs competitive with short-read workflows.


Shotgun metagenomics with HiFi sequencing recovers more high-quality MAGs and more circular, single-contig MAGs than other technologies, even at lower coverage. With an average of[eight intact genes per HiFi read](https://www.pacb.com/wp-content/uploads/BugSeq-Taxonomic-and-functional-profiling-with-HiFi-metagenomics-Application-brief.pdf) , the data provides far richer functional information than short reads. As Mikhail Kolmogorov of the National Cancer Institute[noted](https://www.pacb.com/blog/long-read-sequencing-myths-debunked-part-5-microbiology/) , HiFi reads make it possible to sequence complete genomes of nearly all abundant bacteria in a microbiome, whereas short-read studies rarely provided complete sequences of even a single microbe.


Closing a bacterial genome used to require combining short and long reads and manually stitching the result together. Now with HiFi sequencing,[reference-grade closed chromosomes and plasmids are the default output](https://www.pacb.com/wp-content/uploads/Application-Brief-Microbial-whole-genome-sequencing-Best-Practices.pdf) , with consensus accuracies consistently above 99.99% and methylation signatures captured from the same native DNA run. That completeness is what makes it possible to see the plasmids carrying resistance genes, resolve the repeat-dense regions that draft assemblies leave ambiguous, and track the mobile vectors mediating AMR spread.


Viral sequencing benefits from the same combination of length and accuracy. HiFi reads deconvolute complex viral mixtures into quasispecies and unique haplotypes, and detect minor variants that short reads routinely miss. In[work on RSV vaccine candidates](https://www.pnas.org/doi/full/10.1073/pnas.2020969118) , minor variants with large internal deletions that were invisible to short reads but detected by HiFi sequencing turned out to be central to understanding how the virus recovers its ability to replicate.


## Where HiFi microbial sequencing is making a difference across research areas


These capabilities support a wide range of questions across[microbial genomics research](https://www.pacb.com/microbial-genomics/) . Closed genomes and plasmids make it possible to track pathogen outbreaks with greater precision and identify resistance transmission routes that draft assemblies would miss entirely. Phasing entire viral genes or genomes and closing bacterial genomes at modest coverage depths opens new windows into host-pathogen dynamics and drug resistance mechanisms. And complete assemblies from complex environmental samples support better gene discovery and more thorough organism characterization, while strain-level resolution from 16S and shotgun approaches helps researchers connect specific microbial species to outcomes in crop health, livestock disease, and ecosystem function.


The common thread is resolution, not as a technical specification, but as a research-enabling condition. Seeing what is actually present, rather than an approximation of it, changes what questions can be asked and what conclusions can be supported.


## Getting started with HiFi microbial genomics


The[PacBio microbial genomics resource page](https://www.pacb.com/microbial-genomics/) brings together case studies, informational literature, and workflow documentation across sequencing methods and research areas. If human microbiome research is your focus, join the[live rebroadcast and expert Q&A](https://programs.pacb.com/l/1652/2026-06-02/45js1l) with Jeremy Wilkinson, PhD, and come join the PacBio team at[ASM Microbe](https://programs.pacb.com/l/1652/2026-06-02/45js1h) .
