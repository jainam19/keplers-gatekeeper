# Kepler's Gatekeeper — Exoplanet triage with ML 
*End‑to‑end workflow turning Kepler light‑curve features into fast, reproducible exoplanet triage.*

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jainam19/keplers-gatekeeper/blob/HEAD/notebooks/model.ipynb)
<!-- CI badge (enable in Step 6)
[![CI](https://github.com/jainam19/keplers-gatekeeper/actions/workflows/nbtest.yml/badge.svg)](https://github.com/jainam19/keplers-gatekeeper/actions)
-->

## Results in 10 seconds
- **Metric (LightGBM):** ROC‑AUC ≈ **0.97**, accuracy ≈ **0.90** (hold‑out).  
- **So‑what:** Fewer false positives → reviewers spend time on real planets first.  
- **Speed:** Prediction ≈ **0.05 s** for test split (fast triage).  
*(Full details in `docs/FinalPaper.pdf`.)*

---


<details>
<summary><b>Data Analyst (DA)</b></summary>

- Clean EDA → Insights narrative in the notebook (`notebooks/model.ipynb`).
- One key chart exported to `figs/key_plot.png`.
- Clear “so‑what” bullets above for fast skim.
</details>

<details>
<summary><b>Data Engineer (DE)</b></summary>

- **Data contract:** `data/README_download.md` with exact steps (no raw data in git).
- Pinned environment (`requirements.txt`) and sensible `.gitignore`.
- CI workflow scaffold in `.github/workflows/nbtest.yml.disabled`.
</details>

<details>
<summary><b>Data Scientist (DS)</b></summary>

- Baseline (LogReg) → tree ensembles (RF, LightGBM) with k‑fold CV & grid search.
- Feature importance & error‑aware metrics (AUC/F1/recall).
- Top drivers (e.g., `koi_prad`, `koi_period`, `koi_depth`, `koi_score`). 
</details>

<details>
<summary><b>ML Engineer (MLE)</b></summary>

- Notebook runs on a small sample (<5 min) with a stable file path (`data/cumulative.csv`).
- Ready for a tiny Streamlit app (threshold slider) in a follow‑up PR.
- CI-ready (enable when data sample or synthetic generator is added).
</details>

---

## Quickstart
```bash
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab  # or: jupyter notebook
```

Open `notebooks/model.ipynb` and **Restart & Run All**.

## Data
Follow `data/README_download.md` to place `data/cumulative.csv`.  
*(Do not commit Kaggle data; keep the repo lightweight.)*

## Docs
- Your paper: [`docs/FinalPaper.pdf`](docs/FinalPaper.pdf)

## Repo layout
```
/data/                      # raw data kept locally only; see data/README_download.md
/figs/                      # exported plots (key_plot.png)
/notebooks/model.ipynb      # main, cleaned notebook
/src/                       # helpers (optional)
/docs/FinalPaper.pdf        # authored write-up with full details
.github/workflows/nbtest.yml.disabled  # CI scaffold (enable later)
requirements.txt
README.md
```
