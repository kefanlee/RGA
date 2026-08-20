# **Resequencing Genome Analysis Toolkit**

![Version](https://img.shields.io/badge/version-3.24-1f6feb)
![Platform](https://img.shields.io/badge/platform-Linux-2f855a)
![Distribution](https://img.shields.io/badge/distribution-binary--only-f59e0b)
![License](https://img.shields.io/badge/license-PolyForm%20Noncommercial%201.0.0-d73a49)

RGA is a command-line toolkit for reproducible analysis of paired-end whole-genome resequencing data. It integrates read alignment, BAM processing and quality assessment, SNP/INDEL calling, structural-variant detection, target-sample-specific candidate filtering, functional annotation, result merging, and optional IGV batch snapshots in a single workflow.

Website: [https://rga.kefan.work/](https://rga.kefan.work/)  
Contact: [Zhe Li](mailto:lizhe@impcas.ac.cn) | [Yan Du](mailto:duyan@impcas.ac.cn)  
Citation: [How to cite RGA](#citation)

> [!IMPORTANT]
> This repository distributes compiled RGA release packages, documentation, and release information. RGA source code is not published in this repository. RGA is therefore described as **binary-distributed research software**, not as open-source software.

---


## Overview

**RGA** is an integrated command-line toolkit for automated and reproducible analysis of paired-end whole-genome resequencing data. It was developed to simplify multi-step resequencing workflows by integrating commonly used bioinformatics tools into a unified analysis framework with standardized execution and output organization.

The RGA workflow covers the major stages of whole-genome variant analysis, including read alignment, BAM processing and quality assessment, SNP and INDEL calling, structural-variant detection, variant filtering, functional annotation, result merging, and optional IGV-based visualization. RGA supports **BWA or BWA-MEM2** for read alignment, **GATK and/or VarScan** for SNP and INDEL detection, **Qualimap** for alignment quality assessment, **snpEff** for functional annotation, and **sv-callers** for optional structural-variant analysis using multiple SV callers.

A central function of RGA is **multi-sample candidate variant screening**. For each target sample, candidate variants can be filtered according to alternative-allele frequency and read support in the target sample while simultaneously evaluating the corresponding genomic positions across non-target samples. This strategy helps reduce shared background variation and prioritize target-sample-specific candidate variants, making RGA particularly suitable for large mutant populations and other resequencing studies involving multiple related samples.

RGA also supports multi-threaded analysis, resume-aware execution, optional removal of large intermediate alignment files, automated IGV batch snapshots, and analysis-completion notifications. These functions reduce repetitive manual operations and improve the consistency and reproducibility of large-scale resequencing analyses.

RGA was developed primarily for genomic analysis of experimentally induced mutant populations and is applicable to studies involving radiation mutagenesis, heavy-ion irradiation, space mutagenesis, chemical mutagenesis, and other mutant resources. It can also be applied to general multi-sample whole-genome resequencing projects when appropriate reference genome and annotation resources are available.

RGA is currently distributed as **compiled Linux research software**. This repository provides official release packages, documentation, and version information; the RGA source code is not publicly distributed.

---

## Citation

If RGA is used in your research, please report the RGA version and major analysis parameters.

Until the corresponding RGA publication is available, the software can be cited as:

```text
Formal citation information will be updated after publication of the corresponding RGA manuscript.


```

In the Methods section, RGA may be described as:

```text
Whole-genome resequencing data were analyzed using the
Resequencing Genome Analysis Toolkit (RGA, version 3.24).
```

Please also cite the original publications of the external bioinformatics tools actually used in the analysis, including BWA/BWA-MEM2, Samtools, GATK, VarScan, Qualimap, snpEff, IGV, **sv-callers**, and the structural-variant callers used by the selected sv-callers workflow.

Formal citation information will be updated after publication of the corresponding RGA manuscript.

---

## Installation

Download the latest RGA package from the **Releases** page.

```bash
tar -xzf rga-v3.24-linux-x86_64.tar.gz
cd rga-v3.24-linux-x86_64
chmod +x rga
```

Create the main Conda environment:

```bash
conda env create -n rga -f conda-bioinfo-environment.yml
conda activate rga
```

If structural-variant analysis through **sv-callers** is required, create the corresponding workflow environment:

```bash
conda env create -n wf -f conda-wf-environment.yml
```

Before the first analysis, check the software environment:

```bash
./rga -envcheck
```

For structural-variant analysis with sv-callers:

```bash
./rga -enable-sv -envcheck
```

The RGA release package includes an unmodified copy of the official **sv-callers v1.2.2** release archive. When SV analysis is enabled, RGA prepares the bundled sv-callers workflow automatically unless a custom sv-callers path is specified.

---

## Input Data

Input FASTQ files should be placed under:

```text
data/group_data/
```

Each sample group must have its own directory.

```text
project/
├── rga
└── data/
    └── group_data/
        ├── group_A/
        │   ├── sample01_1.clean.fq.gz
        │   ├── sample01_2.clean.fq.gz
        │   ├── sample02_1.clean.fq.gz
        │   └── sample02_2.clean.fq.gz
        └── group_B/
            ├── sample03_1.clean.fq.gz
            └── sample03_2.clean.fq.gz
```

Required FASTQ naming format:

```text
<sample>_1.clean.fq.gz
<sample>_2.clean.fq.gz
```

A minimal analysis can be started with:

```bash
./rga \
  -R /absolute/path/to/reference.fa \
  -sdn snpEff_database_name
```

Example using BWA-MEM2 and both GATK and VarScan:

```bash
./rga \
  -R /absolute/path/to/reference.fa \
  -sdn snpEff_database_name \
  -t 16 \
  -mt bwa-mem2 \
  -c both
```

To additionally enable structural-variant detection with sv-callers:

```bash
./rga \
  -R /absolute/path/to/reference.fa \
  -sdn snpEff_database_name \
  -t 16 \
  -mt bwa-mem2 \
  -c both \
  -enable-sv
```

---

## Core Options

| Option                      | Description                                           | Default  |
| --------------------------- | ----------------------------------------------------- | -------- |
| `-R`, `-ref FILE`           | Reference-genome FASTA                                | required |
| `-sdn`, `-snpeffdbname STR` | snpEff database name                                  | required |
| `-t`, `-threads INT`        | Number of threads                                     | `16`     |
| `-mt`, `-mappingtool STR`   | `bwa` or `bwa-mem2`                                   | `bwa`    |
| `-c`, `-caller STR`         | `gatk`, `varscan`, or `both`                          | `gatk`   |
| `-maxf`, `-max-freq FLOAT`  | Minimum ALT frequency in target sample                | `0.25`   |
| `-minf`, `-min-freq FLOAT`  | Maximum ALT frequency in non-target samples           | `0.10`   |
| `-tr`, `-total-reads INT`   | Minimum total read support                            | `0`      |
| `-ar`, `-alt-reads INT`     | Minimum ALT read support                              | `1`      |
| `-enable-sv`                | Enable structural-variant analysis through sv-callers | disabled |
| `-enable-snp-indel-igv`     | Generate SNP/INDEL IGV snapshots                      | disabled |
| `-enable-sv-igv`            | Generate SV IGV snapshots                             | disabled |
| `-autoclear`                | Remove alignment intermediates                        | disabled |
| `-send-email`               | Send completion notification                          | disabled |
| `-lang STR`                 | Interface language: `en`, `zn`, `zh`                  | `en`     |
| `-envcheck`                 | Check runtime environment and exit                    | disabled |


---

## Outputs

Final alignment files:

```text
data/group_data/<group>/<sample>/<sample>_final.bam
data/group_data/<group>/<sample>/<sample>_final.bam.bai
```

Caller-specific results:

```text
data/group_data/<group>/gatk_snp_indel/
data/group_data/<group>/varscan_snp_indel/
data/group_data/<group>/sv_detection/
```

The `sv_detection/` directory contains structural-variant results generated through the **sv-callers** workflow when `-enable-sv` is enabled.

Final annotated candidate VCF files are generated in the project working directory:

```text
The_Final_All.CustomFiltering.gatk.ann.<timestamp>.vcf
The_Final_All.CustomFiltering.varscan.ann.<timestamp>.vcf
The_Final_All.CustomFiltering.sv.ann.<timestamp>.vcf
```

Candidate variants generated by RGA should be further evaluated using sequencing quality, read support, genomic context, IGV inspection, and experimental validation when appropriate.

---

## License

RGA-authored binary software and documentation are distributed under the **PolyForm Noncommercial License 1.0.0**.

See:

[LICENSE](./LICENSE)

RGA may be used for qualifying noncommercial purposes under the terms of this license. Commercial use requires separate written authorization from the copyright holder.

RGA is distributed as **binary-only research software** and is not an open-source software distribution.

Third-party software and bundled components remain subject to their respective licenses.

The RGA release package includes an unmodified copy of the official **sv-callers v1.2.2** release archive. sv-callers remains subject to its original **Apache License 2.0**, and the individual software packages used within the workflow remain subject to their respective licenses.

See:

[THIRD_PARTY_NOTICES.md](./THIRD_PARTY_NOTICES.md)

---

## Support

For questions, bug reports, or reproducibility issues:

* **Website:** https://rga.kefan.work/
* **Email:** [lizhe@impcas.ac.cn](mailto:lizhe@impcas.ac.cn) | [duyan@impcas.ac.cn](mailto:duyan@impcas.ac.cn)
* **Issues:** use this repository's **Issues** page

When reporting an issue, please include the RGA version, operating system, command used, relevant log output, and error message.
