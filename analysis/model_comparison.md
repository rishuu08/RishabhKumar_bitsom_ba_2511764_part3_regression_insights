# Model Comparison Report

## Overview
This document compares three regression models built to explain and predict **monthly sales** across 80 retail stores over 4 months (320 observations). All models use `monthly_sales` as the dependent variable and are estimated using Ordinary Least Squares (OLS).

---

## Model 1 — Simple Regression: Footfall

### Variables Used
- **Dependent**: `monthly_sales`
- **Independent**: `footfall` (number of customer visits per month)

### Regression Equation
```
monthly_sales = 446,411 + 35.68 × footfall
```

### R-squared
| Metric | Value |
|---|---|
| R² | **0.7363** |
| Interpretation | Footfall alone explains **73.6%** of the variation in monthly sales |

### Significant Variables
| Variable | Coefficient | P-value | Significant? |
|---|---|---|---|
| Intercept | 446,410.58 | < 0.001 | ✅ Yes |
| footfall | 35.68 | < 0.001 | ✅ Yes |

### Business Usefulness
Footfall is the **single strongest individual predictor** of monthly sales. Each additional customer visit is associated with approximately **£35.68 in additional monthly sales**. This model is easy to understand and operationalise — store managers can track footfall as a leading indicator of sales performance. However, it ignores other important factors.

### Limitations
- Does not account for marketing spend, discounting, staffing, or store characteristics
- Assumes a constant return per visitor regardless of store type or location
- Cannot explain why some high-footfall stores underperform
- Not suitable for scenario planning across diverse store formats

---

## Model 2 — Simple Regression: Marketing Spend

### Variables Used
- **Dependent**: `monthly_sales`
- **Independent**: `marketing_spend` (monthly promotional investment, £)

### Regression Equation
```
monthly_sales = 560,777 + 2.13 × marketing_spend
```

### R-squared
| Metric | Value |
|---|---|
| R² | **0.1672** |
| Interpretation | Marketing spend explains only **16.7%** of sales variation — a weak standalone predictor |

### Significant Variables
| Variable | Coefficient | P-value | Significant? |
|---|---|---|---|
| Intercept | 560,777.35 | < 0.001 | ✅ Yes |
| marketing_spend | 2.13 | < 0.001 | ✅ Yes |

### Business Usefulness
While marketing spend is statistically significant, its standalone explanatory power is limited. The coefficient of **2.13** means each additional **£1 spent on marketing is associated with approximately £2.13 in additional monthly sales** — a positive but modest return. This model alone is not sufficient for decision-making but confirms marketing does have a measurable effect.

### Limitations
- Very low R² (0.17) means 83% of sales variation is unexplained
- The simple model may overstate the ROI of marketing in isolation
- Cannot separate marketing effect from store type, location, or traffic
- Sensitive to outliers (one store had marketing spend of £172K — nearly 3× the average)

---

## Model 3 — Multiple Regression Model (Final Model)

### Variables Used
- **Dependent**: `monthly_sales`
- **Independent (Numerical)**: `marketing_spend`, `footfall`, `avg_discount_pct`, `inventory_availability_pct`, `customer_rating`
- **Independent (Dummies – Region)**: `region_North`, `region_South`, `region_West` (Reference: East)
- **Independent (Dummies – Store Type)**: `type_Airport`, `type_HighStreet`, `type_Mall` (Reference: Residential)

### Regression Equation
```
monthly_sales = 49,913
              + 1.20 × marketing_spend
              + 34.00 × footfall
              − 45,709 × avg_discount_pct
              + 3,002 × inventory_availability_pct
              + 13,627 × customer_rating
              + 6,185 × region_North
              + 18,685 × region_South
              + 18,111 × region_West
              + 41,880 × type_Airport
              + 18,093 × type_HighStreet
              + 29,086 × type_Mall
```

### R-squared
| Metric | Value |
|---|---|
| R² | **0.8321** |
| Adjusted R² | **0.8261** |
| Interpretation | The model explains **83.2%** of the variation in monthly sales |

### Significant Variables
| Variable | Coefficient | P-value | Significant? | Business Meaning |
|---|---|---|---|---|
| footfall | 34.00 | < 0.001 | ✅ *** | Each extra visitor → +£34 in sales |
| marketing_spend | 1.20 | < 0.001 | ✅ *** | Each £1 of marketing → +£1.20 in sales |
| inventory_availability_pct | 3,002 | < 0.001 | ✅ *** | 1% more stock in-store → +£3,002 in sales |
| type_Airport | 41,880 | < 0.001 | ✅ *** | Airport stores earn £41.9K more than Residential |
| type_Mall | 29,086 | < 0.001 | ✅ *** | Mall stores earn £29.1K more than Residential |
| customer_rating | 13,627 | 0.005 | ✅ ** | 1-point rating increase → +£13,627 in sales |
| type_HighStreet | 18,093 | 0.003 | ✅ ** | High Street stores earn £18.1K more than Residential |
| region_West | 18,111 | 0.004 | ✅ ** | West region earns £18.1K more than East |
| region_South | 18,685 | 0.009 | ✅ ** | South region earns £18.7K more than East |
| avg_discount_pct | −45,709 | 0.211 | ❌ Not sig. | Discounting not a reliable sales driver |
| region_North | 6,185 | 0.380 | ❌ Not sig. | North vs East difference is not statistically meaningful |

### Business Usefulness
This is the **most complete and actionable model** for leadership decisions. It identifies multiple controllable levers: footfall (driven by location strategy and marketing), marketing budget, inventory management, and customer experience. It also quantifies the structural advantage of Airport and Mall stores over Residential ones, informing future expansion strategy.

### Limitations
- OLS assumes store-months are independent; the panel structure (same store over 4 months) means some autocorrelation may exist
- `avg_discount_pct` is not significant — the model cannot confirm or deny the profitability of discounting on its own
- `competitor_distance_km` was excluded after testing — it was not statistically significant and had missing values
- The model captures ~83% of variance; ~17% remains unexplained (store-specific factors, local events, product mix, etc.)
- Coefficients represent associations, not causal effects — controlled experiments (A/B tests) are needed to confirm ROI of specific interventions

---

## Summary Comparison Table

| Item | Model 1 (Simple – Footfall) | Model 2 (Simple – Marketing) | Model 3 (Multiple) |
|---|---|---|---|
| **Model Name** | Simple Regression: Footfall | Simple Regression: Marketing Spend | Multiple Regression (Full Model) |
| **Dependent Variable** | monthly_sales | monthly_sales | monthly_sales |
| **Independent Variables** | footfall | marketing_spend | footfall, marketing_spend, inventory_availability_pct, avg_discount_pct, customer_rating, region dummies, store type dummies |
| **R²** | 0.7363 | 0.1672 | **0.8321** |
| **Adjusted R²** | 0.7354 | 0.1645 | **0.8261** |
| **Significant Variables** | footfall | marketing_spend | footfall, marketing_spend, inventory_availability_pct, customer_rating, type_Airport, type_Mall, type_HighStreet, region_West, region_South |
| **Business Usefulness** | High — simple and intuitive | Low–Moderate — confirms marketing ROI | **Very High — complete picture** |
| **Limitations** | Ignores all other factors | Very low explanatory power | Assumes independence; some variables not significant |

## Recommended Model: **Model 3 (Multiple Regression)**
Model 3 is selected as the final model because it provides the highest explanatory power (R² = 0.83), identifies multiple actionable business levers, accounts for structural differences between store types and regions, and remains interpretable for non-technical stakeholders.
