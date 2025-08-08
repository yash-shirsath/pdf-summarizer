# Section 5: Analysis Methods, References, and Supplementary Information

## Overview

This section provides a comprehensive overview of the computational methods, technical implementations, and supplementary materials used in the single-cell atlas of human DNA methylation and 3D genome structure. The study employed novel and improved analytical approaches to handle the large-scale, multi-modal dataset comprising 86,689 cells across 16 human tissues.

## Cell Embedding and Clustering Approaches

### Novel 5kb Bin-Based Clustering Method

The study developed an improved method for clustering single-cell methylation data using **5kb genomic bins** as features, which outperformed traditional 100kb-bin-based methods, particularly for brain cells. This approach addressed the challenge of identifying cell types in tissues where fewer long and specific methylation features were observed compared to neuronal tissues.

**Key Features:**
- Universal adaptability across different tissue types
- Enhanced sensitivity for cell type identification
- Improved resolution for distinguishing cellular subtypes
- Overcame limitations of promoter-focused or enhancer-dependent methods

### Anchor-Based Integration Method

To address batch effects across donors and tissues, the researchers implemented:
- **Anchor-based method** for data integration between donors
- **Geometric distance-based filtering** to refine anchors
- Comparison of two embedding strategies:
  - Direct concatenation of mCG and 3C embeddings
  - Weighted nearest neighbor (WNN) framework

The direct concatenation approach was selected as it better preserved cluster structures when modalities showed different separation patterns.

## Quality Control and Data Processing

### Exclusion List Generation

A critical quality control measure involved creating an **exclusion list for 3D genome contacts** to remove artifactual contacts:
- Removed misalignments over repeat regions due to 3-base pair genome alignment
- Filtered regions with unusually high signals overlapping with highly repeated regions
- Applied consistent filtering across different donors and cell types
- Used median signal >1 as selection criterion for exclusion

### Contact Distance Thresholds

The study established a **2.5kb cutoff** for classifying read pairs as chromatin contacts by:
- Comparing snmC-seq3 (continuous DNA molecules) with snm3C-seq data
- Analyzing distance-dependent decay patterns
- Distinguishing true chromatin contacts from artifacts

### Doublet Removal and Quality Control

Comprehensive quality control procedures included:
- Rigorous doublet identification and removal
- Validation of clustering quality through cross-donor comparisons
- Integration with existing datasets (ENTEx project, snATAC-seq data)

## Comparative Analysis Methods

### Cross-Modal Validation

The study employed multiple validation strategies:

**Correlation Analysis:**
- Strongest correlations observed between identical cell types across donors
- Lower correlations between different subtypes/major types
- Validation against previous sorted cell populations and bulk tissues

**Adjusted Rand Index (ARI):**
- Quantified consistency between DNA methylation and chromatin contact clusters
- Revealed variable agreement across different lineages
- Identified cases where modalities show distinct clustering patterns

### Integration with External Datasets

**Comparison with Historical Data:**
- Schultz et al. 2015 methylation data
- ENTEx collaborative project data
- GTEx consortium data
- Previous snATAC-seq studies

**Data Format Conversions:**
- Genome coordinate mapping from hg19 to hg38 using LiftOver
- ALLC format processing and beta format conversions
- Generation of sample-by-1kb genomic bin matrices

## ATAC-seq Analysis Procedures

### Peak-DMR Overlap Analysis

The study performed comprehensive comparisons between DNA methylation and chromatin accessibility:

**Overlap Statistics:**
- 48% of ATAC-seq peaks overlapped with DMRs within major cell types
- 33% of DMRs overlapped with ATAC-seq peaks within major cell types
- 91.9% of ATAC-seq peaks overlapped DMRs across all tissues
- 61.9% of DMRs overlapped ATAC-seq peaks globally

**Methylation Depletion Analysis:**
- Systematic depletion of both mCG and mCH at ATAC-seq peaks
- Stronger depletion in cell types where peaks were originally called
- Identification of small fraction of hyper-methylated peaks

### Transcription Factor Motif Analysis

**Multiple Analytical Approaches:**
1. **PycisTarget** - Used for multi-group comparisons with comprehensive motif collections
2. **Homer** - Applied for loop-specific transcription factor inference
3. **SCENIC+ motif collection** - Employed for broad motif enrichment analysis

