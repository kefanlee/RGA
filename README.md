# RGA

## Resequencing Genome Analysis Toolkit

**RGA** is an integrated command-line toolkit for automated and standardized analysis of whole-genome resequencing data. It was developed to simplify large-scale variant analysis, particularly for experimentally induced mutant populations, by integrating major steps from sequence alignment and variant detection to multi-sample comparison, functional annotation, quality assessment, and downstream result organization.

RGA is designed for Linux-based computing environments and supports parallel processing of large resequencing datasets.

> **This repository is the official software distribution repository for RGA.**  
> It provides packaged RGA releases, documentation, and version information.  
> **RGA source code is not publicly distributed through this repository.**

---

## Overview

Whole-genome resequencing analysis typically requires multiple independent bioinformatics tools and a series of interconnected processing steps, including:

- sequencing data quality assessment;
- reference genome preparation;
- read alignment;
- BAM processing;
- variant detection;
- quality filtering;
- multi-sample comparison;
- functional annotation;
- structural variant analysis;
- result summarization and visualization.

For large mutant populations, additional challenges arise from the need to distinguish candidate induced mutations from shared background variants and to process large numbers of samples using consistent analytical criteria.

RGA provides an integrated workflow for these tasks and organizes the resulting outputs into a standardized structure, reducing the amount of manual workflow construction required for large-scale resequencing projects.

---

## Current Release

**Current stable release: RGA v3.24**

The latest RGA distribution package is available from the **[Releases](../../releases)** section of this repository.

Users are encouraged to use the latest stable version unless a specific version is required for reproducibility.

For scientific publications, the exact RGA version used in the analysis should always be reported.

---

## Key Features

### Reference Genome Preparation

RGA prepares the reference genome and associated index files required for downstream analyses.

### Read Alignment

Whole-genome sequencing reads can be aligned to a user-specified reference genome using supported alignment tools.

### BAM Processing

RGA performs standardized processing of alignment files, including sorting, indexing, and preparation for downstream variant analysis.

### SNP and InDel Detection

RGA integrates established variant-calling approaches for identification of:

- single-nucleotide polymorphisms (SNPs);
- small insertions and deletions (InDels).

### Variant Quality Filtering

Candidate variants can be filtered using standardized quality-control criteria to remove low-confidence calls.

### Multi-sample Comparison

RGA supports comparative analysis across multiple samples.

This function is particularly useful for experimentally induced mutant populations, in which variants shared among multiple individuals may represent:

- parental background polymorphisms;
- naturally occurring variants;
- recurrent technical signals;
- common population-level variation.

Cross-sample comparison can therefore facilitate the identification of sample-specific candidate mutations.

### Sample-specific Mutation Screening

RGA supports allele-frequency-based screening across target and non-target samples to identify candidate variants associated with individual mutant materials.

### Functional Annotation

Candidate genomic variants can be annotated according to their genomic locations and predicted functional consequences.

### Structural Variant Analysis

RGA provides optional structural variation analysis through supported SV detection tools.

### Quality Assessment

Sequencing and alignment quality metrics can be generated for individual samples to facilitate quality control of large resequencing datasets.

### Batch Processing

RGA supports multi-threaded and multi-sample processing and is suitable for large-scale resequencing projects involving tens to hundreds of samples.

### Standardized Output

Analysis results are automatically organized into standardized directories to facilitate:

- downstream statistical analysis;
- manual inspection;
- visualization;
- candidate mutation screening;
- data archiving.

---

## Integrated Bioinformatics Tools

Depending on the selected analysis modules and RGA configuration, the workflow can interface with established bioinformatics software including:

- **BWA / BWA-MEM2**
- **SAMtools**
- **GATK**
- **VarScan2**
- **snpEff**
- **DELLY**
- **Manta**
- **LUMPY**
- **Qualimap**
- **IGV-related utilities**

These programs are independent third-party software packages and remain subject to their respective licenses and terms of use.

Unless explicitly stated for a specific release, third-party software should be installed separately by the user.

RGA does not modify or replace the licensing terms of any third-party software.

See [`THIRD_PARTY_SOFTWARE.md`](THIRD_PARTY_SOFTWARE.md) for additional information.

---

## Typical Analysis Workflow

```text
Raw whole-genome sequencing data
                │
                ▼
        Input data checking
                │
                ▼
      Reference preparation
                │
                ▼
          Read alignment
                │
                ▼
          BAM processing
                │
                ▼
          Quality control
                │
                ▼
          Variant calling
          ├── SNP
          ├── InDel
          └── SV
                │
                ▼
        Variant filtering
                │
                ▼
      Multi-sample comparison
                │
                ▼
 Sample-specific variant screening
                │
                ▼
       Functional annotation
                │
                ▼
     Standardized result output
                │
                ▼
 Statistical analysis / visualization /
 candidate mutation and gene screening
```

Individual modules can be selected according to the experimental design and analysis requirements.

---

## Applications

RGA was developed with particular consideration for genomic analysis of experimentally induced mutant populations.

Potential applications include:

- heavy-ion beam mutagenesis;
- heavy-ion microbeam mutagenesis;
- radiation mutagenesis;
- space mutagenesis;
- chemical mutagenesis;
- mutant population resequencing;
- functional genomics;
- candidate mutation identification;
- candidate gene screening;
- large-scale plant resequencing analysis.

Although RGA was initially developed and evaluated using plant genomic datasets, its core resequencing workflow may also be applicable to other organisms when appropriate reference genomes and annotation resources are available.

