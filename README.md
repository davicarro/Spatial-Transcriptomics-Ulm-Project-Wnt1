# Spatial-Transcriptomics-Ulm-Project-Wnt1
R-based spatial transcriptomics pipeline for analyzing WNT1 G177C-associated gene expression changes across murine musculoskeletal tissues, integrating quality control, Seurat normalization, pseudobulk analysis, PCA, differential expression, and gene set enrichment analysis (GSEA).

# Spatial Transcriptomics Analysis of WNT1-Associated Musculoskeletal Alterations

### R-Based Bioinformatics Pipeline | Ulm University Collaboration

**Author:** David Carro Vázquez, PhD  
**Research collaboration:** Ulm University, Germany  
**Programming language:** R  
**Research area:** Spatial Transcriptomics | Musculoskeletal Biology | Computational Genomics

---

## Project Overview

This repository documents an R-based computational workflow developed for the analysis of spatial transcriptomics data from murine musculoskeletal tissues, focusing on gene expression alterations associated with the *Wnt1* G177C mutation.

The project compares wild-type (*Wnt1*+/+) and homozygous knock-in (*Wnt1* G177C/G177C) samples to characterize genotype-associated transcriptomic changes across different musculoskeletal tissue compartments.

The pipeline integrates spatially resolved transcriptomic data processing, quality control, normalization, dimensionality reduction, differential expression analysis, and functional pathway enrichment.

The workflow was developed as part of a research collaboration with Ulm University, Germany.

## Research Objectives

1. Characterize spatially resolved gene expression patterns across musculoskeletal tissues.
2. Identify transcriptomic differences between wild-type and WNT1 G177C knock-in samples.
3. Investigate tissue-specific molecular signatures associated with the WNT1 mutation.
4. Identify biological pathways potentially affected by genotype-associated transcriptional changes.
5. Develop an integrated computational framework for reproducible spatial transcriptomics analysis.

## Biological Samples and Tissue Regions

The analysis focuses on two experimental genotypes:

- **Wild-type (WT):** *Wnt1*+/+
- **Knock-in (KI):** *Wnt1* G177C/G177C

The spatial transcriptomics analysis encompasses the following tissue regions:

- Bone marrow (BM)
- Callus cartilage
- Callus bone
- Cortical bone
- Muscle

These tissue-specific analyses enable investigation of molecular alterations across distinct musculoskeletal compartments.

## Computational Analysis Pipeline

### 1. Data Import and Quality Control

- Import of 10x Genomics spatial transcriptomics expression matrices in HDF5 format.
- Creation of Seurat objects for individual samples.
- Assignment of spatial barcodes to tissue-specific anatomical regions.
- Calculation and visualization of barcode-level quality metrics, including:
  - Number of detected genes per barcode.
  - Total unique molecular identifiers (UMIs).
  - Transcriptomic complexity.
  - Fraction of expression contributed by the 50 most abundant genes.
- Generation of quality-control summaries and diagnostic plots.

### 2. Data Normalization and Preprocessing

- Processing of tissue-specific expression matrices using Seurat.
- Normalization of transcriptomic expression profiles.
- Preparation of normalized and raw-count expression matrices for downstream analyses.
- Organization of datasets by genotype and anatomical region.

### 3. Pseudobulk Gene Expression Analysis

- Aggregation of transcript counts into pseudobulk expression profiles.
- Library-size normalization using counts per million (CPM).
- Calculation of genotype-associated log2 fold changes.
- Comparison of gene expression profiles across musculoskeletal tissues.
- Identification of genes displaying tissue-specific expression patterns.

### 4. Principal Component Analysis (PCA)

- Dimensionality reduction using normalized pseudobulk expression profiles.
- Visualization of transcriptomic variation between genotypes.
- Extraction of principal component gene loadings.
- Identification of genes contributing to genotype-associated transcriptomic variation.
- Generation of PCA-based gene signatures for downstream functional analysis.

### 5. Differential Gene Expression Analysis

- Differential expression analysis comparing WNT1 G177C knock-in and wild-type samples.
- Application of MAST for modeling barcode-level gene expression differences.
- Estimation of genotype-associated expression changes.
- Identification and visualization of differentially expressed genes.
- Comparison of differential expression signatures across tissue regions.

### 6. Gene Set Enrichment Analysis (GSEA)

- Functional enrichment analysis using the `fgsea` R package.
- Integration of curated gene sets from MSigDB.
- Pathway enrichment analysis based on:
  - Pseudobulk log2 fold-change rankings.
  - PCA-derived gene loadings.
  - Differential expression-derived gene rankings.
- Identification of biological pathways associated with genotype-dependent transcriptomic alterations.

### 7. Comparative Transcriptomic Analysis

- Comparison of gene expression signatures across analytical approaches.
- Evaluation of shared and tissue-specific molecular alterations.
- Visualization of overlapping gene signatures.
- Investigation of transcriptomic relationships between anatomical regions.

### 8. Spatial and Transcriptomic Neighborhood Analysis

- Exploration of transcriptomic relationships between spatially defined regions.
- Comparison of spatial proximity and gene expression similarity.
- Visualization of neighborhood relationships to investigate tissue organization.

## Technologies and R Packages

**Core analysis**

- R and R Markdown
- Seurat and SeuratObject
- Matrix
- edgeR
- MAST

**Functional genomics**

- fgsea
- msigdbr

**Data processing and visualization**

- dplyr
- data.table
- ggplot2
- patchwork
- ggtext
- readxl
- knitr
- htmltools

## Data Availability

The workflow is designed to process 10x Genomics spatial transcriptomics expression matrices together with tissue-specific barcode annotation files.

Raw sequencing data and sample-specific expression matrices are not included in this repository.

The analytical code is provided to document the computational methodology and support reproducibility, subject to the availability of appropriately formatted input datasets.

## Author and Scientific Contributions

**David Carro Vázquez, PhD**

Computational bioinformatics researcher specializing in transcriptomics, spatial omics, and statistical analysis of biological datasets.

This repository documents contributions to the development and implementation of a spatial transcriptomics analysis workflow, including:

- Computational preprocessing and quality-control procedures.
- Tissue-specific gene expression analysis.
- Pseudobulk normalization and transcriptomic comparisons.
- Principal component analysis and gene signature extraction.
- Differential expression analysis.
- Gene set enrichment and functional interpretation.
- Integration and visualization of genotype-associated transcriptomic patterns.

The computational workflow was developed in the context of a scientific collaboration with researchers at Ulm University, Germany.

## Reproducibility and Usage

The analysis is implemented in R and uses established bioinformatics packages for transcriptomic data processing.

To reproduce the analyses, users should:

1. Install the required R and Bioconductor packages.
2. Obtain compatible spatial transcriptomics expression matrices and barcode annotation files.
3. Configure the input directory and sample identifiers in the R Markdown workflow.
4. Execute the analysis sections in their documented order.

The workflow may require adaptation to different experimental designs, sample annotations, and sequencing platforms.

## License

Please refer to the repository's LICENSE file for the applicable terms of use.

## Citation and Contact

**David Carro Vázquez, PhD**

GitHub: https://github.com/davicarro

For scientific inquiries or collaboration requests, please contact the repository author through GitHub.
