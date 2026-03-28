# Reproducible Benchmark for Authentication Anomaly Detection (FSLAD-2025)

This repository contains the full experimental pipeline for a reproducible benchmark of machine learning methods for authentication anomaly detection using the **FinnGen Synthetic Login Activity Dataset (FSLAD-2025)**.

This repository supports the accompanying research paper:

> *A Reproducible Benchmark for Authentication Anomaly Detection Using the FinnGen Synthetic Login Activity Dataset*

---

## Overview

Authentication anomaly detection is a critical component of modern cloud security, yet research progress is constrained by the lack of realistic, publicly accessible datasets and reproducible evaluation frameworks.

This repository implements a **fully reproducible benchmark pipeline**, including:

- Data preprocessing and feature engineering  
- Supervised and unsupervised model evaluation  
- Threshold optimization  
- Precision–recall and ROC analysis  
- Operational **top-k alert evaluation**

The goal is not only to compare models, but to **characterize the practical limits of authentication anomaly detection under realistic behavioural conditions**.

---

## Dataset

This study uses:

**FinnGen Synthetic Login Activity Dataset (FSLAD-2025)**  
- Production-derived  
- Fully synthetic and privacy-preserving  
- Preserves temporal and behavioural structure  

Dataset available at:  
https://doi.org/10.5281/zenodo.17858297

> The dataset is not included in this repository.  
> Please download it from Zenodo and place it in your working directory before running the notebook.

---

## Reproducibility

This repository is designed to support **end-to-end reproducibility** of the benchmark.

### Key properties:
- Fixed random seed (`42`)
- Deterministic preprocessing pipeline  
- Explicit feature engineering steps  
- Fixed and fully specified model configurations  
- No leakage from test set into training  
- Fully specified evaluation procedure  

All implementation code, preprocessing steps, and evaluation pipelines are publicly available and executable via the provided Jupyter notebook.

---

## Pipeline Overview

The notebook follows a structured pipeline:

1. Data loading and parsing  
2. Feature engineering  
   - Temporal encoding (cyclical features)  
   - Categorical encoding (one-hot encoding)  
   - Behavioural frequency features (computed from training data only)  
3. Train–test split (stratified 80/20 with fixed random seed)  
4. Model training  
5. Threshold optimization  
6. Evaluation:
   - PR-AUC, ROC-AUC  
   - F1-score  
   - Precision@K (top-k alerts)

---

## Threshold Optimization

Decision thresholds are selected by:

- Sweeping thresholds over model output scores  
- Selecting the threshold that maximizes **F1-score on the evaluation set**

> This approach characterizes the **maximum observable operating point under identical evaluation conditions across models**, rather than a deployment-calibrated threshold.

---

## Models Evaluated

- Logistic Regression  
- Random Forest  
- XGBoost  
- Isolation Forest (unsupervised baseline)

---

## Outputs

The repository includes precomputed outputs consistent with the paper:

- Model comparison metrics  
- Ablation study results  
- Top-k alert performance  
- Precision–recall curves (`precision_recall_curves2.png`)  

Precomputed outputs are available in the `results/` directory to enable immediate inspection without re-running the full pipeline.

---

## How to Run

### 1. Install dependencies
```bash
pip install -r requirements.txt
