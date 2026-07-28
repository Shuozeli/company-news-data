---
schema_version: "1.0.0"
document_id: "d5313ef7c2831986668e4dfba3ba7cedc59bf50207de836e8098182a73ed5565"
company_key: "crowdstrike-holdings-inc-class-a-common-stock"
company: "CrowdStrike Holdings Inc. Class A Common Stock"
source_id: "crowdstrike-holdings-inc-class-a-common-stock-news-import-26dc963e5592"
canonical_url: "https://www.crowdstrike.com/en-us/blog/crowdstrike-researchers-develop-custom-xgboost-objective/"
published_at: null
first_seen_at: "2026-07-25T01:07:09.054440+00:00"
fetched_at: "2026-07-28T21:36:14.883471+00:00"
content_hash: "sha256:023fa771998c5fc3001358d10367f8842029f8280ce8bd0978d66a9a6492f204"
---

# CrowdStrike Researchers Develop Custom XGBoost Objective to Improve ML Model Release Stability

- Extreme Gradient Boosting (XGBoost) is a valuable tool for training machine learning (ML) classifiers, which often come with the problem of surprise false positives (FPs) and false negatives (FNs).
- Surprise FPs consume threat researcher bandwidth and have a negative impact on customer confidence.
- CrowdStrike data scientists have developed a practical XGBoost custom objective function that retains the advantages of XGBoost while delivering more predictable model behavior, which reduces threat researcher cycles lost to surprise FP remediation.


Research is the cornerstone of CrowdStrike’s focus on innovation, and it enables us to stay a step ahead of the most sophisticated adversaries. The work of our dedicated team of researchers and data scientists is reflected in the industry-leading protection delivered by the AI-native CrowdStrike Falcon® platform. This team is not only involved in groundbreaking new developments — it is also constantly exploring ways to make existing cybersecurity technology more effective. This is the case with the newly identified (patent-pending) method for improving XGBoost in the use of ML model training.


CrowdStrike data scientists have identified a method for improving XGBoost classifier consistency between releases. This new XGBoost training method results in more predictable model behavior and less disruption in customer environments when new models are deployed. In addition, threat researchers spend significantly less time remediating the surprise FPs that are a noted downside to successive releases of XGBoost models.


This blog post outlines the current challenge with using XGBoost, the issue of surprise FPs, and the solution of an XGBoost custom objective function.


## The Surprise FP Problem


XGBoost is a popular ML algorithm for creating robust, high-accuracy classifiers. It is considered to be one of the leading ML libraries for classification, regression, and ranking problems. With support for parallel processing, XGBoost can train models efficiently and quickly.


However, there is a complication: Successive releases of XGBoost models — even when trained on the same data — can exhibit significant shuffling of detection probabilities on a fixed ordered test set of portable executable files. This shuffling represents a hidden risk within model deployment because models with a propensity for detection probability — or “decision value” (DV) — shuffling are unpredictable with respect to previously observed behavior. This unpredictability comes in the form of FNs and FPs. The objective leveraged to optimize XGBoost models can be manipulated to improve consistency between model releases, resulting in safer customer environments.


An organization that deploys ML classifiers to customers must ensure each model release represents an improvement over the previous version. To accomplish this goal, understanding what constitutes an improvement from the customer’s point of view is key. An ML classifier considered in isolation should be optimized according to receiver operating characteristic (ROC) curve behavior near critical thresholds. However, no customer-facing ML classifier exists in isolation, so optimizing the model cannot be confined to maximizing the efficacy of a single release. Rather, developers must frame the optimization problem in terms of customer experience over time and through an ongoing series of model releases. In what follows, we will refer to successive model releases as “model N” and “model N+1.”


In the security space, endpoint malware detection models serve as the front line of defense against adversaries. Because the base rate of actual malware is low compared to that of benign files, the problem that plagues customers most often is FPs. Security analysts spend too much time investigating FPs. This hurts the SOC’s ability to respond quickly to real threats and contributes to alert fatigue.


FPs can be classified into two categories.


The first category consists of clean samples that are new to the customer environment and that the model falsely classifies as dirty. Minimizing FPs in this first category is a complex problem that can only be addressed by improvements in the subsequent model or by near real-time allowlisting.


The second category consists of surprise FPs. A surprise FP is a clean sample that is known within the customer environment such that the previous model scored it as clean and the new model has falsely scored it as dirty. This latter category is especially pernicious due to valuable threat researcher time being wasted and confidence in prior releases being lost by the customer. Remediating FPs in this category is therefore critical and can be accomplished by first understanding the mathematical root of surprise FPs.


