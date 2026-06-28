# Part 3: Regression-Based Business Insights

## Business Problem Summary

The leadership team of a retail chain wants to understand what drives monthly sales across their stores. They are considering several business actions - increasing marketing budgets, improving inventory management, changing discount strategy, reallocating staff, and prioritizing certain store types or regions. The goal is to use regression analysis to figure out which factors actually matter and provide a data-backed recommendation.

---

## Dataset Description

- **Source:** business_regression_data.xlsx
- **Records:** 320 rows (80 stores x 4 months, January to April 2025)
- **Regions:** East (104 rows), West (92), North (64), South (60)
- **Store Types:** High Street (116), Residential (100), Mall (76), Airport (28)

### Variables

| Variable | Type | Role | Description |
|----------|------|------|-------------|
| store_id | Categorical (ID) | Identifier | Unique store code (not used in regression) |
| month | Date | Identifier | Reporting month (not used in regression) |
| region | Categorical | Independent | East, North, South, West |
| store_type | Categorical | Independent | Mall, High Street, Residential, Airport |
| marketing_spend | Numerical | Independent | Monthly marketing budget per store |
| footfall | Numerical | Independent | Monthly visitor count |
| avg_discount_pct | Numerical | Independent | Average discount percentage |
| staff_count | Numerical | Independent | Number of store staff |
| inventory_availability_pct | Numerical | Independent | Product availability percentage |
| competitor_distance_km | Numerical | Independent | Distance to nearest competitor |
| holiday_flag | Binary (0/1) | Independent | Whether the month had a holiday effect |
| customer_rating | Numerical | Independent | Average customer rating (scale of 1-5) |
| **monthly_sales** | **Numerical** | **Dependent** | **Target variable for regression** |
| monthly_profit | Numerical | Not used | Secondary metric, excluded from regression |

### Data Cleaning
- **competitor_distance_km:** 6 missing values, filled with median (3.29 km)
- **customer_rating:** 8 missing values, filled with median (3.90)
- **store_id, month:** Used for identification only, not included in regression
- **monthly_profit:** Excluded - it is an outcome variable, not a predictor

---

## Dependent and Independent Variables

- **Dependent variable:** monthly_sales
- **Numerical independent variables:** marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating
- **Categorical independent variables (converted to dummies):** region, store_type

---

## Regression Approach

I ran the analysis in three stages:

### Stage 1: Simple Regressions
I tested individual predictors one at a time against monthly_sales to see which variables have standalone predictive power:
- **Model 1:** monthly_sales ~ marketing_spend (R-squared = 0.167)
- **Model 2:** monthly_sales ~ footfall (R-squared = 0.736)
- **Model 3:** monthly_sales ~ inventory_availability_pct (R-squared = 0.013)

Footfall stood out as the strongest individual predictor by far.

### Stage 2: Multiple Regression
I combined all available predictors into one model, including dummy variables for region and store type. The full model achieved an R-squared of 0.857 (adjusted: 0.850), meaning it explains about 86% of sales variation.

### Stage 3: Residual Analysis
I calculated residuals (actual - predicted) to identify stores that are systematically outperforming or underperforming their model predictions, and looked for patterns.

---

## Dummy Variable Approach

Two categorical variables were converted to dummy (0/1) variables:

| Original Variable | Categories | Reference Category | Dummies Created |
|-------------------|------------|-------------------|-----------------|
| region | East, North, South, West | East (most observations) | region_North, region_South, region_West |
| store_type | Airport, High Street, Mall, Residential | Residential (baseline format) | type_Airport, type_High Street, type_Mall |

Each dummy coefficient tells us how different that category is from the reference category. For example, the coefficient for type_Airport (44,695) means Airport stores sell about 44,695 more per month than comparable Residential stores.

One category is always dropped to avoid the "dummy variable trap" (perfect multicollinearity).

---

## Model Comparison Summary

| Model | R-squared | Adj R-squared | Significant Variables |
|-------|-----------|---------------|-----------------------|
| Simple: marketing_spend | 0.1672 | 0.1646 | marketing_spend |
| Simple: footfall | 0.7363 | 0.7355 | footfall |
| Simple: inventory_availability_pct | 0.0131 | 0.0100 | inventory_availability_pct (barely) |
| **Multiple: Full Model** | **0.8570** | **0.8504** | **12 out of 14 variables significant** |

The full multiple regression model is clearly the best. It captures the combined effects of all factors and explains 86% of sales variation.

---

## Final Model Selected

**Multiple Regression (Full Model)** with the equation:

monthly_sales = 41,624 + 1.21 x marketing_spend + 27.34 x footfall - 41,243 x avg_discount_pct + 3,508 x staff_count + 3,062 x inventory_availability_pct - 3,438 x competitor_distance_km + 15,157 x holiday_flag + 12,509 x customer_rating + 9,949 x region_North + 21,090 x region_South + 25,291 x region_West + 44,695 x type_Airport + 20,219 x type_High Street + 32,833 x type_Mall

### Why this model?
1. Highest R-squared (0.857) and adjusted R-squared (0.850)
2. 12 of 14 predictors are statistically significant
3. Captures the combined effect of operational, locational, and market factors
4. Provides actionable insights leadership can use for decision-making

---

## Business Recommendation

### Top priorities for leadership:

1. **Drive footfall** - This is the single biggest lever for sales. Invest in strategies that bring more visitors.
2. **Keep shelves stocked** - Inventory availability has a strong effect. A 10-percentage-point improvement is worth over 30,000 rupees per store per month.
3. **Invest in store experience** - Customer ratings matter. Better service leads to better ratings, which is associated with higher sales.
4. **Prioritize Airport and Mall locations** for new store openings.

### What to be cautious about:
- The discount variable is not significant - do not assume discounts automatically drive sales.
- North region is not statistically different from East - do not over-read regional differences.
- Regression shows association, not causation. The findings should guide further investigation and testing, not be taken as guaranteed outcomes.

For detailed analysis, see the model_comparison.md, residual_analysis.md, model_equations.md, and final_recommendation.md files.

---

## Assumptions and Limitations

1. **Linear relationships assumed** - Regression assumes a straight-line relationship between each predictor and sales. Real relationships may be curved.
2. **No causation claim** - These are associations, not causal effects. A controlled experiment would be needed to prove causation.
3. **Data is from a 4-month window** - The patterns might change over longer timeframes or in different economic conditions.
4. **Some multicollinearity present** - Some predictors may be correlated with each other, which makes individual coefficient estimates less precise.
5. **Missing values imputed with medians** - 6 missing values in competitor_distance_km and 8 in customer_rating were filled with medians, which is reasonable but adds a small amount of imprecision.
6. **Residual analysis** suggests the model is slightly less accurate for some stores in the West region.

---

## Screenshots Included

| Screenshot | Description |
|-----------|-------------|
| screenshots/simple_regression_output.png | Scatter plots with regression lines for marketing_spend and footfall models |
| screenshots/multiple_regression_output.png | Coefficient table for the full multiple regression model |
| screenshots/residuals_preview.png | Residual vs predicted scatter plot and residual distribution histogram |
| screenshots/model_comparison_preview.png | Side-by-side comparison table of all four models |
