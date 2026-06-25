
# Final Business Recommendation

## Which factors appear most strongly associated with monthly sales?
Based on the final multiple regression model, four factors show a strong and
statistically significant association with monthly sales:
1. **Footfall** — the strongest driver (coefficient = 33.78, p < 0.001)
2. **Inventory availability** — a large positive effect (coefficient = 2991.99, p < 0.001)
3. **Marketing spend** — positive and significant (coefficient = 1.19, p < 0.001)
4. **Customer rating** — positive and significant (coefficient = 11255.19, p = 0.025)

## Which variables should leadership focus on?
- **Footfall and inventory availability** should be top priorities, since they have the
  largest, most statistically significant effects on sales. Ensuring stores are
  well-stocked and driving foot traffic (location, store hours, local promotions) appears
  to matter more than any other measured factor.
- **Customer rating** also matters — improving in-store experience and service quality is
  linked to higher sales.
- **Marketing spend** has a positive effect, but its impact per unit is smaller than
  footfall or inventory, suggesting marketing should be used to support footfall growth
  rather than as a stand-alone lever.

## Which variables should not be over-interpreted?
- **Region (Region_north dummy)** was not statistically significant (p = 0.667).
  Leadership should not conclude that one region inherently performs better or worse than
  another based on this model — any observed regional difference in raw sales is likely
  explained by the other variables (footfall, inventory, etc.), not geography itself.
- The **intercept** (p = 0.091) is also not statistically significant and should not be
  treated as a meaningful "baseline" sales figure.

## What business action would you recommend?
1. Prioritize **inventory management** — reduce stockouts and ensure high product
   availability, since this has one of the largest measurable effects on sales.
2. Invest in initiatives that **increase footfall** — e.g., store placement, local
   marketing, hours of operation, partnerships — since footfall is the single strongest
   predictor of sales.
3. Continue **marketing spend**, but treat it as a supporting investment rather than the
   primary growth lever.
4. Invest in **customer experience/service quality** to improve customer ratings, which
   has a measurable positive link to sales.
5. **Do not reallocate resources based on region alone** — region differences are not
   statistically supported once other factors are controlled for.

## What risks or limitations should leadership keep in mind?
- The model explains about 81% of the variation in sales, meaning roughly 19% is driven
  by factors not captured here (e.g., discounting strategy, staffing levels, local
  competition, seasonality).
- Region_north's lack of significance does not prove region has zero effect — it may
  simply not be detectable with this data/structure (e.g., only one region dummy, limited
  regional variation, or interaction effects not modeled).
- The data is observational, not from a controlled experiment — so we cannot rule out
  confounding variables affecting both the independent variables and sales simultaneously.

## Why does regression show association but not automatically prove causation?
Regression analysis identifies statistical relationships between variables based on
historical, observational data — it shows that certain variables move together with
sales, but it does not control for every possible confounding factor, nor does it test
cause-and-effect through experimentation. For example, stores with higher footfall may
also happen to be in better locations, have better managers, or run more frequent local
promotions — any of these unmeasured factors could be the "true" cause of higher sales,
with footfall simply moving alongside it. To establish causation, a controlled experiment
(e.g., randomly increasing marketing spend in some stores and not others, then comparing
outcomes) would be needed. Until then, these results should be treated as strong
evidence of association, useful for guiding business priorities, but not definitive proof
that changing one variable will directly cause a specific change in sales.
