---
schema_version: "1.0.0"
document_id: "f63fe8c8d4f6c6848bd940d62d19407120a55280a9d5f4ae48ae4553583b0659"
company_key: "certara-inc-common-stock"
company: "Certara Inc. Common Stock"
source_id: "certara-inc-common-stock-news-import-6fa26b21f70d"
canonical_url: "https://www.certara.com/blog/63-runs-and-no-convergence-when-rsnlme-succeeded-where-others-couldnt/"
published_at: "2026-06-23T15:40:06+00:00"
first_seen_at: "2026-07-22T21:45:01.422888+00:00"
fetched_at: "2026-07-28T21:45:29.554500+00:00"
content_hash: "sha256:7e55eb6a64700160e36010c14841dfe88c0132be9d2b350d2859e93842cf57ac"
---

# 63 runs and no convergence: When RsNLME succeeded where other PK/PD solutions couldn’t

ShareShareShare


Stephen Duffull Senior Scientific Advisor, Quantitative Science Services (New Zealand)


June 23, 2026


Sometimes the most instructive project stories are the ones that didn’t go to plan. This case study started as a straightforward population PK/PD modeling project but ended up becoming an unexpected comparison of two modeling platforms, not by design, but by necessity.


The goal was to develop a population PK/PD model for drug-induced neutropenia. The model needed to accommodate the influence of rescue treatments, specifically granulocyte colony-stimulating factor (GCSF) and its longer-acting pegylated form (pegGCSF). The intended use was simulation: predicting the extent of neutropenia and estimating GCSF or pegGCSF dosing requirements to optimize patient outcomes.


The original plan was to use a tool that is widely known and used in the pharmacometrics world. It didn’t turn out that way.


## The Model: A Semi-Mechanistic ANC-GCSF Framework


Rather than building a neutrophil model from scratch, the team identified a suitable published model from Pastor et al. (2013)¹. The model had everything needed: GCSF, pegylated GCSF, and maturation dynamics for absolute neutrophil count (ANC).


The structure is worth describing briefly, because its complexity sets the scene for what followed.


At its core, the model follows a Friberg-style neutrophil framework: a proliferation compartment feeds into a series of maturation transit compartments, which in turn feed the circulating ANC – the observable endpoint. Both GCSF formulations can be administered as subcutaneous depot injections. The key biological feature is a feedback loop: circulating ANC drives receptor expression, and receptors bind and sequester GCSF. This means that when ANC falls, receptor levels drop, GCSF rises, and neutrophil production is stimulated, a self-correcting control mechanism. When ANC recovers, the system damps itself back down.


GCSF, notably, acts differently from standard feedback models: it not only stimulates proliferation but also decreases transit time through the maturation compartments, an important mechanistic distinction captured in the Pastor framework


The compound-specific PK was added as a standard two-compartment model with transit absorption from a depot site. Receptor states were calculated algebraically. In total, the final model comprised 16 ordinary differential equations — a level of structural complexity that places it firmly at the demanding end of population PK/PD modeling.


## The Planned Workflow


The analysis plan was systematic and pragmatic:


1. Recreate the Pastor model in R and reproduce key figures to confirm the model behaved correctly.
2. Translate the model from R into the target modeling software and verify that predictions matched.
3. Conduct a structural identifiability analysis on the Pastor model parameters and the available data.
4. Replace the original chemotherapy compound (carboplatin) with the compound of interest.
5. Run identifiability analysis on the redesigned model and data template.
6. Estimate the base PK/PD model, add covariates, and simulate dosing scenarios.


Steps 1 through 5 went smoothly. Step 6 was where things became difficult.


## When Estimation Refuses to Converge


The dataset contained approximately 55,000 records. This is not an unusual scale for nonlinear mixed-effects modeling, but combined with a 16-ODE system and a complex biological feedback structure, it created significant numerical demands on the estimation algorithms.


Estimation was conducted across a wide range of configurations in an effort to achieve stable convergence.


The estimation methods tested included FOCEI, SAEM, importance sampling, and the iterative two-stage EM algorithm. ODE integration was attempted using ADVAN6, ADVAN8, ADVAN13, and ADVAN14, with various combinations of SIGL/DIFFS/TOL settings. Subsets of the data – excluding particular studies or individuals – were also tested to improve stability.


In total, 63 runs were attempted. The results were consistent and discouraging.


