---
schema_version: "1.0.0"
document_id: "790e602dfe027849894a4e12933421c2b3a009ea63cb7741b8597dc755cf89be"
company_key: "pacific-biosciences-of-california-inc-common-stock"
company: "Pacific Biosciences of California Inc. Common Stock"
source_id: "pacific-biosciences-of-california-inc-common-stock-news-import-446448bf94cc"
canonical_url: "https://www.pacb.com/blog/improving-hifi-sequencing-accuracy-with-google-deepconsensus-and-alphaevolve/"
published_at: "2026-04-30T13:00:20+00:00"
first_seen_at: "2026-07-22T08:02:43.432836+00:00"
fetched_at: "2026-07-28T22:15:30.724879+00:00"
content_hash: "sha256:d106521889118a491b1536715d7d829877f80278a80810e6157f643fc18c4e93"
---

# Improving HiFi sequencing accuracy with Google DeepConsensus and AlphaEvolve

Scientists rely on HiFi long-read sequencing for one reason above all else: it delivers highly accurate, information-rich sequence data needed to answer complex biological questions. That quality is driven both by PacBio chemistry and the analysis algorithms that interpret sequencing signals. On the[Revio system](https://www.pacb.com/revio/) , HiFi reads are generated using DeepConsensus, a transformer-based deep learning model developed through a collaboration between PacBio and the Google AI Genomics team.


An upcoming Revio update, headlined by multi-use SMRT Cells and[SPRQ-Nx chemistry](https://www.pacb.com/blog/how-sprq-nx-enables-affordable-long-read-whole-genome-sequencing-without-added-complexity/) that together reduce the cost per HiFi human genome to ~$345, also brings meaningful advances in DeepConsensus that further improve read quality. These latest improvements originate from the Google – PacBio collaboration, including key contributions enabled by Google’s[AlphaEvolve](https://deepmind.google/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/) AI coding agent.


This is a clear example of how AI is shaping genomics at multiple levels: HiFi data provides a strong foundation for training AI models such as those behind the[Trillion Gene Atlas](https://www.pacb.com/blog/how-hifi-metagenomic-sequencing-is-powering-ai-driven-discovery-with-basecamp-research/) ; that data is generated using models like DeepConsensus; and now AI systems are helping improve those models themselves.


For researchers and developers alike, these advances mean access to more accurate data at greater scale and lower cost, making it easier to train better models, resolve challenging genomic regions, and generate insights with greater confidence. **As sequencing and AI continue to evolve together, this feedback loop is accelerating discovery across population health, drug discovery, rare disease, and beyond**


.


### Sign up to stay informed about how advances like DeepConsensus are powering the latest SPRQ-Nx chemistry.


[Sign up here](https://programs.pacb.com/l/1652/2026-04-21/45hbps)


---


## How Google DeepConsensus generates highly accurate reads with HiFi sequencing


[DeepConsensus](https://github.com/google/deepconsensus) has powered HiFi read generation on Revio since day one. Because Revio is the highest-throughput and most widely adopted PacBio system, more than three-quarters of all bases ever produced by PacBio sequencing have been processed using DeepConsensus.


To understand how DeepConsensus improves read accuracy, it helps to first consider the underlying[HiFi sequencing approach](https://www.pacb.com/technology/hifi-sequencing/) , which relies on repeated observation of a single DNA molecule. While individual observations can be imperfect, multiple passes enable construction of a highly accurate consensus sequence. The original PacBio[consensus method](https://www.nature.com/articles/nmeth.2474) used a hidden Markov model (HMM), which established HiFi reads as the most accurate long reads available, but did not fully leverage all available signals. not fully leverage all available signal.


DeepConsensus now extends this approach using a transformer-based model that incorporates raw base calls along with the draft HMM consensus to produce improved sequences and quality values. The impact has been substantial.


**DeepConsensus**[reduced errors in HiFi reads by ~42%](https://www.nature.com/articles/s41587-022-01435-7) **and increased the yield of high-accuracy reads. These improvements translate directly into downstream benefits: assemblies are more contiguous, complete, and accurate, and variant calling shows fewer errors compared to prior consensus approaches.**


## How Revio delivers faster HiFi data processing


At launch in 2023, Revio processed ~12 Gb of HiFi data per hour on high-end NVIDIA GPUs. Subsequent engineering work between PacBio and Google improved efficiency, with updates increasing throughput to ~16 Gb/hour through:


- Model optimization to reduce computational overhead
- Floating point quantization to accelerate inference while maintaining accuracy
- Adoption of updated inference frameworks such as ONNX for improved hardware utilization


The upcoming release in 2026 pushes that even further to ~18 Gb/hour, unlocking its fastest data processing to date.


## How AlphaEvolve improved DeepConsensus HiFi sequencing accuracy


Work on DeepConsensus has focused not only on runtime improvements, but also on accuracy. Updates since launch have improved performance at read ends, expanded training to better handle telomeric regions, and generated[non-human datasets](https://github.com/google/deepconsensus/releases) like maize.


One area of continued focus has been the DeepConsensus loss function. Deep learning models are trained by optimizing a loss function that quantifies how far predictions deviate from true labels. A key innovation in DeepConsensus is AlignmentLoss, which incorporates principles from DNA sequence alignment to better account for insertion and deletion errors during training.


Because alignment between long sequences can be imprecise and the most useful information for correcting errors can be found in small local regions, the Google team initially investigated whether constraining alignments to a sliding band could improve accuracy. Early experiments with this banded alignment approach did not show measurable gains, so the method was not pursued further at the time, though related functions remained in the codebase.


Now with access to AlphaEvolve, the Google team revisited this earlier work. AlphaEvolve identified and optimized the existing banded alignment components, refining both the implementation and parameterization to produce a version that improved DeepConsensus accuracy.


Building on this result, the Google team worked with AlphaEvolve and Gemini to further analyze and extend the method, introducing a “convex hull” modification that expands the alignment band toward the diagonal edge of the prediction window.


Together, these changes produce a more effective strategy for training DeepConsensus. This refined approach, available as[open source](https://github.com/google/deepconsensus/tree/banded_alignment) , focuses training on relevant local alignments, improving the model’s ability to represent insertion and deletion errors while reducing the influence of distant alignment noise.


**Banded AlignmentLoss** **plot** showing an example comparison of sequences. The starting sequence is represented on the y-axis and the predicted sequence on the x-axis. Locations where the input and predicted base match are shown as green boxes. The alignment bands considered are in region A around y=x and region C, which is longer due to predicted gaps, and region B, where they overlap.


The updated DeepConsensus banded AlignmentLoss is now integrated onto Revio systems, delivering:


- Increased percentage of reads that achieve empirical Q30 accuracy from 47.9% to 53.2% (+5.3% of reads)
- Improved quality calibration, particularly near the Q20 HiFi threshold


For Revio users, this improved DeepConsensus means more usable high-quality reads per run, more reliable quality values, and faster time to results.


## Driving higher sequencing accuracy and lower cost with SPRQ-Nx chemistry


DeepConsensus improvements are part of a broader set of updates to the Revio platform planned for mid-2026 and available now to select sites.


SPRQ-Nx chemistry enables multi-use SMRT Cells, improving consumable efficiency and reducing human whole genome sequencing cost to ~$345. These chemistry and software advances reinforce each other: Faster analysis supports increased throughput from chemistry, and higher accuracy reduces the need for excess coverage, improving both efficiency and cost-effectiveness.


Importantly, these improvements are delivered within the existing Revio workflow, so users benefit without additional complexity.


For scientists, this means the ability to run larger studies within the same budget, generate higher-confidence results with less sequencing, and move from raw data to biological insight more quickly. Together, these gains help unlock more ambitious research questions, from population-scale studies to increasingly complex genomes.


## How AI and HiFi sequencing are shaping the evolving future of genomics


AI is increasingly woven into every step of genomics, from how data is generated to how it’s interpreted. HiFi sequencing provides the high-quality foundation needed to train biological models, while tools like DeepConsensus,[DeepVariant](https://github.com/google/deepvariant) , and[DeepSomatic](https://github.com/google/deepsomatic) turn raw sequencing signals into meaningful insights.


With tools like AlphaEvolve, a new layer is emerging: AI systems that help design and improve other AI systems. This creates a feedback loop where better data enables better models, and better models improve data generation.


As SPRQ-Nx and updated DeepConsensus models are adopted, they are expected to support larger-scale projects and extend the trend of the majority of PacBio data being analyzed with the highest-performing DeepConsensus algorithms.


Together, these advances are accelerating a shift toward more scalable, precise, and insight-driven biology, bringing the field closer to routinely decoding the full complexity of genomes at population scale.


Connect with a PacBio scientist directly or sign up for the latest updates on SPRQ-Nx chemistry.


[Sign up for updates](https://programs.pacb.com/l/1652/2026-04-21/45hbps)
