# ATAC-seq Pipeline

This is an ATAC-seq pipeline that I developed for my BF528 Applications in Translational Bioinformatics course at Boston University. The data consisted of two replicates from human lymphoblastoid B-cells from Buenrostro et al. I constructed the pipeline to analyze the regions of open chromatinand identify nucleosome-bound and nucleosome-free positions in regulatory regions. The accompanying Rmarkdown file contains a full report and analysis of the data.

# Jackson Faulx ATAC-seq Final Project

## Methods

First, QC was performed on the paired-end reads using fastqc (v0.12.1) and the reads were trimmed using trimmomatic (v0.39). The reads were then aligned using bowtie2 (v2.5.3) keeping all unique reads that are less than 2kb in size. The reads were then sorted and mitochondrial alignments were removed using samtools (v1.19.2) sort and view respectively. The reads were then shifted using alignmentSieve from deeptools (v3.5.4). Read size distribution was then visualized using the ATACSeqQC (v1.26.0) package from bioconductor in R. Peak calling was then performed by MACS3 (v3.0.1) with default parameters. I then used the homer (v4.11) packages makeTagDirectory, findPeaks, and pos2bed.pl to generate bed files for the peaks in each sample. Peak intersection and filtering was then performed for the samples using bedtools (v2.31.1) intersect. After the interscting peaks have been found, homer is then used again to generate a file of annotated peaks. enrichr will then be used for analysis.



## Questions

1. Briefly remark on the quality of the sequencing reads and the alignment statistics, make sure to specifically mention the following:
  - Are there any concerning aspects of the quality control of your sequencing reads?
    - No, the QC metrics look fine. There are duplicate reads however that is expected due to potential binding motifs present in the non coding regions
  - Are there any concerning aspects of the quality control related to alignment?
    - The sequences aligned well, with no discernable issues
  - Based on all of your quality control, will you exclude any samples from further analysis?
    - no samples need to be excluded from analysis
2. After alignment, quickly calculate how many alignments were generated from each sample in total and how many alignments were against the mitochondrial chromosome
  - Report the total number of alignments per sample
  - Report the number of alignments against the mitochondrial genome
3. After performing peak calling analysis, generating a set of reproducible peaks and filtering peaks from blacklisted regions, please answer the following:
  - How many peaks are present in each of the replicates?
  - How many peaks are present in your set of reproducible peaks? What strategy did you use to determine “reproducible” peaks?
  - How many peaks remain after filtering out peaks overlapping blacklisted regions?
4. After performing motif analysis and gene enrichment on the peak annotations, please answer the following:
  - Briefly discuss the main results of both of these analyses
  - What can chromatin accessibility let us infer biologically?


## Deliverables

Produce a fragment length distribution plot for each of the samples

Produce a table of how many alignments for each sample before and after filtering alignments falling on the mitochondrial chromosome

Create a signal coverage plot centered on the TSS (plotProfile) for the nucleosome-free regions (NFR) and the nucleosome-bound regions (NBR)

You may consider fragments (<100bp) to be those from the NFR and the rest as the NBR.
A table containing the number of peaks called in each replicate, and the number of reproducible peaks

A single BED file containing the reproducible peaks you determined from the experiment.

Perform motif finding on your reproducible peaks

Create a single table / figure with the most interesting results
Perform a gene enrichment analysis on the annotated peaks using a well-validated gene enrichment tool

Create a single table / figure with the most interesting results
Produce a figure that displays the proportions of regions that appear to have accessible chromatin called as a peak (Promoter, Intergenic, Intron, Exon, TTS, etc.)

