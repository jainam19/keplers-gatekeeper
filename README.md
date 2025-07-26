# Kepler’s Gatekeeper — Exoplanet candidate triage on Kepler KOIs

A reproducible pipeline on the **Kepler exoplanet search results** (“cumulative.csv”, Kaggle: `nasa/kepler-exoplanet-search-results`) to classify **KOI disposition** from tabular features.  
Focus: clear EDA, baseline → improved models, and transparent evaluation.

---

## 1) Dataset
- Source: Kepler KOI cumulative table (download instructions in `data/README_download.md`).
- Target: `koi_disposition` (e.g., CANDIDATE / FALSE POSITIVE / CONFIRMED; converted to a binary classification for modeling).
- Typical important fields observed: `koi_prad`, `koi_period`, `koi_depth`, `koi_score`, among others.

> This repo does **not** commit raw data; follow the data README to place `data/cumulative.csv`.

## 2) Method
- **Preprocessing:** select numeric features, basic cleaning; train/validation split with a fixed random seed.
- **Baselines:** Logistic Regression (reference), Random Forest (tree ensemble).
- **Improved model:** LightGBM with a small grid search and k‑fold cross‑validation.
- **Metrics:** ROC‑AUC (primary), accuracy/F1 (secondary). Class balance and error trade‑offs are noted in the notebook.

## 3) Results (reproducible on small sample)
| Model                | ROC‑AUC | Accuracy | Notes                      |
|----------------------|:------:|:--------:|----------------------------|
| Logistic Regression  | ~0.94  | ~0.83    | Baseline linear model      |
| Random Forest        | ~0.97  | ~0.89    | Ensemble, default tuning   |
| LightGBM (tuned)     | ~0.97  | ~0.90    | Fast inference; small grid |

> Numbers depend on split/seed and feature selection. See `notebooks/model.ipynb` for exact runs.

## 4) Reproduce locally
```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
# Place data as data/cumulative.csv (see data/README_download.md)
jupyter lab  # open notebooks/model.ipynb and "Restart & Run All"
```

## 5) Notes & limitations
- Kaggle data may be updated over time; this repo targets the public export at download time.
- Model aims at triage (quick sorting), not final astrophysical confirmation.
- No domain-specific vetting beyond the public KOI fields is included here.

## 6) References
Kaggle dataset: nasa/kepler-exoplanet-search-results

Libraries: scikit‑learn, LightGBM, pandas, numpy, matplotlib
