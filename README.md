

# 🚨 Transaction Fraud Detection at Scale

---

## 🎯 Problem Statement

Given millions of transaction records with **<1% fraud rate**, build a machine learning system that:

* Identifies high-risk fraudulent transactions
* Maximizes recall without overwhelming false alerts
* Produces a ranked **fraud risk score** per transaction

---

## 📊 Dataset

**PaySim – Synthetic Financial Fraud Dataset**

* Source: Kaggle
* Link: [https://www.kaggle.com/datasets/ealaxi/paysim1](https://www.kaggle.com/datasets/ealaxi/paysim1)
* Records: ~6.3 million
* Fraud Rate: < 1%

PaySim simulates real mobile money behavior, making it ideal for testing **fraud detection pipelines under realistic conditions**.

---

## 🧠 End-to-End Solution Architecture

```
Raw Transactions
        ↓
Data Cleaning & Encoding
        ↓
Domain-Driven Feature Engineering
        ↓
Stratified Train-Test Split
        ↓
Imbalance Handling (Class Weights / SMOTE)
        ↓
Model Training (LightGBM)
        ↓
Threshold Optimization
        ↓
Precision@K / Recall@K Evaluation
        ↓
Fraud Risk Scoring (CSV Output)
```

---

## 🔬 Feature Engineering (Key Innovation)

Instead of relying only on raw fields, the model learns **fraud behavior patterns** through:

* Balance change before vs after transaction
* Transaction amount to balance ratio
* Zero-balance anomaly indicators
* Behavioral inconsistencies across transaction types

These features significantly improve the model’s ability to detect **subtle fraud signals**.

---

## ⚖️ Handling Severe Class Imbalance

Three strategies were evaluated:

| Technique               | Purpose                           |
| ----------------------- | --------------------------------- |
| Baseline (No balancing) | Reference comparison              |
| Class Weighting         | Penalizes fraud misclassification |
| SMOTE                   | Synthetic fraud sample generation |

👉 **Class weighting with LightGBM** provided the best balance between recall and false positives.

---

## 🤖 Models Implemented

* Logistic Regression (baseline)
* Random Forest
* **LightGBM (Final Model)**

### Why LightGBM?

* Optimized for large-scale tabular data
* Handles class imbalance natively
* Faster training and superior recall
* Widely adopted in real fraud detection systems

---

## 📐 Evaluation Strategy (Business-Aligned)

Traditional accuracy is misleading for fraud problems.
This project evaluates models using:

* **Precision@K** → Are the top K alerts actually fraud?
* **Recall@K** → How many fraud cases are captured?
* ROC-AUC
* Confusion Matrix

Additionally, **decision thresholds were tuned**, reflecting real-world alerting systems.

---

## 📈 Key Results

* Substantial improvement in fraud recall over baseline
* High precision for top-ranked fraud alerts
* Reduced false positives while maximizing fraud capture
* Stable generalization on unseen data

---

## 📤 Output: Fraud Risk Scoring

Final output is a **ranked fraud score CSV**:

```text
transaction_id, fraud_score, fraud_prediction
100231, 0.93, 1
100232, 0.08, 0
```

This format is ready for:

* Fraud alert systems
* Risk dashboards
* Automated decision pipelines

---

## 🧰 Tech Stack

* **Language:** Python
* **ML:** scikit-learn, LightGBM
* **Imbalance Handling:** imbalanced-learn
* **Data:** pandas, numpy
* **Visualization:** matplotlib
* **Experiment Tracking (Optional):** MLflow
* **Platform:** Jupyter Notebook

---

## ▶️ How to Run

```bash
pip install -r requirements.txt
jupyter notebook fraud_detection.ipynb
```

---

## 🚀 Future Extensions

* Ensemble stacking (LightGBM + ANN)
* Explainability using SHAP
* Real-time fraud detection API
* Adaptive thresholds based on transaction risk

---

## 🏁 Hackathon Impact Summary

✔ Real-world fraud detection framing
✔ Imbalanced ML best practices
✔ Business-relevant metrics
✔ Scalable and deployable pipeline
✔ Clear, judge-friendly documentation
