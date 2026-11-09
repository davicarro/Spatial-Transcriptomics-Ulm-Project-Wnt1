# 🧬 Spatial Transcriptomics Analysis of WNT1-Associated Musculoskeletal Alterations

### 🔬 R-Based Bioinformatics Pipeline | Ulm University Research Collaboration

**Author:** David Carro Vázquez, PhD  
**Research collaboration:** Ulm University, Germany  
**Programming language:** R  
**Research area:** Spatial Transcriptomics | Musculoskeletal Biology | Computational Genomics

---

## 📖 Project Overview

This repository documents an R-based computational pipeline developed to investigate spatially resolved gene expression alterations associated with the *Wnt1* G177C mutation in murine musculoskeletal tissues.

The study compares wild-type (*Wnt1*+/+) and homozygous knock-in (*Wnt1* G177C/G177C) samples to characterize genotype-associated transcriptional changes across anatomically distinct tissue compartments.

The computational framework integrates spatial transcriptomics preprocessing, quality control, normalization, pseudobulk expression profiling, dimensionality reduction, differential expression analysis, gene set enrichment analysis, and spatial neighborhood exploration.

The workflow was developed in the context of a research collaboration with Ulm University, Germany.

## 🎯 Research Objectives

1. Characterize spatially resolved gene expression patterns across musculoskeletal tissues.
2. Identify transcriptional alterations associated with the *Wnt1* G177C mutation.
3. Investigate tissue-specific molecular signatures distinguishing wild-type and knock-in samples.
4. Identify biological pathways potentially affected by genotype-associated transcriptional changes.
5. Compare molecular signatures obtained through complementary transcriptomic analysis methods.
6. Develop a documented computational framework for spatial transcriptomics analysis.

## 🧪 Biological Samples and Tissue Regions

The analysis focuses on two experimental genotypes:

- **Wild-type (WT):** *Wnt1*+/+
- **Knock-in (KI):** *Wnt1* G177C/G177C

The spatial transcriptomics datasets encompass five musculoskeletal tissue regions:

| Tissue Region | Abbreviation | Biological Context |
|---|---|---|
| Bone marrow | BM | Hematopoietic and skeletal microenvironment |
| Callus cartilage | — | Cartilaginous component of the repair tissue |
| Callus bone | — | Bone formation and remodeling within the callus |
| Cortical bone | — | Structural skeletal compartment |
| Muscle | — | Musculoskeletal tissue surrounding the skeletal region |

Tissue-specific analyses allow the investigation of heterogeneous transcriptional responses to the WNT1 mutation across distinct anatomical compartments.

---

## ⚙️ Computational Analysis Pipeline

### 🔹 1. Data Import and Barcode Quality Control

The pipeline imports 10x Genomics spatial transcriptomics expression matrices and integrates spatial barcode annotations with anatomical region information.

**Main analytical steps:**

- Import HDF5 gene expression matrices using `Read10X_h5()`.
- Generate Seurat objects for individual samples.
- Match spatial barcode identifiers with tissue-specific annotation tables.
- Construct tissue-specific expression datasets.
- Calculate barcode-level quality-control metrics, including:
  - Number of detected genes per barcode.
  - Total unique molecular identifiers (UMIs).
  - Transcriptomic complexity.
  - Fraction of total expression contributed by the 50 most abundant genes.
- Generate quality-control tables, histograms, violin plots, and diagnostic scatter plots.

These procedures support the characterization of transcriptomic data quality and the identification of technical differences between samples and tissue compartments.

### 🔹 2. Data Normalization and Preprocessing

Expression matrices are processed using Seurat-based workflows to prepare the data for downstream analyses.

**Main analytical steps:**

- Organize expression matrices by genotype and anatomical region.
- Preserve raw transcript counts for count-based analyses.
- Normalize gene expression profiles for comparative analyses.
- Prepare tissue-specific datasets for dimensionality reduction and differential expression analysis.
- Generate normalized expression matrices for downstream statistical analyses.

### 🔹 3. Pseudobulk Gene Expression Analysis

