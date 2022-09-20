https://www.science.org/doi/10.1126/sciadv.abd6991?url_ver=Z39.88-2003&rfr_id=ori:rid:crossref.org&rfr_dat=cr_pub%20%200pubmed

# Predicting tissue-specific gene expression from whole blood transcriptome

GTEx - Genotype-Tissue Expression
WBGE - Whole Blood Gene Expression
WBT - Whole Blood Transcriptome
WBSp - Whole Blood Splicing
TSGE - Tissue Specific Gene Expression
TEEBoT - Tissue Expression Estimation using Blood Transcriptome
TSPG - Tissue Specific Predictable Genes

Most common complex (non-Mendelian) diseases involve dysfunction in multiple tissues organs. For instance, hypertension, which is characterized by elevated arterial pressure, involves metabolic changes in the heart, blood vessels, brain, kidney, etc.

Transcriptional variance mediates, in large part, causal links between genotype and complex traits. Thus, the knowledge of tissue-specific gene expression (TSGE) profile can lead to a better understanding of diseases etiology, enabling patient subtyping and assessing drug efficacy.

 A widely used tool, PrediXcan, predicts the TSGE of a gene based on the gene’s eQTL single-nucleotide polymorphisms (or eSNPs). However, a priori, such a tool has limited scope, as it can only predict expression of a minority of genes (about 10% genes on average across tissue) that have significant tissue-specific eSNPs. Furthermore, the previous prediction models based on blood expression do not use the expression of other genes to predict the expression of a given gene, missing on the possibility of exploiting potentially shared regulatory programs between tissues.

We proceed by building a linear model based on Genotype-Tissue Expression (GTEx) data for 32 primary tissues having at least 65 samples each. We find that an individual’s WBGE and splicing profile significantly inform tissue-specific expression levels (above and beyond various demographic variable) for substantive fractions of genes, with a mean of 59% of genes across 32 tissues, up to 81% for muscle-skeletal tissue, based on likelihood ratio test with false discovery rate (FDR) threshold of 5%. We find that the genes with highly predictable expression are not biased toward housekeeping genes, proportionally representing tissue-specific genes. Moreover, these genes tend to have a greater number of protein interaction partners, which may suggest a contribution by shared gene networks toward expression predictability. Last, in many cases, the predicted tissue-specific expression can be used as a surrogate for actual expression in predicting disease state for several complex diseases far better than using the whole blood expression.

Pipeline uses readily available information, such as WBT, their genotype, and basic demographic information (age, sex, race).

Normalized expression data were obtained from GTEx V6 for 32 primary tissues (60% of all tissues) for which both the gene expression and WBT were available for at least 65 individuals.


## Models
For each tissue and for each gene, we have fit three nested regression models to estimate TSGE: The <strong style="color:lightpink">prime model</strong>, whose results are described in the main text, is based on WBGE, WBSp information, and three demographic confounding factors—age, race, and sex.

To assess the value of using splicing information, we additionally built and tested our base model, “WBGE + CF” model (M1), which uses only the WBGE PCs and CF variables.

Last, to estimate the contribution of SNPs, we fit a third “WBGE + WBSp + SNP + CF” model (M3); although this model is most inclusive, it covers only a small fraction of about 10% of the genes, those having at least one eSNPs, as reported previously by the GTEx consortium.

### The predictive power of WBSp and expression information (the M2 model)

For each of the 17,031 genes, in each of the 32 tissues, we fit the regression model M2 and estimate the CV accuracies using a Pearson correlation coefficient (PCC) between the predicted and observed expression across individuals. First, as baseline, we assessed the contribution of WBT over the demographic CFs via a LLR test and found that, on average, across tissues, for 59% of genes, WBT makes a significant contribution toward TSGE prediction, with a maximum of 81% of the genes in the muscle-skeletal tissue.

While SNPs are expected to contribute to TSGE prediction, as mentioned earlier, SNP-based prediction is applicable to ~10% of the genes that have a significant eSNP.

We have also compared model M2 with an SNP-only model M4 that we have constructed (comparable to a previous tool PrediXcan) and found that overall WBT is a better predictor of TSGE than eSNPs alone. We also found that genes that have eSNPs exhibit greater predictability by M2, although M2 does not include SNPs


### Characteristics of genes whose TSGE is predictable by WBT (model M2)

In each tissue, we identified TSPG as the genes for which WBT contributed significantly relative to CF and were among the top 25% most predictable based on CV PCC. First and quite notably, we observe that the TSPGs were quite different in each tissue.

By and large, TSPGs are enriched for numerous fundamental cellular processes, including metabolic processes, RNA processing, translation, transcription, etc. But notably, in a few cases, there is an enrichment for highly tissue-specific or tissue-relevant processes, such as “cardiac muscle cell action potential” in the heart and “cell morphogenesis involved in neuron differentiation” in the nerve.


Next, we assessed whether the predictability of TSPG may be related to their interactions with other genes, which tend to be functionally related and have similar expression profile. TSPGs have much greater connectivity, both overall, and relative to housekeeping genes.

For each of the most highly predictable genes _g_ in a tissue (PCC ≥ 0.7), we tested whether _g_ preferentially interacts with those genes whose expression values are most predictive of _g_’s TSGE. In 11 of the 12 tissues in which we could test this hypothesis, it is supported.

Tissue specific prediction uses destinct features, particularly, those with higher expression in the specific tissue.

We ascertained that predictability of a particular gene _g_ is minimally dependent on the expression of gene _g_ in blood.


### Utility of WBT predicted tissue-specific expression in predicting complex diseases

Last, we assessed the extent to which the predicted TSGE can reveal tissue-specific disease-associated genes (DGs) and predict disease states. We first assessed the extent to which DGs, ascertained based on observed TSGE, can be identified on the basis of the predicted TSGE.

We then quantified the accuracy with which the predicted TSGE could distinguish DGs from the rest of the genes. As shown in table S6, on average, across 83 cases, predicted TSGE could distinguish DGs from the other genes with an area under the receiver operating characteristic curve (auROC) of 0.6 (with 19 cases having >0.7 of auROC). In contrast, WBGE failed to predict DGs (average auROC of 0.52 with zero cases having >0.7 of auROC).



Next, we assessed the extent to which the TSGE can predict the disease state. For this, in each disease-tissue pair, we used the genes that were highly predictable in the tissue from WBGE (LLR FDR ≤ 0.05 and PCC ≥ 0.3) as features for building the pertaining disease/control predictors. We then compared the prediction accuracy when using their (i) actual TSGE, (ii) predicted TSGE, and (iii) WBGE (see Methods).

These results show that (i) the accuracies using the predicted TSGE is comparable to those using observed TSGE (average fractional difference = 0.3%), (ii) predicted TSGE performs substantially better than WBGE (average fractional difference = 12%). Overall, these results suggest that predicted TSGE can provide insights into tissue-specific disease-linked genes, can predict disease-state, comparable to observed TSGE, and is superior to WBGE.