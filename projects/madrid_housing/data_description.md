# Madrid housing rent dataset

- **Purpose**: Supervised learning dataset to predict monthly rent for residential properties in Madrid using listing metadata and simple structural features.

- **Raw data source & size**

  - **File**: `data/houses_for_rent_madrid.xlsx`
  - **Observations**: 2,089 listings (rows)
  - **Columns**: 15 original fields before cleaning/feature engineering
  - **Geography**: Neighborhoods (`Area`) nested within city districts (`District`) of Madrid.

- **Key raw columns**

  - **Id**: Integer listing identifier (not used as a feature).
  - **District**: City district name (≈20 categories).
  - **Address**: Listing title / address text.
  - **Number**: Street number, stored as text / mixed.
  - **Area**: Neighborhood / sub-district name (≈140 categories). Later impact‑encoded.
  - **Rent**: Monthly asking rent in euros. This is the **target** variable.
  - **Bedrooms**: Number of bedrooms (0–8, numeric).
  - **Sq.Mt**: Built area in square meters (15–1,250).
  - **Floor**: Floor number (−1 for basement, 0 ground, up to high‑rise values; extreme outliers are later filtered).
  - **Outer**: 0/1 flag indicating an exterior‑facing unit.
  - **Elevator**: 0/1 flag indicating whether the building has an elevator.
  - **Penthouse**, **Cottage**, **Duplex**, **Semidetached**: 0/1 flags indicating specific dwelling types.

- **Cleaning and preprocessing in the notebook**

  - **Missing values**
    - Replaced string `"NaN"` values with actual `NaN`.
    - Imputed missing **Bedrooms**, **Floor**, and **Sq.Mt** using each column’s median (fit on the full dataset).
    - After imputation, dropped any remaining rows containing `NaN` in any column to obtain a fully dense table for modeling.
  - **Column selection**
    - Dropped non‑predictive or high‑cardinality identifier / free‑text fields: `Id`, `District`, `Address`, `Number`.
    - Retained numeric/binary structural features and `Area` for encoding.
  - **Outlier filtering**
    - Removed listings with **Floor > 20** to discard implausible floor values (e.g., 43,039), keeping only realistic residential high‑rise floors.

- **Train / validation / test splits**

  - **Split strategy**: Random split using `train_test_split` on the **filtered** dataset.
  - **Initial split (before encoding, after floor filter)**:
    - **Train**: 70% – 1,456 rows, 15 columns.
    - **Validation**: 15% – 312 rows, 15 columns.
    - **Test**: 15% – 313 rows, 15 columns.
  - **Impact encoding of `Area`**
    - On the **training set only**, computed mean `Rent` per `Area`.
    - Created an `Area_encoded` feature via mapping, applied consistently to train/val/test.
    - Dropped rows in val/test whose `Area` was unseen in training (their encoding would be undefined).
    - Replaced the original categorical `Area` with the numeric impact‑encoded `Area` column.
  - **Final modeling‑ready tables**:
    - Three dense, numeric datasets (train/val/test) containing: impact‑encoded `Area`, `Rent` (target), `Bedrooms`, `Sq.Mt`, `Floor`, and binary property‑type / amenity flags.
    - Exact row counts after dropping unseen‑`Area` rows are slightly smaller than the initial 1,456 / 312 / 313, but maintain the same ~70/15/15 proportions.

- **Intended downstream use**
  - Baseline and benchmark regression models (e.g., regularized linear models, tree‑based models) predicting **Rent** from cleaned and encoded features.
  - Fair comparison across models is supported by the fixed train/validation/test split and the consistent impact encoding learned only on the training data.
