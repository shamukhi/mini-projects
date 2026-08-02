# Mini Projects

A collection of small, self-contained machine learning and data science projects, each one lives in its own folder with its own notebook, README, and dependencies.

## Projects

| Project | Description | Tech |
|---|---|---|
| [music-recommendation-ncf](./music-recommendation-ncf) | Neural Collaborative Filtering (NCF) recommender that suggests artists to users based on implicit listening data from the Last.fm dataset. | PyTorch |



## Structure

Each project folder is independent and contains everything needed to run it:

```
mini-projects/
├── README.md                       ← you are here
├── music-recommendation-ncf/
│   ├── README.md
│   ├── music_recommendation.ipynb
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

