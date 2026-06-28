# Model Comparison

## Overview

I ran three simple regression models and one multiple regression model, all with monthly_sales as the dependent variable. The idea was to first check which individual variables seem to matter on their own, and then combine everything into a fuller model to see the bigger picture.

---

## Models at a Glance

| Model | Variables Used | R-squared | Adj R-squared | Significant Variables | Business Usefulness | Key Limitations |
|-------|---------------|-----------|---------------|----------------------|--------------------|-----------------| 
| Simple Model 1 | marketing_spend | 0.1672 | 0.1646 | marketing_spend (p < 0.001) | Limited - explains only ~17% of sales variation. Marketing spend alone is not enough to predict sales. | Ignores footfall, store type, location, and other important factors. |
| Simple Model 2 | footfall | 0.7363 | 0.7355 | footfall (p < 0.001) | Strong - footfall alone explains ~74% of sales. This is clearly the single strongest driver. | Still leaves ~26% unexplained. Does not account for store type, region, or operational factors. |
| Simple Model 3 | inventory_availability_pct | 0.0131 | 0.0100 | inventory_availability_pct (p = 0.041) | Very limited - explains only ~1.3% of sales variation. Barely useful on its own. | Almost no practical predictive value as a standalone model. |
| Multiple Regression (Full Model) | marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating, region dummies, store type dummies | 0.8570 | 0.8504 | marketing_spend, footfall, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating, region_South, region_West, type_Airport, type_High Street, type_Mall | Very high - explains ~85% of sales variation. Gives a well-rounded picture of what drives sales. | avg_discount_pct and region_North are not statistically significant. Condition number is high, suggesting possible multicollinearity. |

---

## Detailed Comparison

### Simple Model 1: monthly_sales ~ marketing_spend
- **R-squared:** 0.1672 - Marketing spend explains about 17% of sales variation.
- **Coefficient:** 2.13 - For every extra rupee spent on marketing, monthly sales go up by roughly 2.13 rupees.
- **P-value:** < 0.001 - Statistically significant.
- **Verdict:** It helps, but on its own it is too weak. Marketing is just one piece of the puzzle.

### Simple Model 2: monthly_sales ~ footfall
- **R-squared:** 0.7363 - Footfall on its own explains about 74% of sales variation. That is really strong.
- **Coefficient:** 35.68 - Each additional visitor is associated with roughly 35.68 rupees more in monthly sales.
- **P-value:** < 0.001 - Very significant.
- **Verdict:** Footfall is by far the strongest single predictor. This makes intuitive sense - more people coming in means more purchases.

### Simple Model 3: monthly_sales ~ inventory_availability_pct
- **R-squared:** 0.0131 - Basically explains almost nothing on its own.
- **Coefficient:** 2,217.83 - Each percentage point increase in inventory availability corresponds to about 2,218 rupees more in sales.
- **P-value:** 0.041 - Just barely significant.
- **Verdict:** On its own, pretty useless for prediction. But interestingly, this variable becomes much more significant in the multiple regression model (p < 0.001), suggesting that once you control for other factors, inventory availability actually plays a meaningful role.

### Multiple Regression: Full Model
- **R-squared:** 0.8570 - The combined model explains about 85.7% of sales variation. Big jump from any single variable.
- **Adj R-squared:** 0.8504 - Adjusting for the number of predictors, it is still solid at 85%.
- **F-statistic:** 130.55, p-value = 1.25e-119 - The overall model is highly significant.
- **Significant variables (p < 0.05):** marketing_spend, footfall, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating, region_South, region_West, type_Airport, type_High Street, type_Mall
- **Not significant:** avg_discount_pct (p = 0.224), region_North (p = 0.131)
- **Verdict:** This is the best model. It captures the combined effect of all major drivers.

---

## Which Model Should Leadership Use?

The **Multiple Regression (Full Model)** is the recommended model. Here is why:

1. It has the highest R-squared (0.857 vs 0.736 for the best simple model).
2. Most of its variables are statistically significant.
3. It captures the reality that sales are driven by many factors together, not just one thing.
4. It accounts for store type and regional differences, which the simple models completely ignore.

The simple regression with footfall (Model 2) is a decent fallback if leadership wants a quick, easy-to-explain number. But for actual decision-making, the full model gives a much more complete and accurate picture.

---

## Limitations

1. **Not causal proof** - Regression shows association, not causation. Just because footfall correlates with sales does not mean artificially increasing footfall will always increase sales proportionally.
2. **avg_discount_pct is not significant** - The discount variable does not show a significant effect in this model, which may be because discounts have complex, nonlinear effects on sales.
3. **region_North is not significant** - North region stores do not seem statistically different from East (the reference category) in this dataset.
4. **Possible multicollinearity** - The condition number is high (1.23e+06), which means some predictors may be correlated with each other. This does not invalidate the model, but it means we should be cautious about interpreting individual coefficients too literally.
5. **Time-based patterns not captured** - This model treats each month-store row independently. It does not account for trends over time or seasonality beyond the holiday_flag variable.
