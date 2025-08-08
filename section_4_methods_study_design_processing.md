# Methods: Study Design, Experimental Techniques, and Data Processing

## Human Subjects and Sample Collection

The study employed samples from 16 human tissues collected as part of a comprehensive single-cell atlas effort. Key aspects of human subjects and sample collection include:

- **Sample sources**: Tissues obtained from multiple human donors with at least two donors per tissue
- **ENTEx collaboration**: 12 out of 16 tissues were previously profiled as part of the ENTEx collaborative project, providing rich complementary datasets including single-nucleus ATAC-seq (snATAC-seq) from the same tissue samples
- **Placenta samples**: Two placenta samples obtained as part of the ENCODE4 sampling effort with detailed metadata available on the ENCODE Project website
- **Donor information**: Complete donor metadata and biosample-specific information documented with specific accession numbers

## Nuclei Isolation Procedures

The nuclei isolation protocol follows a standardized approach detailed in protocols.io:

### Pre-processing and Storage
- Human tissue samples pre-ground in liquid nitrogen and stored at -80°C in 50-75 mg aliquots
- Storage conditions maintained to preserve nuclear integrity

### Isolation Protocol
1. **Lysis buffer preparation**: NIMT buffer (250 mM Sucrose, 25 mM KCl, 5 mM MgCl₂, 10 mM Tris-Cl pH 8.0) supplemented with:
   - 0.1% Triton X-100
   - 1 mM DTT
   - Protease inhibitor (1:100 dilution)

2. **Homogenization**: Tissue aliquots transferred to Dounce homogenizer with 2.4 mL lysis buffer
3. **Centrifugation**: Lysate divided into 2 mL tubes and centrifuged at 1,000 × g for 10 min at 4°C using swing-bucket rotor
4. **Nuclear pellet recovery**: Supernatant discarded, nuclear pellet retained for downstream processing

## Chromosome Conformation Capturing (3C) Techniques

The 3C protocol is based on Arima Genomics 3C kits with specific modifications for single-cell applications:

### Cross-linking and Conditioning
1. **Nuclei conditioning**: Crosslinked nuclei resuspended in 20 µL DPBS
2. **SDS treatment**: 24 µL Conditioning Solution (0.5% SDS) added, incubated at 62°C for 10 min
3. **Triton neutralization**: 20 µL Stop Solution 2 (10% Triton X-100) added, incubated at 37°C for 15 min

### Enzymatic Reactions
- **Restriction digest**: Sample mixed with 28 µL master mix containing enzymes H1, H2, and CutSmart Buffer (NEB)
- **Incubation conditions**: 1 hour at 37°C followed by inactivation at 65°C
- **Quality control**: Enzymatic efficiency monitored throughout process

### FACS Sorting
- **Sorting platform**: BD Influx cell sorter in single-drop mode
- **Gating strategy**: 2N gating based on Hoechst staining to isolate intact nuclei
- **Collection format**: Nuclei sorted into 384-well plates pre-loaded with digestion buffer containing proteinase K
- **Scale**: 8-10 plates prepared per sort
- **Post-sorting processing**: Proteinase K lysis performed using thermal cycler (20 minutes at 50°C)
- **Storage**: Plates stored at -20°C prior to library preparation

## Library Preparation and Sequencing Methods

### Automation and Scale
- **Automation platforms**: Beckman Biomek i7 and Tecan Freedom Evo instruments used for large-scale applications
- **Protocol documentation**: Detailed protocols available at protocols.io

### Sequencing Configuration
- **Platform**: Illumina NovaSeq 6000 instrument
- **Flow cell usage**: One S4 flow cell per 16 384-well plates
- **Read configuration**: 150 bp paired-end sequencing
- **Output scale**: Generated 195 billion non-clonal methylation reads and 18 billion long-range chromatin contacts across 86,689 cells

## Data Processing Workflows

### Quality Control and Exclusion Lists

#### False Positive Signal Identification
1. **Problem identification**: Unusually high signals observed in certain genomic regions, particularly near diagonal and off-diagonal positions
2. **Control experiments**: snmC-seq3 data (without chromosome conformation capture) from MTG and PBMC samples used to identify mapping artifacts
3. **Exclusion list generation**:
   - 768 cells from each sample mapped with yap and "m3c" mapping mode
   - Contact matrices summed at 10kb resolution per donor
   - Normalization to average depth across all 14 samples
   - 10kb bin-pairs with median signal >1 selected as exclusion list
   - Contacts with both ends overlapping exclusion list removed

#### Distance Threshold Determination
- **Cutoff establishment**: 2.5kb threshold defined for classifying read pairs as chromatin contacts
- **Rationale**: Based on differences in distance-dependent decay patterns between snmC-seq3 (continuous DNA) and snm3C-seq (chromatin contacts)

### Cell Clustering and Integration

#### Multi-Modal Clustering Workflow
1. **mCG embedding computation** for each cell
2. **Integration** of mCG embedding between donors
3. **3C embedding computation** for each cell  
4. **Integration** of 3C embedding between donors
5. **Combination** of mCG and 3C embeddings
6. **Consensus clustering** on joint embedding

