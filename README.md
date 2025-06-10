# Music Recommendation System

A hybrid music recommendation system that blends collaborative filtering, content-based filtering, and popularity-based ranking to generate personalized playlists.

## Course Submissions

This repository includes four submissions from my MIT program, showcasing different stages and areas of focus:

- `mit_submissions/mit_capstone_rec_sys_milestone_submission.html` — Early milestone for the capstone recommendation system project, focusing on foundational collaborative filtering.
- `mit_submissions/mit_capstone_rec_sys_final_submission.html` — Final capstone submission with refined hybrid recommender logic and evaluation.
- `mit_submissions/mit_elective_rec_sys_submission.html` — Elective project exploring alternative recommendation approaches and evaluation strategies.
- `mit_submissions/mit_eda_project_foodhub.html` — EDA-focused analysis of FoodHub order data, exploring customer behavior and delivery insights.

These notebooks demonstrate the progression of my work in recommender systems and applied data analysis across multiple course modules.

## Post Course Refinements

This directory includes continued experiments and refinements beyond the original coursework. These notebooks extend the initial project with improved model performance, alternative architectures, and more modular pipelines.

- Notebooks in this directory are not optimized for local Docker execution and were run in a cloud environment due to memory and processing constraints.
- For example, the latest SVD-based model was developed and tested here after being initially discovered in the working notebook. It was then ported back cleanly for structured evaluation.


## Current Working Notebook

The actively developed version of this project is:

- `notebooks/music_recommendation_system.ipynb` — A post-course, production-oriented notebook that builds on my MIT capstone work. It includes:
  - FAISS-powered content-based filtering
  - Modular hybrid recommendation logic
  - Batch processing and checkpointing for scalability
  - Dockerized environment for reproducibility

This notebook reflects my continued growth and interest in recommender systems beyond the formal coursework, with a focus on performance, maintainability, and real-world use cases.



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

## Project Structure

```
music-rec-system/
├── notebooks/
│   ├── mit_submissions/
│   │   ├── mit_capstone_rec_sys_milestone_submission.html   # MIT capstone milestone submission
│   │   ├── mit_capstone_rec_sys_final_submission.html       # Final MIT capstone recommender submission
│   │   ├── mit_elective_rec_sys_submission.html             # Elective recommender system project
│   │   └── mit_eda_project_foodhub.html                     # EDA project analyzing FoodHub order data
│   └── music_recommendation_system.ipynb                    # Post-course version with FAISS, hybrid logic, Docker
├── data/                                                    # Original data files (excluded), FAISS indices, TF-IDF cache
├── requirements.txt                                         # Python dependencies
├── .gitignore                                               # Excludes large files, local data, and backups
└── docker-compose.yml                                       # Containerized environment for consistent execution
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
