---
title: "solida-core"
keywords: homepage solida-core
tags: [solida-core]
sidebar: docs_sidebar
permalink: index.html
summary: Robust, and ready-to-use collection of extensively validated bioinformatic pipelines
---


## Motivation

Next Generation Sequencing projects are rapidly increasing worldwide and with them, the need to ensure reproducibility and reusability of the computational bioinformatic workflows, now consisting of many pieces of third-party software with complex dependency trees and configuration requirements. Furthermore, it is acknowledged that the full exploitation of genetic information in clinical practice is largely limited not only by the complexity of variants interpretation but also to the lack of standardization of data processing procedures, and of datasets. 

Starting from 2017 we have developed NGS analysis pipelines using Snakemake, one of the most popular workflow management system. [Snakemake](https://bitbucket.org/snakemake/snakemake) provides all the features needed to create reproducible and scalable data analyses ensuring a logical separation between the workflow description and its execution details. In fact, Snakemake can handle software dependencies using Conda or Docker and can execute workflows on a great number of different computing environments such as workstations, clusters and cloud environments.

To organize the deployment, the data management and the execution of the Snakemake based workflows on different environments, we initially developed a software named [SOLIDA](https://github.com/solida-core/solida). Leveraging on SOLIDA, here we present [solida-core](https://github.com/solida-core), an open source repository where we have collected all the Snakemake-based workflows developed at CRS4 and that are now available to the other research groups and core genomics facilities. 

## Methods

The solida-core project was born at the end of 2017, with the aim of creating a reproducible and portable set of extensively validated Snakemake-based bioinformatic pipelines and to share them with a larger community of users. 

According to the Snakemake pipeline management scripts organization, we defined a standard template with a common structure as a *scaffold* for pipeline development. In this way, each analysis workflow consists of a section with the description of the analysis steps, and a configuration file containing the user parameters which are queried during the execution of the pipeline.

Furthermore, Pipelines, in solida-core, come with a project-related virtual
environment enabled via [Conda](ihttps://conda.io/en/latest/). This feature permits the portability of a
pipeline since the whole configuration will be automatically deployed by
SOLIDA. All the pipeline of solida-core are built, as a first step, following
the GATK Best Practices for DNA and RNA sequencing analysis.

Further improvements and refinements were then incorporated after their testing
with real data in various research sequencing projects. For example, the Exome
Sequencing Data Analysis Pipeline ([DiVA](https://github.com/solida-core/diva))
was thoroughly tested and validated **on ~1000 samples from > 20 projects.** This
workflow performs the annotation of variants discovered in Exome data starting
from FASTQ files, with the contextual production of a complete quality control
report. More pipelines are available on solida-core and continuously supported,
optimized, and updated. We refer to the solida-core repository for a complete
list.

As the computational skills of the target users can range from beginners to advanced users, these pipelines can be executed via command-line in a virtual environment containing Snakemake or alternatively, exploiting SOLIDA which takes care of the pipeline management, configuration and of their deployment on the computing environment of choice. SOLIDA is written in Python and is available in a command-line version or via a recently developed friendly graphical interface based on Django.

## Results

solida-core is a robust, and ready-to-use collection of extensively validated bioinformatic pipelines which are routinely used for complex large-scale genetic analysis at the [CRS4 Next Generation Sequencing Core Facility](http://next.crs4.it), one of the largest sequencing facilities in Italy.

solida-core ensures both portability and stability of code between different computing environments and the reproducibility of the results. The solida-core open-source curated collection is publicly released with SOLIDA, a pipeline manager that guides the user during pipeline configuration and deployment. The combination of these resources represents a complete easy-to-use bioinformatic analysis framework which can be used by both researchers facing with bioinformatics for the first time and by experienced bioinformaticians. Moreover, since the resource is public other users can also contribute to the development of new pipelines or to the improvement of existing ones.

{% include links.html %}
