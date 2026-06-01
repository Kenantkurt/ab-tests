# Funnel Experiments — CTR → Conversion → AOV → ARPU → Retention

Statistical A/B testing across a full e-commerce funnel, using **Python, pandas, scipy, and statsmodels**.

Each notebook walks one metric end to end: data-quality checks → metric computation → the correct statistical test → interpretation and the business decision. The goal is to show not just *how* to run the test, but *why* each choice is made (which test, which filter, when a non-significant result is still informative).

## Dataset

`data/ab_test_data.parquet` — 12,000 users (6,000 control + 6,000 treatment), one row per user.

| Column | Description |
|---|---|
| `user_id` | Unique user id |
| `group` | `control` or `treatment` |
| `clicked` | 1 if the user clicked the banner |
| `purchased` | 1 if the user made a purchase |
| `order_value` | Order value in € (0 for non-buyers) |
| `returned_30d` | 1 if the user came back within 30 days |

## Notebooks

| # | Notebook | Metric | Test | Result |
|---|---|---|---|---|
| 01 | [Click-Through Rate](notebooks/01_click_through_rate.ipynb) | proportion | two-proportion z-test | 0.29 → 0.37, significant |
| 02 | [Conversion Rate](notebooks/02_conversion_rate.ipynb) | proportion | two-proportion z-test | 5.45% → 9.18%, significant |
| 03 | [Average Order Value](notebooks/03_average_order_value.ipynb) | mean (buyers only) | Welch's t-test | 86.12 → 86.03, not significant |
| 04 | [Revenue Per User (ARPU)](notebooks/04_revenue_per_user.ipynb) | mean (all users) | Welch's t-test | 4.69 → 7.90, significant |
| 05 | [Retention](notebooks/05_retention.ipynb) | proportion | z-test + confidence interval | 38.6% → 39.9%, not significant |

## Key ideas demonstrated

- **Choosing the test:** binary outcome → proportion → z-test; continuous outcome → mean → t-test.
- **AOV vs ARPU:** AOV is per *order* (filter to buyers); ARPU is per *user* (no filter). `ARPU ≈ conversion rate × AOV`.
- **Welch's t-test** as a safe default for comparing means with unequal variances.
- **Central Limit Theorem:** why a t-test stays valid on skewed, zero-inflated data at large sample sizes.
- **Confidence intervals & power:** distinguishing "no effect" from "real but undetected".
- **Decision framework:** primary vs downstream vs guardrail metrics, novelty effect, and the "should we ship?" pattern.

## Run locally

```bash
pip install -r requirements.txt
jupyter lab    # open any notebook under notebooks/
```
