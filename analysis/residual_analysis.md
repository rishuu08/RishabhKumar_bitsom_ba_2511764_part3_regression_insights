# Residual Analysis Report

## Overview
This analysis examines the residuals of the **Multiple Regression Model** (Model 3 — our selected final model). Residuals are the difference between each store's **actual monthly sales** and the sales **predicted** by the model.

```
Residual = Actual Monthly Sales − Predicted Monthly Sales
```

A positive residual means the store **outperformed** predictions. A negative residual means the store **underperformed** predictions.

---

## Predicted vs Actual Sales — Summary Statistics

| Metric | Value |
|---|---|
| Model R² | 0.8321 |
| Mean Residual | ≈ £0 (by OLS construction) |
| Residual Std Dev | ≈ £42,700 |
| Max Positive Residual | +£112,751 (STR-1028) |
| Max Negative Residual | −£159,513 (STR-1017) |

---

## Stores with Largest Positive Residuals
*(Actual Sales > Predicted Sales — model under-predicted these stores)*

| Rank | Store ID | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|
| 1 | STR-1028 | £713,611 | £600,860 | **+£112,751** |
| 2 | STR-1073 | £813,317 | £707,150 | **+£106,167** |
| 3 | STR-1019 | £788,088 | £695,490 | **+£92,597** |
| 4 | STR-1069 | £686,738 | £595,018 | **+£91,720** |
| 5 | STR-1050 | £735,787 | £646,314 | **+£89,472** |

### Business Interpretation — Positive Residuals
These stores are **outperforming what their observable characteristics would predict**. This could mean:
- **Strong local management** or superior execution not captured in the data
- **Local demand drivers** (nearby office complexes, schools, transport hubs) not captured by competitor distance or footfall alone
- **Loyal repeat customers** — word-of-mouth and community reputation that inflates conversion above the average
- **Product mix advantages** — a more premium or locally relevant assortment that commands higher basket value
- **Marketing quality vs quantity** — efficient and well-targeted campaigns delivering above-average return on spend

These stores represent **best practice candidates** worth studying more closely. Leadership should conduct site visits or qualitative interviews to understand what these stores do differently.

---

## Stores with Largest Negative Residuals
*(Actual Sales < Predicted Sales — model over-predicted these stores)*

| Rank | Store ID | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|
| 1 | STR-1017 | £685,379 | £844,892 | **−£159,513** |
| 2 | STR-1023 | £627,172 | £773,115 | **−£145,943** |
| 3 | STR-1012 | £595,468 | £715,299 | **−£119,831** |
| 4 | STR-1007 | £800,452 | £913,151 | **−£112,699** |
| 5 | STR-1014 | £463,534 | £563,493 | **−£99,959** |

### Business Interpretation — Negative Residuals
These stores are **underperforming relative to what their characteristics suggest they should achieve**. Possible explanations include:
- **Operational issues** — poor service quality, long queues, or inefficient store layout reducing conversion despite adequate footfall
- **Local competitive pressure** not fully captured by a single competitor distance metric (e.g., multiple nearby competitors, online retail dominance in the area)
- **Staffing challenges** — high turnover or inexperienced staff leading to poor customer experience
- **Structural disadvantages** — difficult access, limited parking, or declining neighbourhood foot traffic patterns
- **Product ranging problems** — misalignment between stock and local customer preferences, leading to high footfall but low basket size

These stores require **operational review**. Leadership should investigate whether the gap is due to fixable operational issues or structural/location factors.

---

## Model Bias Assessment: Over-predicting or Under-predicting Certain Types?

### By Store Type
Based on residual patterns:
- **High Street stores** (STR-1017, STR-1014) appear in the most under-predicted group — the model may slightly **over-predict High Street stores** whose local competitive environment is tougher than average
- **Mall and Residential stores** (STR-1028, STR-1050, STR-1073) appear in the most over-predicted group, suggesting the model may **under-predict strong-performing Residential/Mall stores** that have local advantages

### Recommendation
The model performs well overall (R² = 0.83), but the residuals suggest:
1. **High Street stores** may need an additional predictor (e.g., local competition index or high street health score) to improve prediction accuracy
2. **Some Residential stores outperform systematically** — a possible "hidden variable" like proximity to residential density data or local school proximity could improve the model
3. The spread of residuals appears **roughly symmetric** around zero with no strong trend vs predicted value — this is a good sign that the model is not systematically biased

---

## Visual Evidence
See: `screenshots/residuals_preview.png`

The residual plots show:
- Residuals scatter roughly randomly around zero (no clear curved pattern) — confirming the linear model is appropriate
- The distribution of residuals is approximately bell-shaped (near-normal) — supporting the validity of OLS inference
- No dramatic heteroscedasticity (variance doesn't strongly increase with predicted value)
