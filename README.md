# Credit Card Fraud Detection & Analysis

An end-to-end data analytics project focused on identifying transaction patterns associated with fraudulent credit card activity.

The project uses Python for data cleaning, exploratory data analysis, statistical analysis, and fraud-pattern investigation, followed by an interactive Power BI dashboard for visualization and business reporting.

## Project Overview

Credit card fraud is a highly imbalanced classification problem where fraudulent transactions represent a very small proportion of total transactions.

This project analyzes transaction-level data to:

- Understand the distribution of legitimate and fraudulent transactions
- Explore transaction amount patterns
- Analyze fraud rates across elapsed-time periods
- Identify anonymized features associated with fraudulent transactions
- Investigate high-risk ranges of important features
- Develop analytical fraud-alert rules based on observed patterns
- Present the findings through an interactive Power BI dashboard

## Dataset

The dataset contains **284,807 transactions** with the following main columns:

| Column | Description |
|---|---|
| `Time` | Seconds elapsed between each transaction and the first transaction in the dataset |
| `V1`–`V28` | Anonymized PCA-transformed transaction features |
| `Amount` | Transaction amount |
| `Class` | Target variable: `0` = legitimate, `1` = fraud |

After removing duplicate records, the analysis contains approximately **283,726 transactions**.

### Class Distribution

- Legitimate transactions: **283,253**
- Fraudulent transactions: **473**
- Fraud rate: approximately **0.17%**

The severe class imbalance is an important consideration throughout the analysis.

## Tools & Technologies

- **Python**
  - Pandas
  - NumPy
  - Matplotlib
- **Jupyter Notebook**
- **Power BI**
- **Power Query**
- **GitHub**

## Analysis Workflow

### 1. Data Quality Check

The dataset was examined for:

- Missing values
- Duplicate transactions
- Data types
- Class distribution
- Numerical feature distributions

Duplicate records were identified and removed before continuing with the analysis.

### 2. Transaction Amount Analysis

Transaction amounts were analyzed overall and separately for legitimate and fraudulent transactions.

Key observations:

- Overall median transaction amount: **22.00**
- Legitimate transaction median: **22.00**
- Fraudulent transaction median: **9.82**
- Fraudulent transactions had a higher mean transaction amount despite having a lower median, indicating the influence of high-value transactions.

### 3. Time Analysis

The original `Time` column represents **elapsed seconds from the beginning of the dataset**, rather than an actual clock time.

An `Hour` feature was derived from this elapsed time to investigate whether fraud rates varied across different periods of the dataset.

### 4. Feature Analysis

The mean values of `V1`–`V28` were compared between legitimate and fraudulent transactions.

The largest differences were observed in:

1. **V3**
2. **V17**
3. **V14**
4. **V12**
5. **V7**

These features were investigated further using distribution analysis and binning.

### 5. High-Risk Feature Ranges

Selected features were divided into quantile-based ranges to compare fraud rates.

The analysis showed substantially higher fraud rates in the lowest ranges of:

- **V3**
- **V14**
- **V17**

For example, the lowest V14 range contained:

- 4,940 transactions
- 144 fraudulent transactions
- Fraud rate of approximately **2.92%**

This is substantially higher than the overall fraud rate of approximately 0.17%.

## Fraud Alert Rule Exploration

Based on the observed patterns in V3, V14, and V17, two analytical alert strategies were explored.

### Tight Rule

A transaction is flagged when all three conditions are satisfied:

```text
V14 < -1
AND
V3 < -1.8
AND
V17 < -0.8
