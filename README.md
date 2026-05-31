# D2C Customer Churn Intelligence & Retention Analytics

## Part 1: Data Audit, Exploratory Data Analysis & Business Understanding

### Student Information

**Name:** Mayank Gopal Sharma

**Project:** D2C Customer Churn Intelligence & Retention Analytics

---

# Project Overview

Before developing any churn prediction model or retention strategy, it is important to understand the available data, identify quality issues, and discover business patterns that may contribute to customer churn.

This repository contains the complete implementation for **Part 1** of the capstone project. The work focuses on:

* Raw dataset inspection
* Data quality assessment
* Join validation across datasets
* Exploratory Data Analysis (EDA)
* Churn-risk pattern identification
* Business hypothesis generation
* Business recommendations

The objective of this phase is to transform raw business data into actionable insights that can guide future retention strategies.

---

# Repository Structure

```text
Part_1_Data_Audit_EDA_Business_Understanding/
│
├── eda_audit.ipynb
├── README.md
├── requirements.txt
├── data_quality_report.md
├── business_memo.md
│
└── outputs/
    ├── charts/
    ├── tables/
    └── exported_csv_files
```

---

# Datasets Used

The analysis uses the following datasets provided in the project package:

1. customers.csv
2. orders.csv
3. support_tickets.csv
4. web_events_snapshot.csv
5. churn_labels.csv
6. intervention_history.csv
7. rfm_modeling_snapshot.csv

Additional project documentation files:

* DATA_DICTIONARY.md
* STUDENT_FACING_PROBLEM_STATEMENT.md

---

# Tasks Performed

## 1. Raw Data Audit

All datasets were loaded and inspected for:

* Number of rows and columns
* Data types
* Missing values
* Duplicate records
* Key relationships
* Schema consistency

---

## 2. Data Quality Assessment

A detailed data quality review was performed covering:

* Missing value analysis
* Duplicate record analysis
* Invalid value detection
* Outlier detection
* Join/key validation
* Date consistency validation
* Potential data leakage identification

---

## 3. Exploratory Data Analysis

EDA was performed on:

### Customer Demographics

* City Tier
* Age Group
* Acquisition Channel
* Loyalty Tier
* Preferred Category

### Order Behaviour

* Order frequency
* Order value
* Delivery performance
* Ratings

### Monetary Behaviour

* Customer spending patterns
* Revenue distribution
* Discount behaviour

### Support Behaviour

* Ticket frequency
* Resolution time
* Sentiment analysis
* Reopened tickets

### Return & Refund Behaviour

* Return patterns
* Product return rates

### Web/App Behaviour

* Sessions
* Product views
* Cart activity
* Wishlist activity
* Campaign engagement

### Campaign History

* Marketing interventions
* Campaign exposure
* Customer engagement

### Churn Distribution

* Churn rate analysis
* Churn segment comparison

---

## 4. Churn Risk Hypotheses

Multiple churn-risk hypotheses were developed based on observed patterns.

Each hypothesis is supported by:

* Visual evidence
* Statistical observations
* Business interpretation

Examples include:

* Customers with low engagement are more likely to churn.
* Customers with high support-ticket frequency may exhibit higher churn risk.
* Customers with long periods of inactivity may be at elevated churn risk.
* Lower loyalty tiers may experience higher churn rates.
* Customers with repeated negative support experiences may be more likely to leave.

---

## 5. Business Memo

A business-focused memo was prepared summarizing:

* Major findings
* Potential churn drivers
* Areas requiring investigation
* Recommendations before launching retention campaigns

---

# How to Run the Project

## Step 1: Clone Repository

```bash
git clone <repository-link>
```

---

## Step 2: Navigate to Project Folder

```bash
cd Part_1_Data_Audit_EDA_Business_Understanding
```

---

## Step 3: Create Virtual Environment

### Windows

```bash
python -m venv venv
```

Activate:

```bash
venv\Scripts\activate
```

### Mac/Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## Step 4: Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Step 5: Place Dataset Files

Create a folder named:

```text
Datasets
```

Place all provided CSV files inside this folder.

Example:

```text
Datasets/
│
├── customers.csv
├── orders.csv
├── support_tickets.csv
├── web_events_snapshot.csv
├── churn_labels.csv
├── intervention_history.csv
└── rfm_modeling_snapshot.csv
```

---

## Step 6: Launch Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
eda_audit.ipynb
```

Run all cells sequentially.

---

# Outputs Generated

The notebook generates:

### Tables

* Missing value summary
* Duplicate record summary
* Join validation summary
* Date consistency summary
* Outlier summary

### Charts

* Demographic analysis charts
* Behaviour analysis charts
* Churn pattern charts
* Campaign analysis charts
* Customer activity charts

All generated outputs are saved inside the **outputs** folder.

---

# Key Findings

Some important observations identified during analysis include:

* Missing values exist in customer loyalty and skin type attributes.
* Order ratings contain a small number of missing records.
* High-value order outliers are present.
* A significant portion of customers have never created support tickets.
* Customer engagement indicators vary considerably across the user base.

These findings are further discussed in the data quality report and business memo.

---

# Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Jupyter Notebook
* VS Code

---

# Author

**Mayank Gopal Sharma**

Capstone Project Submission
