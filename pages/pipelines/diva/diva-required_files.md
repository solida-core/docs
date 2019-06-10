---
title: DiVA Required Files
keywords: solida, solida-core, bioinformatics pipelines, diva, DNA Variants CCallings
tags: [pipelines]
sidebar: docs_sidebar
summary: "DiVA (DNA Variant Analysis) is a pipeline for Next-Generation Sequencing Exome data anlysis"
permalink: diva-required_files.html
folder: pipelines/diva
---

## Reference Files

[DiVA](https://github.com/solida-core/diva) reference files are stored within a particular folder-tree common with all solida-core pipelines.

This organization must be kept because the pipelines have built-in functions which search for reference and accessory files in these folders.

This is a representation of it:
```
REFERENCE FOLDER
    │
    └── PROVIDER
            |
            └── RELEASE
                   |
                   ├── genome.fasta
                   |
                   ├── genome.idx
                   |    
                   └── known_varians
                            |
                            └── accessory files
```
There is a `main reference folder` in which can be present reference files from different `PROVIDER` (like ucsc or ncbi).

For each provider can be present multiple `RELEASES` of human genome, where are placed the relative files.

We refer to this first described three elemets as `REFERENCE`, `PROVIDER` and `RELEASE` and must be declared in the pipeline `config.yaml` file. 
Starting from this, a pipeline function is able to generally manage and use reference files from the correct provider and release.


The `RELEASE` folder is the directory in which are stored the reference genome files with relative indexes and, inside the "known_variants" folder, several GATK accessory files (useful for Variant Recalibration step).


### Reference downloader

To facilitate users in reference organization, we developed a simple script aimed at downloading and correctly placing reference files.
The script is part of a *[TOOLKIT](https://github.com/solida-core/toolkit#solida-core-toolkit)* where useful pipeline-related scripts will be collected.

**INSTALL and RUN:**  **[reference_organizer](https://github.com/solida-core/toolkit#reference_organizerpy)**

## User Files
**DiVA** (DNA Variant Analysis) pipeline can process fastq files from Exome sequencing to obtain filtered and annotated tables.
The standardization provided by [solida-core]() requires perhaps accessory user-defined files to have a given organization.

#### Definition of "unit"
To deal with the high number of samples and even multiple files for a single sample, in our pipelines we adopted the usage of `units` for sample organization. 

For each individual, a `unit` refers to a set of reads that were generated from a single lane of a sequencing instrument. 
In the simple case where a single library preparation derived from a single biological sample was run on a single lane of a flowcell, all the reads from that lane run belong to the same unit. 
If a sample is present in multiple lanes, then each subset of reads originating a lane will constitute a separate unit. 
Units are used to correctly assign [Read Groups](https://gatkforums.broadinstitute.org/gatk/discussion/6472/read-groups).

`unit IDs` are composed using the `flowcell ID`, the `lane number` and the `sample ID`, separated by the `.` character, making them a globally unique identifier across all sequencing data.
```
Given the sample ID "DNA2019-AAAA", sequenced in the lane 006 of the flowcell with ID "HXXBBCXY"
the unique unit ID will be:

HXXBBCXY.L006.DNA2019-AAAA
```
After mapping, units from each sample are merged into single-sample files.
This organization results in a speed-up of mapping process and, on the other hand, the very easy integration with new sequencing data for a sample, i.e. in case of low coverage.


#### Required Input Files
**DiVA** pipeline requires three different mandatory user inputs:
* [samples](#samplestsv)
* [units](#unitstsv)
* [sets](#setstsv)

These files contain **tab-separated** information about samples to be analyzed and must be declared into the `config.yaml` file:
```
samples: "path_to_input_files/samples.tsv"
units: "path_to_input_files/units.tsv"
sets: "path_to_input_files/sets.tsv"
```

#### samples.tsv
Samples file include information about sample names and the unit IDs related to each sample.
In addiction, we specify information about "Optical Distance Pixel Distance" relative to sequencing instrument for [Picard MArkDuplicates](https://software.broadinstitute.org/gatk/documentation/tooldocs/4.1.2.0/picard_sam_markduplicates_MarkDuplicates.php) step.

The file structure is described in the example below::
```
sample          odp	    units
ERS179576	100	    HSQ1008_141.L005.ERS179576,HSQ1008_141.L007.ERS179576,HSQ1009_88.L001.ERS179576
ERS179577	100	    HSQ1009_86.L001.ERS179577

``` 
Where:

* sample: sample ID;
* odp: Optical Distance Pixel Distance (default=100), check official [Picard](https://software.broadinstitute.org/gatk/documentation/tooldocs/4.1.2.0/picard_sam_markduplicates_MarkDuplicates.php#--OPTICAL_DUPLICATE_PIXEL_DISTANCE) documentation;
* units: one or more unique unit IDs


#### units.tsv
Units file include information about sample IDs and the unit IDs related to each sample, with the absolute path of sequencing data files. 

The file structure is described in the example below::
```
sample  	unit	                        fq1	                                fq2
ERS179576	HSQ1008_141.L005.ERS179576	path_to_datasets/ERR174310_1.fastq.gz	path_to_datasets/ERR174310_2.fastq.gz
ERS179576	HSQ1008_141.L007.ERS179576	path_to_datasets/ERR174312_1.fastq.gz	path_to_datasets/ERR174312_2.fastq.gz
ERS179576	HSQ1009_88.L001.ERS179576	path_to_datasets/ERR174314_1.fastq.gz	path_to_datasets/ERR174314_2.fastq.gz
ERS179577	HSQ1009_86.L001.ERS179577	path_to_datasets/ERR174324_1.fastq.gz	path_to_datasets/ERR174324_2.fastq.gz
``` 
Where:

* sample: sample IDs, in this file a sample ID can be present in multiple lines according with the number of units;
* unit: one unique unit ID
* fq1-fq2: complete path and R1- and R2-fastq files (for paired-end sequencing).


#### sets.tsv
Sets file include information about sample names and the analysis set they belong to.
This information is used in the annotation step and allows per-set output organization.

The file structure is described in the example below::
```
set	sample
setA	ERS179576,ERS179577
``` 
Where:

* set: an user-defined set name;
* sample: sample IDs being part of the given set.
