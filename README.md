# Mini Projects

A collection of small, self-contained machine learning and data science projects — each one lives in its own folder with its own notebook, README, and dependencies.

## Projects

| Project | Description | Tech |
|---|---|---|
| [music-recommendation-ncf](./music-recommendation-ncf) | Neural Collaborative Filtering (NCF) recommender that suggests artists to users based on implicit listening data from the Last.fm dataset. | PyTorch |
| [decision-tree-id3-c45](./decision-tree-id3-c45) | Decision tree classifier (ID3 & C4.5) implemented from scratch to predict college attendance, with a head-to-head accuracy comparison. | scikit-learn (metrics only) |
| [pantheon-project](./pantheon-project) | EDA on ~11,000 historical figures, exploring fame, occupation, geography, and time via static and interactive visualizations. | pandas, Plotly |
| [spotify-dataset-analysis](./spotify-dataset-analysis) | EDA on Spotify track/artist metadata, exploring popularity, genre, and release trends over time. | pandas, Plotly, Altair |

*(More projects will be added here over time.)*

## Structure

Each project folder is independent and contains everything needed to run it:

```
mini-projects/
├── README.md                       ← you are here
├── music-recommendation-ncf/
│   ├── README.md
│   ├── music_recommendation.ipynb
│   └── requirements.txt
├── decision-tree-id3-c45/
│   ├── README.md
│   ├── decision_tree_id3_c45.ipynb
│   └── requirements.txt
├── pantheon-project/
│   ├── README.md
│   ├── pantheon_project.ipynb
│   └── requirements.txt
├── spotify-dataset-analysis/
│   ├── README.md
│   ├── spotify_dataset_analysis.ipynb
│   └── requirements.txt
└── <future-project>/
    ├── README.md
    ├── <notebook>.ipynb
    └── requirements.txt
```

## Running a project

1. Open the project's folder and read its `README.md` for specifics
2. Install its dependencies:
   ```bash
   cd <project-folder>
   pip install -r requirements.txt
   ```
3. Open the `.ipynb` file in Jupyter or Google Colab and run the cells

## License

Unless noted otherwise inside an individual project folder, code in this repository is available under the MIT License.
