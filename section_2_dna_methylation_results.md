# Section 2: DNA Methylation Analysis Results

## Overview

This section presents comprehensive findings on DNA methylation patterns across human cell types, revealing novel insights into CG and non-CG methylation variability, compartmentalization effects, and the relationship between DNA methylation and 3D chromatin architecture.

## CG Methylation Variability Across Cell Types

### DNA Methylation Compartments

The study identified distinct "DNA methylation compartments" based on Partially Methylated Domains (PMDs) patterns across different cell lineages:

- **Partially Methylated Compartment**: Regions showing variable degrees of partial methylation across lineages
- **Fully Methylated Compartment**: Regions maintaining high methylation levels across cell types
- These compartments show strong correlation with A/B chromatin compartments from 3D genome data
- DNA methylation compartments provide more fine-grained resolution than traditional Hi-C-based compartment analysis

### Cell Type-Specific Methylation Patterns

Key observations include:

- **Lineage Specificity**: Related cell types share similar methylation patterns, with regions called PMDs in one cell type showing decreased methylation in related cell types
- **Correlation with Chromatin State**: Most cell types show negative correlation between mCG and compartment score, consistent with active chromatin being A compartment and mCG-depleted
- **PMD-Associated Lineages**: Seven cell types showed positive correlation between mCG and compartment score, all exhibiting explicit PMD presence
- **Mechanistic Implications**: PMD-like compartments may be "primed" to become full PMDs upon rapid cell division

## Non-CG Methylation Patterns

### mCH Distribution and Characteristics

- **Tissue Specificity**: Most cells show low levels of mCH except neuronal lineages, which exhibit high mCH levels
- **Functional Significance**: Despite low levels in non-neuronal cells, mCH patterns are non-random and cell-type informative
- **Trinucleotide Context**: Local correlation in mCH patterns according to specific trinucleotide contexts observed across cell types
- **Regulatory Element Association**: mCH is specifically enriched or depleted at genes and regulatory elements across most cell types

### Neuronal vs. Non-Neuronal Differences

- **Compartment Association**: 
  - Non-neuronal lineages: mCH enriched in A-compartment regions
  - Neuronal lineages: mCH enriched in B-compartment regions
- **Regulatory Mechanism**: In neurons, high mCH levels over genes influence MECP2 repressor binding
- **Universal Depletion**: mCH is depleted at domain boundaries separating compartments of similar type across all lineages

## Key Findings About Methylation Differences

### Relationship with 3D Chromatin Architecture

#### Compartment-Level Associations

- **General Pattern**: Strong association between B compartments and partially methylated DNA methylation compartments
- **Constitutive Regions**: Regions consistently B compartment across lineages were consistently partially methylated
- **Dynamic Regions**: Lineage-specific A/B compartment switches correspond with methylation compartment changes
- **Notable Exception**: Neural lineages showed weak correlation between B compartment regions and partially methylated compartments

#### Domain Boundary Analysis

- **mCG Patterns**: Domain boundaries demarcate regions of mCG enrichment and depletion across nearly all lineages
- **Focal Depletion**: Most lineages show relative focal mCG depletion at or adjacent to domain boundaries
- **Compartment-Specific Effects**: 
  - PMD-containing lineages: Lower mCG in B compartment regions adjacent to boundaries
  - Other lineages: mCG depletion in A compartment regions

### Chromatin Loop Associations

- **DMR Enrichment**: Differentially methylated regions (DMRs) are enriched at chromatin loop anchors across all major cell types
- **Transcription Factor Motifs**: CTCF motifs enriched in loop-associated DMRs across almost all cell types
- **Lineage-Specific Factors**: 
  - IRF2 and ISRE in immune lineages
  - NR5A2 in pancreas acinar cells  
  - GATA factors in trophoblasts
- **Variable Correlations**: Different lineages show varying relationships between DNA methylation and chromatin looping at differential loops

## Cell Type-Specific Methylation Signatures

### Major Lineage Distinctions

#### Hematopoietic Cells
- Show compartment-dominant phenotype with shorter chromatin loops
- Exhibit clear PMD patterns in some subsets (memory T cells)
- Strong association between B compartments and partially methylated regions

#### Neuronal Cells  
- Unique mCH distribution patterns (B-compartment enriched)
- Domain-dominant phenotype with longer chromatin loops
- High overall mCH levels with gene body distribution
- Weak correlation between methylation and chromatin compartments

#### Epithelial and Fibroblast Cells
- Variable PMD presence across subtypes
- Shared chromatin loop patterns within lineages
- Strong methylation-chromatin architecture correlations in some subtypes

### Discrepancies Between Modalities

The study revealed important cases where DNA methylation and chromatin contact data provide different cellular classifications:

#### Skeletal Muscle Example
- **3D Chromatin Clustering**: Separates cells by discrete cell states (satellite cells vs. mature fibers)
- **Methylation Clustering**: Shows continuum from progenitor to mature cells
- **Interpretation**: Suggests DNA methylation matures over longer timescales than chromatin reorganization

#### Trophoblast Cells
- **Chromatin Contacts**: Better reflect true cell type differences (villous cytotrophoblast vs. syncytiotrophoblast)
- **DNA Methylation**: Dominated by global methylation level differences rather than cell-type-specific patterns
- **Implication**: Local methylation patterns may be more informative than global patterns for some cell types

## Biological Implications

### Developmental Dynamics
- 3D genome structures typically change earlier than DNA methylation during differentiation
- Some cells retain methylation signatures of progenitor states while acquiring mature chromatin architectures
- Different epigenetic features may mature at different rates during cell differentiation

### Regulatory Mechanisms
- DNA methylation compartments may represent distinct mechanisms for maintaining methylation in different genomic contexts
- The correlation between PMD-like compartments and B-compartments suggests shared regulatory pathways
- Cell-type-specific transcription factors contribute to both chromatin organization and methylation pattern establishment

### Technical Considerations
- DNA methylation-based compartment calling provides cost-effective, high-resolution chromatin state information
- Joint analysis of multiple epigenetic modalities reveals complementary information about cell states
- Single-cell resolution enables detection of cellular heterogeneity and transitional states

## Conclusions

This comprehensive analysis reveals that DNA methylation patterns across human cell types are highly organized and cell-type-specific, with distinct compartmentalization that correlates strongly with 3D chromatin architecture. The identification of DNA methylation compartments provides new insights into how methylation is regulated across different genomic contexts, while the analysis of both CG and non-CG methylation reveals universal and lineage-specific regulatory mechanisms. The discrepancies between DNA methylation and chromatin contact-based cell classifications highlight the complementary nature of these epigenetic features and suggest they may reflect different aspects of cellular state and developmental timing.