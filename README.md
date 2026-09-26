# 💳 Credit Card Fraud Detection Analysis


## 📌 Business Question

> **Which transaction patterns consistently signal fraudulent behaviour, and what triggers should be set in a real-time fraud alert system?**

This project answers that question end to end — using plain, explainable data analysis so every finding can be traced back to a specific, reproducible step.

---

## 📊 Dataset

[Credit Card Fraud Detection dataset](https://www.kaggle.com/mlg-ulb/creditcardfraud) (Kaggle) — 284,807 anonymized European card transactions.

| | |
|---|---|
| **Total transactions (cleaned)** | 283,726 |
| **Confirmed fraud cases** | 473 |
| **Fraud rate** | 0.17% |
| **Features** | Time, V1–V28 (anonymized via PCA), Amount, Class |

---

## 🛠️ Tools Used

- **Python** — Pandas, Matplotlib — data cleaning, exploratory analysis, threshold discovery
- **Power BI** — 3-page interactive dashboard

---

## 🔍 Approach

1. **Cleaned the data** — removed 1,081 duplicate rows, checked for missing values
2. **Ranked all 28 anonymized features** by how strongly their average value differs between fraud and legitimate transactions
3. **Identified the 3 strongest, non-overlapping signals** — V14, V3, V17
4. **Found the exact "danger zone"** for each, using bucket analysis
5. **Built and tested two rule-based alert triggers** — a strict rule and a broad rule
6. **Checked supporting patterns** — time-of-day and transaction amount

---

## 💡 Key Findings

- Fraud is rare (0.17%) but not random — it concentrates in specific, provable value ranges
- Three features — **V14, V3, V17** — are the strongest, most independent fraud indicators
- Fraud shows a strong, recurring spike within a specific 2–3 hour window each day
- Fraud transactions tend to involve small "test" amounts, with occasional large outliers

---

## 🚨 Recommended Alert Triggers

| Rule | Logic | Catch Rate | False Alarms | Precision | Best Use |
|---|---|---|---|---|---|
| **Tight** | `V14 < -1 AND V3 < -1.8 AND V17 < -0.8` | 66.8% | 414 | 43.29% | Automatic hold/block |
| **Wide** | `V14 < -1 OR V3 < -1.8 OR V17 < -0.8` | 92.8% | 76,109 | 0.57% | Human review queue |

**Conclusion:** No single rule serves both jobs a real fraud system needs. A **two-layer system** — a strict rule for safe automatic action, paired with a broader rule that routes borderline cases to human review — reflects how real fraud detection systems are actually designed.

---

## 📈 Dashboard Preview

A 3-page interactive Power BI dashboard — see `fraud_dashboard.pdf` for the full preview.

| Page | What it shows |
|---|---|
| **Overview** | KPIs, fraud vs. legit split, amount comparisons, fraud rate by hour |
| **Fraud Patterns** | Danger-zone charts for V14, V3, V17, and time-of-day |
| **Fraud Alert Rules** | Recommended triggers, with tested performance numbers |

---

## 📁 Files in This Repo

```
├── fraud_analysis_final.ipynb     # Full Python analysis, cleaned and documented
├── fraud_analysis_report.docx     # Written report with findings, charts, and dashboard visuals
└── fraud_dashboard.pdf            # All 3 Power BI dashboard pages, exported for preview
```

*The Power BI `.pbix` source file is available on request — it exceeds GitHub's direct upload size limit.*

---

## ⚠️ Limitations

- This dataset is from 2013 and one specific region — real-world fraud patterns evolve constantly
- The anonymized features (V1–V28) have unknown real-world meaning, by design, for privacy
- The Wide rule, as-is, is too noisy for automatic deployment
- These are **proposed analytical triggers**, not a production-ready system — a real deployment would combine many more signals and require ongoing monitoring

---

## 🤖 Why No Machine Learning

Simple, explainable threshold rules are fast to compute, transparent, and easy for a non-technical fraud team to trust and adjust — which matters more for a real-time alert system than squeezing out marginal accuracy gains from a black-box model. Every finding in this project traces back to a specific, reproducible calculation.

---

**Author:** Shalini | Data Analyst Portfolio Project