**Technical Parameters:**
- Normalized enrichment score (NES) >3 as cutoff for enriched motifs
- Fixed region size of ±500 bp from region centers
- Separate analyses for peak DMRs vs. non-peak DMRs

## Specialized Analyses

### Repeat-Based Clustering

The study examined cell-type specificity of DNA methylation across different repeat element categories:

**Repeat Element Types Analyzed:**
- **DNA transposons** - Strong cell type separation capability
- **LINE** (Long Interspersed Nuclear Elements) - Effective for clustering
- **LTR** (Long Terminal Repeats) - Good discrimination power
- **SINE** (Short Interspersed Nuclear Elements) - Lower performance due to coverage limitations
- **Satellite DNA** - Weaker specificity for cell clustering
- **Retroposons** - Limited accuracy due to size constraints

### Chromatin Compartments Analysis

**A/B Compartment Characterization:**
- Analysis of compartment interactions as function of genomic distance
- Comparison between domain-dominant (neuronal) vs. compartment-dominant (hematopoietic) lineages
- Calculation of compartment scores across lineages

**Methylation Compartment Framework:**
- Division of genome into four compartments based on mCG patterns
- Correlation with traditional A/B compartments
- Exception noted in neural lineages

### Chromatin Domains and Loops

**Contact Decay Analysis:**
- Identification of two prominent enrichment peaks (100kb-1Mb and >10Mb)
- Classification of lineages as "domain dominant" vs. "compartment dominant"
- Analysis of Topologically Associating Domains (TADs)

**Loop Analysis:**
- Variable loop patterns across cell types
- Integration with DMR analysis
- Motif enrichment at loop anchors

## Key Technical Implementations

### Data Processing Pipeline

**Mapping and Processing:**
- m3c mapping pipeline using yap framework
- Bisulfite conversion handling
- Read splitting optimization

**Statistical Methods:**
- Cosine distance calculations for sample comparisons
- Principal Component Analysis (PCA) and Latent Semantic Indexing (LSI)
- t-distributed Stochastic Neighbor Embedding (t-SNE)

### Interactive Data Browser

Development of comprehensive web-based tool:
- URL: https://humancellepigenomeatlas.arcinstitute.org
- Display of DNA methylation and chromatin contact data
- Navigation across tissues, major types, and subtypes
- Public accessibility for community use

## Supplementary Materials Overview

### Figure Supplements

**Technical Validation (Fig. S1):**
- Chromatin contact quality control procedures
- Contact decay plot comparisons
- Mapping method validations

**Methodological Improvements (Fig. S2):**
- LSI-based vs. PCA-based clustering comparisons
- Batch effect correction method evaluations
- Anchor filtering optimization

**Extended Analyses (Fig. S3-S26):**
- Comprehensive cell type characterizations
- Cross-modal comparison analyses
- Tissue-specific findings
- Technical parameter optimizations

### Data Tables

**Table S1:** Sample metadata including donor information and tissue sources
**Tables S2-S4:** Additional analytical parameters and results

### Reference Integration

The supplementary materials include **references 66-97**, encompassing:
- Technical methodology citations
- Comparative dataset references
- Statistical method publications
- Validation study sources

## Data Availability and Resources

### Public Data Access

**Primary Dataset:**
- 86,689 high-quality single cells
- 195 billion non-clonal methylation reads
- 18 billion long-range chromatin contacts
- Coverage across 16 human tissues with multiple donors per tissue

**Integration with Existing Resources:**
- ENTEx collaborative project compatibility
- Cross-reference with GTEx consortium data
- Compatibility with Human Cell Atlas initiatives

### Community Resource Value

This comprehensive atlas represents:
- First single-cell body map of human DNA methylation patterns
- First single-cell atlas of 3D genome architecture across human tissues
- Valuable resource for understanding gene regulatory mechanisms
- Foundation for studying cellular identity establishment
- Reference for human disease risk studies

## Conclusions

The methodological framework presented demonstrates significant advances in:
1. **Multi-modal single-cell analysis** capabilities
2. **Quality control procedures** for complex genomic datasets
3. **Integration strategies** across different data modalities
4. **Comparative analysis methods** for validation and discovery
5. **Community resource development** for broad scientific impact

The comprehensive nature of these methods and the resulting dataset provides unprecedented insights into the relationship between DNA methylation and 3D genome architecture across human cell types, establishing new standards for single-cell epigenomic analysis.