## The Root of Surprise FPs


ML binary classifiers typically output a float within a fixed range of values. Model developers then set a threshold to transform a float output by the model into a binary decision. The best method for setting a threshold is tying it to a target FP rate (FPR), as the expected behavior for the model at that threshold can then be quantified. Because of different initial conditions (new data, different hyperparameters, etc.) in model training between releases, successive models can operate differently on the same sample. These differences manifest as different DVs between two successive models for the exact same set of samples.


DVs that vary from one model to the next are not necessarily a problem if the ordering remains the same. Indeed, because thresholds are set by the target FPR, if all DVs shift down by some small value , then the given threshold would shift by the same value, resulting in equal model behavior. However, successive model releases do not typically preserve DV ordering. The far more common shuffling of DVs is what is responsible for surprise FPs.


### Connecting DV Shuffling to Surprise FPs


DV shuffling can be visualized by considering a DV density plot, as shown in the chart below. The probability density of clean sample DVs is green, and for dirty samples, the probability density is red. Along the sample space axis we have exactly two clean samples presented as green dots. The leftmost green dot is scored dirty by model N and clean by model N+1, as indicated by the left-oriented blue arrow. The other sample is scored clean by model N and dirty by model N+1, as indicated by the right-oriented blue arrow. The red boundary around the rightmost instances of the green dots indicates a clean sample that is falsely scored as dirty by a given model version.


Figure 1. Clean samples which move from below to above the threshold between model iterations are ‘swap-in’ false positives, and clean samples which move from above to below the threshold are ‘swap-out’ false positives. The latter could also be described as a ‘swap-in’ true negative.


Consider the following simple example consisting of a training set with exactly 10 clean samples and a threshold defined by a target 10% FPR.


Figure 2. The impossibility of swap-in false positives in the absence of decision value shuffling can be visualized as the sliding of the threshold to maintain the fixed target false positive rate.


The existence of a sample whose DV moves from above to below a given threshold necessitates the existence of a companion sample whose DV moves from below the same threshold to above it. This is true because otherwise, the FPR for that threshold would change. The result is the reordering of the DVs corresponding to these companion samples.


Figure 3. A rank order change between a given clean sample and the threshold necessitates a rank order change between the given sample and another clean sample if the threshold value is set based on a target false positive rate.


All of this means that if we want to minimize surprise FPs between model releases, we must ensure DV ordering preservation.


XGBoost is flexible because its Newton-Raphson solver requires only the gradient and Hessian of the objective rather than the objective itself. By adding small perturbations to the gradient and to the Hessian, we can replace the standard XGBoost objective function with one that includes a loss for failing to rank DVs according to the DV ranking defined by the previous model release, thereby promoting model release stability.


## Mathematical Description of XGBoost Optimization


