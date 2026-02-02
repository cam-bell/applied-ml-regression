<!-- ...existing code... -->

# Used-car Pricing — README

## TL;DR

Predict used-car sale Price from listing features (≈100K records). Notebook includes cleaning, feature engineering, PCA, tree-based modelling, and SHAP interpretation.

## Overview

This project builds and interprets pricing models for used-car listings to support valuation and pricing decisions. The dataset (~100,000 rows) is stored at `data/Cars_rdm.csv` and the modelling target is `Price`. The materials are aimed at recruiters, ML engineers, and data scientists looking for a compact, reproducible example of feature engineering, modelling, and explainability.

## Dataset

| Item    | Value               |
| ------- | ------------------- |
| File    | `data/Cars_rdm.csv` |
| Rows    | 100,000             |
| Columns | 11                  |
| Target  | `Price`             |

Key columns include Country, Manufacturer, Model, Price, Km, Automatic_Manual (transmission), Year and other listing attributes. See `data_description.md` for full schema.

Preprocessing notes

- Missing-value handling and simple imputation applied where required.
- Outlier treatment via IQR filtering.
- Categorical encoding: one-hot and label/impact encoders used in experiments.

## Objective & Target

- Objective: Predict listing Price to enable automated valuations and detect mispriced listings.
- Target variable: `Price` (vehicle price in EUR).

## Methods & Pipeline

- Load data and run basic sanity checks (duplicates, dtypes).
- Cleaning: remove invalid rows, impute missing values, IQR-based outlier trimming.
- Feature engineering: parse text fields, derive age/mileage features, and encode categorical fields (label and one‑hot).
- Dimensionality reduction: PCA on correlated numeric features for some model variants.
- Modelling: tree-based ensembles (Random Forest baseline; Gradient Boosting tuned as best model).
- Explainability: feature importance and SHAP values for local/global interpretation.
- Validation: train/validation/test splits and cross-validation where noted.

## Key Results

- Best model: Gradient Boosting (label-encoded, tuned).
- Primary metric (test): R² = 0.655 (best model).
- Error metrics (test): MAE ≈ €4,688; RMSE ≈ €7,200.
- Top predictive features (approx. importance / SHAP): Year (~40%), kW (~25%), Km (~11%), plus Model, Manufacturer, Country, Transmission, Fuel.

Interpretation: The tuned Gradient Boosting model explains ~65.5% of price variance; age and engine power are the strongest drivers, with mileage also important.

## How to run

Run from repository root so relative data paths resolve.

1. Clone & create venv

```bash
git clone <repo-url>
cd applied-ml-regression
python -m venv .venv
source .venv/bin/activate
```

2. Install dependencies

```bash
pip install -r requirements.txt
```

3. Open the notebook

```bash
jupyter lab   # or jupyter notebook
# then open:
# projects/used_car_pricing/vehicle_pricing_valuation.ipynb
```

4. Reproduce

- Run preprocessing cells first, then modelling and analysis cells in order.

## Reproducibility notes

- Random seed used: 42 — check the notebook top cells.
- Data split details: 80/20 (train/test proportions).
- Required file: `data/Cars_rdm.csv`.
- Working directory: run from repository root so paths in the notebook resolve as-is.

## Files & Structure

- projects/used_car_pricing/vehicle_pricing_valuation.ipynb — analysis and modelling notebook
- projects/used_car_pricing/data_description.md — dataset schema and source notes
- projects/used_car_pricing/results_summary.md — concise metrics and interpretation
- data/Cars_rdm.csv — primary dataset (used-car listings)

## Limitations & Next steps

- Limitations: potential selection bias in listings; no external market signals or time-aware features included.
- Next steps:
  - Add time-series / market-demand features and external price indices.
  - Try probabilistic/quantile regression to capture prediction uncertainty.
  - Add a lightweight inference script or API for single-listing valuation.

## Contact / Attribution

- Author: Cameron Bell — see repo top-level attribution.
- License / data use: check repository root for license and data usage notes.
