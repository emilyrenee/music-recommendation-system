# Music Recommendation System

A hybrid music recommendation system that blends collaborative filtering, content-based filtering, and popularity-based ranking to generate personalized playlists.

## Notebook Versions

This project includes three versions that reflect both the original MIT coursework and continued development:

- `mit_submissions/milestone_v1_mit_submission.html` — HTML export of the initial milestone submission for the MIT course. Run in a cloud environment and focuses on core model development.
- `mit_submissions/final_v2_mit_submission.html` — HTML export of the final submission for the MIT course, including improved evaluation and presentation formatting.
- `music_recommendation_system.ipynb` — The post-course, production-ready version with:
  - FAISS-based content filtering
  - Batch processing and checkpointing
  - Docker support for reproducibility
  - Modular hybrid logic

These versions showcase the project’s evolution from academic prototype to scalable system.


## Features

- **Hybrid Recommendation System** combining:
  - User-User Collaborative Filtering (best performing model)
  - Content-Based Filtering using TF-IDF and FAISS
  - Popularity-based ranking for diversity
- **Multiple Model Types**:
  - SVD (Hypertuned) – Best overall performance
  - User-User CF (Hypertuned)
  - Item-Item CF
  - Co-Clustering
- **Efficient content-based filtering** using FAISS for fast similarity search
- **Batch processing** for handling large datasets
- **Checkpoint system** for long-running operations

## Getting Started

1. Clone the repository  
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the Jupyter notebook:
   ```bash
   jupyter notebook notebooks/music_recommendation_system.ipynb
   ```

## Important Notes

- The first run will build the TF-IDF matrix and FAISS indices, which can take several hours depending on your system. This is a one-time process — subsequent runs will load the pre-computed results.
- The system uses batch processing (100,000 records per batch) to handle the large dataset efficiently.
- Checkpoints are saved after each batch, so you can safely interrupt and resume the process.

## Model Performance

Best performing models (in order):

1. **SVD_Hypertuned_2** – RMSE: 0.597, Precision: 0.828, Recall: 0.624  
2. **SVD_Hypertuned_3** – RMSE: 0.597, Precision: 0.828, Recall: 0.624  
3. **User-User CF (Hypertuned)** – RMSE: 0.870, Precision: 0.633, Recall: 0.469  
4. **Hybrid (CF + Content + Popularity)** – Qualitatively best for diversity and cold start; not scored via RMSE

## Data

The system uses the Million Song Dataset, which includes:

- Song metadata (title, artist, release, year)
- User-song play counts
- 1,000,000 unique songs
- 2,000,000 user-song interactions

## Docker Support

The project includes Docker support for consistent development environments:

```bash
docker-compose up
```

This will start a Jupyter notebook server at [http://localhost:8888](http://localhost:8888)

## Future Improvements

- Add lyrics analysis for better content-based filtering  
- Incorporate audio features for more accurate similarity matching  
- Implement real-time recommendation updates  
- Add genre and mood-based filtering  

## Setup

1. **Build and start the container:**
   ```bash
   docker compose up -d --build
   ```

2. **Access Jupyter Notebook:**
   - Open your browser and go to [http://localhost:8888](http://localhost:8888)

  
## Project Structure

```
music-rec-system/
├── notebooks/
│   ├── mit_submissions/
│   │   ├── milestone_v1_mit_submission.html   # Early checkpoint
│   │   └── final_v2_mit_submission.html       # Final submission for the MIT course
│   └── music_recommendation_system.ipynb       # Post-course enhanced version (Docker + FAISS + batch)
├── data/                                       # Original data files (excluded from repo), FAISS indices, TF-IDF cache
├── requirements.txt                            # Python dependencies
├── .gitignore                                  # Excludes large files, data backups, and local artifacts
└── docker-compose.yml                          # Containerized environment for consistent execution
```


## Using Preprocessing

```python
from preprocessing import load_and_preprocess_data

# Process data with parallel clustering
df_small_content, df_content = load_and_preprocess_data(
    "data/song_data.csv",
    n_jobs=-1  # Use all available cores
)

# Display the results
print("\nContent DataFrame shape:", df_content.shape)
print("\nSmall Content DataFrame shape:", df_small_content.shape)
print("\nSample of preprocessed data:")
display(df_small_content.head())
```

## Common Docker Commands

```bash
# Rebuild container
docker compose down && docker compose up -d --build

# View logs
docker compose logs notebook

# Stop container
docker compose down
```

## Dependencies

See `requirements.txt` for the full list of Python packages.

## Author

Emily Hagood  
Data Engineer | Recommender Systems Enthusiast  
Built with Python, FAISS, and ❤️

## Acknowledgements

This project leverages the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/) and the incredible open-source tools in Python’s data science ecosystem.
