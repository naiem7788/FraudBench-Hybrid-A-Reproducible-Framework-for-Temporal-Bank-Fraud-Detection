# FraudBench-Hybrid

## A reproducible research framework for temporal bank fraud detection

FraudBench-Hybrid is a reproducible research-based framework for temporal bank fraud detection. This repository will include the dataset configuration, leakage-controlled Heavy Hybrid ensemble implementation, experimental evaluation, research results, visual analysis, and necessary components for future research extensions.

## 1. Project Overview

The main goal of this project is to develop a leakage-controlled and temporally robust machine-learning framework for detecting potential fraudulent transactions in banking transactions.

The research uses a Heavy Hybrid ensemble architecture, where predictions from different machine-learning models are combined to generate final predictions using a LightGBM meta-learner.

The entire experimental pipeline follows temporal data separation, feature-level leakage audit, out-of-fold stacking, and validation-only threshold selection.

## 2. Main features of the study

- Temporal bank fraud detection
- Leakage-controlled feature selection
- 15 final Heavy Hybrid features
- 6 heterogeneous base learners
- 5-fold out-of-fold stacking
- LightGBM meta-learner
- Validation-based threshold selection
- Untouched temporal test evaluation
- Reproducible final configuration
- Storage of final model and prediction artifacts

## 3. Final Heavy Hybrid Architecture
### Base Models

1. LightGBM
2. XGBoost
3. ExtraTrees
4. CatBoost
5. Linear SVM
6. MLPs

### Meta-Learner

LightGBM

### OOF Configuration

5-fold out-of-fold stacking

### Final Threshold

0.72

## 4. Final Features

The final Heavy Hybrid model uses 15 features:

1. `hour_of_day`
2. `is_weekend`
3. `is_night_transaction`
4. `customer_age`
5. `credit_score`
6. `account_age_years`
7. `account_balance`
8. `transaction_amount`
9. `num_prev_transactions`
10. `transaction_freq_monthly`
11. `distance_from_home_km`
12. `time_since_last_txn_hrs`
13. `is_international`
14. `failed_attempts`
15. `pin_changed_recently`

## 5. Temporal Data Split

A total of 1,000,000 transaction observations are split into three parts while maintaining temporal ordering:

| Dataset | Samples |
|---|---:|
| Training | 700,000 |
| Validation | 150,000 |
| Temporal Test | 150,000 |

Validation and Test sets were not used for model training.

## 6. Leakage Control

The following variables were not used as model inputs in the Final Heavy Hybrid model:

- `fraud_type`
- `transaction_id`
- `customer_id`
- `transaction_date`
- `transaction_time`
- `is_fraud`

Specifically, `fraud_type` is excluded from the model input because it is target-derived.

## 7. OOF Stacking

A 5-fold Out-of-Fold prediction was used to combine the predictions of the base models.

An OOF prediction was created for each observation in the training data. LightGBM meta-learner was trained using OOF predictions.

Validation and temporal test set were not part of OOF training.

## 8. Final Test Results

Final leakage-controlled heavy hybrid model's locked temporal test performance:

| Metric | Result |
|---|---:|
| Accuracy | 0.902613 |
| Precision | 0.158791 |
| Recall | 0.179876 |
| F1-score | 0.168677 |
| ROC-AUC | 0.707951 |
| PR-AUC | 0.119196 |

Final operating threshold: **0.72**

### Confusion Matrix

| | Predicted Non-Fraud | Predicted Fraud |
|---|---:|---:|
| Actual Non-Fraud | 133,910 | 7,851 |
| Actual Fraud | 6,757 | 1,482 |


## 9. Reproducibility

Important artifacts of the final implementation have been preserved:

- `final_configuration.json`

- `meta_model.pkl`

- `final_test_predictions.csv`

These are the final model configuration, trained meta-model and temporal test predictions preserved for review and reuse.

## 10. Visual Analysis

Various visual figures have been created for the experimental analysis of the study, including:

- Model architecture
- Temporal data split
- Leakage-control workflow
- Model comparison
- ROC curve
- Precision-Recall curve
- Confusion matrix
- False-positive and false-negative error analysis
- Final methodology workflow

## 11. Future Research

The following topics can be researched in the future based on this framework:

- Improved temporal modeling
- Explainable fraud detection
- Cross-dataset evaluation
- Concept-drift analysis
- Real-time fraud detection
- More advanced ensemble architecture
- Deep-learning based fraud detection
- Generalization testing on different datasets and real-world transaction environments


## 12. Research Objectives

The objective of this repository is to provide a transparent, reproducible and future-expandable research foundation for temporal bank fraud detection.
