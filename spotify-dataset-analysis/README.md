# Spotify Global Music Dataset — EDA & Visualization

An exploratory analysis of a global Spotify tracks dataset, examining what makes tracks and artists popular across genres, artists, and time.

## Overview

This project cleans and visualizes a dataset of Spotify tracks and their associated artist/album metadata, using both static plots and interactive Plotly visualizations to explore relationships between popularity, genre, followers, and release trends over time.

## Dataset

- **Source:** Spotify track/artist/album metadata export
- **Size:** 8,582 tracks × 15 raw columns (17 after feature engineering)
- **Key fields:** `track_name`, `track_popularity`, `explicit`, `artist_name`, `artist_popularity`, `artist_followers`, `artist_genres`, `album_name`, `album_release_date`, `album_total_tracks`, `track_duration_min`

## Data Cleaning & Feature Engineering

- `album_release_date` parsed to datetime, with missing values filled using the earliest valid date
- Numeric columns (`track_popularity`, `artist_popularity`, `artist_followers`, `track_duration_min`, `album_total_tracks`) coerced to numeric with median imputation
- Categorical columns (`track_name`, `artist_name`, `album_name`, `artist_genres`, `album_type`) filled with the column mode
- Multi-genre strings split into a `artist_genres_list` column to support genre-level aggregation
- A `Year` column derived from release date for time-series analysis

## Visualizations

- **Artist popularity vs. track popularity** bubble chart, sized by artist follower count
- **Top 10 most popular genres**
- **Average track popularity by year (2009–2025)** — overall trend line
- **Genre → Artist → Track sunburst** for top genres, showing hierarchical composition
- **Multi-line time series** of average track popularity over time for top artists (interactive dropdown to select artists)
- **Box plots** of numeric feature distributions (popularity, followers, duration, etc.)
- **Correlation heatmap** across numeric features

## Tech Stack

`Python` · `pandas` / `numpy` · `matplotlib` / `seaborn` · `plotly.express` / `plotly.graph_objects` · `altair`

## Getting Started

This project is a single Jupyter/Colab notebook (`spotify_dataset_analysis.ipynb`).

1. Provide the dataset as `spotify_data_clean.csv` (update the file path in the notebook if not using Google Drive/Colab)
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run all cells sequentially — cleaning runs first, followed by each visualization

## Notes

- Some visualizations (sunburst, dropdown-filtered time series) are interactive and best viewed by running the notebook directly rather than via a static file preview — GitHub's notebook renderer will show these as static, non-interactive snapshots.
- This is a descriptive/exploratory analysis; popularity metrics reflect Spotify's platform-specific scoring and may not generalize to other measures of musical success.
