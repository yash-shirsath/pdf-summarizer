# Section 3: 3D Genome Architecture and Methylation-Chromatin Relationships

## Overview

This section presents a comprehensive analysis of the three-dimensional genome architecture and its relationship with DNA methylation patterns across different cell types. The research demonstrates how chromatin conformation and DNA methylation work together to regulate gene expression and cellular identity, revealing significant variability in 3D genome organization across cell types and tissues.

## 3D Genome Architecture Variability Across Cell Types

### Single-Cell Hi-C Analysis Framework

The study employed **scHiCluster** to generate single-cell embeddings at 100 kb resolution, providing unprecedented insight into chromatin organization at the single-cell level. Key methodological approaches include:

- **Contact Matrix Processing**: Upper triangle contact matrices within 1Mb distance were reshaped to 1D arrays for each chromosome
- **Dimensionality Reduction**: Singular Value Decomposition (SVD) was performed on chromatin contacts, retaining the first 50 dimensions per chromosome
- **Multi-Chromosomal Integration**: All chromosomes were concatenated horizontally followed by another round of SVD
- **Embedding Generation**: Significant dimensions reaching the 0.01 threshold were used to produce t-SNE embeddings

### Chromatin Compartment Analysis

The research revealed distinct **A and B compartment patterns** across cell types:

#### Compartment Identification
- **100 kb resolution** pseudo-bulk contact matrices generated for each chromosome
- **Principal Component Analysis (PCA)** performed on distance-normalized, Pearson correlation matrices
- **PC1 used as compartment score** with positive scores corresponding to higher CpG density regions
- **Reference establishment** through merged contact maps from all 86,689 cells

#### Compartment Strength Quantification
Compartment strength was calculated using a sophisticated binning approach:
- 100 kb bins ranked by compartment scores and divided into 50 equal groups
- Distance-normalized interaction frequencies averaged within and between groups
- **Compartment strength formula**: [Sum(BB) + Sum(AA)] / [Sum(AB) + Sum(BA)]
- This ratio reflects the relative enrichment of same-compartment versus cross-compartment interactions

## Association Between Chromatin Conformation and DNA Methylation

### Methylation Compartment Discovery

The study identified **partially methylated domains (PMDs)** as a distinct genomic feature:

- **10 kb bin analysis** using CpG methylation level histograms as features
- **KMeans++ clustering** with 100 equally sized bins between 0 and 1
- **PMD density scores** computed as the proportion of 10kb bins assigned to partially methylated compartments within each 100kb bin
- Strong association between methylation compartments and chromatin structure

### Integration of Methylation and 3D Organization

#### Multi-Modal Data Integration
The research developed innovative approaches to combine methylation (mCG) and chromatin contact (3C) data:

- **Direct concatenation** of embeddings from both modalities
- **Weighted Nearest Neighbor (WNN)** framework testing
- **Concatenated approach preferred** when modalities separate cells along different axes
- **50 dimensions** used from both modalities for all-cell clustering

#### Methylation-Contact Correspondence
Key findings include:
- **Cell-type-specific compartmentalization** varies significantly between neuronal and non-neuronal cells
- **Non-neuronal cells** show higher proportion of intra-compartment contacts at long distances
- **Distance-normalized contact patterns** reveal cell-type-specific 3D organization preferences

## Discrepancies Between DNA Methylation and Chromatin Contact

### Methodological Challenges in Integration

The study identified several important discrepancies and limitations:

#### WNN vs. Concatenation Trade-offs
- **WNN embedding** maintained clustered cells from both modalities but expanded them according to other modality variations
- **Concatenated embedding** preserved 3C cluster structures but distorted mC clusters
- **Context-dependent performance**: Some tissues showed weak mC clustering, requiring algorithm preference for 3C modality

#### Resolution and Coverage Issues
- **Raw vs. imputed matrices**: Raw matrices provided higher resolution for large cell populations, while imputed matrices performed better for smaller populations
- **Coverage filtering**: Bins retained with coverage between 99th percentile and twice median minus 99th percentile
- **Distance normalization** required before correlation matrix computation

### Cell-Type-Specific Patterns

#### Neuronal vs. Non-Neuronal Differences
Significant variations observed between cell types:
- **Long-range interaction patterns** differ substantially between neuronal and non-neuronal cells
- **Compartment boundary transitions** identified with AUROC thresholds > 0.9 or < 0.1
- **Domain boundary analysis** at 25kb resolution using TopDom wrapper

## Key Insights About Genome Organization

### Hierarchical Organization Principles

#### Multi-Scale Architecture
The research reveals genome organization operates at multiple scales:
- **Compartment level** (A/B compartments at 100kb resolution)
- **Domain level** (Topologically Associating Domains at 25kb resolution)
- **Loop level** (Specific chromatin interactions)

#### Cell-Type Specificity
- **206 subtypes** identified across all 86,689 cells through iterative supervised learning
- **Consensus Leiden clustering** with 500 different random initializations
- **Separation scores** (AUROC and AUPR) used to validate cluster distinctions

### Regulatory Implications

#### Methylation-Mediated Regulation
- **Differentially methylated regions (DMRs)** associated with cell-type-specific chromatin organization
- **Hypo-methylated regions** typically correspond to active regulatory elements
- **PMDs** represent distinct regulatory domains with specific chromatin conformations

#### Functional Integration
- **Multi-modal clustering** reveals functional relationships between methylation and 3D structure
- **Tissue-specific patterns** demonstrate coordinated regulation of epigenetic and structural features
- **Developmental trajectories** reflected in both methylation and chromatin organization changes

## Technical Innovations

### Computational Advances
- **Sparse matrix optimization** for large-scale single-cell analysis
- **Geosketch sampling** to handle cell-type abundance differences
- **Distance-based anchor filtering** to prevent cross-cell-type integration artifacts

### Quality Control Measures
- **Doublet detection** using methylation-based simulation methods
- **Coverage normalization** across different sequencing depths
- **Batch effect correction** through canonical correlation analysis

This comprehensive analysis demonstrates that 3D genome architecture and DNA methylation are intimately linked regulatory systems that vary significantly across cell types, with important implications for understanding cellular identity and function.