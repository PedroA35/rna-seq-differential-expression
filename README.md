# Differential Expression Analysis of RNA-seq Data in Lung Adenocarcinoma (LUAD)

A reproducible, end-to-end bioinformatics portfolio project investigating transcriptional alterations between lung adenocarcinoma (LUAD) and adjacent normal lung tissue using public bulk RNA-seq data.

## Biological Question

> *What are the key transcriptional changes that drive the transition from normal lung epithelium to adenocarcinoma, and which essential cellular processes (e.g., loss of pneumocyte differentiation markers vs. cell cycle hyperactivation and extracellular matrix remodeling) dominate this oncogenic shift?*

## Key Highlights

- **End-to-End Workflow:** From raw FASTQ files through quality control, alignment/quantification, statistical modeling, to functional enrichment and literature-based biological validation.
- **Reproducibility:** Version-controlled dependencies via Conda/Docker and standardized pipeline execution with Nextflow (`nf-core/rnaseq`).
- **Statistical Rigor:** Paired experimental design modeling in `DESeq2` to control for inter-individual patient variability, followed by False Discovery Rate (FDR) control and independent filtering.
- **Functional Context:** Over-representation analysis (ORA) and Gene Set Enrichment Analysis (GSEA) to contextualize differential expression within established molecular pathways (GO, KEGG, Reactome).

---

## Repository Structure

```text
.
├── .gitignore               # Ignores large raw/intermediate files and temporary artifacts
├── README.md                # Project overview, setup, and instructions
├── environment.yml          # Conda environment definition for reproducibility
├── data/
│   ├── raw/                 # Raw FASTQ files downloaded from SRA/GEO (untracked)
│   ├── metadata/            # Curated sample sheet and experimental covariates (tracked)
│   └── reference/           # Reference genome and annotation files (untracked)
├── results/
│   ├── 01_fastqc/           # Initial and post-trimming FastQC/MultiQC reports
│   ├── 02_trimmed/          # Cleaned/filtered FASTQ files (untracked)
│   ├── 03_quant/            # Gene/transcript count matrices from nf-core/rnaseq
│   └── 04_de_analysis/      # DESeq2 statistical results, normalized counts, and gene lists
├── figures/                 # High-resolution figures (PCA, Volcano plots, Heatmaps)
├── scripts/
│   ├── 00_download_data.sh  # SRA data download and metadata retrieval
│   ├── 01_run_qc.sh         # Quality control (FastQC) and adapter/quality trimming (fastp)
│   ├── 02_run_nfcore.sh     # Nextflow pipeline orchestration
│   ├── 03_qc_and_deseq2.R   # Exploratory data analysis (PCA, clustering) and differential expression
│   └── 04_enrichment.R      # Functional enrichment analysis (GO/KEGG/GSEA via clusterProfiler)
└── reports/
    └── report.qmd           # Complete analytical report in Quarto/R Markdown
```

---

## Workflow Overview

1. **Phase 0 & 2 — Data Acquisition & Metadata Curation:** Public bulk RNA-seq dataset selection (LUAD vs. adjacent normal) and systematic metadata extraction.
2. **Phase 3 — Quality Control & Preprocessing:** Base-call quality assessment via FastQC/MultiQC and read filtering/adapter clipping via `fastp`.
3. **Phase 4 — Alignment & Quantification:** Robust workflow orchestration using the `nf-core/rnaseq` pipeline (STAR + Salmon) against the human reference genome (GRCh38 / Ensembl).
4. **Phase 5 & 6 — Exploratory QC & Differential Expression:** Unsupervised clustering and PCA for batch/outlier detection; negative binomial generalized linear model fitting using `DESeq2`.
5. **Phase 7 & 9 — Functional Enrichment & Biological Validation:** Pathway analysis (GO Biological Process, KEGG) and literature benchmark against established LUAD hallmarks (e.g., TCGA landmarks).

---

## Setup & Getting Started

### Prerequisites

- [Conda](https://docs.conda.io/en/latest/) or [Mamba](https://mamba.readthedocs.io/en/latest/)
- [Docker](https://www.docker.com/) or [Singularity](https://sylabs.io/singularity/) (for running Nextflow pipelines)
- [Nextflow](https://www.nextflow.io/) (>= 22.10.0)

### Environment Installation

```bash
# Clone the repository
git clone https://github.com/PedroA35/rna-seq-differental-expression.git
cd rna-seq-differental-expression

# Create and activate the conda environment
conda env create -f environment.yml
conda activate rnaseq-luad
```

---

## Author

- **Pedro Afonso**, Faculdade de Ciências da Universidade do Porto (FCUP)
