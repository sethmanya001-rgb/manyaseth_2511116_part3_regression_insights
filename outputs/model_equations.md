## Dummy Variable Explanation 

### Why This Variable Was Chosen
As a business analyst, one of leadership's key questions was whether **geography**
plays a role in store performance — should certain regions be prioritized for
investment, staffing, or marketing budget over others? To answer this with regression,
the categorical variable **region** needed to be converted into a numeric format the
model could process.

### Variable Created
**Region_north**
- 1 = Store is located in the North region
- 0 = Store is located in the South region

### Reference Category Selected: South
South was chosen as the reference (baseline) category. This means every interpretation
of the region effect in this model is read as: *"How does a North store compare to a
South store, all else being equal?"* This is a standard regression convention — one
category must always be excluded to avoid redundancy, and the excluded category becomes
the implicit benchmark against which all other categories are measured.

### Why Only One Dummy Variable Was Used
Region has only two categories in this dataset (North and South). Including a dummy for
*both* categories would have caused perfect multicollinearity — known as the **dummy
variable trap** — since knowing one column's value (e.g., Region_north = 0) automatically
tells you the value of the other (the store must be South). Excel's regression engine
cannot reliably estimate coefficients in this situation, so only one dummy was created.
The general business rule applied here: for a categorical variable with *n* categories,
create *(n − 1)* dummy variables.

### Business Interpretation of the Coefficient
The coefficient on Region_north was **-2786.97**. In plain business terms:

> "After accounting for differences in marketing spend, footfall, inventory
> availability, and customer satisfaction, stores in the North region generate, on
> average, ₹2,786.97 less in monthly sales than otherwise similar stores in the South
> region."

At first glance, this might suggest leadership should deprioritize the North region or
investigate what's holding those stores back. However, this is where statistical rigor
matters for sound decision-making.

### Why This Result Should Not Be Acted On (Statistical Caveat)
The p-value for Region_north was **0.667** — far above the standard 0.05 significance
threshold. In business terms, this means:

> "We cannot be confident this -2786.97 difference reflects a real, repeatable pattern.
> It is statistically indistinguishable from zero — it could simply be due to random
> variation in this particular sample of stores, not an actual regional effect."

**As a business analyst, this is an important finding to communicate carefully to
leadership.** It would be a mistake to recommend reallocating budget, staff, or
inventory away from North stores based on this number alone. Doing so could mean
penalizing a region for a difference that doesn't actually exist in reality — essentially
making a costly decision based on statistical noise rather than evidence.

### What This Tells Leadership
- Region, on its own, does **not** appear to be a meaningful driver of sales once
  operational factors (footfall, inventory, marketing, customer satisfaction) are
  accounted for.
- This is actually a **useful and reassuring insight** — it suggests that performance
  gaps between regions are likely explained by *operational execution* (e.g., how well a
  store manages inventory, drives footfall, or satisfies customers) rather than by
  uncontrollable geographic factors.
- **Recommended action:** Instead of focusing on "North vs. South" as a strategic lever,
  leadership should focus on the variables that *were* statistically significant —
  footfall, inventory availability, marketing spend, and customer rating — since these
  are the levers proven to move sales, and they are factors leadership can directly
  influence at any store, regardless of region.

### If Future Data Supports a Region-Based Strategy
If leadership still suspects regional effects exist, the recommendation would be to:
1. Collect more granular regional data (e.g., more than 2 region categories, or
   sub-regions/cities) to test for differences with more statistical power.
2. Test interaction effects (e.g., does marketing spend work differently in North vs.
   South?) rather than assuming a flat regional difference.
3. Avoid making region-based budget decisions until a statistically significant and
   consistent pattern is found across multiple analysis periods.
# Model Equations

## Simple Regression Equations

**Model 1: Marketing Spend**
monthly_sales = 560777.35 + 2.13 * marketing_spend

- Intercept (560777.35): Estimated baseline monthly sales when marketing_spend = 0.
- Coefficient (2.13): For every 1 unit increase in marketing_spend, monthly_sales is
  expected to increase by approximately 2.13 units, holding nothing else constant.

**Model 2: Footfall**
monthly_sales = 446410.58 + 35.68 * footfall

- Intercept (446410.58): Estimated baseline monthly sales when footfall = 0.
- Coefficient (35.68): For every additional customer visit (footfall), monthly_sales is
  expected to increase by approximately 35.68 units.

## Multiple Regression Equation (Final Model)

monthly_sales = 83893.92 + 1.19 * marketing_spend + 33.78 * footfall
                + 2991.99 * inventory_availability_pct + 11255.19 * customer_rating
                - 2786.97 * Region_north

### Coefficient Explanations
- **Intercept (83893.92):** Baseline predicted sales when all numerical variables are 0
  and the store is in the reference region. Not statistically significant (p = 0.091),
  so it should not be interpreted as a meaningful real-world baseline.
- **marketing_spend (1.19):** Holding all other variables constant, each additional unit
  of marketing spend is associated with a 1.19 unit increase in monthly sales.
- **footfall (33.78):** Holding all other variables constant, each additional customer
  visit is associated with a 33.78 unit increase in monthly sales. This is the strongest
  driver in the model.
- **inventory_availability_pct (2991.99):** Holding all else constant, each 1 percentage
  point increase in inventory availability is associated with a 2991.99 unit increase in
  monthly sales — meaning stockouts likely hurt sales significantly.
- **customer_rating (11255.19):** Holding all else constant, each 1-point increase in
  customer rating is associated with an 11255.19 unit increase in monthly sales.
- **Region_north (-2786.97):** Stores in the North region are predicted to have 2786.97
  lower monthly sales than stores in the reference region, holding other factors
  constant. However, this is NOT statistically significant (p = 0.667), so this
  difference cannot be reliably distinguished from zero/random noise.

### Dummy Variable Explanation
- The categorical variable **region** was converted into a dummy variable: Region_north
  (1 = store is in North region, 0 = store is not in North region).
- **Reference category: South.** All region comparisons in this model are made relative
  to stores in the South region. Only one dummy variable was created to avoid
  multicollinearity/redundancy (the "dummy variable trap") — since one category must
  always be left out as the baseline.

### Final Model Selected
**Multiple Regression Model**

### Reason for Selection
This model has the highest R-squared (0.8077) and Adjusted R-squared (0.8046) among all
models tested, includes multiple statistically significant and business-relevant
predictors (marketing_spend, footfall, inventory_availability_pct, customer_rating), and
provides the most complete and realistic explanation of what drives monthly sales
performance across stores.
