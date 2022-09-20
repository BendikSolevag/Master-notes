ahttps://www.science.org/doi/10.1126/sciadv.abd6991?url_ver=Z39.88-2003&rfr_id=ori:rid:crossref.org&rfr_dat=cr_pub%20%200pubmed

# Predicting tissue-specific gene expression from whole blood transcriptome

GTEx - Genotype-Tissue Expression
WBGE - Whole Blood Gene Expression
WBT - Whole Blood Transcriptome
WBSp - Whole Blood Splicing
TSGE - Tissue Specific Gene Expression
TEEBoT - Tissue Expression Estimation using Blood Transcriptome

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


For each of the 17,031 genes, in each of the 32 tissues, we fit the regression model M2 and estimate the CV accuracies using a Pearson correlation coefficient (PCC) between the predicted and observed expression across individuals.