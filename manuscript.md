---
author-meta:
- Venkat S. Malladi
- Anusha Nagari
- Hector L. Franco
- W. Lee Kraus
date-meta: '2018-05-01'
keywords:
- enhancers
- transcription
- transcription factor
- epigenome
lang: en-US
title: Total Functional Score of Enhancer Elements Identifies  Lineage-Specific Enhancers
  that Drive Differentiation of Pancreatic Cells
...






<small><em>
This manuscript
([permalink](https://vsmalladi.github.io/tfsee-manuscript/v/2a174e2afb77240f6d10301634570259a4ec3694/))
was automatically generated
from [vsmalladi/tfsee-manuscript@2a174e2](https://github.com/vsmalladi/tfsee-manuscript/tree/2a174e2afb77240f6d10301634570259a4ec3694)
on May 1, 2018.
</em></small>

## Authors



+ **Venkat S. Malladi**<br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0002-0144-0564](https://orcid.org/0000-0002-0144-0564)
    · ![GitHub icon](images/github.svg){height="13px" width="13px"}
    [vsmalladi](https://github.com/vsmalladi)
    · ![Twitter icon](images/twitter.svg){height="13px" width="13px"}
    [katatonikkat](https://twitter.com/katatonikkat)<br>
  <small>
     The Laboratory of Signaling and Gene Regulation, Cecil H. and Ida Green Center for Reproductive Biology Sciences and Division of Basic Reproductive Biology Research, Department of Obstetrics and Gynecology, University of Texas Southwestern Medical Center; Department of Bioinformatics, University of Texas Southwestern Medical Center"
  </small>

+ **Anusha Nagari**<br><br>
  <small>
     The Laboratory of Signaling and Gene Regulation, Cecil H. and Ida Green Center for Reproductive Biology Sciences and Division of Basic Reproductive Biology Research, Department of Obstetrics and Gynecology, University of Texas Southwestern Medical Center
  </small>

+ **Hector L. Franco**<br><br>
  <small>
     The Laboratory of Signaling and Gene Regulation, Cecil H. and Ida Green Center for Reproductive Biology Sciences and Division of Basic Reproductive Biology Research, Department of Obstetrics and Gynecology, University of Texas Southwestern Medical Center; Department of Genetics and Lineberger Comprehensive Cancer Center, University of North Carolina at Chapel Hill"
  </small>

+ **W. Lee Kraus**<br><br>
  <small>
     The Laboratory of Signaling and Gene Regulation, Cecil H. and Ida Green Center for Reproductive Biology Sciences and Division of Basic Reproductive Biology Research, Department of Obstetrics and Gynecology, University of Texas Southwestern Medical Center
  </small>



## Abstract {.page_break_before}

The ability to integrate different genome data sets to systematically identify active enhancers together with their cognate transcription factors (TF) remains a difficult and somewhat arbitratry process.
We have developed a computational framework that systematically identifies active enhancers in any cell or tissue type together with the TFs bound at the enhancers by integrating multiple genomic assays that probe the transcriptional (GRO-seq and RNA-seq) and epigenetic (ChIP-seq) states of the cells.
Our method, called Total Functional Score of Enhancer Elements (TFSEE), integrates the magnitude of enhancer transcription as a measure of enhancer activitity, enrichment of histone modifications typically associated with enhancers (H3K4me1 and H3K27ac), TF expression levels, and TF motif p-values to compute a probability score of TF binding events at active enhancers across the genome.
This method has allowed us to define the enhancer landscape during differentiation of embryonic stem cells into pancreatic lineages and in breast cancer cells  to define the regulatory pathways of the distinct molecular subtypes of breast cancer.
Using TFSEE, we have identified key breast cancer subtype-specific transcription factors that are bound at active enhancers and dictate gene expression patterns determining growth outcomes.
To demonstrate the broader utility of our approach, we have used this algorithm to identify transcription factors during the differentiation of embryonic stem cells into pancreatic cells.
The analysis has revealed transcription factors maintaining the multipotency of endoderm stem cells and promoting differentiation into pancreatic progenitor cells.
Taken together our results show that TFSEE can be used to perform multilayer genomic data integration to uncover novel cell type-specific transcription factors that control lineage-specific enhancers.


## Background {.page_break_before}

Enhancers and the transcription factors (TFs) regulating their formation have been shown to play an important role in cell type-specific activation of gene expression [@sJDRq7sP; @d09ELIR1].
Although thousands of potential enhancers have been identified in cell lines and tissues, identification of the enhancers that are active versus not active or poised remains remains a major challenge [@r7FNQqrP].
In addition, the ability to identify the TFs acting at the numerous enhancers in each cell type is technically challenging [@15J98V2qM; @sLkFMFZj].

Active enhancers have been shown to share several common features; such as increased chromatin accessibility (as measured by DNase-seq or ATAC-seq) [@NqDGzVRS; @x2PdIgDj; @6xCXy2Jy] and enrichment of post-translational modification of histone tails (as assessed by ChIP-seq), including H3K4me1 and H3K27ac [@vCijBy88; @O5G8lPNO; @LkrR69b9]. While these epigenetic features can successfully identify the location of many enhancers across the genome, they cannot readily differentiate between active and non-active enhancers [@1CNxOwAG6; @UIPf9Y7q]. However, recent genomic assays have shown that enhancers tend to be bound by RNA polymerase II (Pol II) and transcribed, producing non-coding RNAs known as enhancer RNAs (‘eRNAs’) [@3ZN37fOe; @5i6RU9Zx; @1BkIYUDLC].
While the functions of the enhancer RNA transcripts are unknown, we and others have shown that enhancer transcription (as measured by total RNA-seq, GRO-seq or PRO-seq) can be used in the absence of any other genomic information to as a predictor of enhancer activity [@1BkIYUDLC; @9nnd7Ryc; @14GXIWfT0; @1DE6cLccI; @18olkFjWD; @lPKPHCBB; @d09ELIR1; @GvDoUOfC; @2eAh2YIr; @5i6RU9Zx].

In recent years, advances in technology have facilitated the large scale functional characterization of enhancer activity [@14L6kLUE3; @sKU362wY; @jjAPfyKA; @5zmE7Qkb] and annotation of genome-wide binding sites of TFs in various cell types and tissues [@15J98V2qM; @ZnmOeYfS]. However, due to countless cell types, experimental conditions and the large number of TFs [@EkABaVh5], integration of these independent data sets to achieve a comprehensive analysis of gene expression and actionable predictions of TFs driving cell type-specific gene expression can be very challenging. Furthermore, analyses that predict TF binding sites (TFBSs), which are usually 4-12 nucleotides in length [@uOXPLhWz], using TF binding profile databases [@1AqKyPkB5; @1DrZNoXOU; @1C9AIanMe], fail to consider that such sequences occur frequently by chance throughout the genome and that TF binding is cell type specific [@uuBDz4a3]. To overcome these limitations, we established a novel method called Total Functional Score of Enhancer Elements (TFSEE), which can be used to identify location and activity of enhancers in any cell or tissue type together with their cognate TFs.

In TFSEE, we integrate enhancer location and activity, TF motif prediction for each enhancer and the level of TF expression (Figure @fig:overview_tfsee). We have previously demonstrated TFSEE in the identification of
key breast cancer subtype-specific transcription factors determining growth outcomes [@Iu6Tq2rd]. In the studies presented herein, we demonstrate the broader use of TFSEE to identify enhancers and TFs during the differentiation of embryonic stem cells into pancreatic progenitor cells.
Taken together our results show that TFSEE can be used to perform multilayer genomic data integration to uncover novel cell type-specific transcription factors that control lineage-specific enhancers (Figure {@fig:enhancer_predictions}A).


## Results

### The TFSEE model

The TFSEE model integrates multiple genomics assays, GRO-seq, RNA-seq, and ChIP-seq, data with TF motif information to predict TFs driving the formation of active enhancers and the locations of their cognate enhancers.
The TFSEE model consists of five key data processing steps (Figure {@fig:tfsee_processing}) followed by a data integration stage (Figure {@fig:overview_tfsee}).
In step 1 of TFSEE, a universe of active enhancers across the different constituent cell types are identified. The enhancers can be identified either by enhancer transcription (GRO-seq or total RNA-seq) (Figure {@fig:enhancer_pipeline}A) or enrichment of epigenomic marks (H3K4me1 and H3K27ac) (Figure {@fig:enhancer_pipeline}B).
In step 2 of TFSEE, genome-wide enhancer activity levels are assessed by calculating the enrichment (H3K4me1 and H3K27ac) and eRNA transcription (GRO-seq or total RNA-seq) profiles under the universe of enhancers per cell type.
TFSEE was designed to detect enhancer activity changes and TF:enhancer links for each cell type.
All TF to enhancer links are determined by a de novo motif search and summarizing the probability of that TF using the tools in steps 3-4 of TFSEE, which creates a table annotating enhancer to TF for each cell type.
For all TFs identified TFSEE calculates the expression profile using (GRO-seq or RNA-seq) across every cell type in step 5.

The final stage integrates all the data in steps 1-5 (Figure {@fig:overview_tfsee}) to determine TFSEE score matrix and heatmap.
First, we generate an enhancer activity matrix A<sub>CxE</sub> for all cell types C for the universe active of E enhancers, as determined from step 2.
We assume that the enhancer activity of each cell type is linearly correlated to the amount enhancer transcription (GRO-seq or total RNA-seq, G), and to the epigenomic marks (H3K4me1, M and H3K27ac, H).
To reduce bias each individual enhancer enrichment is scaled between 0 and 1.
Enhancer activity can be expressed as the following formula:

<center>$A = G + M + H$</center>

Next, the enhancer activity matrix A<sub>CxE</sub>, is combined with motif prediction matrix T<sub>ExF</sub>, represent scaled motif prediction p-values, T, for each enhancer E, to form an intermediate matrix product. This matrix product is entrywise combined with TF expression matrix R, from step 5, the expression of each TF F for each cell type C, into a resulting matrix Z composed of C cell types and F TFs.
TFSEE can be expressed as the following formula:

<center>$Z =( A \times T) \circ  R$</center>

### Choice of biological model system and data

To better understand the TF-driven transcriptional programs using TFSEE, we used previously published transcriptional and epigenomic data from time course differentiation of human embryonic stem cells (hESC) towards pancreatic cell type [@BTqz3DNL; @18a6G1TE5] (Figure {@fig:enhancer_predictions}A).
For these analyses, we used GRO-seq and RNA-seq, as well as ChIP-seq for 3 different histone modifications at five defined stages of differentiation: hESCs, definitive endoderm (DE), primitive gut tube (GT), posterior foregut (FG), and pancreatic endoderm (PE) (Figure {@fig:enhancer_predictions}A, Table {@tbl:data-sets}).
This embryonic development model allows us to explore the spatiotemporal gene regulation during development, by enhancers and TFs.

### Unbiased Identification of Enhancers during Pancreatic Differentiation

We and other have shown that enhancers can be identified using enrichment of histone modifications (e.g. H3K4me1 and H3K27ac) [@vCijBy88; @O5G8lPNO; @LkrR69b9] or by enhancer transcription [@1BkIYUDLC].
We used a computational pipeline to identify a universe of eRNA transcripts from GRO-seq (Figure {@fig:enhancer_pipeline}A) or enrichment of epigenomic marks (H3K4me1 or H3K27ac) (Figure {@fig:enhancer_pipeline}B) for the cell lines
in the pancreatic differentiation time course model.
All potential enhancers were filtered to be $>$ 3 kb away from known transcription start sites (TSSs) of protein-coding genes from Gencode version 19 annotations [@15rkMH6SD], and active promoters, as identified by H3K4me3 [@9O9ugXze] (Figure {@fig:density_plot}A) to avoid complications in the analysis associated with overlapping promoter transcription.

Using enrichment of H3K4me1 and H3K27ac, RPKM cutoff of $\geq$ 1 (Figure {@fig:density_plot}B and C) in at least one cell line, we determined there to be set of 182,335 candidate enhancers across all stages of pancreatic differentiation (Figure {@fig:enhancer_predictions}B).
We categorized these candidate enhancers for each cell line and found that $\le$ 20% of the enhancers, as determined by presences of H3K4me1 and H3K27ac, are active in each cell line and the majority are marked by only H3K4me1 (Figure {@fig:enhancer_predictions}B).
These results confirm the enhancer landscape across pancreatic differentiation reported by Wang *et al*.
We then identified a set of 4,974 candidate enhancers (Figure {@fig:enhancer_predictions}B) by GRO-seq as described previously [@1DE6cLccI], using RPKM $\geq$ 0.5 or $\geq$ 1 (Figure {@fig:density_plot}D and E) in at least one cell line.
Compared to active enhancer by histone modifications, we found that the number of active enhancers in each cell line ranged from 77-25% of all candidate enhancers.

We compared the overlap from histone enhancer prediction methods (H3K4me1 or H3K27ac) to output from an enhancer transcription based approach (GRO-seq).
We found that 12% of enhancers called based on enhancer transcription using GRO-seq data are identified by all the of the other methods (enrichment of H3K4me1 and H3K27ac) (Figure {@fig:enhancer_predictions}C, {@fig:genome_browser}A).
In contrast, greater than 75% of the enhancers were solely identified by enhancer transcription (Figure {@fig:enhancer_predictions}C and D, {@fig:genome_browser}B).
Although H3K27ac and H3K4me1 might be two histone modifications commonly associated with enhancers, these are not the only chromatin mark involved and other modifications may be present that were not assayed for [@crCcep4D].
Additionally, less than 1% of enhancers called based on enrichment of H3K4me1 or H3K27ac are identified by the other methods (Figure {@fig:enhancer_predictions}C).
This may be due, in part, to the fact that enhancer calling based on H3K4me1 or H3K27ac enrichment, yields much larger numbers of putative enhancers (Figure {@fig:enhancer_predictions}D), many of which may be false positives or inactive as the true regulatory elements (Figure {@fig:genome_browser}C and D). Nonetheless, as we show below, incorporating enhancer transcription into an TFSEE pipeline that includes information about H3K4me1 and H3K27ac enrichment, improves the identification cell type-specific enhancers.

### TFSEE identifies cell type-specific enhancers and their cognate TFs

We used the enhancer calls by Figure {@fig:enhancer_predictions}B, to identify cell type-specific enhancers and their cognate TFs, using TFSEE, either by enhancer transcription or enrichment of epigenomic marks.
We visualized the results from TFSEE using unsupervised hierarchical clustering, which grouped the cell types into two major clades: (1) FG, and PE (2) hESC, DE, and GT (Figure {@fig:tfsee_groseq}A, {@fig:tfsee_histone}A).
To better understand the TF:enhancer dynamics across all differentiation stages we clustered the TSEE score across all differentiation stages, revealing four major categories using enhancer transcription (Figure {@fig:tfsee_groseq}B).
We examined the enrichment of putative enhancers and their associated TFs across stages by quantifying their normalized TFSEE score. This analysis revealed four major clusters: 1. driving early (hESC, DE) and late pancreatic differentiation (FG and PE), 2. enriched in GT, 3. driving pre-pancreatic linage (hESC, DE and GT), and 4. driving late-pancreatic differentiation (FG and PE) (Figure {@fig:tfsee_groseq}D). In contrast, using only histone enrichment to identify enhancers, we retrieve only three clusters (Figure {@fig:tfsee_histone}B). These results highlight TF:enhancers driving pre-pancreatic lineage (hESC, DE and GT), and late-pancreatic differentiation (FG and PE), but fails to highlight any other stage specific drivers (Figure {@fig:tfsee_histone}C). We were particularly interested in TFs and enhancers that provided a clear demarcation of enrichment between pre- and late- pancreatic differentiation.

To investigate the the distinct roles of lineage specific enhancers and their cognate TFs, we first examined the mRNA levels of the corresponding predicted TFs of each cluster in each of the stages.
Our analysis revealed that TFs identified in pre-pancreatic lineage show equal expression across stages, while late-pancreatic TFs are highly expressed in FG and PE (Figure {@fig:late_pre_diff}A, {@fig:late_pre_histone}A) coinciding with pancreatic induction at the FG stage (Figure {@fig:enhancer_predictions}A).
Conversely, we didn't see an enrichment of TFs in a stage specific manner for either TFs enriched early (hESC, DE) and late pancreatic differentiation (FG and PE) or those maintaining GT pluripotency (Figure {@fig:primitive_gut}A).

Next, we determined if enhancer transcription corresponding to the enriched TFs, using TFSEE score, and the regulation of their nearby genes might regulate differentiation biology.
To do so, we identified the enhancers corresponding to the predicted TFs using enriched binding motif prediction, and then determined the level of transcription for each enhancer, using GRO-seq or H3K27ac ChIP-seq, (Figure {@fig:late_pre_diff}B, {@fig:late_pre_histone}B, {@fig:primitive_gut}B) and the nearest neighboring gene (upstream or downstream), using RNA-seq (Figure {@fig:late_pre_diff}C, {@fig:late_pre_histone}C, {@fig:primitive_gut}C).
Interestingly, transcribed enhancers exhibited stage specific enrichment, which doesn't correspond to the patterns found from TFSEE enrichment (Figure {@fig:late_pre_diff}B, {@fig:late_pre_histone}B, {@fig:primitive_gut}B).
This result reflects that 48% - 99% of the enhancers are shared between clusters and the variation between
clusters is due to differences in TF expression and affinity to motifs.
Likewise, the nearest neighboring gene for each transcribed enhancer doesn't exhibit stage specific enrichment (Figure {@fig:late_pre_diff}C, {@fig:late_pre_histone}C, {@fig:primitive_gut}C) due to the vast abundance of enhancers and thus
neighboring genes shared between the clusters.
However, without further high-throughput data to study promoter-enhancer linking (as measured by 4C, ChIA-PET, or Hi-C) [@zQrKrStO, @Z4cumk9R, @SNLehHrw]
it is difficult to understand the stage specific regulatory network.

To further understand the potential regulators of each cluster we determined a rank order frequency distribution for all TFs within each cluster (Figure {@fig:late_pre_diff}D and E, {@fig:late_pre_histone}D and E, {@fig:primitive_gut}D and E).
This analysis reveled enrichment of HINFP, RARG, ZIC3, and SP1-like family TFs (SP1 and SP8) [@gM7zvZej, @rj3cD1pL, @197694eEU, @1EnCQmxEg] which are important regulators of embryonic development.


## Discussion


## Acknowledgments


## Material and Methods {.page_break_before}

### Genomic Data Curation

We used previously published GRO-seq, ChIP-seq and RNA-seq data from [@BTqz3DNL; @18a6G1TE5] time course differentiation of human embryonic stem cells (hESC) to pancreatic endoderm (PE). All data sets are available from NCBI’s Gene Expression Omnibus [@Bc3QGVe7] or EMBL-EBI’s ArrayExpress [@937jwJMM] repositories using the accession numbers listed in Table @tbl:data-sets.

| Assay | Accessions |
| :--------------------: | :------------------------------------------------------------: |
| GRO-seq | GSM1316306, GSM1316313, GSM1316320, GSM1316327, GSM1316334 |
| H3K4me3 ChIP-seq | ERR208008, ERR208014, ERR207998, ERR20798, ERR207999 |
| H3K4me1 ChIP-seq | GSM1316302, GSM1316303, GSM1316309, GSM1316316, GSM1316317, GSM1316310, GSM1316323, GSM1316324, GSM1316330, GSM1316331 |
| H3K27ac ChIP-seq | GSM1316300, GSM1316301, GSM1316307, GSM1316308, GSM1316314, GSM1316315, GSM1316321, GSM1316322, GSM1316328, GSM1316329 |
| Input ChIP-seq | ERR208001, ERR208012, ERR207984, ERR208011, ERR207986, GSM1316304, GSM1316305, GSM1316311, GSM1316312, GSM1316318, GSM1316319, GSM1316325, GSM1316326, GSM1316332, GSM1316333 |
| RNA-seq | ERR266333, ERR266335, ERR266337, ERR266338, ERR266341, ERR266342, ERR266344, ERR266346, ERR266349, ERR266351 |

Table: **Description and accession numbers of GRO-seq, ChIP-seq and RNA-seq datasets.**
{#tbl:data-sets tag="S1"}

### Analysis of ChIP-seq Data Sets

The raw reads were aligned to the human reference genome (GRCh37/hg19) using default parameters in Bowtie version 1.0.0 [@RU8ikjzP]. The aligned reads were subsequently filtered for quality and uniquely mappable reads were retained for further analysis using Samtools version 0.1.19 [@IPc8cy7s] and Picard version 1.127 [@tfF98ztu]. Library complexity was measured using BEDTools version 2.17.0 [@1HWiAHnIw] and meets ENCODE data quality standards [@hvhWxir9]. Relaxed peaks were called using MACS version 2.1.0 [@Bhecn2fS] with a p-value of $1 \times 10^{-2}$ for each replicate, pooled replicates’ reads and pseudoreplicates. Peak calls from the pooled replicates that are either observed in both replicates, or in both pseudoreplicates were used for subsequent analysis.

### Analysis of RNA-seq Data Sets

The raw reads were aligned to the human reference genome (GRCh37/hg19) using default parameters in STAR version 2.4.2a [@tTu8Ds9Z]. Quantification of genes against Gencode version 19 [@15rkMH6SD] annotations was done using default parameters in RSEM version 1.2.31 [@Dh2n1EV3].

### Analysis of GRO-seq Data

The GRO-seq reads were trimmed to the first 36 bases to trim adapter and low quality sequence, using default parameters of fastx_trimer in fastx-toolkit version 0.0.13.2 [@jwUQ55cX].  The trimmed reads were aligned to the human reference genome (GRCh37/hg19) using default parameters in BWA version 0.7.12 [@roi5bwXL].

### Kernel Density

Kernel density plot representations were used to express the univariate distribution of ChIP-seq reads under peaks, RNA-seq reads for protein-coding genes and GRO-seq reads for short paired and short unpaired eRNAs.  The kernel density plots were calculated in Python (ver. 2.7.11) using the kdeplot function from [seaborn](http://seaborn.pydata.org/) version 0.7.1 [@qxfTM222] with default parameters.

### Defining Transcription Start Sites and Promoters

We made distinct transcription start sites (TSS) for protein-coding genes from Gencode version 19 [@15rkMH6SD] annotations using MakeGencodeTSS [@tDy18Yol]. We identified active promoters, as identified by H3K4me3 [@9O9ugXze]. A RPKM cutoff of $\geq$ 1 for H3K4me3 in at least one cell line was used to identify a peak as an active enhancer (Figure {@fig:density_plot}A).

### Enhancer calling by ChIP-seq

#### *Calling Active Enhancers*.

We built a universe of peak calls by merging the peaks from individual cell lines for histone modifications (H3K4me1 and H3K27ac) and stratifying the boundaries to remove overlaps/redundancies occurring from the union of all peaks. Potential enhancers were defined as peaks that were $>$ 3kb from known TSS, protein coding genes from Gencode version 19 annotations [@15rkMH6SD], and H3K4me3 peaks. A RPKM cutoff of $\geq$ 1 for H3K4me1 and H3K27ac (Figure {@fig:density_plot}B and C) in at least one cell line was used to identify a peak as an active enhancer. The universe of active enhancers was assembled using the cutoffs noted above for each cell line and was used for further analyses.

#### *Motif Analyses*.

De novo motif analyses were performed on a 1 kb region ($\pm$ 500 bp) surrounding the peak summit for the top 10000 enhancers, using the command-line version of MEME-ChIP from MEME Suite version 4.11.1 [@dwj6qSn3; @TfukIx2u]. The following parameters were used for motif prediction: (1) zero or one occurrence per sequence (-mod zoops); (2) number of motifs (-nmotifs 15); (3) minimum, maximum width of the motif (-minw 8, -maxw 15). All the other parameters were set at the default. The predicted motifs from MEME were matched to known motifs in the JASPAR database (JASPAR_CORE_2016_vertebrates.meme) [@1DrZNoXOU] using TOMTOM [@1C9AIanMe].


### Enhancer calling by GRO-seq

#### *Transcript calling*.  

Transcript calling was performed using a two-state hidden Markov model using the groHMM data analysis package version 3.4 [@1BkIYUDLC; @1HVy2rbI; @lPKPHCBB] on each individual cell lines. The negative log transition probability of the switch between transcribed state to non-transcribed state and the variance in read counts in the non-transcribed state that are used to predict the transcription units for the cell lines in this study are listed Table @tbl:groseq-tune.

| Cell Line | -Log Transition Probability | Variance in read counts
| :---: | :--------: | :--------: |
| hES | 50 | 45 |
| DE | 50 | 35 |
| GT | 50 | 50 |
| FG | 50 | 35 |
| PE | 50 | 35 |

Table: **groHMM tunning parameters.**
{#tbl:groseq-tune tag="S2"}

We then built a universe of transcripts by merging the groHMM-called transcripts from individual cell lines and stratifying the boundaries to remove overlaps/redundancies occurring from the union of all transcripts.

#### *Calling Enhancer Transcripts*.  

We filtered and collected a subset of short intergenic transcripts $<$ 9 kb in length and $>$ 3 kb away from known transcription start sites (TSSs) of protein-coding genes from Gencode version 19 annotations [@15rkMH6SD], and H3K4me3 peaks. These were further classified into (1) short paired eRNAs and (2) short unpaired eRNAs as described previously [@1DE6cLccI]. For the short paired eRNAs, the sum of the GRO-seq RPKM values for both strands of DNA was used to determine if an enhancer transcript pair is expressed using a cutoff of RPKM $\geq$ 0.5 (Figure {@fig:density_plot}D). An RPKM cutoff of $\geq$ 1 was used to determine the universe expressed short unpaired eRNAs (Figure {@fig:density_plot}E). The comprehensive of expressed eRNAs (short paired and short unpaired) was assembled using the cutoffs noted above for each cell line was used for further analyses.

#### *Motif Analyses*.

De novo motif analyses was performed on a 1 kb region ($\pm$ 500 bp) surrounding the overlap center or the transcription start site for short paired and short unpaired eRNAs, respectively, using the command-line version of MEME from MEME Suite version 4.11.1 [@dwj6qSn3]. The following parameters were used for motif prediction: (1) zero or one occurrence per sequence (-mod zoops); (2) number of motifs (-nmotifs 15); (3) minimum, maximum width of the motif (-minw 8, -maxw 15); and (4) search for motif in given strand and reverse complement strand (-revcomp). The predicted motifs from MEME were matched to known motifs in the JASPAR database (JASPAR_CORE_2016_vertebrates.meme) [@1DrZNoXOU] using TOMTOM [@1C9AIanMe].


### Generating Heatmaps and Clusters

For each cell line, the functional scores were Z-score normalized.  To identify cognate transcription factors by cell type, we performed hierarchical clustering by calculating the Euclidean distance using clustermap from [seaborn](http://seaborn.pydata.org/) version 0.7.1 [@qxfTM222]. For visualization of the multidimensional TFSEE scores, we performed t-distributed stochastic neighbor embedding analysis (t-SNE) [@N7ngUHQX] using the TSNE function and labeled the clusters by calculating K-means clustering using the KMeans function with the expectation-maximization algorithm in [scikit-learn](http://scikit-learn.org/) version 0.17.1 [@vHIKEjNs; @GGWEfSeb; @r8BJ7tJV].

### Nearest Neighboring Gene Analyses and Box Plots

The universe of expressed genes in each cell line was determined from the RNA-seq data using a FPKM cutoff of $>$ 0.4 (Figure {@fig:density_plot}F). The set of nearest neighboring expressed genes for each enhancer defined by an expressed eRNA or the enrichment of active histone marks was determined for each cell line. Box plot representations were used to express the levels of transcription or enrichment for each called enhancer and transcription of their nearest neighboring expressed genes. The read distribution (RPKM) for each enhancer or (FPKM) gene was calculated and plotted using the boxplot function from [matplotlib](https://matplotlib.org/) version 2.0.2 [@1026Gxdsi; @oaruRtzO]. Wilcoxon rank sum tests were performed to determine the statistical significance of all comparisons.


## Figures and Figure Legends {.page_break_before}

![**Data Processing for Total Functional Score of Enhancer Elements (TFSEE) Method.**
The TFSEE method has five data processing steps that are used to identify enhancer location and activity and their cognate transcription factors (TFs).
In step 1, epigenomic (ChIP-seq) or the transcriptional (GRO-seq or total RNA-seq) profiles are used to generate a universe of active enhancers across the different constituent cell types. In step 2, TFSEE calculates the enrichment (H3K4me1 and H3K27ac) and eRNA transcription (GRO-seq and total RNA-seq) profiles under all identified active enhancers per cell type. Cell type-specific enhancers are used as input for step 3, where a de novo motif search is performed to identify potential TFs at each enhancer. If a motif is represented multiple times for a given enhancer location, TFSEE combines the probability of that motif into a single p-value in step 4. Step 5 integrates the amount of eRNA transcription (GRO-seq or total RNA-seq) and the expression of the TFs whose motifs were predicted in step 3 and 4 for all cell types, to provide an output of TF expression profiles across every cell type.
](images/tfsee_processing.png){#fig:tfsee_processing}


![**Overview of Total Functional Score of Enhancer Elements (TFSEE) Method.**
TFSEE combines diverse data sets to identify enhancer location and activity and their cognate transcription factors (TFs).
An illustration of TFSEE data integration stage, taking the outputs generated in panel A, to identify the location, activity level, and predicted TFs at each enhancer across all cell types. (Top) All matrices represent scaled enhancer activity for each cell type in each enhancer prediction method (G, H, and M). All matrices are linearly combined into a resulting matrix A, to provide a total enhancer activity score. (Bottom) Enhancer activity matrix A, is combined with motif prediction matrix T, represent scaled motif prediction p-values for each enhancer, to form an intermediate matrix product. This matrix product is entrywise combined with TF expression matrix R (scaled TF expression for each cell type), into a resulting matrix Z, on which TFSEE clustering is performed.
](images/overview_tfsee.png){#fig:overview_tfsee}



![**Comparison of genome-wide prediction of enhancers during pancreatic differentiation.**
**(A)**	*(Top)* Schematic of pancreatic differentiation starting from Human embryonic stem cells (hESCs) to pancreatic endoderm (PE). *(Bottom)* Depiction of epigenomic (ChIP-seq) and transcriptional (GRO-seq and RNA-seq) profiles for each cell line used for analysis.
**(B)**	Stacked bar chart comparing expression of candidate enhancers categorized by *(Top)* H3K4me1 and H3K27ac enrichment, or *(Bottom)* enhancer transcription (GRO-seq).
**(C)**	Stacked bar chart comparing enhancer prediction methods in pancreatic differentiation. Enhancers were called using enhancer transcription (GRO-seq) or by using H3K4me1 enrichment, or H3K27ac enrichment. The percentage of called enhancers from one prediction method that overlap with enhancers called using other methods is shown.
**(D)**	UpSet plot showing the set intersection of enhancer identification methods shown in panel C.](images/enhancer_predictions.png){#fig:enhancer_predictions}



![**TFSEE identifies cell type-specific enhancers and their cognate TFs that drive gene expression during pancreatic differentiation.**
**(A)**	Unsupervised hierarchical clustering of cell type-normalized TFSEE scores shown in a heatmap representation. hESC (human embryonic stem cell); DE (definitive endoderm); GT (primitive gut tube); FG (posterior foregut); PE (pancreatic endoderm).
**(B)**	Biaxial t-SNE clustering plot of cell type-normalized TFSEE scores showing evidence of four distinct clusters, each point represents an individual TF.
**(C)**	Box plots of normalized TFSEE score for clusters identified in pancreatic differentiation (panel B), number of TFs are indicated in each cluster. Bars marked with different letters are significantly different (Wilcoxon rank sum test, $p \lt 1 \times 10^{-4}$). Cluster 1, TFs associated with early (hESC, DE) and late pancreatic differentiation (FG and PE). Cluster 2, TFs associated with GT pluripotency. Cluster 3, TFs associated with pre-pancreatic lineage induction (hESC, DE and GT). Cluster 4, TFs associated with late-pancreatic differentiation (FG and PE).](images/tfsee_groseq.png){#fig:tfsee_groseq}



![**TFSEE-Predicted TFs are enriched in pre- and late- pancreatic differentiation.**
**(A-C)** Box plots of normalized TF expression (panel A), enhancer transcription (panel B), and gene expression for the nearest neighboring genes to active enhancers (panel C) in pre- (cluster 3) and late-pancreatic (cluster 4) differentiation across the different cell types. Bars marked with different letters are significantly different from each other (Wilcoxon rank sum test). hESC (human embryonic stem cell); DE (definitive endoderm); GT (primitive gut tube); FG (posterior foregut); PE (pancreatic endoderm).
**(A)**	TFs identified in cluster 3 by TFSEE show equal expression across differentiation. While, cluster 4 highlights TFs highly expressed in FG and PE. TF expression as measured by RNA-seq. Number of TFs in each cluster are in parenthesis. ($p \lt 1 \times 10^{-4}$)
**(B)**	Enhancer transcription as measured by GRO-seq. Number of enhancers in each cluster are in parenthesis. $p \lt 1 \times 10^{-4}$).
**(C)**	Gene expression as measured by RNA-seq. Number of genes in each cluster are in parenthesis. ($p \lt 0.05$)
**(D and E)** Rank order of TFs enriched in the Cluster 3 and the Cluster 4 identified using TFSEE.  The top ten TFs in each Cluster are noted.](images/late_pre_diff.png){#fig:late_pre_diff}  




![**Unbiased, genome-wide prediction of active enhancers.**
**(A)** Overview of the computational pipeline used for the genome-wide annotation of enhancer transcripts (eRNAs) and prediction of active enhancers using GRO-seq data.
**(B)** Overview of the computational pipeline used for the genome-wide annotation of and prediction of active enhancers using ChIP-seq (H3K4me1 and H3K27ac) data.](images/enhancer_pipeline.png){#fig:enhancer_pipeline tag='S1'}




![**Density plots of enhancer and gene expression levels across all cell types.**
Kernel density plots of log-transformed RPKM and FPKM values for determining active enhancers and genes. The dashed grey line represents the minimum expression cutoff.
**(A)**	Density plot of H3K4me3 (promoter mark) cutoff RPKM $\geq 1$.
**(B)**	Density plot of H3K4me1 (enhancer mark) cutoff RPKM $\geq 1$.
**(C)**	Density plot of H3K27ac (enhancer mark) cutoff RPKM $\geq 1$.
**(D)**	Density plot of short-short paired GRO-seq transcription (SSP) (enhancer mark) cutoff RPKM $\geq 1$.
**(E)**	Density plot of short-unpaired GRO-seq transcription (SUNP) ( enhancer mark)  cutoff RPKM $\geq 0.5$.
**(F)**	Density plot of RNA-seq (gene expression) cutoff FPKM $\geq 0.4$](images/density_plot.png){#fig:density_plot tag='S2'}




![**Enhancer transcription is a better predictor of enhancer activity and target gene expression than other features of active chromatin.**
**(A-D)** UCSC Genome browser views of GRO-seq, histone modification ChIP-seq and RNA-seq data showing a transcribed enhancer *(black box with dashed line)* and its nearest neighboring gene. hESC (human embryonic stem cell); DE (definitive endoderm); GT (primitive gut tube); FG (posterior foregut); PE (pancreatic endoderm).
**(A)**	Browser view showing a transcribed enhancer and its nearest neighboring gene (SMAD7). The data highlights histone modifications typically enriched at enhancers *(green)*, however the increased transcription determined by GRO-seq *(red/blue)* for DE correlates to expression of nearest genes determined by RNA-seq *(orange/light green)*.
**(B)**	Browser view showing a transcribed enhancer and its nearest neighboring gene (ATG5. The data highlights an enhancer identified by GRO-seq *(red/blue)*, however lacks typical histone modifications enriched at enhancers *(green*). The increased transcription determined by GRO-seq for hESC correlates to expression of nearest genes determined by RNA-seq *(orange/light green)*.
**(C)**	Browser view showing a transcribed enhancer and its nearest neighboring gene (PDX1). The data highlights an enhancer identified by histone modifications enriched at enhancers *(green)*, however increased transcription determined by GRO-seq *(red/blue)* correlates with antisense gene (AS-PDX1).
**(D)**	Browser view showing a transcribed enhancer and its nearest neighboring gene (RGS4). The data highlights an enhancer identified by histone modifications enriched at enhancers *(green)*, however lacks enhancer transcription identified by GRO-seq *(red/blue)*. The increased enhancer signal determined by histone modifications for PE shows correlates to expression of nearest genes determined by RNA-seq *(orange/light green)* and GRO-seq *(red/blue)*.](images/genome_browser.png){#fig:genome_browser tag='S3'}




![**TFSEE defined by histone modifications identifies cell type-specific enhancers and their cognate TFs that drive gene expression in pancreatic differentiation.**
**(A)**	Unsupervised hierarchical clustering of cell line normalized TFSEE scores shown in a heatmap representation.  
**(B)**	Biaxial t-SNE clustering plot of cell type-normalized TFSEE scores showing evidence of three distinct clusters, each point represents an individual TF.
**(C)**	Boxplots of normalized TFSEE score for clusters identified in pancreatic differentiation. Bars marked with different letters are significantly different from each other (Wilcoxon rank sum test, $p \lt 1 \times 10^{-2}$). Number of TFs in each cluster are in parenthesis. Cluster 1, TFs associated across pancreatic lineage Cluster 2, TFs associated with pre-pancreatic lineage induction (hESC, DE and GT). Cluster 3, TFs associated with late-pancreatic differentiation (FG and PE).](images/tfsee_histone.png){#fig:tfsee_histone tag='S4'}




![**TFSEE-Predicted TFs, by histone modifications, are enriched in pre- and late- pancreatic differentiation.**
**(A-C)** Box plots of normalized TF expression (panel A), enhancer transcription (panel B), and gene expression for the nearest neighboring genes to active enhancers (panel C) in pre- (cluster 2) and late-pancreatic (cluster 3) differentiation across the different cell types. Bars marked with different letters are significantly different from each other (Wilcoxon rank sum test). hESC (human embryonic stem cell); DE (definitive endoderm); GT (primitive gut tube); FG (posterior foregut); PE (pancreatic endoderm).
**(A)**	TFs identified in cluster 2 by TFSEE show equal expression across differentiation. While, cluster 3 highlights TFs highly expressed in FG and PE. TF expression as measured by RNA-seq. Number of TFs in each cluster are in parenthesis. ($p \lt 1 \times 10^{-4}$)
**(B)**	Enhancer transcription as measured by ChIP-seq (H3K27ac enrichment). Number of enhancers in each cluster are in parenthesis. ($p \lt 1 \times 10^{-4}$).
**(C)**	Gene expression as measured by RNA-seq. Number of genes in each cluster are in parenthesis. ($p \lt 0.05$).
**(D and E)** Rank order of TFs enriched in the Cluster 2 and the Cluster 3 identified using TFSEE.  The top ten TFs in each Cluster are noted.](images/late_pre_histone.png){#fig:late_pre_histone tag='S5'}




![**TFSEE-Predicted TFs are enriched and depleted in Primitive Gut Tube during pancreatic differentiation.**
**(A-C)** Box plots of normalized TF expression (panel A), enhancer transcription (panel B), and gene expression for the nearest neighboring genes to active enhancers (panel C) in depleted (cluster 1) and enriched (cluster 2) in primitive gut tube during pancreatic differentiation across different cell types. Bars marked with different letters are significantly different from each other (Wilcoxon rank sum test). hESC (human embryonic stem cell); DE (definitive endoderm); GT (primitive gut tube); FG (posterior foregut); PE (pancreatic endoderm).
**(A)**	TF expression as measured by RNA-seq. Number of TFs in each cluster are in parenthesis. ($p \lt 1 \times 10^{-2}$)
**(B)**	Enhancer transcription as measured by GRO-seq. Number of enhancers in each cluster are in parenthesis. ($p \lt 1 \times 10^{-4}$).
**(C)**	Gene expression as measured by RNA-seq. Number of genes in each cluster are in parenthesis. ($p \lt  0.05$).
**(D and E)** Rank order of TFs enriched in the Cluster 1 and the Cluster 2 identified using TFSEE.  The top five TFs in each Cluster are noted.](images/primitive_gut.png){#fig:primitive_gut tag='S6'}


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>