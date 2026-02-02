# Vehicle Pricing Valuation — Results Summary

Quick overview of what was achieved. See README and the notebook for full detail.

---

## Best Model per Study

| Study                    | Best Model                                     | R²        | MAE        | RMSE (approx) |
| ------------------------ | ---------------------------------------------- | --------- | ---------- | ------------- |
| Label-encoded baseline   | Random Forest (n=200, depth=5)                 | 0.605     | €5,281     | ~€7,700       |
| **Label-encoded, tuned** | **Gradient Boosting** (lr=0.1, depth=3, n=100) | **0.655** | **€4,688** | ~€7,200       |
| Grid search (sample)     | Random Forest                                  | 0.459     | €6,086     | ~€9,015       |

**Primary best model:** Gradient Boosting with label-encoded features — R² 0.655, MAE €4,688.

---

## Top Metrics (Gradient Boosting)

- **R² = 0.655** — explains ~65.5% of price variance.
- **MAE ≈ €4,688** — average absolute error per prediction.
- **RMSE ≈ €7,200** — penalizes larger errors more.

---

## Feature Importance (Price Drivers)

1. **Year** (~40%) — registration age is the strongest driver.
2. **kW** (~25%) — engine power.
3. **Km** (~11%) — mileage.
4. Model, Manufacturer, Country, Transmission, Fuel — smaller contributions.

---

## Business Takeaways

1. **Age and power drive price.** Registration year and power (kW) account for most of the explained variance. Pricing tools should emphasize these first.
2. **Predictable error band.** MAE ~€4,700 on a mean price ~€27,500 gives roughly ±17% error. Suitable for listings guidance and rough valuations rather than exact appraisal.
