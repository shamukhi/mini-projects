# Pantheon Project — Historical Popularity Index Analysis

An exploratory data analysis and visualization project examining what drives lasting fame, using the Pantheon dataset of ~11,000 historical figures spanning millennia of recorded history.

## Overview

The Pantheon dataset tracks historical figures by birth year, location, occupation, and a computed "Historical Popularity Index" (along with page views and article language counts) as a proxy for enduring fame. This project cleans the raw dataset and answers six guiding questions about how fame is distributed across occupation, time, and geography, using a mix of static (Matplotlib/Seaborn) and interactive (Plotly) visualizations.

## Dataset

- **Source:** Pantheon historical figures dataset
- **Size:** 11,341 records × 17 columns
- **Key fields:** `full_name`, `birth_year`, `city`, `country`, `continent`, `occupation`, `industry`, `domain`, `article_languages`, `page_views`, `average_views`, `historical_popularity_index`

## Data Cleaning

- Numeric columns (`birth_year`, `latitude`, `longitude`, `article_languages`, `page_views`, `average_views`, `historical_popularity_index`) coerced to numeric and missing values filled with the column median
- Categorical columns (`full_name`, `sex`, `city`, `state`, `country`, `continent`, `occupation`, `industry`, `domain`) filled with the column mode
- Verified zero missing values remained after cleaning

## Questions Explored

1. **What are the ten most repeated occupations** in the dataset? *(bar chart)*
2. **How has representation across domains** (Humanities, Institutions, Sports, etc.) **changed over time**, binned in 50-year birth-year windows? *(stacked area chart)*
3. **What is the distribution of historical popularity** for the top 5 occupations, and how do their medians compare? *(box plot)*
4. **Is there a relationship between how many figures come from a country and their average page views**, grouped by continent? *(bubble chart, log scale)*
5. **How is the figure count distributed hierarchically** across continent → country → city? *(sunburst chart)*
6. **What is the long-term trend in total page views** (overall recognition) by birth year? *(line chart, log scale)*

## Key Findings

- **Politician, Actor, Soccer Player, Writer, and Religious Figure** are the top 5 most represented occupations (6,259 of 11,341 records combined)
- Fame recognition (page views) trends show clear long-run growth patterns tied to birth year, visualized on a log scale to handle the wide range of magnitudes across millennia
- Geographic distribution reveals concentration effects — a relatively small number of countries account for a disproportionate share of highly-viewed historical figures

## Tech Stack

`Python` · `pandas` / `numpy` · `matplotlib` / `seaborn` · `plotly.express`

## Getting Started

This project is a single Jupyter/Colab notebook (`pantheon_project.ipynb`).

1. Provide the dataset as `database.csv` (update the file path in the notebook if not using Google Drive/Colab)
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run all cells sequentially — cleaning runs first, followed by each numbered visualization (Q1–Q6)

## Notes

- Plotly figures are interactive when run in a notebook environment (hover tooltips, zoom, legend toggling) — static image exports will lose this interactivity.
- This is an exploratory/descriptive analysis; no causal claims are made about *why* certain occupations or regions show higher popularity — the goal is to surface patterns for further investigation.
