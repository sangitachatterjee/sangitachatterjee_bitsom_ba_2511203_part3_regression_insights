# Model Equations

## Simple Regression Equations

### Model 1: Monthly Sales vs Marketing Spend

**monthly_sales = 560,777.35 + 2.1296 x marketing_spend**

- **Intercept (560,777.35):** When marketing spend is zero, the model estimates a baseline sales level of about 5.61 lakhs. This is a theoretical baseline - in practice, no store would have zero marketing spend.
- **Coefficient (2.1296):** For every 1 rupee increase in marketing spend, monthly sales increase by about 2.13 rupees. Or to put it differently, an additional 10,000 rupees in marketing is associated with roughly 21,296 rupees more in sales.
- **R-squared:** 0.1672 - Marketing spend alone explains about 17% of sales variation. Not great, but marketing clearly has a positive effect.
- **P-value:** < 0.001 - Highly significant.

### Model 2: Monthly Sales vs Footfall

**monthly_sales = 446,410.58 + 35.6780 x footfall**

- **Intercept (446,410.58):** Baseline sales when footfall is zero (theoretical).
- **Coefficient (35.6780):** Each additional visitor is associated with about 35.68 rupees more in monthly sales. So if a store gets an additional 1,000 visitors in a month, that translates to roughly 35,678 rupees more in sales.
- **R-squared:** 0.7363 - Footfall alone explains about 74% of sales variation. This is really strong.
- **P-value:** < 0.001 - Very significant.

### Model 3: Monthly Sales vs Inventory Availability

**monthly_sales = 484,814.26 + 2,217.83 x inventory_availability_pct**

- **Intercept (484,814.26):** Baseline sales when inventory availability is zero (theoretical).
- **Coefficient (2,217.83):** Each 1 percentage point improvement in inventory availability is linked to about 2,218 rupees more in sales. On its own, this is a weak model.
- **R-squared:** 0.0131 - Inventory availability alone explains only 1.3% of variation.
- **P-value:** 0.041 - Just barely significant at the 5% level.

---

## Multiple Regression Equation

**monthly_sales = 41,624.05 + 1.2099 x marketing_spend + 27.3362 x footfall - 41,243.15 x avg_discount_pct + 3,508.40 x staff_count + 3,062.21 x inventory_availability_pct - 3,438.11 x competitor_distance_km + 15,157.29 x holiday_flag + 12,509.46 x customer_rating + 9,948.71 x region_North + 21,089.57 x region_South + 25,291.42 x region_West + 44,695.09 x type_Airport + 20,219.26 x type_High Street + 32,832.85 x type_Mall**

### Coefficient Explanations

