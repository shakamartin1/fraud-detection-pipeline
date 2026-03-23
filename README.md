# Fraud Detection Pipeline
> End-to-end fraud detection system built on 590K real-world financial transactions using AWS, Python, and Machine Learning.

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![AWS](https://img.shields.io/badge/AWS-S3%20%7C%20Glue%20%7C%20Athena-orange)
![Python](https://img.shields.io/badge/Python-pandas%20%7C%20sklearn-blue)

---

## The Problem

Financial fraud costs businesses and consumers billions annually. Traditional rule-based detection systems are static — sophisticated fraudsters learn the rules and find the gaps. This project builds a machine learning pipeline that identifies non-obvious behavioral patterns that rules-based systems miss.

**Core question:** Can we detect fraud not just from what information is provided, but from the pattern of what is deliberately left out?

---

## Dataset

**IEEE-CIS Fraud Detection Dataset** — Kaggle / Vesta Corporation
- 590,540 real e-commerce transactions
- 394 features across transaction and identity data
- 3.5% fraud rate (severely imbalanced)
- Two raw files: `train_transaction.csv` and `train_identity.csv`

---

## Project Architecture
```
Raw Data (Kaggle)
      ↓
AWS S3 — Raw Layer
s3://bucket/fraud-detection/raw/
      ↓
AWS Glue Notebook — EDA + Feature Engineering
      ↓
AWS S3 — Processed Layer
s3://bucket/fraud-detection/processed/
      ↓
ML Pipeline (sklearn, XGBoost)
      ↓
AWS S3 — Curated Layer + Model Output
      ↓
Tableau Dashboard — Fraud Pattern Visualization
```

---

## Project Phases

| Phase | Focus | Status |
|-------|-------|--------|
| Week 1 | Data ingestion, EDA, feature engineering | ✅ In Progress |
| Week 2 | Statistical analysis, hypothesis testing | 🔲 Upcoming |
| Week 3 | Unsupervised learning — PCA + clustering | 🔲 Upcoming |
| Week 4 | Supervised learning — fraud prediction model | 🔲 Upcoming |
| Week 5 | AI integration — LLM insight generation | 🔲 Upcoming |
| Week 6 | Visualization + portfolio output | 🔲 Upcoming |

---

## Key Findings So Far

### Day 1 — EDA + Feature Engineering

**Class Imbalance**
- Only 2.65% of transactions are fraudulent
- Accuracy is a misleading metric — precision and recall are the evaluation standard

**H1 Validated — Identity Inconsistency Predicts Fraud**
- Transactions with missing address data show a **5.4x higher fraud rate** (10.3% vs 1.9%)
- Fully anonymous transactions (all 4 identity fields missing) show **38.9% fraud rate** vs 2.65% baseline

**Key Insight — Non-Linear Fraud Distribution**
- identity_null_count follows a U-shaped fraud distribution, not linear
- 1 missing field = lowest fraud rate (1.7%) — the "sweet spot" sophisticated fraudsters exploit
- 0 missing fields AND 4 missing fields are both high-risk for different reasons

**Engineered Features**
- `is_addr_missing` — binary flag for missing address
- `is_identity_complete` — all 4 identity fields present
- `is_identity_empty` — all 4 identity fields missing

---

## Tech Stack

| Layer | Tools |
|-------|-------|
| Storage | AWS S3 |
| Processing | AWS Glue, Python, pandas |
| Query | AWS Athena |
| ML | scikit-learn, XGBoost |
| Visualization | Tableau, matplotlib, seaborn |
| AI Layer | Claude API / OpenAI API (Week 5) |

---

## How to Run
```bash
# Clone the repo
git clone https://github.com/shakamartin1/fraud-detection-pipeline

# Download dataset from Kaggle
# kaggle.com/competitions/ieee-fraud-detection/data

# Upload to S3
aws s3 cp train_transaction.csv s3://your-bucket/fraud-detection/raw/
aws s3 cp train_identity.csv s3://your-bucket/fraud-detection/raw/
```

---

## What's Next

- Join transaction + identity datasets
- Statistical hypothesis testing on transaction amounts
- PCA dimensionality reduction on 394 features
- XGBoost fraud prediction model
- LLM-generated insight summaries

---

## Author

**Shukura Martin**
Data Engineer | Data Scientist in Progress
[LinkedIn](https://linkedin.com/in/yourprofile) | [GitHub](https://github.com/shakamartin1)

> *This project is part of a 45-day focused upskilling sprint in data engineering, data science, and AI/ML.*