Pseudobulk analysis is used to investigate genotype-associated gene expression changes at the tissue level.

**Main analytical steps:**

- Aggregate raw transcript counts from spatial barcodes into tissue- and genotype-specific expression profiles.
- Apply library-size normalization using counts per million (CPM).
- Calculate log2 fold changes between knock-in and wild-type expression profiles.
- Identify genes displaying increased or decreased expression in knock-in tissues.
- Compare gene expression changes across anatomical compartments.
- Investigate tissue-enriched transcriptional patterns.

**Expression comparison:**

`log2FC = log2(Expression_KI / Expression_WT)`

Positive log2 fold changes indicate higher relative expression in knock-in samples, whereas negative values indicate higher relative expression in wild-type samples.

### 🔹 4. Principal Component Analysis (PCA)

PCA is applied to normalized pseudobulk expression profiles to investigate transcriptomic variation and genotype-associated molecular signatures.

**Main analytical steps:**

- Perform dimensionality reduction using normalized expression matrices.
- Visualize transcriptomic differences between wild-type and knock-in samples.
- Examine the contribution of individual genes to principal components.
- Extract principal component gene loadings.
- Identify genes associated with major axes of transcriptomic variation.
- Generate PCA-derived gene rankings for downstream functional enrichment analysis.

PCA-based signatures complement differential expression analysis by identifying genes contributing to transcriptomic variation rather than exclusively measuring differences in mean expression.

### 🔹 5. Differential Gene Expression Analysis Using MAST

The pipeline implements MAST to investigate genotype-associated gene expression differences at the spatial barcode level.

**Main analytical steps:**

- Compare wild-type and WNT1 G177C knock-in expression profiles.
- Apply MAST-based statistical modeling to barcode-level expression data.
- Account for differences in gene detection rates through the configured model.
- Estimate genotype-associated expression changes.
- Identify candidate differentially expressed genes.
- Generate gene expression comparisons and visualizations.
- Compare differential expression signatures across tissue regions.

Spatial barcodes are treated as transcriptomic observations and do not necessarily represent individual cells.

### 🔹 6. Gene Set Enrichment Analysis (GSEA)

Functional enrichment analysis is performed to identify biological pathways associated with genotype-dependent transcriptional alterations.

**Main analytical steps:**

- Retrieve curated mouse gene sets from MSigDB using `msigdbr`.
- Perform enrichment analysis using `fgsea`.
- Investigate Hallmark, C2, and C5 gene set collections.
- Generate ranked gene lists based on:
  - Pseudobulk log2 fold changes.
  - PCA-derived gene loadings.
  - MAST differential expression results.
- Calculate enrichment statistics and adjusted significance values.
- Compare enriched biological pathways across tissue regions and analytical methods.

This approach supports the functional interpretation of transcriptomic changes associated with the WNT1 mutation.

### 🔹 7. Comparative Transcriptomic Analysis

The workflow integrates complementary gene expression signatures to investigate the consistency and tissue specificity of genotype-associated transcriptional changes.

**Main analytical steps:**

- Compare gene rankings generated through pseudobulk analysis, PCA, and MAST.
- Identify overlapping and method-specific gene signatures.
- Evaluate shared and tissue-specific transcriptional alterations.
- Generate comparative visualizations, including gene-overlap diagrams.
- Investigate molecular patterns associated with the WNT1 mutation across musculoskeletal compartments.

### 🔹 8. Spatial and Transcriptomic Neighborhood Analysis

The pipeline includes exploratory analyses of spatial and molecular relationships between transcriptomic observations.

**Main analytical steps:**

- Investigate relationships between spatially defined transcriptomic neighborhoods.
- Evaluate spatial proximity between observations.
- Compare spatial adjacency with gene expression similarity.
- Visualize neighborhood relationships using shared low-dimensional representations.
- Explore the relationship between anatomical organization and transcriptomic heterogeneity.

---

## 📂 Input Data Format and Structure

The pipeline requires two complementary input types.

### 1. Gene Expression Matrices

10x Genomics HDF5 files:

`{SampleID}_filtered_feature_bc_matrix.h5`

