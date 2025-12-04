# Nextflow joint variant calling QC Pipeline with Automated Testing Integration

![Nextflow](https://img.shields.io/badge/nextflow-%E2%89%A522.10.1-brightgreen.svg)
![Docker](https://img.shields.io/badge/docker-ready-blue.svg)
![Testing](https://img.shields.io/badge/tests-passing-success)

## 📌 Overview
This repository contains a Nextflow DSL2 implementation of a Joint Variant Calling pipeline. It is designed to demonstrate scalable, reproducible genomic analysis workflows using modern software engineering practices.

The pipeline follows the logic of the GATK variant discovery:

    Per-Sample Calling: Generating GVCFs from aligned BAM files.

    Consolidation: Merging GVCFs across the cohort.

    Joint Genotyping: Calling variants simultaneously across all samples to improve sensitivity for rare variants.

    Note: This is a practice repository created to demonstrate proficiency in Nextflow orchestration, module reusability, and containerized execution.

Pipeline Steps

The workflow consists of the following modular processes:

    1. Index BAMs: (samtools index) - Prepares input alignments.
    
    2. HaplotypeCaller: (GATK4) - Runs in GVCF mode on each sample independently (Scatter).

    3. CombineGVCFs: (GATK4) - Merges individual GVCFs into a single cohort GVCF (Gather).

    4. GenotypeGVCFs: (GATK4) - Performs the final joint genotyping step.
Repo Structure:

├── data
│   ├── bam
│   │   ├── reads_father.bam
│   │   ├── reads_mother.bam
│   │   ├── reads_mother.bam.bai
│   │   └── reads_son.bam
│   ├── ref
│   │   ├── intervals.bed
│   │   ├── ref.dict
│   │   ├── ref.fasta
│   │   └── ref.fasta.fai
│   ├── sample_bams.txt
│   └── samplesheet.csv
├── genomics-1.nf
├── genomics-2.nf
├── genomics-3.nf
├── joint-variant-calling-pipeline.nf
├── modules
│   ├── gatk
│   │   ├── haplotypecaller
│   │   │   ├── main.nf
│   │   │   └── tests
│   │   │       ├── main.nf.test
│   │   │       └── main.nf.test.snap
│   │   └── jointgenotyping
│   │       ├── main.nf
│   │       └── tests
│   │           ├── inputs
│   │           │   ├── reads_father.bam.g.vcf
│   │           │   ├── reads_father.bam.g.vcf.idx
│   │           │   ├── reads_mother.bam.g.vcf
│   │           │   ├── reads_mother.bam.g.vcf.idx
│   │           │   ├── reads_son.bam.g.vcf
│   │           │   └── reads_son.bam.g.vcf.idx
│   │           └── main.nf.test
│   └── samtools
│       └── index
│           ├── main.nf
│           └── tests
│               ├── main.nf.test
│               └── main.nf.test.snap
├── nextflow.config
├── nf-test.config


🧪 Testing & Validation

To ensure pipeline stability, this repository utilizes a basic testing strategy:

    Unit Tests: Each module (e.g., HaplotypeCaller) can be tested independently.

    Integration Test: The whole pipeline also can be tested in a single go.
