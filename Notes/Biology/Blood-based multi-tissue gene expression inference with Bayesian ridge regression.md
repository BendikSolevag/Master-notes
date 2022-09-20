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
To reduce the dimension of the feature space, we quantify the linear dependencies of target genes in tissue Tk on feature genes in B and select a small set of the most relevant B features for each target gene q expressed in Tk.

- Step 1: for each target gene qq⁠, we compute coefficient of variation (⁠cv = δ/μ⁠) of each features and rank them in descending order. We select those top 10% features to construct a low-dimensional new subsets.
- Step 2: next, we further reduce the dimension of feature space. yi(q) of a group of samples forms an expression value vector y(q) and expression value vectors of feature genes form the columns of matrix x0(q)⁠. We assume that one feature gene is important when the absolute of cosine similarity between vector y(q) and the corresponding column of x0(q) is close to 1


### 3.1 Construction of optimal feature sets

The optimal feature sets of gene expression inference are tissue-specific. We consider a given feature set as the best for a specific tissue when the baseline model trained with this reduced feature sets have both the smallest average MAE and the largest average rr in the serial experiments of this tissue’s target gene expression inference tasks. For each tissue, we do experiments with feature number range of [5, 10, 15, 20, 25, 30], rank the experiments by average MAE in ascending order. The ranking #1 experiment represents the optimal feature set in each tissue with respect to MAE. We observe that the optimal feature number is constantly 5 according to MAE metric and 5 ∼ 15 according to r metric.


### 3.2 Usage pattern of selected blood features

We define the feature gene usage as how many times a specific feature gene has been selected across all target genes of a tissue. We calculate the usage of blood genes in each target tissue then categorize 2942 blood genes as 5 groups by usage counts: ‘0’, ‘11∼10’, ‘11∼100’, ‘101∼400’ and ‘401∼’. The usage pattern of feature genes with respect to 26 tissues suggests that there are two clusters. The results agree with the fact that blood expressing genes have intricate correlations with tissue expressing genes.

We then focus on the most frequently selected feature genes by each tissue. Taking a union of top 10 feature genes from each tissue, a representative set of 112 most frequently selected feature genes was made. Here, 97.1% of most frequently selected blood genes are shared by two tissues; 90.2% of most frequently selected blood genes are shared by three and more tissues. The results suggest that a small proportion of blood genes of highest usage indeed has both strong and broad gene expressing correlation with multiple tissues.

### 3.3 Performance of inference models

Gene expression inference using blood gene expression profile may not be successful for all genes and all tissues. As quality check point, we designed two assessment rules to help decide whether blood-based inference models are satisfactory for each gene and each tissue.
- Rule 1, if target gene’s MAE < 0.7 and r > 0.3⁠, the gene is predictable. 
- Rule 2, if the ratio of predictable genes to total genes > 0.2, the tissue is predictable. A total of 16 out of 26 tissues is considered predictable.

In all, BayR inference model outperforms the other candidate models in most of our experiments.


### 3.5 B-GEX inference of tissue-specific genes

To better understand the tissue-specific performance of B-GEX, we look closer at B-GEX performance on a published set of more than 2000 tissue-specific genes named TissGene. We found that the gene-level MAE and rr distribution of one tissue’s TissGenes under B-GEX inference model are comparable to that of the tissue’s non-TissGenes. This observation shows B-GEX can infer the expression level of tissue-specific genes as well as other target genes and further validated the B-GEX model has no bias toward genes.


### 3.6 Usage guide of B-GEX

Our results suggest that the method can partially infer gene expression of 16 predictable tissues out of 26 available tissues and robustly infer gene expression of 20%∼60% genes in a given tissue.


## 4 Discussion

In this article, we present a machine-learning method for gene expression inference in multiple tissues using gene expression level in whole blood. B-GEX depends on blood-tissue transcriptome correlation and only requires user to input gene expression profile of blood.

B-GEX model used multi-task linear regression to address ‘cross-tissue’ inference. Similar design has recently been used to do ‘within-tissue’ gene expression inference. ‘within-tissue’ inference focus on how to complete an expression profile based on partially measured expression profiles.

By comparing four inference models, we have shown that B-GEX outperforms the baseline LSR and its two derivative models on GTEx RNAseq data. LSR-L2 inference model is a competitive model in target genes of several tissues. We believe more accurate inferences of gene expression can be achieved if complicated models or latent variable based models are developed in future.