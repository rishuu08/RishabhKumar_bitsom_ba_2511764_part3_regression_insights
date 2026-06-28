# Final Business Recommendation

## Executive Summary
Based on regression analysis of 320 store-month observations across 80 retail locations, this report identifies the key drivers of monthly sales and provides actionable recommendations for leadership.

The selected model (Multiple Regression, R² = 0.83) explains **83% of the variation in monthly sales** and identifies several controllable factors that leadership can use to improve performance.

---

## 1. Which Factors Are Most Strongly Associated with Monthly Sales?

| Rank | Factor | Effect Size | Statistical Confidence |
|---|---|---|---|
| 1 | **Footfall** (customer visits) | +£34 per visitor/month | Very High (p < 0.001) |
| 2 | **Store Type** – Airport | +£41,880 vs Residential | Very High (p < 0.001) |
| 3 | **Store Type** – Mall | +£29,086 vs Residential | Very High (p < 0.001) |
| 4 | **Inventory Availability** | +£3,002 per 1% improvement | Very High (p < 0.001) |
| 5 | **Marketing Spend** | +£1.20 per £1 invested | Very High (p < 0.001) |
| 6 | **Region** – South & West | +£18K–19K vs East | High (p < 0.01) |
| 7 | **Customer Rating** | +£13,627 per 1-point gain | High (p < 0.01) |
| 8 | **Store Type** – High Street | +£18,093 vs Residential | High (p < 0.01) |

**Footfall is the single most important predictor of monthly sales**, and it is influenced by both store location choices and marketing effectiveness.

---

## 2. Which Variables Should Leadership Focus On?

### Priority 1: Drive Footfall
- Footfall explains the majority of within-store sales variation
- Every 1,000 additional visitors per month = approximately **£34,000 in additional revenue**
- Actions: improve in-store events, digital marketing campaigns targeting local audiences, loyalty programmes, and strategic store placement in high-traffic areas

### Priority 2: Inventory Management
- Each 1% improvement in inventory availability = **£3,002 in additional monthly sales**
- For a store averaging 85% availability, improving to 95% implies approximately **£30,000 in additional monthly revenue**
- Actions: invest in demand forecasting, strengthen supplier relationships, reduce stockout frequency

### Priority 3: Customer Experience
- A 1-point increase in customer rating = **£13,627 in additional monthly sales**
- Actions: staff training, faster checkout, better signage and layout, complaint resolution processes

### Priority 4: Marketing Spend
- Each £1 of marketing generates approximately **£1.20 in incremental sales** after controlling for all other factors
- Marketing is most effective when combined with footfall-driving activities (not just brand awareness)

### Priority 5: Location and Format Strategy
- Airport and Mall formats earn **£30K–£42K more per month** than Residential stores of equivalent size and footfall
- South and West regions earn approximately **£18K–£19K more per month** than East-region stores
- New store location decisions should weight these structural advantages heavily

---

## 3. Which Variables Should NOT Be Over-Interpreted?

### Average Discount Percentage
- **Not statistically significant** in the multiple regression (p = 0.211)
- Discounting does **not reliably increase monthly sales** once footfall and other factors are controlled for
- Leadership should not assume that running deeper promotions will systematically lift revenue — evidence is weak
- Discounting may harm profit margins without delivering proportional top-line growth

### Region — North
- The North region shows a positive coefficient (+£6,185) vs East, but this is **not statistically significant** (p = 0.38)
- Do not conclude that North region stores outperform East region stores based on this data

### Competitor Distance
- Competitor proximity was not statistically significant and was excluded from the final model
- The simple measure of distance to the nearest competitor does not adequately capture local competitive pressure in this dataset

---

## 4. Recommended Business Actions

### Short-Term (0–6 months)
1. **Audit inventory availability** across all stores — target 90%+ in-store availability. Focus on high-footfall stores where stockouts cause the greatest sales loss
2. **Review customer rating drivers** — conduct mystery shopping and exit surveys at stores rating below 3.5 to identify specific issues
3. **Redirect marketing spend** to stores with lower-than-expected footfall relative to their marketing investment (use the model's residuals to identify underperforming stores)

### Medium-Term (6–18 months)
4. **Evaluate Residential store upgrades** — consider whether any Residential-format stores could be repositioned to High Street or Mall formats (£18K–£42K monthly uplift per store)
5. **Expand in South and West regions** — prioritise new store openings or acquisitions in South and West, which earn a structural premium over East-region stores
6. **Investigate Airport store model** — Airport stores earn the highest premium; explore whether additional Airport locations are available

### Long-Term
7. **Build a real-time footfall and sales dashboard** — the regression model provides coefficients that can be used to set monthly sales targets based on predicted footfall
8. **Conduct controlled experiments (A/B tests)** — to confirm causal impact of marketing spend and customer rating improvements before committing large budgets

---

## 5. Risks and Limitations Leadership Should Keep in Mind

| Risk | Description |
|---|---|
| **Correlation ≠ Causation** | All findings reflect associations, not proven causes. Increasing marketing spend may not always yield £1.20 per £1 if the relationship is driven by other unmeasured factors |
| **Panel data limitations** | The same 80 stores were observed over 4 months — observations are not fully independent. A fixed-effects model would be more rigorous for monthly tracking |
| **Model accounts for 83%, not 100%** | About 17% of sales variation is unexplained — local events, product mix, competitor promotions, and management quality all play a role |
| **Outlier sensitivity** | One store (STR-1007) had marketing spend of £172K — nearly 3× the average — which may distort the marketing coefficient |
| **Data period is short** | Four months of data (Jan–Apr 2025) may not capture seasonal patterns (e.g., holiday trading in Q4) |

---

## 6. Why Regression Shows Association, Not Causation

Regression tells us that, **across our observed stores and time periods**, higher footfall tends to occur alongside higher sales. But it does not prove that **driving footfall causes higher sales** in every scenario.

For example:
- A flagship Airport store may have high footfall because it is in a busy terminal, but that footfall is not something management can control directly
- Marketing spend may be higher in months when management already expects strong sales (reverse causality)
- Customer rating improvements may reflect store improvements that also led to better product selection — the rating alone may not be what drives sales

**Leadership should use this model as a diagnostic and prioritisation tool**, not as a guarantee that any single lever will deliver the predicted uplift. Controlled experiments (e.g., testing higher marketing spend in select stores while holding others constant) are needed to establish causality before committing to large strategic investments.

---

## Conclusion
The data strongly supports that **footfall, inventory availability, customer satisfaction, marketing spend, and store format** are the most reliable predictors of monthly sales. Leadership should focus first on driving footfall and ensuring product availability — these are the highest-leverage, highest-confidence levers available. Expansion in South and West regions and into Airport/Mall formats offers strong structural advantages worth factoring into medium-term growth strategy.

*Analysis based on Multiple Regression Model — R² = 0.8321 — 320 observations, 80 stores, Jan–Apr 2025.*
