# Third-Party Software Notices

RGA invokes, bundles, or assists with the installation of third-party software. Each third-party component remains the property of its respective copyright holder and is governed by its own license. The RGA license applies only to RGA-authored material and does not replace, extend, or restrict the rights granted by third-party licenses.

## Components Included in the RGA Distribution

### sv-callers v1.2.2

- Bundled file: `svtools/sv-callers-1.2.2.zip`
- Upstream project: [GooglingTheCancerGenome/sv-callers](https://github.com/GooglingTheCancerGenome/sv-callers)
- Archived release: [Zenodo record 7351790](https://zenodo.org/records/7351790)
- Distribution form: unmodified copy of the official v1.2.2 release archive
- Official archive MD5: `2877aec92c0dec276cc0b7621b6d2f92`
- Upstream license: Apache License 2.0
- License copy: `sv-callers-1.2.2/LICENSE` inside the archive

The Apache License 2.0 permits redistribution in source or object form subject to its license, attribution, modification-notice, and NOTICE-preservation requirements. RGA preserves the upstream license inside the unmodified release archive. If the archive is modified in a future RGA release, the changed files must carry prominent modification notices. Any upstream `NOTICE` file must also be preserved and distributed as required by Apache License 2.0.

The sv-callers workflow may install or invoke additional software, including DELLY, Manta, LUMPY, GRIDSS, BCFtools, Viola-SV, and SURVIVOR. These programs retain their own licenses and citation requirements; they are not relicensed by either RGA or the Apache-2.0 license of the sv-callers workflow.

Suggested citation:

> Kuzniar A, Maassen J, Verhoeven S, et al. sv-callers: a highly portable parallel workflow for structural variant detection in whole-genome sequence data. PeerJ. 2020;8:e8214. doi:10.7717/peerj.8214.

### VarScan v2.3.9

- Bundled file: `varscan/VarScan.v2.3.9.jar`
- Upstream project: [VarScan](https://github.com/dkoboldt/varscan)
- Legacy v2.3.9 site: [VarScan on SourceForge](https://varscan.sourceforge.net/)
- Upstream terms: noncommercial use by academic, government, and nonprofit/not-for-profit institutions

RGA does not grant any rights to VarScan beyond those granted by the VarScan copyright holder. Organizations that do not clearly qualify under the upstream noncommercial terms must obtain the appropriate permission or commercial license before using the VarScan workflow.

The public upstream statement reviewed for VarScan describes permitted noncommercial use but does not clearly state a general right to redistribute the v2.3.9 JAR. The RGA release maintainer must therefore confirm or obtain redistribution authorization before publishing a release that contains this file. If redistribution authorization is not available, the JAR should be obtained by the end user from an authorized upstream source rather than included in the RGA release.

Suggested citation:

> Koboldt DC, Zhang Q, Larson DE, et al. VarScan 2: somatic mutation and copy number alteration discovery in cancer by exome sequencing. Genome Research. 2012;22:568-576. doi:10.1101/gr.129684.111.

## External Runtime Dependencies

The following programs are normally installed separately by the user or through Conda and are not licensed under the RGA license:

| Software | Role in RGA |
| --- | --- |
| BWA / BWA-MEM2 | Reference-genome indexing and read alignment |
| Samtools | FASTA indexing, BAM processing, indexing, and mpileup generation |
| GATK | Reference dictionary creation and SNP/INDEL calling |
| Qualimap | BAM quality assessment |
| snpEff | Variant-effect annotation |
| IGV | Batch visualization and snapshot generation |
| Xvfb | Virtual display for graphical programs on headless Linux servers |
| Conda | Runtime environment management |
| Snakemake | sv-callers workflow execution |

Users must review the license and citation requirements of the exact versions installed in their environments. Availability through a public package repository does not imply that a program is covered by the RGA license.

## Reporting License Issues

If a distributed component appears to be missing an attribution, license text, or required notice, stop redistributing the affected release and contact [lizhe@impcas.ac.cn](mailto:lizhe@impcas.ac.cn) with the component name and RGA release version.
