# Business Regression Analysis — 

## 1. Business Problem Summary
A retail chain wants to understand what drives **monthly sales** across its store network. By identifying the strongest predictors — such as customer footfall, marketing spend, inventory availability, store type, and regional factors — leadership can make data-driven decisions to allocate budgets, prioritise store improvements, and set realistic sales targets.

## 2. Dataset Description
| Attribute | Detail |
|---|---|
| File | `business_regression_data.xlsx` |
| Sheet | `store_performance` |
| Rows | 320 observations |
| Stores | 80 unique stores (STR-1001 to STR-1080) |
| Time Period | Jan 2025 – Apr 2025 (4 months each) |
| Missing Values | `competitor_distance_km` (6 missing), `customer_rating` (8 missing) → imputed with median |

## 3. Dependent and Independent Variables

### Dependent Variable
- **`monthly_sales`** — Total monthly revenue per store (£). This is the outcome we are trying to predict and explain.

### Independent Variables
| Variable | Type | Role |
|---|---|---|
| `marketing_spend` | Numerical | Key predictor — investment in promotion |
| `footfall` | Numerical | Key predictor — number of customer visits |
| `avg_discount_pct` | Numerical | Potential predictor — average discount offered |
| `staff_count` | Numerical | Potential predictor — workforce size |
| `inventory_availability_pct` | Numerical | Potential predictor — stock availability |
| `competitor_distance_km` | Numerical | Weak predictor — proximity to competition |
| `holiday_flag` | Numerical (binary) | Contextual — whether month includes public holiday |
| `customer_rating` | Numerical | Moderate predictor — customer satisfaction score |
| `region` | Categorical | Regional dummy — East / North / South / West |
| `store_type` | Categorical | Store type dummy — Residential / High Street / Mall / Airport |

### Variables Requiring Cleaning/Transformation
- **`competitor_distance_km`**: 6 missing values → imputed with median (5.27 km)
- **`customer_rating`**: 8 missing values → imputed with median (3.9)
- **`region`** and **`store_type`**: Categorical → encoded as dummy variables (see Task 3)
- **`month`**: Stored as date; not used as numeric predictor (treated as a panel grouping variable)
- **`monthly_profit`**: Excluded from regression (it is an outcome, not a predictor; also collinear with `monthly_sales`)
- **`store_id`**: Excluded — identifier, not a predictor

### Variables Not Useful for Regression
- `store_id` — unique identifier with no predictive value
- `monthly_profit` — another outcome variable; should not be used as an independent variable

## 4. Regression Approach
- **Simple regression**: Run separately with `footfall` and `marketing_spend` as individual predictors
- **Multiple regression**: Combined model with 5 numerical predictors plus dummy variables for region and store type
- Ordinary Least Squares (OLS) method used throughout
- Reference categories: **East** (region), **Residential** (store_type)

## 5. Dummy Variable Approach
- Region dummies: `region_North`, `region_South`, `region_West` (reference: East)
- Store type dummies: `type_Airport`, `type_HighStreet`, `type_Mall` (reference: Residential)
- Avoided the dummy variable trap by dropping one category per variable

## 6. Model Comparison Summary
| Model | R² | Key Insight |
|---|---|---|
| Simple – Footfall | 0.7363 | Footfall alone explains 74% of sales variation |
| Simple – Marketing Spend | 0.1672 | Marketing spend explains only 17% alone |
| Multiple Regression | 0.8321 | Combined model explains 83% — best model |

## 7. Final Model Selected
**Multiple Regression Model** — chosen for its superior R² (0.8321), inclusion of business-relevant variables, and ability to isolate the independent effect of each predictor while controlling for store characteristics.

## 8. Business Recommendation
Leadership should **focus on footfall and inventory availability** as the primary levers for sales growth. Marketing spend shows a statistically significant but secondary effect. Airport and Mall stores consistently outperform Residential stores. South and West regions outperform the East. Customer rating has a meaningful positive impact — investing in service quality pays off.

## 9. Assumptions and Limitations
- OLS assumes linearity, homoscedasticity, and no multicollinearity — these are approximately satisfied
- The panel nature of the data (same stores across 4 months) means observations are not fully independent; a fixed-effects model would be more rigorous
- Missing values were imputed, which may introduce minor bias
- `competitor_distance_km` was not statistically significant in any model — it may require more granular competitive data
- Correlation does not imply causation — increasing marketing spend does not guarantee proportional sales gains

## 10. Screenshots Included
<img width="2385" height="884" alt="model_comparison_preview" src="https://github.com/user-attachments/assets/75a0776b-a9f0-4340-a9d2-86599ebec64f" />
<img width="2081" height="881" alt="simple_regression_output" src="https://github.com/user-attachments/assets/ddb0d7e1-8f03-4522-8e79-a70abd0b6ea4" />
<img width="2686" height="732" alt="residuals_preview" src="https://github.com/user-attachments/assets/a26f8a1d-b8cc-4f53-8028-34fd425b17d3" />
<img width="2082" height="875" alt="multiple_regression_output" src="https://github.com/user-attachments/assets/5382bc3c-17ce-43d3-a060-6a1547ee43a3" />