---

## System Requirements

RGA is designed for **64-bit Linux systems**.

Recommended environment:

- 64-bit Linux operating system;
- Bash shell;
- multi-core CPU;
- sufficient RAM for genome-scale analysis;
- sufficient disk space for FASTQ, BAM, VCF, and intermediate files.

The exact computational requirements depend on:

- genome size;
- sequencing depth;
- sample number;
- enabled analysis modules;
- number of parallel jobs.

For large resequencing populations, a high-performance workstation or computing server is recommended.

---

## Download

RGA software packages are distributed through the **Releases** section of this repository.

1. Open the **Releases** page.
2. Select the required RGA version.
3. Download the corresponding distribution package.
4. Extract the package to the desired installation directory.

Example:

```bash
tar -xzf RGA-v3.24.tar.gz
cd RGA-v3.24
```

> The exact file name may differ depending on the release package.

---

## Installation

RGA is distributed as a packaged software release rather than as a source-code repository.

After downloading and extracting the package, follow the documentation provided with the corresponding release.

Before starting an analysis, ensure that all required third-party dependencies are correctly installed and accessible from the system environment.

Users are encouraged to verify the software environment before running large-scale analyses.

---

## Input Data

Typical RGA analyses require:

- whole-genome resequencing reads;
- a reference genome in FASTA format;
- genome annotation files when functional annotation is required;
- sample information;
- appropriate analysis parameters.

Paired-end sequencing data are recommended for standard whole-genome resequencing analyses.

Example:

```text
reference.fa

sample1_R1.fastq.gz
sample1_R2.fastq.gz

sample2_R1.fastq.gz
sample2_R2.fastq.gz

sample3_R1.fastq.gz
sample3_R2.fastq.gz
```

---

## Output

Depending on the selected modules, RGA can generate:

- processed BAM files;
- SNP variant files;
- InDel variant files;
- structural variation results;
- filtered candidate variants;
- sample-specific candidate variant sets;
- functional annotation results;
- sequencing quality reports;
- alignment quality reports;
- summary statistics;
- files for downstream visualization and manual inspection.

The standardized output structure is designed to facilitate subsequent statistical analysis and interpretation.

---

## Analysis of Mutant Populations

RGA is particularly suited to resequencing analysis of experimentally induced mutant populations.

In such populations, detected genomic variants may originate from multiple sources, including:

- induced mutations;
- parental background polymorphisms;
- pre-existing genetic variation;
- variants shared among multiple samples;
- technical artifacts.

RGA therefore provides multi-sample comparison and sample-specific screening procedures to reduce shared background variation and prioritize candidate mutations associated with individual mutant materials.

This framework is particularly useful when large mutant populations are subjected to whole-genome resequencing.

---

## Version Information

RGA is under continued development.

Different releases may contain changes in:

- integrated analysis tools;
- variant filtering procedures;
- analysis modules;
- output structure;
- computational performance;
- downstream analysis functions.

For reproducible research, users should always record and report the exact RGA version used.

Example:

```text
RGA version 3.24
```

---

## Citation

If RGA contributes to your research, please cite the corresponding RGA publication.

```text
Citation information will be updated after publication.
```

Before publication of the corresponding manuscript, RGA can be described in the Materials and Methods section as:

```text
Whole-genome resequencing data were analyzed using the
Resequencing Genome Analysis Toolkit (RGA, version 3.24).
```

The final citation information, DOI, and publication details will be added to this repository after publication.

---

## Software Availability

RGA software releases are made available through this repository for **academic and non-commercial research use**.

This repository is intended primarily for:

- software distribution;
- release management;
- documentation;
- version tracking;
- issue reporting.

**The RGA source code is not publicly distributed through this repository.**

---

## License

RGA is distributed under the **RGA Academic Software License**.

The software may be downloaded and used for academic and non-commercial research purposes subject to the terms specified in the [`LICENSE`](LICENSE) file.

Unless explicit written permission is obtained from the copyright holder, users may not:

- redistribute RGA;
- sublicense RGA;
- resell RGA;
- commercially exploit RGA;
- modify or create derivative distributions of RGA;
- reverse engineer, decompile, or disassemble RGA.

Use of third-party software interfaced with RGA remains subject to the licenses of the respective third-party software packages.

Please read the [`LICENSE`](LICENSE) and [`THIRD_PARTY_SOFTWARE.md`](THIRD_PARTY_SOFTWARE.md) files before using or redistributing any software components.

---

## Issues and Feedback

If you encounter a problem while using RGA, please submit an issue through the **Issues** section of this repository.

When reporting an issue, please provide the following information whenever possible:

- RGA version;
- Linux distribution;
- relevant analysis module;
- input data type;
- command or analysis step involved;
- complete error message;
- relevant log information.

Please do not upload large sequencing datasets, confidential data, or sensitive information directly to GitHub Issues.

---

## Repository Scope

This repository is the official distribution repository for the **Resequencing Genome Analysis Toolkit (RGA)**.

It is maintained for:

> **Software download · Version management · Documentation · Issue tracking**

and is **not a public source-code repository**.

---

## Contact

For questions related to RGA, please use the **Issues** section of this repository.

For academic collaboration or other inquiries, contact information can be provided here after the corresponding publication is available.

---

## Disclaimer

RGA is provided for research purposes.

The developers make no warranty regarding the accuracy, completeness, reliability, or suitability of the software for any particular purpose.

Users are responsible for validating analysis results and determining whether the software and its parameters are appropriate for their specific datasets and research applications.
