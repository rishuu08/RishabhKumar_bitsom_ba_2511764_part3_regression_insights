# Model Equations and Coefficient Explanations

## Dummy Variable Approach

### What Are Dummy Variables?
Dummy variables convert categorical text values into numerical 0/1 indicators so they can be included in a regression equation. Each dummy variable asks: "Is this store in this category? Yes (1) or No (0)."

### Reference Categories (Baseline)
To avoid the "dummy variable trap" (perfect multicollinearity), one category per variable is excluded and becomes the **reference group** against which all others are compared:

| Categorical Variable | Reference Category (Excluded) | Reason for Selection |
|---|---|---|
| `region` | **East** | Largest regional group; provides a neutral comparison baseline |
| `store_type` | **Residential** | Most common store type; useful as a baseline for other formats |

### Dummy Variables Created
| Dummy Variable | = 1 When... | = 0 Otherwise |
|---|---|---|
| `region_North` | Store is in North region | Not North |
| `region_South` | Store is in South region | Not South |
| `region_West` | Store is in West region | Not West |
| `type_Airport` | Store is an Airport store | Not Airport |
| `type_HighStreet` | Store is a High Street store | Not High Street |
| `type_Mall` | Store is a Mall store | Not Mall |

---

## Simple Regression Equations

### Model 1: Footfall → Monthly Sales
```
monthly_sales = 446,411 + 35.68 × footfall
```
| Term | Value | Explanation |
|---|---|---|
| Intercept | £446,411 | Expected monthly sales if footfall were zero (theoretical baseline) |
| footfall coefficient | +35.68 | Each additional customer visit in a month is associated with **£35.68 more in monthly sales** |
| R² | 0.7363 | Footfall explains 73.6% of the sales variation across stores |
| P-value | < 0.001 | Highly statistically significant |

**Business meaning**: Footfall is the dominant driver of sales. Strategies that increase the number of customers entering the store (better location, marketing, signage) will have a large direct sales impact.

---

### Model 2: Marketing Spend → Monthly Sales
```
monthly_sales = 560,777 + 2.13 × marketing_spend
```
| Term | Value | Explanation |
|---|---|---|
| Intercept | £560,777 | Expected monthly sales if marketing spend were £0 (baseline — includes all other factors not in the model) |
| marketing_spend coefficient | +2.13 | Each additional **£1 invested in marketing** is associated with **£2.13 more in monthly sales** |
| R² | 0.1672 | Marketing spend alone explains only 16.7% of sales variation |
| P-value | < 0.001 | Statistically significant, but weak standalone predictor |

**Business meaning**: Marketing spend does increase sales, but much of what drives sales (footfall, store type) is not captured here. The 2.13× ROI on marketing spend appears modest in isolation but may be higher when controlling for other factors — see Model 3.

---

## Multiple Regression Equation (Final Model)

```
monthly_sales = 49,913
              + 1.20  × marketing_spend
              + 34.00 × footfall
              − 45,709 × avg_discount_pct
              + 3,002  × inventory_availability_pct
              + 13,627 × customer_rating
              + 6,185  × region_North
              + 18,685 × region_South
              + 18,111 × region_West
              + 41,880 × type_Airport
              + 18,093 × type_HighStreet
              + 29,086 × type_Mall
```

### Coefficient Explanations

| Variable | Coefficient | P-value | Direction | Plain English Explanation |
|---|---|---|---|---|
| **Intercept** | £49,913 | 0.30 | — | The baseline monthly sales for an East-region Residential store with all numerical predictors at zero. Theoretically unlikely but anchors the equation. |
| **marketing_spend** | +1.20 | < 0.001 | ↑ Positive | After controlling for footfall and store characteristics, each extra **£1 of marketing spend** generates approximately **£1.20 in incremental sales**. Statistically very significant. |
| **footfall** | +34.00 | < 0.001 | ↑ Positive | Each additional **customer visit per month** is associated with **£34 more in sales**, holding all other factors constant. The single strongest predictor. |
| **avg_discount_pct** | −45,709 | 0.211 | ↓ Negative | A 1-unit increase in average discount % is associated with lower sales, but this is **not statistically significant** (p = 0.21). Discounting does not reliably drive top-line sales — and may hurt profitability without boosting revenue. |
| **inventory_availability_pct** | +3,002 | < 0.001 | ↑ Positive | Each **1 percentage point improvement in in-store stock availability** is associated with **£3,002 more in monthly sales**. Empty shelves cost sales. |
| **customer_rating** | +13,627 | 0.005 | ↑ Positive | Each **1-point improvement in customer satisfaction rating** (e.g., from 3.5 to 4.5) is associated with **£13,627 more in monthly sales**. Customer experience matters significantly. |
| **region_North** | +6,185 | 0.380 | ↑ Positive | North stores earn £6,185 more than comparable East stores, but this difference is **not statistically significant** (p = 0.38). The North region does not significantly outperform East. |
| **region_South** | +18,685 | 0.009 | ↑ Positive | South stores earn **£18,685 more per month** than comparable East stores. **Statistically significant**. South region has a structural advantage (e.g., higher consumer spending or density). |
| **region_West** | +18,111 | 0.004 | ↑ Positive | West stores earn **£18,111 more per month** than comparable East stores. **Statistically significant**. West region outperforms East similarly to South. |
| **type_Airport** | +41,880 | < 0.001 | ↑ Positive | Airport stores earn **£41,880 more per month** than comparable Residential stores. **Strongly significant**. High-traffic, captive-audience environment commands a major sales premium. |
| **type_HighStreet** | +18,093 | 0.003 | ↑ Positive | High Street stores earn **£18,093 more per month** than Residential stores. **Significant**. Prime high street locations generate higher sales even controlling for footfall. |
| **type_Mall** | +29,086 | < 0.001 | ↑ Positive | Mall stores earn **£29,086 more per month** than Residential stores. **Strongly significant**. Mall environments drive browsing and impulse purchases. |

---

## Final Model Selected

### Model 3 — Multiple Regression

**Reason for Selection:**
1. **Highest R² (0.8321)** — explains 83.2% of monthly sales variation, far better than either simple model
2. **Multiple actionable levers** — leadership can act on marketing spend, inventory levels, customer service, and location strategy simultaneously
3. **Accounts for structural differences** — by including store type and region dummies, the model correctly attributes performance differences to location factors rather than misattributing them to operational variables
4. **Statistically robust** — all key variables have strong p-values (< 0.01); the model is well-specified
5. **Interpretable in business language** — each coefficient has a clear, quantified business meaning for non-technical audiences

The simple models (Models 1 and 2) are useful for quick intuition but are insufficient for strategic planning or resource allocation decisions.
