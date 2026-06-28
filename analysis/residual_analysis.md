# Residual Analysis

## What Are Residuals?

A residual is simply the difference between what the model predicted a store's sales would be and what the store actually sold. If the residual is positive, the store did better than the model expected. If negative, it did worse.

**Residual = Actual Sales - Predicted Sales**

I used the multiple regression (full model) for this analysis since it is the best-performing model (R-squared = 0.857).

---

## Top 5 Positive Residuals (Stores That Outperformed the Prediction)

| Store ID | Month | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|----------|-------|--------|------------|-------------|-----------------|----------|
| STR-1058 | Feb 2025 | East | High Street | 870,937 | 759,920 | +111,017 |
| STR-1028 | Apr 2025 | East | Mall | 713,611 | 610,532 | +103,079 |
| STR-1073 | Mar 2025 | East | Residential | 813,317 | 721,416 | +91,901 |
| STR-1051 | Feb 2025 | East | Airport | 787,716 | 701,381 | +86,334 |
| STR-1026 | Apr 2025 | East | Mall | 625,514 | 540,235 | +85,279 |

### What This Tells Us

All five of these stores are in the **East** region. That is interesting because East is our reference category, so the model is not adding any bonus for being in the East. Yet these stores are beating their predictions by 85,000 to 111,000 rupees.

Possible explanations:
- These stores may have local competitive advantages that our data does not capture (e.g., being in a particularly busy part of town, or having a great store manager).
- There could be local events, promotions, or seasonal factors specific to these locations.
- The model might be slightly under-weighting what makes East region stores succeed.

From a business perspective, it would be worth investigating what these stores are doing differently. If there are operational best practices at STR-1058 or STR-1028, those could potentially be replicated elsewhere.

---

## Top 5 Negative Residuals (Stores That Underperformed the Prediction)

| Store ID | Month | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|----------|-------|--------|------------|-------------|-----------------|----------|
| STR-1023 | Feb 2025 | South | Mall | 627,172 | 764,039 | -136,867 |
| STR-1017 | Mar 2025 | West | High Street | 685,379 | 805,280 | -119,901 |
| STR-1012 | Jan 2025 | West | Residential | 595,468 | 709,914 | -114,446 |
| STR-1007 | Feb 2025 | West | Mall | 800,452 | 912,345 | -111,893 |
| STR-1060 | Jan 2025 | West | Mall | 721,079 | 808,022 | -86,942 |

### What This Tells Us

Four out of five underperforming stores are in the **West** region, and one is in the **South**. The model is predicting higher sales for these stores than they are actually achieving. The gap is pretty large - STR-1023 in the South missed its predicted value by nearly 137,000 rupees.

Possible explanations:
- There may be local issues in these specific locations - construction nearby, parking problems, new competitors not captured in the dataset.
- These stores may have operational problems (poor staff performance, stock management issues, etc.) that the model cannot see.
- The West region might have more variation in store performance than the model can handle with a single dummy variable.

From a business perspective, these stores deserve attention. If the model says they should be selling more (based on their footfall, marketing spend, and other measurable factors), something is going wrong on the ground.

---

## Overall Residual Distribution

Looking at the residual plots:
- The residuals are roughly centered around zero, which is good. It means the model is not systematically biased.
- The spread looks fairly even across different predicted values (no obvious fanning pattern), suggesting the model's accuracy is consistent across low-sales and high-sales stores.
- The histogram of residuals looks roughly normal, no extreme skew.

---

## Under-predicting vs Over-predicting Patterns

When I look at the residual patterns more carefully:

- **Under-prediction (positive residuals)** tends to happen more with **East region** stores. The model may not fully capture what makes certain East region stores perform especially well.
- **Over-prediction (negative residuals)** tends to happen more with **West and South region** stores, especially Malls. Something about these stores is dragging down performance below what the numbers would suggest.

This is useful feedback for leadership. It suggests that:
1. There might be region-specific factors (local economy, competition, demographics) that our current variables do not capture.
2. The performance gap for underperforming stores is actionable - these are stores where the "ingredients for success" (footfall, marketing, etc.) are there, but results are not following.

---

## Key Takeaway

The residual analysis confirms that the model is doing a solid job overall (most residuals are relatively small compared to the ~680K average sales). But it also highlights that there are pockets of the business - particularly in the West region - where actual performance is not matching what the fundamentals would suggest. These are opportunities for operational improvement.
