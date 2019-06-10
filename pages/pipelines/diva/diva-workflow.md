---
title: DiVA Workflow
keywords: solida, solida-core, bioinformatics pipelines, diva, DNA Variants CCallings
tags: [pipelines]
sidebar: docs_sidebar
summary: "DiVA (DNA Variant Analysis) is a pipeline for Next-Generation Sequencing Exome data anlysis"
permalink: diva-workflow.html
folder: pipelines/diva
---

The pipeline workflow is composed by three major analysis sections:
 * [_Mapping_](#mapping): paired-end reads in fastq format are aligned against a reference genome to produce a deduplicated and recalibrated BAM file.

 * [_Variant Calling_](#variant-calling): a joint call is performed from all project's bam files
 
 * [_Annotation_](#annotation): discovered variants are annotated and results are converted in a set of different output file formats enabling downstream analysis for all kind of users

Parallely, statistics collected during these steps are used to generate reports for [Quality Control](#quality-control).

A complete view of the analysis workflow is provided by the [pipeline's
graph](/images/diva.png)



### Mapping
* Trimming
* Alingment
* MarkDuplicates
* Base Recalibration


### Variant Calling
* Call Variants Per-Pample in gVCF mode
* Joint-Call Cohort (Genotype gVCFs)
* Variant Recalibration


### Annotation
* Variant Filtering and Annotation (gene annotation, MAF, pathogeniticy, filter by genetic inheritance...)
* Multiple output format conversion: vcf, tsv, xlsx


### Quality Control
* MULTIQC report including:
    * FASTQC
    * Picard HsMetrics
    * Picard InsertSize
    * Picard GC bias metrics
    * VCFtools relatedness --> **NEW FEATURE!** Check for sample relationships to investigate possible contamination 
* Coverage Heatmap for Target Regions    
* Check for Mendelian Violations
