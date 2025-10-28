# scRNA-Spatial-Python-

# Comprehensive Single-Cell and Spatial Analysis of Lymph Node Data

## Introduction 🔬

This repository documents a full analysis workflow applied to single-cell RNA sequencing (scRNA-seq) data from a human lymph node sample (GSM3660641, part of GSE128033). It also includes a demonstration of spatial transcriptomics analysis using a public 10x Genomics Visium dataset (Human Lymph Node). The analysis covers data preprocessing, cell type identification, differential expression, trajectory inference (pseudotime), pathway enrichment, cell-cell communication prediction (both bulk and spatially-aware), and spatial mapping of transcriptional states.

## Data Sources 💾

* **scRNA-seq:** [GSE128033](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE128033) (Sample GSM3660641) from NCBI GEO.
* **Spatial Transcriptomics:** [10x Genomics Human Lymph Node Dataset (V1\_Human\_Lymph\_Node)](https://www.10xgenomics.com/resources/datasets/human-lymph-node-1-standard-1-1-0) (Loaded via `scanpy.datasets.visium_sge`).

## Workflow Overview ⚙️

**Part 1: Single-Cell RNA Sequencing (scRNA-seq) Analysis (GSM3660641)**

1.  **Data Loading & QC:** Loaded raw 10x counts, performed QC filtering.
2.  **Normalization & Scaling:** Applied normalization, log-transformation, identified HVGs, and scaled data.
3.  **Clustering & Annotation:** Used PCA, Leiden clustering, and UMAP. Annotated cell types based on marker genes, validated with dot plots.
4.  **Differential Expression (DE):** Compared 'Activated Neutrophils' vs. 'Neutrophils (S100A8+)' and visualized with a volcano plot.
5.  **Trajectory Analysis (Pseudotime):** Modeled neutrophil activation using DPT, identified dynamic genes, and visualized the trajectory.
6.  **Pathway Enrichment:** Analyzed neutrophil DE genes using GProfiler.
7.  **Cell-Cell Communication (CCC):** Predicted interactions between cell types using LIANA (CellPhoneDB method).

**Part 2: Spatial Transcriptomics Analysis (10x Visium Lymph Node)**

1.  **Data Loading & QC:** Loaded Visium data, performed QC filtering.
2.  **Normalization & Feature Selection:** Applied normalization, log-transformation, and identified spatial HVGs.
3.  **Spatial Clustering & Annotation:** Used PCA, Leiden clustering. Annotated spatial domains based on marker genes.
4.  **Neighborhood Analysis:** Used Squidpy to quantify spatial adjacency between annotated regions.
5.  **Spatially-Aware CCC:** Ran LIANA/CellPhoneDB grouped by spatial annotations and filtered results based on spatial adjacency.

## Key Findings 💡

* Identified major immune cell populations in the scRNA-seq lymph node sample and characterized a neutrophil activation trajectory involving a switch from protein synthesis to immune defense programs.
* Predicted specific ligand-receptor interactions between single-cell populations.
* Mapped transcriptionally distinct spatial domains in the Visium lymph node data (e.g., B-cell Follicle, T-cell Zone) and quantified their spatial organization.
* Predicted cell-cell communication events specifically occurring between adjacent spatial regions.

## Visualizations 📊

Key plots generated include: Annotated UMAPs, marker gene dot plots, volcano plot, trajectory heatmap, cell composition bar plot, CCC dot plots (bulk and spatial), spatial expression plots, neighborhood enrichment heatmap.

## Tools Used 🛠️

* **Python 3**
* **Scanpy, AnnData, Pandas, NumPy, Matplotlib, Seaborn:** Core analysis and plotting.
* **LIANA:** Cell-cell communication.
* **Squidpy (Optional):** Spatial analysis enhancements.
* **GProfiler:** Pathway enrichment.

## How to Run 🚀

1.  **Clone:** `git clone https://github.com/Dhrupad210/scRNA-Spatial-Python-` and `cd scRNA-Spatial-Python- `
2.  **Environment:** Create a virtual environment and install dependencies:
    ```bash
    # Ensure Python 3.10+ is installed
    python -m venv venv_sc_spatial
    source venv_sc_spatial/bin/activate # Linux/macOS
    # venv_sc_spatial\Scripts\activate # Windows
    pip install --upgrade pip
    pip install -r requirements.txt
    # Note: Squidpy might require additional dependencies.
    ```
3.  **Data:** Download the raw scRNA-seq data (GSE128033/GSM3660641) and place it in the specified `sample_folder` path. The Visium data will be downloaded automatically.
4.  **Execute:** Run the Python script(s) (e.g., `python scRNA_analysis.py`, `python Spatial_analysis.py`) or execute the cells in the Jupyter Notebook.
