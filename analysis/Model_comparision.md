# Model Comparison

## Model 1: Simple Regression – Marketing Spend

**Variables Used**
- Dependent Variable: monthly_sales
- Independent Variable: marketing_spend

**Regression Equation**
monthly_sales = 560777.35 + 2.13 * marketing_spend

**R-squared:** 0.1672
**Adjusted R-squared:** 0.1646

**Significant Variables**
- marketing_spend (p = 2.48E-14) → Statistically significant

**Business Usefulness**
Marketing spend shows a positive and statistically significant relationship with monthly sales. However, it explains only about 17% of the variation in sales, which means it is too weak on its own to guide major budget or forecasting decisions. It can be used as supporting evidence, but not as a standalone driver of strategy.

**Limitations**
- Ignores other major drivers such as footfall, inventory availability, customer satisfaction, and regional differences.
- Low R-squared means a large portion of sales variation remains unexplained.
- Risk of omitted variable bias — marketing_spend may be correlated with other unmeasured factors that are the real drivers of sales.

---

## Model 2: Simple Regression – Footfall

**Variables Used**
- Dependent Variable: monthly_sales
- Independent Variable: footfall

**Regression Equation**
monthly_sales = 446410.58 + 35.68 * footfall

**R-squared:** 0.7363
**Adjusted R-squared:** 0.7355

**Significant Variables**
- footfall (p = 4.75E-94) → Statistically significant

**Business Usefulness**
Footfall alone explains about 74% of the variation in monthly sales, making it a strong single predictor. This suggests that store traffic is one of the most important factors influencing sales performance and could be used as a quick proxy metric for forecasting.

**Limitations**
- Still ignores marketing efficiency, inventory stockouts, customer satisfaction, and regional effects.
- High footfall does not guarantee high sales if conversion rate, inventory, or pricing is poor.
- Correlation does not imply causation — footfall may itself be influenced by external factors like location or promotions.

---

## Model 3: Multiple Regression (Final Selected Model)

**Variables Used**
- Dependent Variable: monthly_sales
- Independent Variables: marketing_spend, footfall, inventory_availability_pct, customer_rating (numerical); Region_north (dummy variable, reference category = South)

**Regression Equation**
monthly_sales = 83893.92 + 1.19 * marketing_spend + 33.78 * footfall + 2991.99 * inventory_availability_pct + 11255.19 * customer_rating − 2786.97 * Region_north

**R-squared:** 0.8077
**Adjusted R-squared:** 0.8046

**Significant Variables (p < 0.05)**
- marketing_spend (p = 2.55E-17)
- footfall (p = 3.97E-100)
- inventory_availability_pct (p = 1.60E-09)
- customer_rating (p = 0.0255)

**Not Significant**
- Region_north (p = 0.667)
- Intercept (p = 0.091)

**Business Usefulness**
This model explains about 81% of the variation in monthly sales — the highest among all models tested. It combines multiple realistic, actionable business levers: marketing spend, store traffic, inventory availability, and customer satisfaction. This makes it the most useful model for guiding leadership decisions on where to allocate resources (e.g., improving inventory availability or customer experience alongside marketing).

**Limitations**
- Region_north is not statistically significant, meaning region (in this dummy form) does not reliably explain sales differences once other factors are controlled for — store-level operational factors matter more than geography here.
- The intercept is not statistically significant, suggesting it should not be interpreted as a meaningful baseline sales value on its own.
- The model does not include discounting strategy or staffing levels, which could still be confounding or missing variables.
- ~19% of sales variation remains unexplained, meaning other unmeasured factors are still at play.
- Regression shows association, not causation — these relationships should not be used to claim that changing one variable will directly cause a proportional change in sales.

---

## Overall Comparison Table

| Model | Variables | R-squared | Adjusted R-squared | Significant Variables | Verdict |
|---|---|---|---|---|---|
| Simple Regression 1 | marketing_spend | 0.1672 | 0.1646 | marketing_spend | Weak — too simplistic, low explanatory power |
| Simple Regression 2 | footfall | 0.7363 | 0.7355 | footfall | Strong single-driver, but still incomplete |
| Multiple Regression (Final) | marketing_spend, footfall, inventory_availability_pct, customer_rating, Region_north | 0.8077 | 0.8046 | marketing_spend, footfall, inventory_availability_pct, customer_rating | **Best model — selected as final model** |

---

## Final Model Selection

**Final Model Selected:** Multiple Regression Model

**Reason for Selection**
- Highest R-squared (0.8077) and Adjusted R-squared (0.8046) among all models tested.
- Includes multiple statistically significant, business-relevant predictors (marketing_spend, footfall, inventory_availability_pct, customer_rating).
- Provides the most complete and realistic picture of what drives monthly sales, supporting more confident business decision-making compared to either simple regression model alone.

## Overall Limitations of Analysis
- All models are based on historical/observational data — they show association between variables, not proven causation.
- Region_north being non-significant does not mean region has no effect at all; it may need a different reference category, more regions, or interaction terms to detect true regional effects.
- Important business variables such as discounting strategy and staffing levels were not included in the multiple regression model and could be confounding factors.
- Results are only as reliable as the quality and completeness of the underlying dataset (e.g., missing values, outliers, or measurement errors could affect conclusions).
