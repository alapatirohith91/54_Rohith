Transaction Fraud Detection at Scale
Imbalanced Classification and Risk-Based Evaluation
Overview

Financial transaction fraud detection is a classic high-imbalance machine learning problem, where fraudulent cases make up less than 1% of total transactions.
In such scenarios, traditional metrics like accuracy fail to reflect real performance.

This project focuses on building a practical fraud detection pipeline that prioritizes high-risk transactions, similar to how fraud systems are deployed in banks and fintech companies.

Problem Statement

Given a large transaction dataset with an extremely low fraud rate, the objective is to:

Detect fraudulent transactions as early as possible

Maximize fraud recall while keeping false alerts manageable

Assign a fraud risk score to each transaction instead of relying only on hard predictions

Dataset

PaySim – Synthetic Financial Transaction Dataset

Source: Kaggle

Dataset Size: ~6.3 million transactions

Fraud Rate: < 1%

PaySim simulates real mobile money behavior and is commonly used to test fraud detection systems under realistic imbalance conditions.

Approach and Workflow

The project follows a structured, end-to-end machine learning pipeline:

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

Feature Engineering

Instead of relying only on raw transaction fields, additional features were created to capture fraud behavior patterns:

Difference between account balance before and after transaction

Transaction amount relative to account balance

Zero-balance and near-zero balance indicators

Inconsistencies across transaction types

These features help the model detect behavioral anomalies, which are often more important than absolute values in fraud detection.

Handling Class Imbalance

Since fraud cases are extremely rare, multiple imbalance-handling techniques were tested:

Method	Description
No balancing	Baseline reference
Class weighting	Penalizes fraud misclassification
SMOTE	Generates synthetic fraud samples

Class weighting combined with tree-based models produced the most stable results, improving recall without introducing excessive noise.

Models Used

Logistic Regression (baseline)

Random Forest

LightGBM (final model)

Why LightGBM?

Designed for large-scale tabular data

Efficient training on millions of rows

Handles imbalance effectively with class weights

Commonly used in real-world fraud detection systems

Evaluation Strategy

Accuracy alone is not meaningful for fraud problems.
Model performance was evaluated using:

Precision@K – Are the top flagged transactions actually fraud?

Recall@K – How many fraud cases are captured in the top K alerts?

ROC-AUC

Confusion Matrix

Decision thresholds were tuned to reflect how alert-based fraud systems work in production.

Results

Significant improvement in fraud recall compared to baseline models

High precision among top-ranked fraud alerts

Better balance between fraud detection and false positives

Stable performance on unseen data

Output Format

The final model generates a ranked fraud risk score for each transaction:

transaction_id, fraud_score, fraud_prediction
100231, 0.93, 1
100232, 0.08, 0


This output can be directly used in:

Fraud monitoring dashboards

Alerting systems

Downstream decision pipelines

Tech Stack

Python

pandas, numpy

scikit-learn

LightGBM

imbalanced-learn

matplotlib

Jupyter Notebook


Future Improvements

Model ensembling for improved robustness

Feature importance and explainability using SHAP

Real-time prediction API

Dynamic thresholding based on transaction risk