SAEM, typically a robust workhorse for difficult models, would begin optimizing and then rapidly collapse to zero, the objective function simply flatlined. FOCEI produced integration errors and either terminated early or exceeded the maximum number of function evaluations. In some cases, estimation appeared to be progressing and then suddenly produced zero gradients that never recovered. FO was the only estimation method that completed successfully, but FO alone was insufficient for a model of this complexity.


Removing studies or individuals from the dataset did not resolve the instability. The problems were consistent across every configuration tried.


After several weeks of troubleshooting and effectively several months of accumulated project time, the decision was made to try RsNLME.


## Moving to RsNLME


RsNLME is an open-source R package that provides scripted access to the NLME engine, the nonlinear mixed-effects modeling engine embedded in Certara’s Phoenix platform. For someone accustomed to a command-line modeling workflow, RsNLME felt familiar: you write code, you run it, you get results. There’s no GUI required.


The migration involved several steps. The model was recoded from NMTran into PML, the Pharmacometric Modeling Language used by NLME. The same parameters that had been fixed in the original run were held fixed in RsNLME. A data format conversion was required – NLME uses wide-format data while the existing dataset was in long format – and a script was developed to handle this.


For estimation, the QRPEM method was used: a quasi-random parametric expectation-maximization algorithm purpose-built for NLME. Functionally it is comparable to SAEM; if SAEM would be the first choice for a problem of this complexity, QRPEM is the equivalent in NLME.


The model was integrated using the LSODA integrator and run across 10 cores. Runtime: 12.5 hours.


It converged. First attempt. Standard errors were produced. All goodness-of-fit plots looked appropriate. Further model development continued within the RsNLME framework, confirming that population PK/PD modeling of this scale is well within its capabilities.


As a final test, the converged model was exported back to the original platform and re-estimated with SAEM. It failed again. The RsNLME solution could not be replicated — a finding that underscores just how much numerical implementation details can matter in nonlinear mixed-effects modeling.


Certification course


## Learn RsNLME from the people who know it best


If this case study made you curious about RsNLME, Certara University’s live online certification short course is the place to go deeper. Stephen Dufull and Ana Henry walk you through the full modeling workflow – from writing PML code to simulation and covariate modelling – across six hands-on sessions starting September 28.


