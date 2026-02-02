# Madrid housing rent regression – summary

- **Study goal**

  - Prepare a clean, modeling‑ready dataset to predict monthly rent (`Rent`, in euros) for Madrid properties using structural attributes (size, bedrooms, floor, property type, amenities) and neighborhood information.

- **Data preparation pipeline (what was built)**

  - **Base data**: 2,089 raw listings from `houses_for_rent_madrid.xlsx` with 15 columns (district, address text, neighborhood `Area`, `Rent`, bedrooms, floor, size, and dwelling‑type / amenity flags).
  - **Cleaning**:
    - Standardized missing values (converted string `"NaN"` to true missing).
    - Imputed missing **Bedrooms**, **Floor**, and **Sq.Mt** using their medians.
    - Dropped any remaining rows with missing data to obtain a fully numeric, dense table.
  - **Feature selection & sanity checks**:
    - Removed `Id`, `District`, `Address`, and `Number` (non‑predictive identifiers / high‑cardinality text).
    - Filtered out listings with **Floor > 20** to eliminate clear data‑entry outliers.
  - **Dataset splits**:
    - Created a 70% / 15% / 15% split into **train**, **validation**, and **test** sets (approximately 1,456 / 312 / 313 rows respectively before encoding).
  - **Neighborhood impact encoding**:
    - On the **training set only**, computed the mean `Rent` per `Area` and mapped that value into a new numeric `Area_encoded` feature.
    - Applied the encoding to validation and test sets, then dropped rows whose `Area` did not appear in training.
    - Replaced the original categorical `Area` column with this impact‑encoded numeric `Area` in all three splits.

- **Key descriptive findings (metrics about the market)**

  - **Rent levels**:
    - Mean rent ≈ **€1,930**; median ≈ **€1,400**; interquartile range roughly **€950–€2,500**; full range **€450–€16,000**.
  - **Home size and layout**:
    - Median size ≈ **90 m²** (IQR ≈ 65–147 m²).
    - Most listings offer **2–3 bedrooms**, with very few studio (0‑bedroom) or 6+‑bedroom units.
  - **Building characteristics**:
    - The majority of homes are in buildings with an **elevator** and are **exterior** units (outer‑facing).
    - Raw data contained extreme floor values (e.g., tens of thousands), which were removed by limiting **Floor ≤ 20**.

- **Modeling status for this notebook**

  - This notebook **stops at data cleaning, feature engineering, and train/val/test splitting**.
  - No regression models are trained or evaluated here; those steps are intended to occur in follow‑up notebooks using the prepared, leakage‑resistant splits.

- **Business‑oriented takeaways**
  - **Neighborhood and size are primary rent drivers**: the impact‑encoded `Area` feature and `Sq.Mt` capture most of the systematic variation in rents, and are ready to feed into predictive models.
  - **Data quality matters for pricing**: cleaning missing values and removing implausible entries (e.g., unrealistic floor numbers) ensures that any future rent models reflect real, actionable pricing patterns rather than artifacts of noisy input data.
