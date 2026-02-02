# Vehicle Pricing Valuation — Data Description

Short reference for recruiters: inputs used in the notebook without opening it.

---

## Cars_rdm.csv (Used Cars)

**Source:** `https://raw.githubusercontent.com/prof-apartida/data-exercises/main/Cars_rdm.csv`  
**Local path:** `data/Cars_rdm.csv`

| Attribute   | Description                  |
| ----------- | ---------------------------- |
| **Rows**    | 100,000                      |
| **Columns** | 11                           |
| **Target**  | `Price` (vehicle price, EUR) |

### Columns

| Column           | Type        | Description                                             |
| ---------------- | ----------- | ------------------------------------------------------- |
| Country          | Categorical | Listing country (8 values: NL, I, B, E, F, A, …)        |
| Manufacturer     | Categorical | Brand (182 values)                                      |
| Model            | Categorical | Model name (2,024 values)                               |
| Price            | Numeric     | **Target** — vehicle price (€1–€4.4M)                   |
| Km               | Numeric     | Odometer (kilometers)                                   |
| Automatic_Manual | Categorical | Transmission (Manual, Automatico, Semiautomatico, etc.) |
| Year             | Datelike    | Registration date (e.g., 1/2/02)                        |
| Fuel             | Categorical | Fuel type (Gasoline, Diesel, Electrico, etc.)           |
| kW               | Numeric     | Power (kilowatts)                                       |
| Horse            | Numeric     | Horsepower                                              |
| Order            | Numeric     | Sort/order index (auxiliary)                            |

### Target summary

- Mean: ~€27,447
- Std: ~€58,900
- Range: €1 – €4,400,000

### Notes

- Categoricals (Country, Manufacturer, Model, Automatic_Manual, Fuel, Year) are encoded (label or one-hot) for modeling.
- Year is parsed to extract registration year.
- `Order` is typically dropped for modeling.
