## Overview

This project focuses on predicting **drug–drug interaction (DDI) side effects** using **LLM-based embeddings of SMILES representations**. The pipeline explores multiple modeling approaches (MLP, Graph Transformer, etc.) and evaluates embedding quality using various analytical techniques.

---

## Repository Structure

```
.
├── dataset/
├── embedding_quality_testing/
├── graphTrans/
├── mlp/
├── results/
├── Embedding.ipynb
├── cross_modal_fusion.ipynb
├── data_preprocessing.ipynb
├── gnn_rdkit.ipynb
├── pair_fusion.ipynb
└── README.md
```

---

## Folder Details

### 1. `embedding_quality_testing/`

Contains experiments and evaluation scripts to assess embedding quality.

**Key functionalities:**

* Clustering analysis
* Similarity preservation checks
* Dimensionality reduction visualizations (t-SNE, UMAP)
* Downstream evaluation (logistic regression, XGBoost)

**Files:**

* `ClusteringQuality.ipynb` → Evaluates how well embeddings cluster similar drugs
* `SimilarityPreservation.ipynb` → Checks whether embedding space preserves chemical similarity
* `TSNE_test.ipynb` → t-SNE visualization
* `UMAP_test.ipynb` → UMAP visualization
* `check_drug_protein.ipynb` → Drug-protein relation validation
* `pytorch_logreg.ipynb` → Logistic regression baseline
* `xgboost.ipynb` → Tree-based evaluation baseline

---

### 2. `mlp/`

Implements MLP-based models for side-effect prediction.

**Files:**

* `MLPModel.py`
  → Core implementation of the MLP architecture

* `mlp.ipynb`
  → Uses **mapped embeddings** as input

* `mlp_pair_mapped_only_256.ipynb`
  → Variant of MLP using a specific mapped embedding configuration

**Key Idea:**

* Evaluates performance using **clean mapped embeddings**

---

### 3. `graphTrans/`

Contains Graph Transformer-based modeling approach.

**Files:**

* `graphtran.ipynb`
  → Main Graph Transformer implementation

* `bipartite` (notebook/script)
  → Generates **bipartite graph input** required for Graph Transformer

**Key Idea:**

* Models drug interactions as a graph problem
* Uses structural relationships between drugs

---

### 4. `results/`

Contains logs and outputs from all experiments.

**Includes:**

* Training logs
* Performance metrics
* Experiment comparisons

**Example files:**

* `graph-transformer-train_log.csv`
* `logsmlp.csv`
* `logsmlp_with_unmapped_fallback.csv`
* `logsmlp_with_unmapped_fallback_mtr.csv`

**Purpose:**

* Centralized tracking of model performance across configurations

---

## Important Notebooks (Root Level)

* `Embedding.ipynb` → Generates embeddings from SMILES using LLM-based models
* `data_preprocessing.ipynb` → Cleans and prepares dataset
* `cross_modal_fusion.ipynb` → Combines multiple feature modalities
* `pair_fusion.ipynb` → Creates pairwise drug representations
* `gnn_rdkit.ipynb` → Graph-based feature extraction using RDKit

---

## Embeddings & Dataset Access

Due to size constraints, the **embedding files and dataset are hosted externally**.

Access them here:

---

## Key Experimental Variants

* **Mapped embeddings** → Clean, aligned representations
* **Unmapped fallback embeddings** → Handles missing mappings
* **Graph-based inputs** → For transformer models
* **Pairwise fusion inputs** → For interaction modeling

---
Here’s a **clean, final, short Results section** combining MLP + Graph Transformer:

---

## Results Summary

| Model             | AUC        | AUPRC      | AP@50      |
| ----------------- | ---------- | ---------- | ---------- |
| MLP (Unmapped)    | 0.8666     | 0.3418     | 0.6738     |
| MLP (Mapped)      | 0.8648     | **0.3593** | **0.6819** |
| Graph Transformer | **0.8224** | **0.7986** | —          |

---

## Logs

Detailed experiment logs are available in:

```bash
/results/
```

---

## Summary

This repository explores:

* Representation learning using **LLM-based SMILES encodings**
* Multiple architectures:

  * MLP
  * Graph Transformer
* Embedding validation techniques:

  * Clustering
  * Similarity preservation
  * Visualization
* Robust experimentation with logging and comparisons
