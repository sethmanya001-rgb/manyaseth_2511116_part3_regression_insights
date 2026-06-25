# Residual Analysis

## Final Model Used
Multiple Regression Model:
monthly_sales = 83893.92 + 1.19 * marketing_spend + 33.78 * footfall
                + 2991.99 * inventory_availability_pct + 11255.19 * customer_rating
                - 2786.97 * Region_north

Residual = Actual monthly_sales − Predicted monthly_sales

A positive residual means the model under-predicted that store's actual sales.
A negative residual means the model over-predicted that store's actual sales.

## Top 5 Largest Positive Residuals (Model Under-Predicted Sales)

| Rank | Residual |
|---|---|
| 1 | 115722.6356 |
| 2 | 103842.7286 |
| 3 | 92104.49523 |
| 4 | 91370.76475 |
| 5 | 89713.84959 |

These stores had actual monthly sales significantly higher than what the model
predicted, based on their marketing spend, footfall, inventory availability, customer
rating, and region.

## Top 5 Largest Negative Residuals (Model Over-Predicted Sales)

| Rank | Residual |
|---|---|
| 1 | -150711.154 |
| 2 | -127901.6994 |
| 3 | -119453.7789 |
| 4 | -119058.108 |
| 5 | -109716.4585 |

These stores had actual monthly sales significantly lower than what the model
predicted, given the same set of inputs.

## Business Interpretation

### Why some stores have large positive residuals (under-predicted)
These stores are outperforming what their measured characteristics would suggest.
Possible business explanations:
- Strong local brand loyalty or a high proportion of repeat customers not captured by
  customer_rating alone
- Effective local promotions or discounting strategy not included in this model
- Favorable competitive conditions (e.g., fewer nearby competing stores)
- Strong store management, staff performance, or operational execution not captured by
  any variable in the model
- Possible seasonal or local demand spikes during the recorded month

### Why some stores have large negative residuals (over-predicted)
These stores are underperforming relative to what the model expects given their inputs.
Possible business explanations:
- High local competition reducing actual sales despite good footfall/marketing inputs
- Operational issues such as poor customer service, slow checkout experience, or
  short-term stockouts not reflected in the monthly average inventory_availability_pct
- Aggressive discounting that reduced revenue without proportionally increasing sales
  volume
- Local economic downturns, demographic shifts, or one-off disruptions (e.g.,
  construction, local events) not captured by the model

## Is the Model Under-Predicting or Over-Predicting Certain Types of Stores?

The magnitude of the largest positive residuals (~89,000 to ~115,000) and the largest
negative residuals (~-109,000 to ~-150,000) are of a similar overall scale. This
suggests the model is not systematically biased in one direction across the full
dataset — errors exist on both sides, rather than the model consistently over- or
under-predicting for all stores.

However, a small number of individual stores show very large deviations in both
directions. To determine whether these outliers belong to a specific **region** or
**store_type**, the Observation ID and corresponding Region/Store_type for each of
these top 10 rows should be cross-referenced in the regression workbook's residual
sheet. If a pattern emerges — for example, several large positive residuals belonging
to one specific store_type, or several large negative residuals concentrated in one
region — this would indicate the model is missing an important factor specific to that
group of stores, and would be a useful follow-up insight for leadership.

## Conclusion
The final model's R-squared of 0.8077 means about 19.23% of the variation in monthly
sales is not explained by marketing spend, footfall, inventory availability, customer
rating, or region. The residuals identified above represent the stores where this
unexplained variation is largest, and should be flagged for manual business review
rather than dismissed. These outlier stores may hold valuable insights — either
positive practices that could be replicated elsewhere (from the top positive
residuals), or operational problems that need correcting (from the top negative
residuals).
