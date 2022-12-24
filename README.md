## Coupling of oxytocin and cholecystokinin pathways in the hypothalamus is required for gut-to-brain homeostatic feeding control

## Summary
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

## Data accessibility
The raw data not yet available.

## Preprocessing
Raw reads were aligned to mm10 and ERCC92 reference using STARa2.7.1a. PCR duplicates were removed using picard tools v2.20.2 before building the count matrix using htseq-count v0.11.3

## Analysis pipeline
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