The following, up to but not including the example, is taken predominantly from the[XGBoost Project docs](https://xgboost.readthedocs.io/en/stable/tutorials/model.html) . The XGBoost model consists of an ensemble of trees


such that


The objective function we leverage for training the binary classifier is the binary logistic loss function with complexity regularization


where


and


For each iteration *(t)* the goal is to find *ft* that minimizes *obj(t)* . In the case of a neural network, loss minimization requires computing the rate of change of the loss with respect to the model weights. In the case of XGBoost, we compute the second-order Taylor expansion of the loss *l* and provide the gradient and Hessian to the Newton-Raphson solver to find the optimal *ft* given previously constructed trees *f(s<t)* .


The second-order Taylor expansion of the objective takes the form


where


The upshot is that if we want to customize the XGBoost objective, we need only provide the updated gradient *gi* and Hessian *hi* .


A note to the observant reader (not from the docs): In the above expansion, the loss function


is being expanded around


where the independent variable is in the form


and


Computing


gives


For the sake of making these equations more interpretable and concrete, assume we have a sample x such that the XGBoost model *f* outputs *0.2 = p = f(x)* , and assume we have a true label *y* = 1. The gradient of the logistic loss for this sample is *g = p-y = -0.8* . This will encourage the *(t+1)st* tree to be constructed so as to push the prediction value for this sample higher.


The adjustment to the gradient and Hessian are then


and


respectively.


The takeaway is that a negative gradient pushes the prediction value and therefore the DV higher, as the sigmoid function is everywhere increasing. This means that if we want to customize the objective function in such a way that the DV of a given sample is pushed higher as subsequent trees are added, we should add a number *v<0* to the gradient for that sample.


## An Intuitive Toy Example


Assume we have sorted the samples in the training corpus of model N by DV in ascending order and stacked the remaining samples below. Assume *ypred =* \[1,2,3,4,5,7,6\]. The resulting addition to the gradient should be something like \[0,0,0,0,0,1,-1\]. The intuition is that we want to move the prediction of the sample whose current prediction is 6 a little higher and the prediction of the sample whose current prediction is 7 a little lower. Keep in mind that the ordering in terms of row position of the underlying samples in the train set is correct by assumption. This will enforce the proper ordering of \[1,2,3,4,5,6,7\].


## Experiments, Code, and Results


### Experimental Setup


Each experiment consists of training exactly three XGBoost binary classifier models on a set of 90/10 dirty/clean PE files. Featurization was performed with an internally developed static parser, but the method itself is agnostic to the parser. One could leverage the EMBER open-source parser, for example. The first model represents the “N” release trained with the standard XGBoost logistic loss objective. We call this the “old” model. The second model represents the standard “N+1” release trained with the same objective as the “old” model but with 10% more data and the same label balance. We call this the “full” model. The third model represents the candidate “N+1” release trained with the custom objective described above and on the same dataset as the “full” model.


We ran two separate experiments, differing only in the number of training samples. The custom objective succeeded in reducing swap-in or “surprise” FPs with a minimal trade-off in true positives.


### Results


Table 1. 119,494 samples: objective restricted to clean DVs within 5% and 80% target FPR thresholds, weight multiplier for *g i = 1e - 11* **Comparison** **Swap-Ins** **Persistent FPS** **Non-Swap New FPS** **Total FPS Old Model** **Total FPS New Model** **Total TPS Old Model** **Total TPS New Model**


Old vs. Full 32 194 23 226 250 25,267 28,111


Old vs. Candidate 26 ****(18.75%)**** 199 25 226 250 25, 267 28,104 **(0.025%)**


Table 2. 284,657 samples: objective restricted to clean DVs within 5% and 80% target FPR thresholds, weight multiplier for *gi = 1e - 11* **Comparison** **Swap-Ins** **Persistent FPS** **Non-Swap New FPS** **Total FPS Old Model** **Total FPS New Model** **Total TPS Old Model** **Total TPS New Model**


Old vs. Full 59 382 56 446 497 62,157 69,059


Old vs. Candidate 53 **(10.2%)** 387 56 446 497 62,157 69,053 **(0.009%)**


### Python Implementation


The perturbation value we decided to use was simply the difference between the pred values of each pair of misordered samples (ordered according to DV output by model N, or “old” model). Note that this requires a perturbation to the Hessian as well. This code assumes the values in the argument “y_pred” are ordered according to values output by model N. Take care to note that this does not mean these values are ordered as on the real number line. The scipy function expit is the sigmoid function with built-in underflow and overflow protection.


The callable CustomObjective class instantiation is then passed to the standard xgb.train function. Incidentally, the callable class is another way, in addition to lambda functions, to pass additional arguments to Python functions called with a signature restriction on the number of arguments.


## Employing an XGBoost Custom Objective Function Results in More Predictable Model Behavior with Fewer FPs


XGBoost classifier consistency between releases can be improved with an XGBoost custom objective function that is easy to implement and mathematically sound, with a minimal trade-off in true positive rate. The results are more predictable model behavior, less chaotic customer environments, and fewer threat researcher cycles wasted on surprise FP remediation.


## CrowdStrike’s Research Investment Pays Off for Customers and the Cybersecurity Industry


Research is a critical function at CrowdStrike, ensuring we continue to take a leadership role in advancing the global cybersecurity ecosystem. The results of groundbreaking work — like that done by the team who conducted the research into the XGBoost custom objective function — ensure CrowdStrike customers enjoy state-of-the-art protection and advance cyber defenses globally against sophisticated adversaries.


#### Additional Resources


- *CrowdStrike was named a Leader in the 2024 Gartner® Magic Quadrant™ for Endpoint Protection Platforms and was positioned furthest right in Vision and highest in Ability to Execute.[Read about it here](https://www.crowdstrike.com/en-us/resources/reports/gartner-mq/)[.](https://www.crowdstrike.com/blog/crowdstrike-named-leader-2023-gartner-magic-quadrant-for-epp/)*
- *Find out how the Falcon platform stops breaches, saves time, and saves money in this IDC analysis:[The Business Value of the CrowdStrike Falcon XDR Platform](https://www.crowdstrike.com/resources/white-papers/idc-security-consolidation-with-crowdstrike/) .*
- *See the Falcon platform in action —[sign up for a free demo](https://www.crowdstrike.com/products/demos/) today.*
