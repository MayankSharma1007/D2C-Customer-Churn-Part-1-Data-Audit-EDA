# Data Quality Assessment Report

## Project Title

**D2C Customer Churn Intelligence & Retention Analytics**

## Submitted By

**Mayank Gopal Sharma**

---

# 1. Introduction

Before performing exploratory data analysis and developing churn-related business hypotheses, it is essential to evaluate the quality and reliability of the available datasets.

The purpose of this audit is to identify data issues that may affect downstream analysis, customer segmentation, churn prediction modelling, and retention strategy design.

The assessment focuses on:

* Missing values
* Duplicate records
* Outliers
* Join-key consistency
* Date consistency
* Potential data leakage risks

---

# 2. Dataset Inventory

The project consists of seven structured datasets covering customer profiles, transactions, support interactions, digital engagement, churn outcomes, marketing interventions, and engineered behavioural metrics.

| Dataset              |  Rows | Columns |
| -------------------- | ----: | ------: |
| customers            |  2400 |       9 |
| orders               | 10009 |      10 |
| support_tickets      |  1921 |       8 |
| web_events           |  2400 |      10 |
| churn_labels         |  2400 |       4 |
| intervention_history |  2400 |       5 |
| rfm_snapshot         |  2400 |      29 |

### Observation

The dataset structure appears well organized. Every major business function relevant to churn analysis is represented, including customer demographics, purchasing behaviour, customer support interactions, marketing exposure, and online engagement activity.

---

# 3. Missing Value Assessment

Missing values can reduce model performance and may introduce bias if not handled carefully.

The following table summarizes missing-value counts across all datasets.

## Table 1: Missing Value Summary

| Dataset              | Total Missing Values |  Rows | Columns |
| -------------------- | -------------------: | ----: | ------: |
| customers            |                 1787 |  2400 |       9 |
| orders               |                   80 | 10009 |      10 |
| support_tickets      |                    0 |  1921 |       8 |
| web_events           |                    0 |  2400 |      10 |
| churn_labels         |                    0 |  2400 |       4 |
| intervention_history |                    0 |  2400 |       5 |
| rfm_snapshot         |                 1386 |  2400 |      29 |

### Observation

The highest concentration of missing information exists within the customers and rfm_snapshot datasets. Most of these missing values are associated with customer loyalty-tier information.

---

## Table 2: Detailed Missing Values

### Customers Dataset

| Column       | Missing Values |
| ------------ | -------------: |
| loyalty_tier |           1386 |
| skin_type    |            401 |

### Orders Dataset

| Column | Missing Values |
| ------ | -------------: |
| rating |             80 |

### RFM Snapshot Dataset

| Column       | Missing Values |
| ------------ | -------------: |
| loyalty_tier |           1386 |

### Interpretation

The missing loyalty-tier information affects more than half of the customer base. This suggests either incomplete enrollment in the loyalty program or a data-capture issue.

Missing ratings are relatively small and most likely represent customers who chose not to provide post-purchase feedback.

---

# 4. Duplicate Record Assessment

Duplicate records can distort customer counts, transaction volumes, and modelling outputs.

## Table 3: Exact Duplicate Records

| Dataset              | Duplicate Rows |
| -------------------- | -------------: |
| customers            |              0 |
| orders               |              0 |
| support_tickets      |              0 |
| web_events           |              0 |
| churn_labels         |              0 |
| intervention_history |              0 |
| rfm_snapshot         |              0 |

### Interpretation

No exact duplicate records were found in any dataset. This indicates strong record-level integrity and suggests that data ingestion pipelines are functioning correctly.

---

# 5. Duplicate-Like Customer Activity Assessment

Although no duplicate rows exist, some datasets naturally contain repeated customer appearances.

## Table 4: Customer Representation Across Datasets

| Dataset              | Total Rows | Unique Customers | Repeated Records |
| -------------------- | ---------: | ---------------: | ---------------: |
| customers            |       2400 |             2400 |                0 |
| orders               |      10009 |             2400 |             7609 |
| support_tickets      |       1921 |             1247 |              674 |
| web_events           |       2400 |             2400 |                0 |
| churn_labels         |       2400 |             2400 |                0 |
| intervention_history |       2400 |             2400 |                0 |
| rfm_snapshot         |       2400 |             2400 |                0 |

### Interpretation

The repeated customer records in orders and support_tickets are expected because customers may place multiple orders and raise multiple support tickets.

Therefore, these are valid business records rather than duplicate-data problems.

---

# 6. Join-Key Consistency Assessment

The customer_id field acts as the primary business key across datasets.

A consistency check was performed to ensure customer records can be joined correctly.

