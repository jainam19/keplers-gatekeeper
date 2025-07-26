# Data download — Kepler exoplanet search results (Kaggle)

We **do not** commit the dataset to git. To run the notebook locally:

## Option A — Kaggle CLI (recommended)
1. Install and authenticate the Kaggle CLI: https://www.kaggle.com/docs/api
2. Download and unzip the dataset:
   ```bash
   kaggle datasets download -d nasa/kepler-exoplanet-search-results -p data
   unzip data/kepler-exoplanet-search-results.zip -d data
   ```
3. Ensure the file exists at: `data/cumulative.csv`

## Option B — Manual download
- Open the dataset page and download `cumulative.csv` manually, then place it under `data/`.

> The notebook expects the path: `data/cumulative.csv`