[Enroll in the RsNLME certification course](https://www.certarauniversity.com/store/5099338-203-live-cert-introduction-to-rsnlme-certification-short-course)


## Workflow Comparison


Looking back at the two approaches side by side, the workflow differences are significant.


The original workflow involved: recreating the literature model in R → verifying in R → translating to the estimation platform → verifying the translation → modeling the data → using external tools to evaluate the model → re-translating back to R for simulation → verifying the simulation code → running scenarios.


The RsNLME workflow collapses this considerably. Because the entire process – model coding, estimation, diagnostics, and simulation – lives within a single R-based ecosystem, there are no re-translations. The same code block used for estimation can be used directly for simulation. Packages like tidyVPC integrate naturally. Steps that previously required maintaining parallel code in two languages simply disappear.


## Reflections


A few observations worth drawing out from this experience.


**RsNLME offered genuine numerical stability advantages for this model.** It’s not that NLME did something magical. Both platforms are solving the same underlying mathematical problem. But for this particular 16-ODE model with a complex feedback structure and a large, heterogeneous dataset, NLME’s estimation algorithms proved considerably more stable than those of the original platform. Whether this reflects differences in how the algorithms are implemented, in how the ODE integration is handled, or in other numerical details is a question worth further investigation.


**The cost of switching platforms late is high.** The 63 runs spanned several weeks of compute time and several months of project calendar time. Had RsNLME been considered from the outset for a model of this complexity, that time could have been redirected to the actual pharmacological questions.


**The integrated simulation workflow is a meaningful advantage.** The overhead of maintaining synchronized model code across two platforms, whether using MRGsolve or other tools, is non-trivial. Translating, verifying, and re-translating creates real project risk. An integrated R-based workflow removes that friction entirely.


**Data and design quality still matter.** NLME is not a remedy for fundamentally poor data. If the study design or dataset itself were the source of identifiability problems, NLME would face the same limitations as any other platform. In this case, the problems appeared to be numerical rather than structural, and that’s where the platform choice made a difference.


*This case study was presented as part of a[webinar on NLME modeling approaches](https://www.certara.com/on-demand-webinar/pharmacometrics-under-pressure-part-3-the-wall-when-the-model-gets-harder-than-planned/) . The work was conducted in collaboration with colleagues including Ayman Akil, Adekemi Taylor, and Alice Toms, who developed the data format conversion script.*


On-demand webinar


## See the 63 failed runs and what finally worked


Stephen Dufull walks through this 16-ODE model, the 63 failed runs, and the RsNLME solution in our on demand webinar Pharmacometrics Under Pressure Part 3: The Wall. See every modeling decision, from platform switch to converged output, in under an hour.


[Watch now](https://www.certara.com/on-demand-webinar/pharmacometrics-under-pressure-part-3-the-wall-when-the-model-gets-harder-than-planned/)


## References


\[1\][https://link.springer.com/article/10.1007/s11095-013-1099-z](https://link.springer.com/article/10.1007/s11095-013-1099-z)


## Done fighting your estimator?


Ready to stop chasing convergence? RsNLME gives you NLME’s numerical power inside a fully R-based workflow – no GUI, no retranslations, just results. If a 16-ODE model with 55,000 records can converge on the first attempt, yours might too.


[Explore RsNLME](https://www.certara.com/software/r-speaks-nlme-rsnlme/)[Contact us](https://www.certara.com/contact-us)


## Author


[Stephen Duffull](https://www.certara.com/teams/stephen-duffull/) Senior Scientific Advisor, Quantitative Science Services (New Zealand)


Stephen provides advanced pharmacometrics guidance for complex drug development challenges.


## FAQs


### What causes convergence problems in nonlinear mixed-effects (NLME) modeling?


Convergence failures typically arise from complex model structures (such as high-dimensional ODE systems with feedback loops), large heterogeneous datasets, or mismatches between the estimation algorithm and the numerical demands of the model.


### How can RsNLME help with difficult PK/PD model estimation?


RsNLME provides access to the NLME engine’s QRPEM algorithm and LSODA ODE integrator within a fully R-based workflow, offering numerical stability advantages for complex models that fail to converge in other platforms.


### When should a different estimation approach be considered for an NLME model?


If standard methods such as FOCEI or SAEM produce integration errors, zero gradients, or objective function collapse across multiple configurations and datasets subsets, it is time to evaluate an alternative platform or estimation algorithm.


### Can RsNLME estimate large and complex population PK/PD models?


Yes, in this case study,


RsNLME


successfully estimated a 16-ODE semi-mechanistic neutropenia model on a dataset of


approximately 55,000


records, converging on the first attempt after 63 failures in another platform.


## You May Also Like


AllModeling and Simulation - PK/PD


[Phoenix Pharmacometrics Day – Korea​](https://www.certara.com/live-events/pmx-day-korea-2026/)


[Phoenix Pharmacometrics Day – Korea​](https://www.certara.com/live-events/pmx-day-korea-2026/)[Live Events](https://www.certara.com/category/live-events/)


### [Phoenix Pharmacometrics Day – Korea​](https://www.certara.com/live-events/pmx-day-korea-2026/)


[Phoenix Roadshow 2026 – Tokyo​](https://www.certara.com/live-events/phoenix-roadshow-tokyo-2026/)


[Phoenix Roadshow 2026 – Tokyo​](https://www.certara.com/live-events/phoenix-roadshow-tokyo-2026/)[Live Events](https://www.certara.com/category/live-events/)


### [Phoenix Roadshow 2026 – Tokyo​](https://www.certara.com/live-events/phoenix-roadshow-tokyo-2026/)


[Model smarter, not harder: How Phoenix Cloud puts the science back at the center of modeling](https://www.certara.com/blog/model-smarter-not-harder-how-phoenix-cloud-puts-the-science-back-at-the-center-of-modeling/)


[Model smarter, not harder: How Phoenix Cloud puts the science back at the center of modeling](https://www.certara.com/blog/model-smarter-not-harder-how-phoenix-cloud-puts-the-science-back-at-the-center-of-modeling/)[Blog](https://www.certara.com/category/blog/)


### [Model smarter, not harder: How Phoenix Cloud puts the science back at the center of modeling](https://www.certara.com/blog/model-smarter-not-harder-how-phoenix-cloud-puts-the-science-back-at-the-center-of-modeling/)