## Table 5: Customer Coverage Validation

| Dataset              | Customers Missing From Master Dataset |
| -------------------- | ------------------------------------: |
| customers            |                                     0 |
| orders               |                                     0 |
| support_tickets      |                                  1153 |
| web_events           |                                     0 |
| churn_labels         |                                     0 |
| intervention_history |                                     0 |
| rfm_snapshot         |                                     0 |

### Interpretation

The support ticket dataset contains only customers who contacted customer support.

Consequently, many customers do not appear in this dataset. This is expected business behaviour and not a data-quality issue.

No join-key inconsistencies were found in the remaining datasets.

---

# 7. Date Consistency Assessment

Temporal consistency is critical for churn modelling because future information must never be used to explain past behaviour.

## Table 6: Date Range Validation

| Dataset              | Earliest Date | Latest Date |
| -------------------- | ------------- | ----------- |
| customers            | 2024-01-01    | 2025-09-15  |
| orders               | 2024-01-09    | 2025-11-29  |
| support_tickets      | 2024-01-13    | 2025-09-30  |
| web_events           | 2025-09-30    | 2025-09-30  |
| churn_labels         | 2025-09-30    | 2025-09-30  |
| intervention_history | 2025-09-30    | 2025-09-30  |
| rfm_snapshot         | 2025-09-30    | 2025-09-30  |

### Interpretation

The date ranges are logically consistent.

The web_events, churn_labels, intervention_history, and rfm_snapshot datasets represent customer snapshots captured on a single reference date.

---

## Table 7: Future-Date Validation

| Validation Check                   | Invalid Records |
| ---------------------------------- | --------------: |
| Orders with Future Dates           |               0 |
| Support Tickets with Future Dates  |               0 |
| Customer Signups with Future Dates |               0 |

### Interpretation

No future-dated records were detected, confirming that timestamp information is reliable.

---

# 8. Outlier Assessment

Outliers may represent data errors or unusual customer behaviour.

The following numerical variables were examined using boxplots and IQR-based detection.

## Table 8: Outlier Summary

| Variable         | Outliers Detected |
| ---------------- | ----------------: |
| gross_amount     |               536 |
| delivery_days    |                 3 |
| resolution_hours |                 9 |

### Gross Amount

The order-value distribution contains several high-value purchases.

These likely represent premium customers, bulk orders, or expensive product categories.

### Delivery Days

Only three delivery records fall outside the normal range.

These may correspond to logistical delays or exceptional fulfillment circumstances.

### Resolution Hours

Nine support tickets required significantly longer resolution times than average.

These cases may represent escalated complaints and could potentially contribute to customer dissatisfaction and churn.

---

# 9. Potential Data Leakage Assessment

During model development, several variables must be handled carefully to avoid introducing target leakage.

## Table 9: Potential Leakage Variables

| Variable       | Risk Description                         |
| -------------- | ---------------------------------------- |
| churn_next_60d | Target variable itself                   |
| split          | Dataset partition information            |
| snapshot_date  | Can leak temporal information if misused |

### Interpretation

These variables should not be used as predictive features during future churn modelling activities.

Improper usage would result in artificially inflated model performance.

---

# 10. Data Quality Risk Prioritization

## Table 10: Business Impact Assessment

| Issue                               | Severity | Business Impact                           |
| ----------------------------------- | -------- | ----------------------------------------- |
| Missing loyalty tier                | High     | Affects segmentation and loyalty analysis |
| Missing skin type                   | Medium   | Affects personalization insights          |
| Missing ratings                     | Low      | Minimal impact                            |
| High-value order outliers           | Medium   | Can skew averages                         |
| Resolution-hour outliers            | Medium   | May indicate churn drivers                |
| Support-ticket coverage differences | Low      | Expected behaviour                        |

---

# 11. Overall Assessment

## Table 11: Dataset Readiness Score

| Area                      | Rating |
| ------------------------- | ------ |
| Missing Values            | 7/10   |
| Duplicate Records         | 10/10  |
| Join Consistency          | 9/10   |
| Date Consistency          | 10/10  |
| Outlier Quality           | 8/10   |
| Overall Dataset Readiness | 9/10   |

---

# 12. Final Conclusion

The datasets are generally clean, internally consistent, and suitable for downstream exploratory analysis and churn investigation.

The most significant issue identified is the high proportion of missing loyalty-tier values within customer-related datasets. However, no major duplicate-record issues, key-matching problems, or date inconsistencies were found.

Overall, the data quality is sufficiently strong to proceed with exploratory analysis, churn-risk hypothesis generation, customer segmentation, predictive modelling, and retention-strategy development.
