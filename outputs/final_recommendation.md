# Final Recommendation

## To: Leadership Team
## From: Business Analyst
## Subject: What Is Driving Monthly Sales - Key Findings and Recommended Actions

---

## Executive Summary

After analyzing 320 store-month records across 80 stores and 4 regions, I built a multiple regression model that explains about 86% of the variation in monthly sales. The model identifies several clear drivers that leadership can act on, and a few variables that should not be over-interpreted.

---

## Which Factors Are Most Strongly Associated with Monthly Sales?

Based on the regression analysis, here are the top drivers ranked by their practical importance:

1. **Footfall (coefficient: 27.34, p < 0.001)** - This is the single biggest lever. Each additional visitor translates to roughly 27 rupees in sales. A store that gets 1,000 more visitors per month can expect about 27,000 rupees more in sales, all else being equal.

2. **Store Type** - Where the store is located makes a huge difference:
   - Airport stores sell about 44,695 rupees more than a comparable Residential store
   - Mall stores sell about 32,833 rupees more than Residential
   - High Street stores sell about 20,219 rupees more than Residential

3. **Region** - Geography matters:
   - West region stores outperform East by about 25,291 rupees
   - South region stores outperform East by about 21,090 rupees

4. **Inventory Availability (coefficient: 3,062, p < 0.001)** - Each percentage point improvement in shelf stock adds about 3,062 rupees. Going from 85% to 95% availability is worth roughly 30,620 rupees per month per store.

5. **Customer Rating (coefficient: 12,509, p = 0.005)** - A 1-point improvement in customer rating is linked to 12,509 rupees more in sales.

6. **Marketing Spend (coefficient: 1.21, p < 0.001)** - Every rupee spent on marketing generates about 1.21 rupees in sales. This is positive but modest. An extra 10,000 rupees in marketing is associated with only about 12,100 rupees in additional sales.

7. **Staff Count (coefficient: 3,508, p = 0.003)** - Each additional staff member is associated with about 3,508 rupees more in monthly sales.

8. **Competitor Distance (coefficient: -3,438, p < 0.001)** - Stores closer to competitors tend to have lower sales. Each km closer to a competitor costs about 3,438 rupees.

9. **Holiday Flag (coefficient: 15,157, p = 0.014)** - Holiday months see a bump of about 15,157 rupees.

---

## What Should Leadership Focus On?

### High-Priority Actions

1. **Drive footfall** - This is the number one lever. Invest in strategies that bring more people through the door - better signage, local advertising, partnerships with nearby businesses, events, etc. The return on footfall is the highest of any variable in the model.

2. **Keep shelves stocked** - Inventory availability has a surprisingly strong effect once you control for other factors. A 10-percentage-point improvement is worth more than 30,000 rupees per month per store. This is often an operational fix that does not require huge capital investment.

3. **Invest in store experience** - Customer rating has a meaningful effect (12,509 per rating point). Train staff, improve store layout, reduce wait times, maintain cleanliness. These things show up in customer ratings and they show up in sales.

4. **Prioritize high-traffic locations for new stores** - Airport and Mall locations have significant sales premiums over Residential locations. When opening new stores or renewing leases, prioritize these formats.

### Medium-Priority Actions

5. **Optimize staffing levels** - Each additional staff member contributes about 3,508 rupees per month. Run an analysis on whether understaffed stores are leaving money on the table.

6. **Monitor competitive landscape** - Stores near competitors sell less. When competitors open nearby, be proactive with marketing and service to defend your position.

### Lower-Priority for Now

7. **Marketing spend** - The return on marketing (1.21 per rupee) is positive but the ROI is thin. Before increasing marketing spend, make sure footfall and operational factors are optimized first.

---

## What Should NOT Be Over-Interpreted?

1. **avg_discount_pct (p = 0.224)** - The discount variable was not statistically significant. This does not mean discounts do not matter at all. It means that in this dataset, with these other variables controlled for, we could not find a reliable, consistent effect. Discounting likely has a more complex relationship with sales that a simple linear model cannot capture.

2. **region_North (p = 0.131)** - North region stores were not significantly different from East. We should not assume all regions perform equally though - it just means the difference between North and East was not large enough to be statistically reliable with this sample.

3. **The intercept (p = 0.359)** - The intercept is not significant either, but that is fine. It would represent a hypothetical store with zero footfall, zero marketing, and zero everything else, which does not exist in practice.

---

## Recommended Business Action

Based on the analysis, I recommend a **three-pronged approach**:

1. **Footfall first** - Run a footfall improvement program across underperforming stores. Even a 10% increase in footfall across the chain could drive significant revenue. Focus on local marketing, community events, and visibility improvements.

2. **Operational excellence** - Launch an inventory availability initiative targeting stores below 90% availability. Pair this with staff training to improve customer ratings. These are relatively low-cost, high-impact improvements.

3. **Strategic store placement** - When making decisions about new store openings, expansions, or closures, use the store type premiums as a guide. Airport and Mall formats consistently outperform Residential locations. If a Residential store is underperforming, assess whether the location itself is the constraint.

---

## Risks and Limitations Leadership Should Keep in Mind

1. **Correlation is not causation.** This is important. The regression shows that footfall is strongly associated with sales. But we did not run a controlled experiment. It is possible that some third factor (like store location quality) is driving both footfall and sales. We should be cautious about assuming that artificially increasing any single variable will produce exactly the effect the model suggests.

2. **The model explains 86%, not 100%.** There is still about 14% of sales variation that we cannot explain with these variables. Some of that is probably random noise, and some of it is factors we do not have in the data (store manager quality, local economic conditions, brand perception in different areas, etc.).

3. **This is a snapshot, not a crystal ball.** The data covers January-April 2025 for 80 stores. Consumer behavior can shift, competitors can change strategy, and macroeconomic conditions can shift. The model should be re-run periodically to check if the relationships still hold.

4. **The coefficients represent average effects.** The model says each visitor is worth 27 rupees on average. But this average hides variation. In an Airport store during a holiday, each visitor might be worth 50 rupees. In a quiet Residential store on a weekday, it might be 15 rupees.

5. **Multicollinearity is present.** Some variables (like footfall and marketing spend) are at least somewhat correlated with each other. This does not invalidate the model, but it means the individual coefficient values should be interpreted with some caution. The overall model is trustworthy; the precise split of "credit" among correlated variables is less certain.

---

## Why Does Regression Show Association But Not Prove Causation?

Regression tells us that two things tend to move together. Stores with higher footfall tend to have higher sales. But it does not tell us why.

Consider footfall. Do more visitors cause more sales? Almost certainly yes, to some degree. But it could also be that stores in better locations naturally get more visitors AND more sales, and the "cause" is really the location, not the footfall itself.

To truly prove causation, we would need a randomized experiment - say, randomly assigning different marketing budgets or staffing levels to stores and measuring the effect. Regression is a powerful tool for identifying where to look and what to test, but it should not be treated as proof that changing one variable will definitely change the outcome by the exact amount the model says.

That said, the associations we found are strong, consistent, and make business sense. They give a solid foundation for making informed decisions - just with the humility to know that real-world impact might differ from the model's estimate.
