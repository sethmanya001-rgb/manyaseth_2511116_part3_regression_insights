
# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary
A retail chain's leadership team wants to understand what factors are driving monthly
sales performance across their stores. They are considering actions such as increasing
marketing spend, improving inventory availability, changing discounting strategy,
reallocating staff, and prioritizing certain store types or regions. This analysis uses
regression to identify which factors are most strongly associated with monthly sales and
to provide a data-driven business recommendation.

## Dataset Description
The dataset (`business_regression_data.xlsx`) contains store-level monthly performance
data, including sales figures and several potential drivers of sales such as marketing
spend, customer footfall, discounting, inventory availability, customer satisfaction,
and store/region classification.

## Dependent and Independent Variables

**Dependent Variable**
- monthly_sales

**Numerical Independent Variables**
- marketing_spend
- footfall
- avg_discount_pct
- inventory_availability_pct
- customer_rating

**Categorical Variables**
- region
- store_type

**Variables Needing Cleaning/Transformation**
- region and store_type required conversion into dummy variables before they could be
  used in regression.

**Variables Not Used in Final Model**
- avg_discount_pct and store_type dummy were not included in the final multiple
  regression model after initial review, as the strongest and most interpretable model
  was built using marketing_spend, footfall, inventory_availability_pct, customer_rating,
  and the region dummy variable.

## Regression Approach
- Two simple linear regression models were run first (single predictor at a time) to
  understand individual relationships with monthly_sales.
- A multiple regression model was then built combining multiple numerical predictors and
  one dummy variable to capture a more complete picture of what drives sales.

## Dummy Variable Approach
The categorical variable **region** was converted into a dummy variable:
**Region_north** (1 = store located in North region, 0 = otherwise).
**Reference category: South.** Only one dummy variable was created (rather than one per
region) to avoid the dummy variable trap / redundancy, since one category must always be
left out as the baseline for comparison.

## Model Comparison Summary

| Model | Variables | R-squared | Adjusted R-squared | Significant Variables |
|---|---|---|---|---|
| Simple Regression 1 | marketing_spend | 0.1672 | 0.1646 | marketing_spend |
| Simple Regression 2 | footfall | 0.7363 | 0.7355 | footfall |
| Multiple Regression (Final) | marketing_spend, footfall, inventory_availability_pct, customer_rating, Region_north | 0.8077 | 0.8046 | marketing_spend, footfall, inventory_availability_pct, customer_rating |

Full details are available in `analysis/model_comparison.md`.

## Final Model Selected
**Multiple Regression Model:**

monthly_sales = 83893.92 + 1.19 * marketing_spend + 33.78 * footfall
                + 2991.99 * inventory_availability_pct + 11255.19 * customer_rating
                - 2786.97 * Region_north

This model was selected because it has the highest R-squared (0.8077) and Adjusted
R-squared (0.8046) of all models tested, and includes multiple statistically significant,
business-relevant predictors.

## Business Recommendation
- Prioritize improving **inventory availability** and **driving footfall**, as these have
  the strongest, most significant effects on monthly sales.
- Continue **marketing spend** as a supporting investment, not the primary lever.
- Invest in **customer experience/service quality** to improve customer ratings, which
  also has a significant positive link to sales.
- Do **not** reallocate resources based on region alone — the Region_north variable was
  not statistically significant (p = 0.667) in the final model.

Full reasoning is available in `outputs/final_recommendation.md`.

## Assumptions and Limitations
- The dataset is observational, not from a controlled experiment, so regression results
  show association, not proven causation.
- The final model explains ~81% of variation in sales; the remaining ~19% is driven by
  factors not captured in this dataset (e.g., discounting strategy, staffing levels,
  local competition, seasonality).
- Region_north's non-significance does not mean region has zero effect — it may not be
  detectable with the current model structure or data variation.
- Residual analysis identified specific stores where actual sales deviated substantially
  from model predictions, suggesting unmeasured factors affect individual stores.

## Screenshots Included
- `screenshots/simple_regression_output.png` — Simple regression output (footfall model)
- `screenshots/multiple_regression_output.png` — Multiple regression output (final model)
- `screenshots/residuals_preview.png` — Predicted values and residuals (top positive/negative)
- `screenshots/model_comparison_preview.png` — Model comparison table

## Repository Structure
```
part3_regression_insights/
├── data/
│   └── business_regression_data.xlsx
├── analysis/
│   ├── regression_workbook.xlsx
│   ├── model_comparison.md
│   └── residual_analysis.md
├── outputs/
│   ├── regression_summary.xlsx
│   ├── final_recommendation.md
│   └── model_equations.md
├── screenshots/
│   ├── simple_regression_output.png
│   ├── multiple_regression_output.png
│   ├── residuals_preview.png
│   └── model_comparison_preview.png
└── README.md
```
