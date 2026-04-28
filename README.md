## Repository Structure

```
.
├── dataset/
├── embedding_quality_testing/
├── graphTrans/
├── mlp/
├── results/
├── embedding_codes/
├── data_preprocessing.ipynb
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

* `MLPModel.py` → Core implementation of the MLP architecture
* `mlp.ipynb` → Uses **mapped embeddings** as input
* `mlp_pair_mapped_only_256.ipynb` → Variant using specific mapped embeddings

**Key Idea:**

* Evaluates performance using **clean mapped embeddings**

---

### 3. `graphTrans/`

Contains Graph Transformer-based modeling approach.

**Files:**

* `graphtran.ipynb` → Main Graph Transformer implementation
* `bipartite` → Generates **bipartite graph input**

**Key Idea:**

* Models drug interactions as a graph problem
* Captures structural relationships between drugs

---

### 4. `results/`

Stores logs and outputs from experiments.

**Includes:**

* Training logs
* Performance metrics
* Model comparisons

**Example files:**

* `graph-transformer-train_log.csv`
* `logsmlp.csv`
* `logsmlp_with_unmapped_fallback.csv`
* `logsmlp_with_unmapped_fallback_mtr.csv`

---

### 5. `embedding_codes/`

Contains core notebooks for **embedding generation, fusion, and feature engineering pipelines**.

**Files:**

* `Embedding.ipynb`
  → Generates **LLM-based embeddings from SMILES representations**
* `drug_bank.ipynb`
  → Processes and integrates **DrugBank-related data**
* `gnn_rdkit.ipynb`
  → Extracts **graph-based molecular features using RDKit**
* `pair_fusion.ipynb`
  → Builds **pairwise drug representations** for DDI modeling
* `cross_modal_fusion_mapped_only.ipynb`
  → Performs fusion using only **clean mapped embeddings**
* `cross_modal_fusion_with_unmapped_fallback.ipynb`
  → Handles missing embeddings using **fallback strategies**

---

## Important Notebooks (Root Level)

* `Embedding.ipynb` → Generates embeddings from SMILES
* `data_preprocessing.ipynb` → Cleans and prepares dataset
* `cross_modal_fusion.ipynb` → Combines multiple modalities
* `pair_fusion.ipynb` → Creates pairwise drug features
* `gnn_rdkit.ipynb` → Graph-based feature extraction

---

## Results Summary

| Model             | AUC        | AUPRC      | AP@50      |
| ----------------- | ---------- | ---------- | ---------- |
| MLP (Unmapped)    | 0.8666     | 0.3418     | 0.6738     |
| MLP (Mapped)      | 0.8648     | **0.3593** | **0.6819** |
| Graph Transformer | **0.8224** | **0.7986** | -          |

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
* Advanced feature pipelines:

  * Cross-modal fusion
  * Pairwise modeling
  * Graph-based representations
* Robust experimentation with logging and comparisons
