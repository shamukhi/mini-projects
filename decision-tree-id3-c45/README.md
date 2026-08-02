# Decision Tree Classifier — ID3 & C4.5 From Scratch

A from-scratch implementation of two classic decision tree induction algorithms — **ID3** and **C4.5** — built without relying on scikit-learn's tree classifier, applied to predicting whether a student will go to college.

## Overview

This project implements decision tree learning from first principles: entropy and information gain calculations, recursive tree building, and the split-selection differences between ID3 (information gain) and C4.5 (gain ratio, which corrects ID3's bias toward high-cardinality features). Both trees are trained and evaluated on the same dataset so their performance can be directly compared.

## Dataset

A student dataset (1,000 records) with features including:
- `type_school`, `school_accreditation`, `gender`, `interest`, `residence`
- `parent_age`, `parent_salary`, `house_area`, `average_grades`
- `parent_was_in_college`
- **Target:** `will_go_to_college` (boolean)

Continuous features (`parent_age`, `parent_salary`, `house_area`, `average_grades`) are discretized into 4 bins to make them usable by the tree-splitting logic.

## Method

- **Entropy & Information Gain** — implemented from scratch to score candidate splits for ID3
- **Gain Ratio** — implemented for C4.5, normalizing information gain by a feature's intrinsic split information to reduce bias toward features with many distinct values
- **Recursive tree building** for both algorithms, with the resulting trees printed in a readable nested structure
- **Evaluation** — precision/recall/F1 via `classification_report`, plus confusion matrices, computed on both train and held-out test splits (85/15)
- **Stability check** — both algorithms are retrained across 49 different random train/test splits to see how sensitive their accuracy is to the particular split chosen

## Results

**Feature information gain (ID3, full dataset):**

`average_grades` (0.229) and `house_area` (0.150) were the strongest single-feature splitters, followed by `parent_salary` (0.148) and `interest` (0.055) — the remaining features contributed comparatively little signal.

**Train/Test performance (single 85/15 split):**

| Model | Train Accuracy | Test Accuracy |
|---|---|---|
| ID3 | 0.97 | 0.90 |
| C4.5 | 0.97 | 0.91 |

**Average test accuracy across 49 random splits (90/10):**

| Model | Mean Accuracy |
|---|---|
| ID3 | 0.850 |
| C4.5 | 0.847 |

Across many random splits, ID3 and C4.5 perform almost identically on this dataset — the gain-ratio correction in C4.5 doesn't provide a meaningful edge here, likely because the discretized features don't have the high-cardinality imbalance that C4.5 is designed to correct for.

## Tech Stack

`Python` · `pandas` / `numpy` · `scikit-learn` (for evaluation metrics only — not the tree itself) · `matplotlib` / `seaborn`

## Getting Started

This project is a single Jupyter/Colab notebook (`decision_tree_id3_c45.ipynb`).

1. Provide the dataset as `data.csv` (update the file path in the notebook if not using Google Drive/Colab)
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run all cells sequentially — the notebook builds both trees, prints their structure, and generates the evaluation reports and stability plot

## Notes

- This is an educational implementation intended to demonstrate the mechanics of decision tree induction (entropy, information gain, gain ratio) rather than to be a production-ready or optimized tree library.
- No pruning is implemented for either algorithm, which is a likely contributor to the train/test accuracy gap observed above.
