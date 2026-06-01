# A/B Testing Portfolio

A collection of end-to-end A/B test analyses on e-commerce data. Each project follows the full testing workflow — **hypothesis → data-quality checks → the correct statistical test → confidence intervals / effect size → business decision** — and explains *why* each choice is made, not just how to run the test.

---

## Projects

| Project | Focus | Metric(s) | Test | Result |
|---|---|---|---|---|
| [E-Commerce Revenue](./ecommerce-revenue/) | Single-metric revenue test | Average revenue per user | Independent t-test | Fail to reject H₀ |
| [Funnel Experiments](./funnel-experiments/) | Full-funnel, 5 metrics | CTR · conversion · AOV · ARPU · retention | Two-proportion z-test & Welch's t-test | Mixed — significant lift on CTR, conversion & ARPU |

---

## What this portfolio demonstrates

- **Choosing the right test** — binary outcome → proportion → z-test; continuous outcome → mean → t-test.
- **AOV vs ARPU** — value *per order* (filter to buyers) vs revenue *per user* (no filter), and the link `ARPU ≈ conversion rate × AOV`.
- **Welch's t-test** as a safe default when variances and group sizes differ.
- **Central Limit Theorem** — why a t-test stays valid on skewed, zero-inflated data at large sample sizes.
- **Confidence intervals & statistical power** — distinguishing "no effect" from "real but undetected".
- **Decision framework** — primary vs downstream vs guardrail metrics, novelty effects, and a repeatable "should we ship?" checklist.

---

## Repository structure

```
ab-tests/
├── ecommerce-revenue/      # Single-metric revenue t-test (Kaggle dataset)
│   ├── data/
│   ├── ab_test.ipynb
│   ├── ab_test_results.png
│   └── README.md
└── funnel-experiments/     # Full e-commerce funnel, 5 notebooks
    ├── data/
    ├── notebooks/
    │   ├── 01_click_through_rate.ipynb
    │   ├── 02_conversion_rate.ipynb
    │   ├── 03_average_order_value.ipynb
    │   ├── 04_revenue_per_user.ipynb
    │   └── 05_retention.ipynb
    ├── requirements.txt
    └── README.md
```

---

## Tech Stack

- Python · pandas · numpy
- scipy · statsmodels
- matplotlib · seaborn
- Jupyter Notebook

---

## Getting started

```bash
git clone https://github.com/Kenantkurt/ab-tests.git
cd ab-tests

# Funnel Experiments
pip install -r funnel-experiments/requirements.txt
jupyter lab    # open any notebook under funnel-experiments/notebooks/
```

Each notebook is self-contained and reads its dataset from the project's local `data/` folder, so it runs immediately after cloning.

---

## Author

**Kenan** — Junior Data Engineer  
Transitioning from data analytics · Learning through [DataTalks.Club DE Zoomcamp](https://github.com/DataTalksClub/data-engineering-zoomcamp)
