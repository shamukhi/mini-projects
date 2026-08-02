# 🎵 Music Recommendation System — Neural Collaborative Filtering

A PyTorch implementation of Neural Collaborative Filtering (NCF) that learns to recommend artists to users based on implicit listening-count feedback from the Last.fm dataset.

## Overview

This project implements the **Neural Collaborative Filtering** architecture ([He et al., 2017](https://arxiv.org/abs/1708.05031)) to model user–artist affinity and generate personalized music recommendations. Instead of relying on a fixed similarity metric like traditional matrix factorization, NCF replaces the inner product with a learned neural network, combining a **Generalized Matrix Factorization (GMF)** branch and a **Multi-Layer Perceptron (MLP)** branch to capture both linear and non-linear user–item interaction patterns.

## Dataset

**Last.fm HetRec-2011**
- ~1,900 users
- ~17,600 artists
- ~92,000 user–artist listening interactions

Data is downloaded automatically from GroupLens and preprocessed with a minimum-interaction filter, contiguous ID re-indexing, and a leave-one-out train/validation/test split (the standard protocol for implicit-feedback recommendation benchmarks).

## Pipeline

```
1. Setup
2. Data Loading & Preprocessing (filtering, re-indexing, leave-one-out split, negative sampling)
3. Model Architecture (GMF + MLP fusion — NCF)
4. Training (BCE loss, Adam optimizer, early stopping)
5. Test Set Evaluation (HR@K, NDCG@K)
6. Making Recommendations (top-N inference for a given user)
7. Embedding Visualization (t-SNE of learned artist embeddings)
8. Model Comparison (GMF vs. MLP-only vs. full NCF)
9. Save & Load the Model
```

## Method Details

- **Negative sampling:** 4 negative (unlistened) items sampled per positive interaction during training, a standard technique for implicit-feedback recommenders
- **Model:** Embedding layers for users and items feed into both a GMF branch (element-wise product) and an MLP branch (stacked dense layers with dropout); their outputs are concatenated and passed through a final sigmoid layer to predict interaction likelihood
- **Loss:** Binary Cross-Entropy
- **Optimizer:** Adam with `ReduceLROnPlateau` scheduling on validation HR@10, plus early stopping
- **Evaluation metrics:**
  - **HR@K (Hit Rate)** — whether the held-out positive item appears in the top-K ranked recommendations
  - **NDCG@K (Normalized Discounted Cumulative Gain)** — rewards ranking the true item higher, not just including it
  - Reported at K = 5, 10, and 20 on the held-out test set

## Extras

- **t-SNE visualization** of learned artist embeddings, colored by popularity and labeled for the most-listened artists — a quick sanity check that the model is learning meaningful structure
- **Ablation comparison** between the full NCF model, a GMF-only model, and an MLP-only model to show the benefit of combining both

## Tech Stack

`Python` · `PyTorch` · `pandas` / `numpy` · `scikit-learn` (t-SNE) · `matplotlib` / `seaborn`

## Results

After filtering (min. 5 interactions per user/artist), the dataset reduces to **1,874 users**, **2,828 artists**, and **71,411 interactions** (99.72% sparse). The model was trained for up to 20 epochs with early stopping (patience 5), reaching its best validation performance at epoch 10.

**Test set metrics (full NCF model):**

| Metric | @5 | @10 | @20 |
|---|---|---|---|
| HR (Hit Rate) | 0.5955 | 0.7289 | 0.8458 |
| NDCG | 0.4497 | 0.4929 | 0.5225 |

**Ablation — model architecture comparison (HR@10 / NDCG@10):**

| Model | HR@10 | NDCG@10 |
|---|---|---|
| GMF only | 0.4604 | 0.2855 |
| MLP only | 0.5364 | 0.3367 |
| **NCF (GMF + MLP)** | **0.7406** | **0.4851** |

The full NCF model substantially outperforms either branch alone, confirming the value of combining linear (GMF) and non-linear (MLP) interaction modeling — consistent with the findings in the original paper.

**Sample recommendation** for a user whose history includes Lady Gaga, Rihanna, Britney Spears, and Katy Perry — the model recommends Beyoncé, Madonna, Evanescence, Mariah Carey, and similar 2000s–2010s pop artists, showing it's picking up on genre/era similarity rather than just popularity.

## Getting Started

This project is packaged as a single Jupyter/Colab notebook (`music_recommendation.ipynb`).

1. Open the notebook in Google Colab or a local Jupyter environment (GPU optional but speeds up training)
2. Install dependencies with `pip install -r requirements.txt` (or let the notebook's setup cell install them)
3. Run all cells sequentially — the Last.fm dataset downloads automatically
4. Training runs for up to 20 epochs with early stopping based on validation HR@10
5. The final cells save the trained model weights for reuse and demonstrate generating top-N recommendations for a sample user

### Installation

```bash
pip install -r requirements.txt
```

## Notes

- This is a from-scratch educational/portfolio implementation of the NCF paper, useful as a reference for building recommendation systems with implicit feedback data.
- Hyperparameters (embedding size, MLP layer sizes, negative sampling ratio, learning rate) are set to reasonable defaults for this dataset size — see the notebook for the specific configuration and comparison results.


