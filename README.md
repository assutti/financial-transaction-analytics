# Financial Transaction Analytics & Fraud Detection

## Project Overview

This project analyzes financial transactions and develops machine learning models to identify potentially fraudulent activity.

The analysis uses the **PaySim dataset**, a synthetic dataset representing mobile money transactions.

The project combines data validation, exploratory data analysis (EDA), feature engineering, and supervised machine learning. Findings are communicated through a two-page Power BI dashboard and a seven-slide project presentation.

## Objectives

- Explore financial transaction patterns and identify characteristics associated with fraud.
- Investigate class imbalance and transaction types.
- Develop and evaluate fraud detection models.
- Compare Logistic Regression and Random Forest.
- Identify the most influential features in fraud detection.

## Dataset

**Source:** PaySim — Synthetic Financial Datasets for Fraud Detection.

The dataset contains:

- 6,362,620 transactions
- 11 original variables
- 8,213 fraudulent transactions
- Approximately 0.129% fraudulent transactions

The dataset includes transaction amounts, transaction types, account balances, and fraud indicators.

The original and processed CSV files are excluded from the Git repository because of their size.

## Project Structure

```text
financial-transaction-analytics/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   └── 04_fraud_detection.ipynb
├── powerbi/                       # Two-page Power BI report (.pbix)
├── presentations/
│   └── Fraud_Detection_Project.pptx
├── .gitignore
└── README.md
```

## Methodology

### 1. Data Collection and Validation

The PaySim dataset was loaded and inspected to understand its structure and validate its contents.

### 2. Data Cleaning

Data quality checks and preparation steps were performed to create a validated dataset for analysis.

### 3. Exploratory Data Analysis

The analysis examined transaction distributions, transaction types, fraudulent activity, and relationships between financial variables.

### 4. Fraud Detection

Two supervised classification algorithms were implemented:

- Logistic Regression
- Random Forest

A chronological data split was used to separate training, validation, and test periods.

Classification thresholds were selected using validation data, with particular attention to precision, recall, and F1-score.

## Exploratory Analysis: Key Findings

- Fraud is rare: **8,213 of 6,362,620 transactions (0.129%)** are labeled fraudulent.
- All labeled fraud cases in PaySim occur in **TRANSFER** and **CASH_OUT** transactions.
- Fraud rates differ by transaction type: approximately **0.769% for TRANSFER** and **0.184% for CASH_OUT**.
- Transactions labeled as fraud represent approximately **12.06 billion simulated monetary units** in total, split almost equally between TRANSFER and CASH_OUT. These amounts are **not verified real-world losses**.

## Model Performance

The following results were obtained on the chronological test dataset (**123,580 transactions**, including **1,654 labeled frauds**).

| Metric | Logistic Regression | Random Forest |
|---|---:|---:|
| Precision (Fraud) | 56.61% | 96.71% |
| Recall (Fraud) | 33.68% | 70.98% |
| F1-score (Fraud) | 42.23% | 81.87% |
| Accuracy | 98.77% | 99.58% |

**Random Forest achieved the best overall performance.**

Its confusion matrix showed:

- 1,174 correctly detected fraudulent transactions
- 480 missed fraudulent transactions
- 40 legitimate transactions incorrectly flagged as fraud

## Feature Importance

According to Random Forest impurity-based feature importance, the most influential variables were:

1. `oldbalanceOrg` — 31.46%
2. `amount` — 24.14%
3. `type_TRANSFER` — 10.01%

These values describe relative feature importance within the fitted model and should not be interpreted as causal relationships.

## Power BI Dashboard

The project includes a **two-page interactive Power BI report** that presents the exploratory analysis and the fraud-detection results.

1. **Financial Transaction Overview** — total transactions, fraud count and fraud rate, transactions by type, fraud rate by type, and fraudulent transaction amounts.
2. **Fraud Detection Models** — Logistic Regression versus Random Forest performance (precision, recall and F1-score), their confusion matrices, and key findings.

The Power BI `.pbix` report is located in the [`powerbi/`](powerbi/) directory.

## Project Presentation

A **seven-slide presentation** summarizes the dataset, transaction patterns, fraud distribution, the machine-learning workflow, model performance, and the project's conclusions and limitations.

[**View the PowerPoint presentation**](presentations/Fraud_Detection_Project.pptx)

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook
- Power BI
- PowerPoint / ONLYOFFICE Presentations
- Git and GitHub

## Limitations

The PaySim dataset is synthetic, so the reported performance cannot be assumed to generalize to real-world financial systems.

The test period was also examined during preliminary experiments. Consequently, the reported test performance should be regarded as exploratory rather than as an entirely independent final evaluation.

Further validation on previously unseen data would be necessary before considering practical deployment.

## Conclusion

The project demonstrates an end-to-end financial transaction analysis and fraud detection workflow.

Random Forest substantially outperformed Logistic Regression, achieving an F1-score of 81.87% on the evaluated test dataset.

The results highlight the importance of selecting appropriate evaluation metrics and classification thresholds when working with highly imbalanced financial data.
