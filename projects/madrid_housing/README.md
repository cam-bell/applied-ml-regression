# Madrid Housing Rent — README

## TL;DR

Predict monthly Rent for Madrid listings from structural attributes and neighborhood (dataset: `data/houses_for_rent_madrid.xlsx`). Notebook demonstrates cleaning, impact encoding for high-cardinality geography, basic feature engineering, and preparation for regression modelling.

## Overview

This project prepares and models Madrid rental listings to estimate Rent from listing features. The notebook focuses on data cleaning, column selection, impact encoding of `Area` (neighbourhood), and modelling-ready pipelines suitable for linear and regularised regression. Intended audience: recruiters, ML engineers, and data scientists interested in applied regression and feature engineering for pricing/valuation.

## Dataset

| Item    | Value                              |
| ------- | ---------------------------------- |
| File    | `data/houses_for_rent_madrid.xlsx` |
| Rows    | 2,089                              |
| Columns | 15 (raw, before cleaning)          |
| Target  | `Rent` (monthly rent in EUR)       |

Key columns: `Area` (neighbourhood), `District`, `Rent`, `Bedrooms`, `Sq.Mt`, `Floor`, `Outer`, `Elevator`, and dwelling-type flags (Penthouse, Cottage, Duplex, Semidetached). See `data_description.md` for the full schema and variable definitions.

### Preprocessing notes

- Converted string "NaN" to true missing values and imputed `Bedrooms`, `Floor`, and `Sq.Mt` with column medians.
- Dropped remaining rows with missing values to produce a dense, numeric modelling table.
- Filtered implausible floor entries by removing rows with `Floor > 20`.
- High-cardinality `Area` (≈140 categories) is impact‑encoded (mean `Rent` per `Area`) computed on training data only.

## Objective & Target

- Objective: estimate monthly `Rent` to support valuation and pricing insights for Madrid rental listings.
- Business value: automate rent estimation, flag unusual listings, and provide interpretable drivers of rent for business stakeholders.

## Methods & Pipeline

- Load and validate data (duplicates, dtypes, plausibility checks).
- Cleaning: standardize missing values, median imputation for key numeric fields, drop remaining NaNs.
- Outlier handling: remove listings with `Floor > 20`.
- Feature engineering: create derived features (e.g., size-per-room, floor indicators), and transform/skew-correct numeric variables where appropriate.
- Encoding: impact encoding for `Area` (learned on train only), plus one-hot/label encoding for other categoricals where needed.
- Splitting: random train/validation/test split (70% / 15% / 15%) performed after filtering.

## Key Results & Modelling Status

- This notebook focuses on data preparation and stops prior to model training; follow-up notebooks or scripts should consume the prepared, leakage-resistant train/val/test splits.

Descriptive market stats (from prepared data):

- Mean rent ≈ €1,930; median ≈ €1,400; IQR ≈ €950–€2,500; full range ≈ €450–€16,000.
- Median size ≈ 90 m² (IQR ≈ 65–147 m²).
- Most listings have 2–3 bedrooms; elevator and exterior flags are common.

Dataset split sizes (before encoding and before dropping rows with unseen `Area` in val/test):

- Train ≈ 1,456 rows (70%)
- Validation ≈ 312 rows (15%)
- Test ≈ 313 rows (15%)

Notes on impact encoding:

- `Area` impact encoding (mean Rent per Area) is computed on the training set and mapped to val/test.
- Any val/test rows with `Area` unseen during training are dropped to avoid undefined encodings; final modeling-ready counts will therefore be slightly smaller than the numbers above.

## How to run

Run from repository root so data paths resolve.

1. Clone & virtual environment

```bash
git clone <repo-url>
cd applied-ml-regression
python -m venv .venv
source .venv/bin/activate
```

2. Install dependencies

```bash
pip install -r requirements.txt
python -m ipykernel install --user --name=applied-ml-regression --display-name "applied-ml-regression"
```

3. Open the notebook

```bash
jupyter lab  # or jupyter notebook
# then open:
# projects/madrid_housing/madrid_housing_rent_regression.ipynb
```

4. Reproduce

- Run preprocessing cells first (imputation, floor filtering), then splitting and impact-encoding cells in order.

## Reproducibility notes

- Random seed used in splits: `random_state=42`.
- Split strategy: random 70/15/15 split performed after filtering (`Floor <= 20`).
- Required file: `data/houses_for_rent_madrid.xlsx`.
- Working directory: run notebooks from repository root so the relative data paths (e.g., `data/houses_for_rent_madrid.xlsx`) resolve as-is.

## Files & Structure

- `projects/madrid_housing/madrid_housing_rent_regression.ipynb` — data cleaning, encoding, and split notebook.
- `projects/madrid_housing/data_description.md` — dataset schema and preprocessing notes.
- `projects/madrid_housing/results_summary.md` — descriptive statistics and modelling status.
- `data/houses_for_rent_madrid.xlsx` — primary dataset (Madrid rental listings).

## Limitations & Next steps

- Limitations: no external market/time signals included; dropping unseen `Area` entries reduces evaluation sample size; some leakage risks remain if encodings are computed incorrectly.
- Next steps: add geospatial features (distance to transport), incorporate time-aware demand signals, compare regularised linear models with tree-based models, and add a reproducible training script and inference example.

## Contact / Attribution

- Author: (Your name) — see repo top-level attribution.
- License / data use: check repository root for license and data usage notes.
