---
schema_version: "1.0.0"
document_id: "37d1428f3980f756ca9286005e0d9d7b9d20d13064fd79b632025ac8ad2430c1"
company_key: "qiagen-n-v-common-shares"
company: "Qiagen N.V. Common Shares"
source_id: "qiagen-n-v-common-shares-news-import-3382321b7330"
canonical_url: "https://digitalinsights.qiagen.com/news/blog/translational/cosmic-and-hsmd-data-for-biopharma/"
published_at: "2025-08-27T19:50:23+00:00"
first_seen_at: "2026-07-25T20:20:54.342051+00:00"
fetched_at: "2026-07-27T23:07:36.305258+00:00"
content_hash: "sha256:a9d10e9326c3f9f85024379c560523e59e0b173e72600fbf67695228e0229f42"
---

# Using trusted cancer data can accelerate drug discovery and development

## How expert-curated cancer data from COSMIC and HSMD can help biopharmaceutical researchers identify and validate targets faster and optimize clinical trial design


In cancer drug discovery and development, data is king. From identifying potential molecular targets to helping predict drug toxicity and optimizing clinical trial design, high-quality data can significantly improve the efficiency and success rate of bringing new cancer therapies to market.


The[Catalogue Of Somatic Mutations In Cancer (COSMIC)](https://digitalinsights.qiagen.com/cosmic-hsmd-biopharma/) and the[Human Somatic Mutation Database (HSMD)](https://digitalinsights.qiagen.com/cosmic-hsmd-biopharma/) are two expert-curated somatic knowledgebases exclusively licensed through QIAGEN that enable biopharmaceutical researchers to avoid pitfalls in early cancer drug discovery, confidently qualify candidate drug targets and accelerate indication expansion and repurposing of existing cancer therapies.


In this blog, we take a closer look at COSMIC and HSMD for biopharmaceutical research, providing an overview of the expert curation processes, what types of data can be found in each database and examples of how this data can be applied through the cancer drug discovery and development pipeline.


### How COSMIC's cancer data supports oncology drug discovery


[COSMIC](https://cancer.sanger.ac.uk/cosmic) is an expert-curated knowledgebase providing data on somatic variants in cancer, supported by a comprehensive suite of tools for interpreting genomic data, discerning the impact of somatic alterations on disease, and facilitating translational research. The catalogue is accessed and used by thousands of cancer and biopharmaceutical researchers and clinicians daily, allowing them to quickly access information from an immense pool of data curated from over 30,000 scientific publications and large studies.


COSMIC integrates somatic data from multiple sources published around the world and allows researchers to access and scrutinize information about somatic mutations and their impact in cancer. Over the past two decades, COSMIC has been diligently collecting, cleaning and organizing genomic data and associated metadata from cancer studies published in scientific literature and various bioinformatics sources. This data is then translated into a standardized format, integrated and made available to the research community through well-structured datasets and user-friendly data exploration websites and tools.


In addition to the main catalog of somatic mutations, six accompanying modules focus on different aspects of oncology (Figure1 ). The Cancer Gene Census (CGC) and Cancer Mutation Census (CMC) provide additional annotations regarding the roles of genes and mutations in oncogenesis, based on a defined set of rules and sufficient evidence obtained through dedicated literature curation and analysis of the content of the core catalog.


→ View the complete database numbers in the latest release[here](https://digitalinsights.qiagen.com/explore/webcosmic/release_notes?cmpid=CM_QDI_CLIN_Biopharmablog3) .


**Figure 1. COSMIC’s seven key resources for understanding cancer and improving cancer patient care.** The main catalog of somatic mutations is supported by six accompanying modules that, together, lay additional layers of knowledge – helping to interpret the impact of somatic mutations on cancer development and presenting available therapeutic options (graphic from Sondka et al., 2024).


### COSMIC's expert curation process


COSMIC’s workflows to manually curate cancer genetic data have been built to deliver high-quality, biologically and clinically relevant data to the research community. Different data sources and types of curated data require different approaches (Figure2 ). However, each case has common core elements.


- First, the information source is identified from peer-reviewed literature or bioinformatic resources and checked for the quality and relevance of the content.
- To enable meaningful analysis by end users, data needs to be adequately and transparently categorized. This is achieved by combining the use of controlled vocabularies that label data and a database schema that is able to represent these vocabularies.
- Before data extraction, all curated features and terms are converted to vocabularies, ontologies and data conventions used by COSMIC. Genes, variants and transcripts use external vocabularies and ontologies. For interoperability, all COSMIC disease classifications have been mapped to the NCI thesaurus ontology; these mappings can be downloaded from the COSMIC website.
- Acquiring the data itself is the final stage of curation.The minimum unit of curation is: a genetic variant, tumor type and the scope of the study (e.g., which genes were tested). In addition, whenever reported by the publication, other clinical features for the patient are curated (e.g., age, gender, ethnicity, therapeutic history, family history of cancer or exposure to DNA-damaging agents). At the tumor level, the curation team extracts information on cancer stage and grade, metastases, drug response and therapy relationship (e.g., if a sample was collected prior to, during or post-therapy).


**Figure 2. The COSMIC data curation flowchart.** Depending on the data source and curation objectives, there are three main curation paths in COSMIC (graphic from Sondka et al., 2024).


### How HSMD's cancer data supports oncology drug development


HSMD is a web-based application that allows biopharmaceutical researchers and clinical NGS testing labs to harness genetic insights from real-world oncology dataset of QIAGEN, enriched with knowledge from two decades of expert curation.


In the latest version of HSMD, the resource focuses on providing deep insight into small variants, such as SNVs, indels, frameshifts, fusions and copy number variants that have been clinically observed or curated from scientific literature to help users better understand and define precise function and actionability. This expert-curated resource contains content from over 870,000 real-world clinical oncology cases combined with content from the QIAGEN Knowledge Base (QKB), providing gene-, alteration- and disease-level information.


HSMD enables users to easily search and explore mutational characteristics across genes, receive detailed annotations for each observed variant and synthesize key findings from drug labels, clinical trials and professional guidelines (Figure 3).


**Figure 3. HSMD's home screen.** HSMD enables users to search by gene, alteration, disease, drugs and clinical trials.


### HSMD's expert curation process


HSMD leverages variant content from two sources: expert-curated content from the QIAGEN Knowledge Base (QKB) and data from real-world oncology cases sourced from our professional clinical interpretation services (Figure 4).


When a variant has been “clinically observed”, it means our professional clinical interpretation service has encountered this alteration in a real-world clinical case. For these variants, our team will have assessed the clinical and biological relevance and calculated the gene and variant prevalence across observed tumor types. Conversely, content from the QKB is proactively curated from scientific literature; therefore, not all variants have yet been directly clinically observed by our professional clinical interpretation services.


**Figure 4. The HSMD curation workflow.** HSMD contains content from the QKB, which pulls information from all public and proprietary databases, clinical articles for the most relevant cancer genes and thousands of clinical articles for somatic genes. Curation then occurs by artificial intelligence (AI) approaches, manual curation or a combination of both. All content then goes through rigorous quality control to ensure consistency, accuracy and reproducibility. In addition, HSMD contains content from over 585,000 somatic mutations submitted to our professional variant interpretation service, QCI Precision Insights (formerly N-of-One). This is de-identified patient data that provides even greater insight into real-world clinical cases.


### Trusted cancer data to accelerate drug discovery and development


COSMIC and HSMD are two expert-curated knowledgebases licensed exclusively through QIAGEN that enable biopharmaceutical companies to improve the drug discovery process, develop more effective clinical trials and enhance the treatment of rare cancers. To learn more about how your research team can use COSMIC and HSMD, visit our product webpage or click the button below for a free trial and personal consultation with our biopharmaceutical research experts.


[COSMIC & HSMD for biopharma](https://digitalinsights.qiagen.com/cosmic-hsmd-biopharma/)[Request free trial](https://go.qiagen.com/LP=4587)
