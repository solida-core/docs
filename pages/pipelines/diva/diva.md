---
title: DiVA Pipeline 
keywords: solida, solida-core, bioinformatics pipelines, diva, DNA Variants CCallings
tags: [pipelines]
summary: "DiVA (DNA Variant Analysis) is a pipeline for Next-Generation Sequencing Exome data anlysis"
sidebar: docs_sidebar
permalink: diva.html
folder: pipelines/diva
---

[![depends](https://img.shields.io/badge/depends%20from-bioconda-brightgreen.svg)](http://bioconda.github.io/)
[![snakemake](https://img.shields.io/badge/snakemake-5.3-brightgreen.svg)](https://snakemake.readthedocs.io/en/stable/)


All **[solida-core](https://github.com/solida-core)** workflows follow GATK Best Practices for Germline Variant Discovery, with the incorporation of further improvements and refinements after their testing with real data in various [CRS4 Next Generation Sequencing Core Facility](http://next.crs4.it) research sequencing projects.

Pipelines are based on [Snakemake](https://snakemake.readthedocs.io/en/stable/), a workflow management system that provides all the features needed to create reproducible and scalable data analyses.

Software dependencies are specified into the `environment.yaml` file and directly managed by Snakemake using [Conda](https://docs.conda.io/en/latest/miniconda.html), ensuring the reproducibility of the workflow on a great number of different computing environments such as workstations, clusters and cloud environments.


### Pipeline Overview
The pipeline workflow is composed by three major analysis sections:
 * [_Mapping_](/diva-workflow.html#mapping): paired-end reads in fastq format are aligned against a reference genome to produce a deduplicated and recalibrated BAM file. This section is executed by DiMA pipeline.

 * [_Variant Calling_](/diva-workflow.html#variant-calling): a joint call is performed from all project's bam files

 * [_Annotation_](/diva-workflow.html#annotation): discovered variants are annotated and results are converted in a set of different output file formats enabling downstream analysis for all kind of users

Parallely, statistics collected during these steps are used to generate reports for [Quality Control](#quality-control).

A complete view of the analysis workflow is provided by the pipeline's [graph](images/diva.png).



### Pipeline Handbook
**DiVA** pipeline documentation can be found in the `docs/` directory:


1. [Pipeline Structure:](/pipeline_struct.html)
    * [Snakefile](/pipeline_struct.html#snakefile)
    * [Configfile](/pipeline_struct.html#configfile)
    * [Rules](/pipeline_struct.html#rules)
    * [Envs](/pipeline_struct.html#envs)
2. [Pipeline Workflow](/diva-workflow.html)
3. [Required Files:](/diva-required_files.html)
    * [Reference files](/diva-required_files.html#reference_files)
    * [User files](/diva-required_files.html#user_files)
4. Running the pipeline:
    * [Manual Snakemake Usage](/diva-snakemake.html)
    * [SOLIDA:](/diva-solida.html)
        * [CLI - Command Line Interface](/diva-solida.html#cli.html)
        * [GUI - Graphical User Interface](/solida-solida.html#gui.html)






### Contact us
[support@solida-core](mailto:m.massidda@crs4.it)