#### Hierarchical Clustering Strategy
- **Level 1**: Tissue-specific modality clustering and donor integration
- **Level 2**: Major type identification using consensus clustering
- **Level 3**: Subtype identification within major types
- **Final output**: 35 major cell types and 206 cellular subtypes

### DNA Methylation Analysis (mCG)

#### 5kb Bin Feature Extraction
1. **Rationale**: Capture methylation dynamics at shorter regulatory elements vs. traditional 100kb bins
2. **Hypo-methylation scoring**: Binomial model accounting for methylation level and coverage
3. **Sparse matrix generation**: Only bins with score >0.9 stored, reducing matrix to ~2% non-zero values
4. **LSI transformation**: Latent Semantic Indexing applied after binarization (threshold >0.95)

#### Processing Steps
- **Column filtering**: Cells having 1 in >5 rows selected
- **Bin selection**: Z-scored log₂ column sums between -2 and 2 retained
- **Normalization**: Row sum normalization to generate term frequency (TF)
- **SVD decomposition**: Applied to log-transformed and weighted matrix
- **Dimensionality**: Top dimensions of U matrix used for downstream analysis

### Chromatin Contact Analysis (3C)

#### Single-Cell Processing
1. **Resolution**: 100kb resolution contact matrices
2. **Distance filtering**: Upper triangle within 1Mb distance analyzed
3. **Matrix reshaping**: 2D contact matrices reshaped to 1D arrays per chromosome
4. **SVD application**: Performed per chromosome (first 50 dimensions retained)
5. **Chromosome concatenation**: All chromosomes combined horizontally
6. **Final SVD**: Applied to concatenated matrix without singular value division
7. **Dimension selection**: Significant dimensions (0.01 threshold) selected for t-SNE embedding

#### Loop and Differential Analysis
- **Loop calling**: scHiCluster used for identifying loops between 50kb and 5Mb
- **Statistical framework**: ANOVA-based approach for comparing interaction strength between cell groups
- **Background correction**: Local and global background subtraction applied
- **Significance testing**: FDR correction using Benjamini-Hochberg procedure
- **Differential loops**: Selected based on converted F-statistics >1.036 (85th percentile) and FDR <0.05

### Donor Integration Methods

#### Canonical Correlation Analysis (CCA)
1. **Anchor identification**: CCA-based method for cross-donor alignment
2. **Tissue-specific approach**: Only anchors between same tissue donors used to avoid overcorrection
3. **Distance filtering**: Top 60% anchors with smallest distances retained to eliminate cell-type mixing
4. **Geosketch sampling**: 1/3 of cells sampled to preserve rare cell types and improve integration

### Doublet Removal

#### Simulation-Based Detection
1. **Doublet simulation**: mCG profiles simulated by adding basecalls from two randomly selected cells
2. **Coverage restriction**: Cells with <3M total reads included in simulation
3. **Scoring method**: Similar to Scrublet but adapted for methylation data
4. **LSI embedding**: Combined dataset of observed and simulated doublets processed
5. **Threshold selection**: Based on score distribution comparison between observed and simulated doublets

## Data Storage and Implementation

### Storage Solutions
- **Methylation data**: ALLC files in TSV format for single-cell basecalls
- **Matrix format**: MCDS (methylcytosine dataset) files for cell-by-bin matrices
- **3D genome data**: Raw contacts in TSV format, imputed data in cooler format
- **Intermediate files**: NPZ format with automatic deletion after downstream processing

### Computational Optimization
- **ALLCools framework**: Custom development for methylation analysis including ratio computation, cell embedding, and compartment calling
- **scHiCluster pipeline**: Custom development for 3D genome imputation, compartment/domain/loop calling
- **Parallelization**: Snakemake pipeline implementation for efficient processing
- **Performance metrics**: 30 minutes at 100kb, 2.5 hours at 25kb, 5 hours at 10kb resolution for 1536 cells with 96 CPUs

### Quality Control Measures

#### Validation Approaches
1. **Cross-donor correlation**: Strongest correlation observed between identical cell types across donors
2. **Historical comparison**: Strong correlations with previous sorted cell and bulk tissue methylomes
3. **Modality consistency**: Both mCG and chromatin contacts show consistent cell type clustering
4. **Integration validation**: snATAC-seq data integration confirms cell type assignments

#### Statistical Validation
- **Correlation analysis**: Pairwise correlations computed across genomic bins and loops
- **Supervised learning**: Logistic regression models used to validate cluster separability
- **Cross-validation**: Five-fold cross-validation applied for performance evaluation
- **Consensus clustering**: 500 random initializations with 0.8 consensus rate

This comprehensive methods section demonstrates a sophisticated multi-modal approach to simultaneously profiling DNA methylation and 3D genome architecture at single-cell resolution across diverse human tissues, with robust quality control and validation measures throughout the analytical pipeline.