# 💼 LendingClub Loan Analysis Project using Pyspark

## 📊 Project Overview
- **Dataset**: LendingClub loan data (CSV format)
- **Size**: 1.7 GB
- **Records**: 2+ million
- **Columns**: 118
- **Tools Used**: PySpark, HDFS

The project required breaking down the raw dataset into multiple logical components to enable modular processing and analysis.

---

## 🧹 Data Engineering Workflow

### 🔹 Step 1: Dataset Segmentation
We extracted and curated **4 primary datasets** from the raw file:

| Dataset Name         | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `customers_data`     | Borrower details including income, employment, and credit grade             |
| `loans_data`         | Loan-level information such as amount, term, interest rate, and status      |
| `loan_repayments`    | Repayment history including principal, interest, and late fees              |
| `loan_defaulters`    | Delinquency and bankruptcy indicators for risk profiling                    |

Additional derived datasets:
- `loan_defaulters_delinq_csv`
- `loan_defaulters_records_inq_csv`

These were written to the *cleaned* folder after preprocessing.

---

### 🔹 Step 2: Data Quality Handling
- Identified and isolated **corrupt or malformed records**
- Moved all bad data to:  
  📁 /user/itv021558/lendingclubproject/bad
  _Note: This data is excluded from processing and will be handled by the upstream data team._

---

### 🔹 Step 3: Table Creation
Created **permanent Hive-compatible tables** on top of the cleaned datasets to enable SQL-based querying and analytics.

---

### 🔹 Step 4: Loan Score Calculation
Engineered a new metric: **Loan Score**, based on repayment behavior and risk indicators.

- Output stored at:  
  📁 `/user/itv021558/lendingclubproject/processed/loan_score`

---

## ✅ Final Output Summary

| Dataset Name                      | Location                                                  |
|-----------------------------------|-----------------------------------------------------------|
| `customers_parquet`               | `/cleaned/customers_parquet`                              |
| `loans_parquet`                   | `/cleaned/loans_parquet`                                  |
| `loans_repayments`                | `/cleaned/loans_repayments`                               |
| `loans_defaulters`                | `/cleaned/loans_defaulters`                               |
| `loan_score` (engineered file)    | `/processed/loan_score`                                   |
|  Bad records                      | `/bad` (excluded from processing)                         |

---

