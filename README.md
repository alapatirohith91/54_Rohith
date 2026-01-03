# Transaction Fraud Detection at Scale

## Overview
Financial transaction fraud detection is a high-imbalance machine learning problem where fraudulent transactions account for less than 1% of all records.  
In such cases, traditional accuracy metrics are misleading.

This project builds a practical fraud detection pipeline that focuses on identifying high-risk transactions using risk-based evaluation methods commonly used in real-world financial systems.

---

## Problem Statement
Given a large-scale transaction dataset with an extremely low fraud rate, the objectives are to:

- Detect fraudulent transactions effectively
- Maximize fraud recall while controlling false alerts
- Generate a fraud risk score for each transaction instead of relying only on binary predictions

---

## Dataset
**PaySim – Synthetic Financial Transaction Dataset**

- Source: Kaggle  
- Number of records: ~6.3 million  
- Fraud rate: < 1%  

The dataset simulates mobile money transactions and reflects realistic fraud patterns, making it suitable for evaluating fraud detection models under severe class imbalance.

---

## Approach and Workflow
The project follows a complete end-to-end machine learning pipeline:

Raw Transaction Data
↓
Data Cleaning and Encoding
↓
Feature Engineering
↓
Stratified Train-Test Split
↓
Class Imbalance Handling
↓
Model Training
↓
Threshold Selection
↓
Precision@K / Recall@K Evaluation
↓
Fraud Risk Scoring Output


---

## Feature Engineering
To capture fraud behavior more effectively, additional features were engineered beyond the raw transaction fields:

- Balance difference before and after transaction
- Transaction amount to balance ratio
- Zero or near-zero balance indicators
- Behavioral inconsistencies across transaction types

These features help the model learn transaction patterns that are commonly associated with fraudulent behavior.

---

## Handling Class Imbalance
Since fraud cases are rare, multiple imbalance handling techniques were evaluated:

| Method | Description |
|------|-------------|
| No balancing | Baseline model for comparison |
| Class weighting | Penalizes misclassification of fraud cases |
| SMOTE | Generates synthetic fraud samples |

Class weighting with tree-based models provided the best balance between recall and false positives.

---

## Models Used
The following models were implemented and compared:

- Logistic Regression (baseline)
- Random Forest
- LightGBM (final model)

LightGBM was selected due to its efficiency on large tabular datasets and its strong performance on imbalanced data.

---

## Evaluation Strategy
Model performance was evaluated using business-relevant metrics rather than accuracy alone:

- Precision@K
- Recall@K
- ROC-AUC
- Confusion Matrix

Decision thresholds were tuned to simulate real-world fraud alert systems.

---

## Results
- Improved fraud recall compared to baseline models
- High precision among top-ranked fraud alerts
- Reduced false positives
- Stable performance on unseen test data

---
