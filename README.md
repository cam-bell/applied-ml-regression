# Applied Machine Learning – Regression & Pricing Models

## Overview

This repository contains **applied regression case studies** focused on pricing, valuation, and continuous prediction using real-world datasets. It is designed to demonstrate end-to-end applied ML skills relevant to **AI/ML engineering**, **software engineering with an AI focus**, and **data science** roles.

---

## What This Repo Covers

| Focus                       | Description                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------- |
| **Regression problems**     | Predicting continuous targets: rent (Madrid housing) and vehicle price (used cars).          |
| **Pricing & valuation**     | Building interpretable models for real-world price/rent outcomes.                            |
| **Feature engineering**     | Impact encoding, one-hot/label encoding, handling missing values and outliers.               |
| **Evaluation**              | Train/validation/test splits, metrics (R², MAE, MSE where applicable), and model comparison. |
| **Business interpretation** | Linking model outputs and feature importance to decisions (e.g. what drives price).          |

---

## Techniques Demonstrated

- **Data quality**: Missing-value imputation (e.g. median), outlier handling (e.g. IQR), duplicate and validity checks.
- **Feature engineering**: Impact encoding (target-based), one-hot and label encoding for categoricals.
- **Modelling**: Linear and regularised regression (e.g. LASSO), tree-based models (Random Forest, Gradient Boosting), train/val/test design.
- **Evaluation**: R², MAE, MSE; cross-validation and holdout evaluation.
- **Interpretation**: Feature importance (e.g. Random Forest, SHAP), hypothesis testing, correlation and EDA.

---

## Case Studies & Notebooks

| Case study                                                | Dataset                                                | Notebook                               |
| --------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------- |
| **Madrid housing rent**                                   | Madrid rental listings (`houses_for_rent_madrid.xlsx`) | `madrid_housing_rent_regression.ipynb` |
| **Vehicle Pricing & Valuation Modelling (100K+ records)** | Used cars, 100K+ listings (`Cars_rdm.csv`)             | `vehicle_pricing_valuation.ipynb`      |

### Madrid housing rent

The Madrid housing notebook works with rental listings from `houses_for_rent_madrid.xlsx` and target **Rent**. It focuses on column selection, missing-value imputation, data filtering (e.g. removing extreme floors), impact encoding of `Area`, and a 70/15/15 train/validation/test split to produce a modelling-ready dataset for linear and regularised regression.

### Vehicle Pricing & Valuation Modelling (100K+ records)

The used-cars notebook analyses **100K+ listings** with target **Price**. It covers EDA, outlier handling (IQR), one-hot and label encoding, PCA, Random Forest feature importance, SHAP, and hypothesis testing — suitable for recruiters looking for regression, pricing models, feature engineering, evaluation, and business interpretation.

---

## Metrics Highlights

- **Madrid housing**: Pipeline through data cleaning, imputation, impact encoding of `Area` w.r.t. `Rent`, and 70/15/15 train/val/test split — ready for linear or regularised regression and R²/MAE/MSE evaluation.
- **Used cars (100K+)**: EDA, outlier treatment (IQR), one-hot and label encoding, PCA, Random Forest feature importance, SHAP, and hypothesis testing on price drivers.

_(Add specific R²/MAE/MSE from your runs here once you run or extend the Madrid modelling section.)_

---

## Repository Structure

```
├── README.md                 # This file
├── requirements.txt          # Python dependencies
├── data/                     # Datasets (paths used in notebooks)
│   ├── houses_for_rent_madrid.xlsx
│   └── ...
└── notebooks/               # Jupyter notebooks
    ├── madrid_housing_rent_regression.ipynb
    └── vehicle_pricing_valuation.ipynb
```

---

## How to Run

1. **Clone** the repo and create a virtual environment (recommended).
2. **Install** dependencies:  
   `pip install -r requirements.txt`  
   _(Ensure `requirements.txt` lists pandas, numpy, scikit-learn, openpyxl, matplotlib, seaborn, and any other packages used in the notebooks.)_
3. **Run** notebooks from the project root so paths like `data/houses_for_rent_madrid.xlsx` resolve, or set `DATA_PATH` / URLs as in the notebooks.
4. **Colab**: Upload the repo or notebooks to Google Drive and open in Colab; mount Drive and set `DATA_PATH` if needed.

_(Optional: add Colab badges linking to copies of the notebooks if you host them on Colab.)_

---

## Key Takeaways

- **Judgement over metrics**: Choices (e.g. impact encoding only from train, IQR for skewed distributions, train/val/test split) show awareness of leakage and evaluation rigour.
- **End-to-end pipelines**: From raw data and quality checks through encoding and train/val/test to (where implemented) model fitting and evaluation.
- **Interpretation**: Emphasis on why features matter (e.g. SHAP, hypothesis tests, business context) rather than only reporting R² or MAE.

---

## Optional: `data_description.md` and `results_summary.md`

| File                      | Purpose                                                                                         | Recommendation                                                                          |
| ------------------------- | ----------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **`data_description.md`** | Short description of each dataset (source, columns, target, sample size, license).              | **Good idea.** Lets recruiters understand inputs without opening a notebook.            |
| **`results_summary.md`**  | Bullet summary of main results: best model per case study, 2–3 metrics, 1–2 business takeaways. | **Good idea.** Complements the README and gives a single place for “what was achieved.” |

Keep both to **one short page each** so they stay skim-friendly. The README stays the main entry point; these two files support deeper but still quick scanning.
