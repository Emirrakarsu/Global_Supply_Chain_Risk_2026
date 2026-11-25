# Global Supply Chain Risk Analysis

A data analysis project built with Python (Pandas, NumPy, Matplotlib) on a dataset of 5,000 global shipments (2024–2025). It estimates shipping costs, classifies shipments by risk, compares transport modes, and looks at monthly shipment trends.

Built as a university project for my Management Information Systems degree.

## Dataset

`GSCR2026.csv`: 5,000 shipments, 16 columns, no missing values.

| Group | Columns |
|---|---|
| Shipment | `Shipment_ID`, `Date`, `Origin_Port`, `Destination_Port`, `Transport_Mode`, `Product_Category` |
| Numeric | `Distance_km`, `Weight_MT`, `Fuel_Price_Index`, `Geopolitical_Risk_Score`, `Carrier_Reliability_Score`, `Lead_Time_Days` |
| Other | `Weather_Condition`, `Disruption_Occurred`, `Total_Estimated_Cost`, `Risk_Category` |

Source: <add the dataset source/link here>

## What the notebook does

1. **Cost estimation**: recalculates `Total_Estimated_Cost` with a simplified formula:
   `(Distance × Fuel Price Index × Weight / 100) + 250 base fee`,
   then compares total cost per transport mode.
2. **Risk categorization**: assigns each shipment a risk level with rule-based logic (`np.where`):
   - `CRITICAL`: geopolitical risk ≥ 7 and a disruption occurred
   - `WARNING`: geopolitical risk ≥ 5 and weather is Storm or Hurricane
   - `STABLE`: everything else
3. **Carrier reliability and delay analysis**: average reliability score and lead time per transport mode, plus a reliability vs. lead time scatter plot.
4. **Time series**: monthly shipment volume (resampled by month-end).

## Key findings

- **Total estimated cost by mode**: Air (~72.2M) > Sea (~67.8M) > Rail (~65.2M) > Road (~64.4M).
- **Risk distribution**: 68.4% STABLE (3,421), 23.0% CRITICAL (1,152), 8.5% WARNING (427).
- **Lead time**: Air averages ~1.6 days, Road ~16.5, Rail ~20.0, Sea ~39.8.
- **Reliability** is almost identical across modes (≈0.75–0.76), so reliability does not explain the lead time differences.
- **Monthly volume** stays fairly stable, between 173 and 231 shipments per month.

## Charts

| | |
|---|---|
| ![Cost by mode](Transport_Mode.svg) | ![Risk distribution](Risk_Scatter.svg) |
| ![Reliability vs lead time](Reliability_Score.svg) | ![Monthly shipments](Shipment_Size.svg) |

## Tech stack

Python 3 · Pandas · NumPy · Matplotlib · Jupyter Notebook

## How to run

```bash
pip install pandas numpy matplotlib jupyter
jupyter notebook main.ipynb
```

Make sure `GSCR2026.csv` is in the same folder as the notebook.

## Notes

- `Total_Estimated_Cost` and `Risk_Category` are recalculated in the notebook with simplified rules, so they replace the values in the original CSV. The cost formula is an approximation for analysis, not real pricing.
- The risk rules and thresholds are my own assumptions for this exercise.

## Author

Baran Emir Akarsu · [LinkedIn](https://linkedin.com/in/emir-akarsu)