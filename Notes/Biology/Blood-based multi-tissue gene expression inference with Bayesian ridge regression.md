https://academic.oup.com/bioinformatics/article/36/12/3788/5819142
# Blood-based multi-tissue gene expression inference with Bayesian ridge regression

Gene expression profiling can explain biological phenotypes by depicting transcriptional changes of tissues. Gene expression level of an affected tissue may be inferred from blood, a readily accessible specimen material in clinical field. The gene expression in blood is reported to be moderately correlated with that in brain tissues, and weakly correlated with that in immune and muscle tissues.

Gene expression inference in tissues usually requires prior knowledge of genotype-transcriptome associations. The performance of imputation relies largely on the completeness of the expression quantitative trait locus (eQTL) reference resource. Because these methods explicitly require genomic features (e.g. SNP genotype and eQTLs) as part of the predictors to infer unmeasured gene expression in target tissues, genotyping patients must be done before gene expression inference.

To the best of our knowledge, no available methods can infer gene expression of multiple tissues without genotype. Here, we present a machine-learning-based method for gene expression inference of multiple uncollected tissues using blood gene expression profile (B-GEX). We define multiple genes in blood as feature variables and each gene in another tissue as one target. 

To achieve this goal, we built an independent model for each target. We used ℓ1ℓ1-norm-based feature selection method to select the most significant correlated genes expressed in blood specific to the target gene. We adopted Bayesian ridge regression (BayR) to model the cross-tissue gene expression correlations between the features and the target. Finally, we explored the most frequently selected blood feature genes to interpret the clustering patterns revealed in the tissue-level comparisons.

The usable samples for tissue gene expression inference are defined as the samples in which both B and T<span style="font-size:10px">k</span> gene expression data are available. A total of 26 tissues have more than 100 usable samples and were chosen for further analysis. Our goal is to infer gene expression in T<span style="font-size:10px">k</span> (⁠k=1, 2, ⋯, 26) with gene expression in B⁠. The inference models are tissue-specific.





### 2.2 Framework of multi-tissue gene expression inference

We formulate an inference framework consisting of multiple tissue-specific models. In this framework, modelkmodelk is a multi-task regression model for inferring gene expressions of tissue Tk using gene expressions of tissue B as input.

Next, we consider how to solve the basic inference task ℱk(q)Fk(q)⁠. Its feature length PP is two orders of magnitudes larger than sample size NN⁠. So ℱk(q)Fk(q) is a typical high-dimensional low-sample-size problem.

### 2.4 Feature selection
