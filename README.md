# Single-Cell-RNA-seq-Analysis
# Project Overview

Single-cell RNA sequencing (scRNA-seq) is a powerful technique used to study gene expression at the resolution of individual cells. This project implements a complete scRNA-seq analysis pipeline using the Scanpy framework in Python. The workflow follows standard practices used in computational biology to process, analyze, and interpret high-dimensional transcriptomic data.

The dataset used in this analysis is the PBMC 3K dataset, which contains gene expression profiles of approximately 3,000 peripheral blood mononuclear cells. The project demonstrates how to preprocess raw data, perform quality control, reduce dimensionality, identify clusters, and detect marker genes.

# Objectives

The main objectives of this project are:

To understand the structure and handling of single-cell data using AnnData
To perform quality control and filtering of raw scRNA-seq data
To normalize and preprocess gene expression data
To reduce dimensionality using PCA and UMAP
To identify clusters of similar cells
To detect marker genes for biological interpretation
# Tools and Technologies
Programming Language: Python
Core Library: Scanpy
Data Structure: AnnData
Supporting Libraries: NumPy, Pandas, Matplotlib
# Understanding AnnData

AnnData is the core data structure used in Scanpy for storing and manipulating single-cell data.

# Key Components:
X → Main data matrix (cells × genes)
obs → Cell metadata (annotations per cell)
var → Gene metadata (annotations per gene)
uns → Unstructured data (e.g., colors, parameters)

A toy dataset was first created to explore:

Data indexing
Subsetting rows (cells) and columns (genes)
Metadata manipulation

This step is crucial for understanding how real datasets are handled.

# Data Loading

The dataset used is the PBMC 3K dataset, loaded using Scanpy’s built-in functionality.

Key Steps:
1. Load dataset into an AnnData object
2. Inspect shape (number of cells and genes)
3. Preview metadata

This step ensures the dataset is correctly imported and ready for preprocessing.

# Quality Control (QC)

Quality control is a critical step to remove low-quality cells and technical noise.

Metrics Calculated:
Total counts per cell → Total RNA molecules detected
Number of genes per cell → Cell complexity
Percentage of mitochondrial genes → Indicator of cell stress or damage
Mitochondrial Gene Identification:

Mitochondrial genes were identified using gene name patterns (e.g., "MT-").

# Visualization:
Violin plots were used to visualize QC metrics
Scatter plots helped detect outliers
Filtering Criteria:
Remove cells with very low gene counts
Remove cells with excessively high mitochondrial percentage
Remove genes expressed in very few cells

This step improves data quality and downstream analysis reliability.

# Data Preprocessing

After filtering, the dataset undergoes preprocessing:

1. Normalization

Each cell is normalized to ensure comparability:

Counts scaled to a fixed total per cell (e.g., 10,000 counts)
2. Log Transformation
Logarithmic transformation applied
Reduces skewness and stabilizes variance
3. Highly Variable Genes (HVGs)
Identifies genes with the most variation across cells
These genes are most informative for downstream analysis
Dataset is subset to include only HVGs
4. Scaling
Data is centered (mean = 0)
Variance scaled to unit variance
Ensures equal contribution of genes
# Dimensionality Reduction

High-dimensional data is reduced to fewer components:

Principal Component Analysis (PCA)
Captures major sources of variation
Reduces thousands of genes into principal components
Helps remove noise
Visualization:
PCA plots show variance explained
Useful for selecting number of components
# Neighborhood Graph Construction

A graph-based representation of cells is constructed:

Each cell is connected to its nearest neighbors
Based on PCA representation
Forms the basis for clustering and visualization

Parameters such as number of neighbors and PCs influence results.

# UMAP Visualization

UMAP is used to project high-dimensional data into 2D space:

Preserves local and global structure
Enables visualization of clusters
Each point represents a cell

UMAP plots provide intuitive insights into cell populations.

# Clustering

Clustering groups similar cells together.

Method Used:
Leiden algorithm
Key Features:
Graph-based clustering
Detects communities in data
Adjustable resolution parameter
Output:
Cells assigned to cluster labels
Cluster sizes and distributions analyzed
# Marker Gene Identification

To interpret clusters biologically:

Process:
Compare gene expression between clusters
Identify genes highly expressed in each cluster
Results:

Top marker genes were extracted per cluster.

Known Marker Genes:
IL7R → T cells
CD14 → Monocytes
MS4A1 → B cells

These markers help assign biological identities to clusters.

# Data Saving

The processed dataset was saved in .h5ad format:

Stores all processed data and metadata
Enables reproducibility
Avoids re-running the pipeline
# Results and Observations
Clear separation of cell populations observed in UMAP
Multiple clusters identified using Leiden clustering
Marker genes successfully detected
Dataset cleaned and normalized for further analysis
# Conclusion

This project successfully demonstrates a complete scRNA-seq analysis workflow using Scanpy. It highlights the importance of each step, from quality control to clustering and marker detection.

The pipeline is scalable and can be applied to larger datasets or extended for advanced analyses such as:

Cell type annotation
Differential gene expression
Batch correction and integration
Trajectory inference
# Repository Structure
├── data/
├── notebooks/
│   └── scRNA-seq Analysis.ipynb
├── results/
│   ├── qc_plots/
│   ├── umap_plots/
│   └── marker_genes/
├── README.md
# How to Run
Install required libraries
Open the Jupyter Notebook
Run cells sequentially
Visualize outputs and interpret results
# Future Improvements
Add automated cell type annotation
Integrate multiple datasets
Perform trajectory analysis
Improve visualization aesthetics