These files contain gene expression count matrices indexed by spatial barcodes.

### 2. Tissue-Specific Barcode Annotation Files

Excel files:

`{SampleID}_{Subregion}.xlsx`

Each annotation file contains:

- **Column 1:** Spatial barcode identifiers.
- **Additional columns:** Tissue-specific annotations and available sample metadata.

The R workflow matches barcode identifiers between the expression matrices and annotation tables to construct tissue-specific Seurat objects.

**Example input structure:**

```text
data/
├── WT_filtered_feature_bc_matrix.h5
├── KI_filtered_feature_bc_matrix.h5
├── WT_BM.xlsx
├── KI_BM.xlsx
├── WT_CallusCartilage.xlsx
├── KI_CallusCartilage.xlsx
├── WT_CallusBone.xlsx
├── KI_CallusBone.xlsx
├── WT_CorticalBone.xlsx
├── KI_CorticalBone.xlsx
├── WT_Muscle.xlsx
└── KI_Muscle.xlsx
```

---

## 🧰 Technologies and R Packages

### 🔬 Core Bioinformatics

- **R and R Markdown:** Computational analysis and reproducible reporting.
- **Seurat / SeuratObject:** Spatial transcriptomics data processing and organization.
- **Matrix:** Efficient manipulation of sparse expression matrices.
- **edgeR:** CPM normalization and pseudobulk expression processing.
- **MAST:** Barcode-level differential expression analysis.

### 🧬 Functional Genomics

- **fgsea:** Gene set enrichment analysis.
- **msigdbr:** Access to curated MSigDB gene sets.

### 📊 Data Processing and Visualization

- **dplyr / data.table:** Data manipulation and organization.
- **ggplot2:** Statistical visualization.
- **patchwork:** Multi-panel figure generation.
- **ggtext:** Formatted scientific plot labels.
- **readxl:** Import of barcode annotation tables.
- **knitr / htmltools:** Automated reporting and HTML output.

---

## ▶️ Reproducibility and Usage

The workflow is implemented in R Markdown and organized into sequential analytical sections.

To reproduce the analysis:

1. Install the required R and Bioconductor packages.
2. Obtain compatible 10x Genomics expression matrices and tissue-specific barcode annotation files.
3. Configure the input data directory in the R Markdown script.
4. Define the sample identifiers and anatomical regions.
5. Execute the quality-control and preprocessing sections.
6. Run the downstream pseudobulk, PCA, differential expression, and enrichment analyses.
7. Review the generated figures, statistical summaries, and functional enrichment results.

The workflow contains dataset-specific configuration parameters and may require adaptation to other experimental designs or sequencing platforms.

---

## 📊 Data Availability

Raw sequencing data, spatial barcode annotation files, and sample-specific expression matrices are not included in this repository.

The computational code is provided to document the analytical methodology and facilitate adaptation of the workflow to compatible datasets.

Reproduction of the original analyses requires access to the corresponding experimental data.

---

## 👨‍🔬 Author and Scientific Contributions

**David Carro Vázquez, PhD**

Computational bioinformatics researcher specializing in transcriptomics, spatial omics, and statistical analysis of biological datasets.

This repository documents computational contributions to the development and implementation of:

- Spatial transcriptomics preprocessing and quality-control workflows.
- Tissue-specific gene expression analysis.
- Pseudobulk normalization and genotype-associated expression comparisons.
- Principal component analysis and gene signature extraction.
- Barcode-level differential expression analysis using MAST.
- Functional pathway enrichment using GSEA.
- Comparative analysis of molecular signatures across musculoskeletal tissues.
- Spatial and transcriptomic neighborhood exploration.
- Statistical visualization and automated reporting.

The computational workflow was developed in the context of a scientific collaboration with researchers at Ulm University, Germany.

---

## 📜 License

This project is distributed under the terms specified in the repository's [LICENSE](LICENSE) file.

---

## 📬 Citation and Contact

**David Carro Vázquez, PhD**

GitHub: https://github.com/davicarro

For questions regarding the computational pipeline or potential scientific collaborations, please contact the repository author through GitHub.
