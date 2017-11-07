---
author-meta:
- Venkat Malladi
date-meta: '2017-11-07'
keywords:
- enhancers
- transcription
- transcription factor
- epigenome
lang: en-US
title: Exploring Lineage-Specific Enhancers by Integrating Enhancer Transcription,
  Epigenomic Features, Sequence Motifs, and Transcription Factor Expression
...






<small><em>
This manuscript was automatically generated
from [vsmalladi/tfsee-manuscript@d873572](https://github.com/vsmalladi/tfsee-manuscript/tree/d873572a766c88335c1973f4d67d3edd7493ce1f)
on November  7, 2017.
</em></small>

## Authors



+ **Venkat Malladi**<br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0002-0144-0564](https://orcid.org/0000-0002-0144-0564)
    · ![GitHub icon](images/github.svg){height="13px" width="13px"}
    [vsmalladi](https://github.com/vsmalladi)
    · ![Twitter icon](images/twitter.svg){height="13px" width="13px"}
    [katatonikkat](https://twitter.com/katatonikkat)<br>
  <small>
  </small>



## Abstract {.page_break_before}

The identification of transcription factors (TF) driving the formation of active enhancers that regulate the expression of target genes remains an open problem.
We have developed a computational framework that identifies cell type-specific enhancers and their cognate TFs by integrating multiple genomic assays that probe the transcriptomes (GRO-seq and RNA-seq) and epigenomes (ChIP-seq) of various samples.
Our method, called Total Functional Score of Enhancer Elements (TFSEE), integrates the magnitude of enhancer transcription (GRO-seq), enrichment of marks associated with enhancers (H3K4me1 and H3K27ac ChIP-seq), TF mRNA expression levels (RNA-seq), and TF motif p-values (MEME).
This method has allowed us to explore the enhancer landscape in different cell types that share common origins or are biologically related, including distinct molecular subtypes of breast cancer, and embryonic stem cells (ESCs) and their derived lineages.
Using TFSEE, we have identified key breast cancer subtype-specific transcription factors that are bound at active enhancers and dictate gene expression patterns determining growth outcomes.
To demonstrate the broader utility of our approach, we have used this algorithm to identify transcription factors during the differentiation of embryonic stem cells into pancreatic cells.
Taken together our results show that TFSEE can be used to perform multilayer genomic data integration to uncover novel cell type-specific transcription factors that control lineage-specific enhancers.


## Introduction


## Results


## Discussion


## Acknowledgments


## Material and Methods {.page_break_before}

### Genomic Data Curation

We used previously published GRO-seq, ChIP-seq and RNA-seq data from [@BTqz3DNL; @18a6G1TE5] of time course differentiation of human embryonic stem cells (hESC) to pancreatic endoderm (PE). All data sets are available from NCBI’s Gene Expression Omnibus [@Bc3QGVe7] or EMBL-EBI’s ArrayExpress [@937jwJMM] repositories using the accession numbers listed in Table @tbl:data-sets.

| Assay | Accessions |
| :--- | :-------- |
| GRO-seq | GSM1316306, GSM1316313, GSM1316320, GSM1316327, GSM1316334 |
| H3K4me3 ChIP-seq | ERR208008, ERR208014, ERR207998, ERR20798, ERR207999 |
| H3K4me1 ChIP-seq | GSM1316302, GSM1316303, GSM1316309, GSM1316316, GSM1316317, GSM1316310, GSM1316323, GSM1316324, GSM1316330, GSM1316331 |
| H3K27ac ChIP-seq | GSM1316300, GSM1316301, GSM1316307, GSM1316308, GSM1316314, GSM1316315, GSM1316321, GSM1316322, GSM1316328, GSM1316329 |
| Input ChIP-seq | ERR208001, ERR208012, ERR207984, ERR208011, ERR207986, GSM1316304, GSM1316305, GSM1316311, GSM1316312, GSM1316318, GSM1316319, GSM1316325, GSM1316326, GSM1316332, GSM1316333 |
| RNA-seq | ERR266333, ERR266335, ERR266337, ERR266338, ERR266341, ERR266342, ERR266344, ERR266346, ERR266349, ERR266351 |

Table: **Description and accession numbers of GRO-seq, ChIP-seq and RNA-seq datasets.**
{#tbl:data-sets}

### Analysis of ChIP-seq Data Sets

The raw reads were aligned to the human reference genome (GRCh37/hg19) using default parameters in Bowtie version 1.0.0 [@RU8ikjzP]. The aligned reads are subsequently filtered for quality and uniquely mappable reads using Samtools version 0.1.19 [@IPc8cy7s] and Picard version 1.127 [@tfF98ztu]. Library complexity is measured using BEDTools version 2.17.0 [@1HWiAHnIw] and meet ENCODE data quality standards [@hvhWxir9]. Relaxed peaks were called using MACS version 2.1.0 [@Bhecn2fS] with a p-value of $1 \times 10^{-2}$ for each replicate, pooled replicates’ reads and pseudoreplicates. Peak calls that are replicated from the pooled replicated that are either observed in both replicates, or in both pseudoreplicates are used for subsequent analysis.

### Analysis of RNA-seq Data Sets

The raw reads were aligned to the human reference genome (GRCh37/hg19) using default parameters in STAR version 2.4.2a [@tTu8Ds9Z]. Quantification of genes against Gencode version 19) [@15rkMH6SD] annotations was done using default parameters in RSEM version 1.2.31 [@Dh2n1EV3].

### Analysis of GRO-seq Data

The GRO-seq reads were trimmed to the first 36 bases, to trim adapter and low quality sequence, using default parameters of fastx_trimer in fastx-toolkit version 0.0.13.2 [@jwUQ55cX].  The trimmed reads were aligned to the human reference genome (GRCh37/hg19) using default parameters in BWA version 0.7.12 [@roi5bwXL].

### Kernel Density

Kernel density plot representations were used to express the univariate distribution of ChIP-seq reads under peaks, RNA-seq reads for protein-coding genes and GRO-seq reads for short paired and short unpaired eRNAs.  The kernel density plots were calculated in Python (ver. 2.7.11) using the kdeplot function from [seaborn](http://seaborn.pydata.org/) version 0.7.1 [@qxfTM222] with default parameters.

### Defining Transcription Start Sites

We made distinct transcription start sites (TSS) for protein-coding genes from Gencode version 19 [@15rkMH6SD] annotations using MakeGencodeTSS [@tDy18Yol].  

### Enhancer calling by GRO-seq

#### *Transcript calling*.  

Transcript calling was performed using a two-state hidden Markov model using the groHMM data analysis package version 3.4 [@1BkIYUDLC; @1HVy2rbI; @lPKPHCBB] on each individual cell lines. The negative log transition probability of the switch between transcribed state to non-transcribed state and the variance in read counts in the non-transcribed state that are used to predict the transcription units for the cell lines are listed Table @tbl:groseq-tune.

| Cell Line | -Log Transition Probability | Variance in read counts
| :--- | :--------: | :--------: |
| hES | 50 | 45 |
| DE | 50 | 35 |
| GT | 50 | 50 |
| FG | 50 | 35 |
| PE | 50 | 35 |

Table: **groHMM tunning parameters.**
{#tbl:groseq-tune}

We then built a universe of transcripts by merging the groHMM-called transcripts from individual cell lines and stratifying the boundaries to remove overlaps/redundancies occurring from the union of all transcripts.

#### *Calling Enhancer Transcripts*.  

We filtered and collected a subset of short intergenic transcripts $<$ 9 kb in length and $>$ 3 kb away from known transcription start sites (TSSs) of protein-coding genes from Gencode version 19 annotations [@15rkMH6SD], and H3K4me3 peaks.  These were further classified into (1) short paired eRNAs and (2) short unpaired eRNAs as described previously [@1DE6cLccI].  For the short paired eRNAs, the sum of the GRO-seq RPKM values for both strands of DNA was used to call an enhancer transcript pair as expressed using a criterion of RPKM $\geq$ 0.5.  For the short unpaired eRNAs, an RPKM cutoff of $\geq$ 1 was used to call an enhancer transcript as expressed.  The universe of expressed eRNAs (short paired and short unpaired) was assembled using the cutoffs noted above for each cell line and was used for further analyses.

#### *Motif Analyses*.

De novo motif analyses were performed on a 1 kb region ($\pm$ 500 bp) surrounding the peak summit or the transcription start site for short paired and short unpaired eRNAs, respectively, using the command-line version of MEME from MEME Suite version 4.11.1 [@dwj6qSn3].  The following parameters were used for motif prediction: (1) zero or one occurrence per sequence (-mod zoops); (2) number of motifs (-nmotifs 15); (3) minimum, maximum width of the motif (-minw 8, -maxw 15); and (4) search for motif in given strand and reverse complement strand (-revcomp).  The predicted motifs from MEME were matched to known motifs in the JASPAR database (JASPAR_CORE_2016_vertebrates.meme) [@1DrZNoXOU] using TOMTOM [@1C9AIanMe].

### Enhancer calling by ChIP-seq

#### *Calling Active Enhancers*.

We built a universe of peak calls by merging the peaks from individual cell lines for histone modifications (H3K4me1 and H3K27ac) and stratifying the boundaries to remove overlaps/redundancies occurring from the union of all peaks. Potential enhancers were defined as peaks that are $>$ 3kb from known TSS, protein coding genes from Gencode version 19 annotations [@15rkMH6SD], and H3K4me3 peaks. A RPKM cutoff of $\geq$ 1 of H3K4me1 and $\geq$ 1 H3K27ac in at least 1 cell line was used to call a peak as an active enhancer. The universe of active enhancers was assembled using the cutoffs noted above for each cell line and was used for further analyses.

#### *Motif Analyses*.

De novo motif analyses were performed on a 1 kb region ($\pm$ 500 bp) surrounding the peak summit for the top 10000 enhancers, using the command-line version of MEME-ChIP from MEME Suite version 4.11.1 [@dwj6qSn3; @TfukIx2u]. The following parameters were used for motif prediction: (1) zero or one occurrence per sequence (-mod zoops); (2) number of motifs (-nmotifs 15); (3) minimum, maximum width of the motif (-minw 8, -maxw 15). All other parameters were set at the default. The predicted motifs from MEME were matched to known motifs in the JASPAR database (JASPAR_CORE_2016_vertebrates.meme) [@1DrZNoXOU] using TOMTOM [@1C9AIanMe].

### Generating Heatmaps and Clusters

For each cell line, the functional scores were Z-score normalized.  To identify cognate transcription factors by cell type, we performed hierarchical clustering by calculating the Euclidean distance using clustermap from [seaborn](http://seaborn.pydata.org/) version 0.7.1 [@qxfTM222]. For visualization of the multidimensional TFSEE scores, we performed t-distributed stochastic neighbor embedding analysis (t-SNE) [@N7ngUHQX] using the TSNE function and labeled the clusters by calculating K-means clustering using the KMeans function with the expectation-maximization algorithm in [scikit-learn](http://scikit-learn.org/) version 0.17.1 [@vHIKEjNs; @GGWEfSeb; @r8BJ7tJV].

### Nearest Neighboring Gene Analyses and Box Plots
The universe of expressed genes in each cell line was determined from the RNA-seq data using an FPKM cutoff $>$ 0.4.  The set of nearest neighboring expressed genes for each enhancer defined by an expressed eRNA or the enrichment of active histone marks was determined for each cell line.  Box plot representations were used to express the levels of transcription or enrichment for each called enhancer and transcription of their nearest neighboring expressed genes. The read distribution (RPKM) for each enhancer or (FPKM) gene was calculated and plotted using the boxplot function from [matplotlib](https://matplotlib.org/) version 2.0.2 [@1026Gxdsi; @oaruRtzO].  Wilcoxon rank sum tests were performed to determine the statistical significance of all comparisons.


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