| Variable | Coefficient | P-value | Significant? | Business Meaning |
|----------|------------|---------|--------------|------------------|
| Intercept (const) | 41,624.05 | 0.359 | No | Theoretical baseline when all predictors are zero. Not meaningful on its own. |
| marketing_spend | 1.2099 | < 0.001 | Yes | Each extra rupee on marketing adds about 1.21 rupees to sales (holding everything else constant). Notice this drops from 2.13 in the simple model - that is because the simple model was giving marketing "credit" for effects that actually belong to other variables like footfall. |
| footfall | 27.3362 | < 0.001 | Yes | Each additional visitor adds about 27.34 rupees in sales. Still the strongest predictor, though lower than the simple model (35.68) because other factors now absorb some of the effect. |
| avg_discount_pct | -41,243.15 | 0.224 | No | Not statistically significant. The negative sign suggests deeper discounts might hurt sales (possibly signaling lower-quality or clearance products), but we cannot be confident in this. |
| staff_count | 3,508.40 | 0.003 | Yes | Each additional staff member is associated with about 3,508 rupees more in sales per month. Probably reflects better customer service, shorter wait times, and more floor coverage. |
| inventory_availability_pct | 3,062.21 | < 0.001 | Yes | Each percentage point increase in inventory availability adds about 3,062 rupees. This is much more significant in the full model than it was alone, showing that once you account for other factors, keeping shelves stocked genuinely matters. |
| competitor_distance_km | -3,438.11 | < 0.001 | Yes | For every 1 km closer a competitor is, sales decrease by about 3,438 rupees. Being far from competitors helps, which makes sense - less direct competition for the same customers. |
| holiday_flag | 15,157.29 | 0.014 | Yes | Holiday months see about 15,157 rupees more in sales. This is a meaningful bump, roughly 2.2% above average sales. |
| customer_rating | 12,509.46 | 0.005 | Yes | Each 1-point increase in customer rating adds about 12,509 rupees in sales. Happy customers spend more, or higher-rated stores attract more spending. |
| region_North | 9,948.71 | 0.131 | No | North region stores sell about 9,949 rupees more than East (the reference region), but this difference is not statistically significant. |
| region_South | 21,089.57 | 0.002 | Yes | South region stores sell about 21,090 rupees more than comparable East stores. |
| region_West | 25,291.42 | < 0.001 | Yes | West region stores sell about 25,291 rupees more than comparable East stores. This is the biggest regional effect. |
| type_Airport | 44,695.09 | < 0.001 | Yes | Airport stores sell about 44,695 rupees more than Residential stores (the reference). This is the biggest store type premium, which makes sense given captive audience and premium pricing. |
| type_High Street | 20,219.26 | < 0.001 | Yes | High Street stores sell about 20,219 rupees more than Residential stores. |
| type_Mall | 32,832.85 | < 0.001 | Yes | Mall stores sell about 32,833 rupees more than Residential stores. |

### Model Summary Statistics
- **R-squared:** 0.8570
- **Adjusted R-squared:** 0.8504
- **F-statistic:** 130.55 (p = 1.25e-119)
- **Observations:** 320

---

## Dummy Variable Explanation

### What are dummy variables?

Categorical variables like "region" and "store_type" cannot be plugged directly into a regression equation as text. We need to convert them into numerical 0/1 columns. Each category gets its own column, where 1 means "yes, this row belongs to this category" and 0 means "no, it does not."

### Region Dummy Variables
- **Reference category: East** - I chose East because it has the most observations (104 out of 320 rows). The coefficients for North, South, and West tell us how different those regions are compared to East.
- **region_North:** 1 if the store is in North, 0 otherwise
- **region_South:** 1 if the store is in South, 0 otherwise
- **region_West:** 1 if the store is in West, 0 otherwise

If a store is in the East region, all three dummies are 0. That is how the model knows it is East.

### Store Type Dummy Variables
- **Reference category: Residential** - Residential was chosen as the baseline because it represents the most common, "standard" type of store location.
- **type_Airport:** 1 if Airport store, 0 otherwise
- **type_High Street:** 1 if High Street store, 0 otherwise
- **type_Mall:** 1 if Mall store, 0 otherwise

If a store is Residential, all three dummies are 0.

### Why drop one category?

If we included all categories (e.g., all four regions), the columns would be perfectly collinear - knowing three of them tells you the fourth. This is called the "dummy variable trap." It breaks the regression. So we always drop one category and treat it as the reference.

---

## Final Model Selected

**Multiple Regression (Full Model)**

### Reason for Selection

1. **Best fit:** R-squared of 0.857 means the model captures about 86% of the variation in monthly sales. The best simple model (footfall) could only get to 74%.
2. **Most variables are significant:** 12 out of 14 predictors are statistically significant at the 5% level.
3. **Business relevance:** It captures the reality that sales depend on many things - how many people walk in, how much you spend on marketing, what type of store it is, where it is located, how well stocked the shelves are, and more.
4. **Actionable insights:** The coefficients give leadership concrete numbers to work with. For example, adding one staff member is worth roughly 3,500 rupees in monthly sales.
