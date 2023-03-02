![](https://img.shields.io/badge/language-R_and_Python-orange.svg) ![version](https://img.shields.io/badge/GiHub_version-1.1.0-519dd9) ![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin) ![GitHub issues](https://img.shields.io/github/issues/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin)

![dependencies](https://img.shields.io/badge/dependencies-up%20to%20date-orange)  	![commit](https://img.shields.io/github/last-commit/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin
) ![GitHub](https://img.shields.io/github/license/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin
)

![image](https://user-images.githubusercontent.com/22052679/221128568-256b9940-ae3a-442e-bcc8-df2277842054.png)

[![Edit with Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin
) 

- [Summary](#summary)
- [Single-nuclei RNA-seq data](#single-nuclei-rna-seq-data)
  * [Preprocessing](#preprocessing)
  * [Analysis pipeline](#analysis-pipeline)
- [Data and analysis](#data-and-analysis)
- [License](#license)
- [References](#references)

# Coupling of oxytocin and cholecystokinin pathways in the hypothalamus is required for gut-to-brain homeostatic feeding control
<img src="https://github.com/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin/blob/main/graphical%20abstract.jpeg" align="center" height="640" width="730">

# Summary
Gut-to-brain communication is pivotal for the regulation of energy homeostasis and its underlying biology is thus piquing great interest in the face of the current obesity pandemic. The emergence of several druggable targets within this communication has now motivated us to systematically interrogate the hitherto elusive intricacies of an alternative pathway that might hold considerable potential. By employing a series of electrophysiological, transcriptomic, and behavioral approaches, we here document novel insights suggesting that obesogenic diets promote reduced CCKA receptor expression and enhanced inhibitory κ-opioid tone, which together constitute a major mechanism to restrain hypothalamic paraventricular oxytocin (PVNOT) neuronal activation to respond to gut-derived anorexigenic cues.
We summarize our main findings as follows:

-	Selective, adult-onset ablation of PVNOT neurons in mice leads to hyperphagic obesity on a standard chow diet, which is rectifiable by pharmacological OT substitution.
-	Mice devoid of PVNOT neurons fail to suppress food intake in response to CCK.
-	CCK robustly induces electrophysiological and transcriptional modifications in PVNOT neu-rons of lean, but not diet-induced obese mice.
-	Chemogenetic activation of PVNOT neurons is sufficient to restore CCK-evoked hypo-phagia despite a high-fat high-sugar (HFHS) diet.
-	Rational combination of OTR and CCKAR agonism confers superior metabolic outcomes over respective monoagonist administration in diet-induced obese mice.
-	Intersecting subpopulations of hypothalamic OT neurons are co-regulated by CCKAR and κ-opioid receptors dependent on dietary context as revealed by single-nuclei RNA-seq.
-	Enhanced κ-opioid tone constitutes a major mechanism restraining PVNOT neuronal acti-vation by CCK under HFHS diet feeding.

We believe that our findings provide a deeper understanding of how peripheral and central satiation pathways converge, and how they are altered in disease states such as obesity. Moreover, we report new insights into the molecular heterogeneity of the OT system and its interactions with gut-hormone signaling, which we are sure will draw significant attention and spur future lines of investigation.

## Single-nuclei RNA-seq data

### Preprocessing
Raw reads were aligned to mm10 and ERCC92 reference using STARa2.7.1a. PCR duplicates were removed using picard tools v2.20.2 before building the count matrix using htseq-count v0.11.3

### Analysis pipeline
1. Filtering:
 - Nuclei are kept if they have 5-90% ERCC reads and at least 1000 genes expressed.
 - We keep genes that are present in at least 1% of the population with at least 250 reads across nuclei
 - Nuclei with more than 7,000 are removed as well as nuclei with library sizes outside the range of 10,000-300,000
2. Normalisation
 - ERCC size factor is calculated as the sum of ERCC reads per nucleus divided by the mean ERCC reads across all nuclei
 - Per gene, the reads are divided by the length of the gene in kb
 - The library size normalisation factor is defined as the sum of gene length-normalised counts divided by 10,000 times the ERCC size factor
 - Per nucleus, the reads are divided by the library size normalisation factor
 - Additional filtering: removing nuclei with more than 50,000 gene length-normalised counts and removing technical replicates Matrix is log-transformed      and batch-correction is done using combat

3. Downstream analysis
 - Visualisation, clustering and differential expression analysis using scanpy functions
 - Cluster annotation based on differential expression and marker genes
 - Gene set enrichment analysis using gprofiler
 - Transcriptional variability is defined as the coefficient of variation calculated on log-transformed data
 - Co-expression of stem cell markers is addressed by calculating Jaccard distances between genes
 - Diffusion pseudotime is calculated on markers of zonation to establish an in-silico order of nuclei along the liver lobule based on their expression        profiles

## Data and analysis
All the data required for performing the analysis and publisch in the reference articles will be soon deposited in the National Center for Biotechnology Information Gene Expression Omnibus (GEO) and are accessible through the GEO Series accession numbers:
| Data type     | GEO number | Notebook |
| ------------- | ------------- | ------------- |
| Transcriptomics  | __`GSE...`__  | [RiboTag_RNAseq-analysis.ipynb](https://github.com/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin/blob/main/RiboTag_RNAseq-analysis.ipynb) |
| Singel-Nuclei RNA-Seq  | __`GSE...`__| [snRNAseq_analysis.ipynb](https://github.com/viktormiok/snRNAseq_RiboTagRNAseq-oxytocin/blob/main/snRNAseq_analysis.ipynb)  |

In order to access one of the data set for instance GSE78279 you need to run the code bellow. Unpacking the data requires tar and gunzip, which should already be available on most systems.

```
cd ../  #To get to the main github repo folder
mkdir -p data/AstrocytesHeterogenityARC/
cd data/AstrocytesHeterogenityARC/
wget ftp://ftp.ncbi.nlm.nih.gov/geo/series/GSE78nnn/GSE78279/suppl/GSE78279_RAW.tar
mkdir GSE78279_RAW
tar -C GSE78279_RAW -xvf GSE78279_RAW.tar
gunzip GSE78279_RAW/*_Regional_*
```
## License

__`snRNAseq_RiboTagRNAseq-oxytocin`__ is distributed under the GPL-3.0 License. Please read the license before using __`snRNAseq_RiboTagRNAseq-oxytocin`__, which it is distributed in the `LICENSE` file.


## References

Publications related to __`snRNAseq_RiboTagRNAseq-oxytocin`__ include:

- Gruber, T., Lechner F., Murat C., Contreras R.E., Sanchez-Quant E., Miok V., Le Thuc O., Gonzales-Garcia I., Williams R.H., Pfluger P.T., Mueller T.D., Woods S.C., Martinez-Jimenez C.P., Tschoep M.H., Grinevich V., Garcia-Caceres C.(2021), Coupling of oxytocin and cholecystokinin pathways in the hypothalamus is required for gut-to-brain homeostatic feeding control", bioRxiv, 4(1).


Please cite the publication if you use __`snRNAseq_RiboTagRNAseq-oxytocin`__.

