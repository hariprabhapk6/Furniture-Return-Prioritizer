# Furniture Return Prioritizer

## Project Overview

The Furniture Return Prioritizer is a data analytics and machine learning project designed to help prioritize furniture returns for inspection.

The system combines return information, product value, severity, safety, transit duration, SLA urgency, and condition-related signals to identify which returned products should receive higher inspection priority.

The project includes:

- Data quality analysis
- Data cleaning
- Feature engineering
- Rule-based baseline prioritization
- Machine learning classification
- Model evaluation
- Trade-off analysis
- Business insights and recommendations

The final machine learning model uses only information that is available before inspection. Post-inspection value-loss information is excluded from the model to prevent data leakage.

---

## Business Problem

Furniture returns may differ significantly in terms of:

- Product value
- Return reason
- Condition
- Severity
- Safety risk
- Transit duration
- SLA urgency

Because inspection resources are limited, every returned product cannot necessarily receive the same level of attention.

The objective of this project is to support the inspection team by identifying higher-risk returns and providing a structured prioritization approach.

The project provides two complementary approaches:

1. A rule-based baseline prioritizer for operational decision-making.
2. A machine learning model for predicting inspection outcomes.

---

## Project Objectives

The main objectives are:

1. Analyze the quality and structure of the furniture return dataset.
2. Clean and standardize the raw data.
3. Create meaningful risk-related features.
4. Develop a rule-based return prioritization system.
5. Build a machine learning model to predict inspection outcomes.
6. Evaluate the model using multiple performance measures.
7. Analyze operational trade-offs and potential exposure.
8. Generate business insights and recommendations.
9. Prevent data leakage by using only pre-inspection information for machine learning.

---

## Dataset

The raw dataset contains **5,195 rows and 12 columns**.

During data cleaning:

- 15 completely blank rows were removed.
- 123 duplicate rows were identified and removed.
- The final cleaned dataset contains **5,057 valid return records**.

The final dataset is used consistently throughout the analytical workflow.

---

## Data Cleaning

The following cleaning steps were performed:

1. Loaded the raw Excel dataset.
2. Created a separate copy for cleaning.
3. Removed completely blank rows before filling missing values.
4. Checked missing values.
5. Identified duplicate records.
6. Converted numerical columns into appropriate numeric data types.
7. Standardized categorical columns.
8. Removed unnecessary whitespace.
9. Standardized categorical text formatting.
10. Filled missing categorical and numerical values using appropriate cleaning rules.
11. Verified the final cleaned dataset.

Final cleaned dataset:

**5,057 records**

---

## Feature Engineering

Additional features were created to support prioritization and machine learning.

### Risk Features

- Value Risk Score
- Severity Score
- Safety Score
- Condition Risk Score
- Transit Risk Score
- SLA Urgency Score

### Priority Features

- Priority Score
- Priority
- Priority Evidence

These features combine business rules and available return information to support inspection prioritization.

---

## Baseline Prioritizer

A rule-based baseline prioritizer was developed using the following weighted factors:

| Factor | Weight |
|---|---:|
| Value Risk | 30% |
| Severity Risk | 20% |
| Safety Risk | 20% |
| Transit Risk | 15% |
| SLA Urgency | 10% |
| Condition Risk | 5% |

The baseline score is used to classify returns into:

- High
- Medium
- Low

### Final Baseline Distribution

| Priority | Number of Returns |
|---|---:|
| High | 341 |
| Medium | 2,384 |
| Low | 2,332 |
| **Total** | **5,057** |

The baseline prioritizer provides an interpretable and business-rule-based approach for inspection planning.

---

## Machine Learning Model

A **Random Forest Classifier** was developed to predict the inspection outcome.

### Target Variable

The target variable is:

`Inspection Outcome`

The model predicts the following classes:

- Major Damage
- Minor Damage
- No Defect
- Repairable
- Scrap
- Unknown

### Machine Learning Features

The model uses only pre-inspection features:

- Product
- Value ₹
- Transit Days
- Return Reason
- Condition Hint
- Severity
- Safety
- SLA hrs
- Resale Before ₹
- Severity Score
- Safety Score
- Condition Risk Score
- Transit Risk Score
- SLA Urgency Score

---

## Data Leakage Prevention

Data leakage was specifically checked and prevented.

The following post-inspection fields were excluded from the machine learning features:

- Resale After ₹
- Value Loss ₹
- Value Loss %
- Value Loss Risk Score

These values depend on information that is available only after inspection.

Using them as model inputs would give the model information that would not be available at the time of prioritization.

Therefore, the final machine learning model uses only information available before inspection.

---

## Model Configuration

The final model uses a Random Forest Classifier with:

- Number of trees: 200
- Maximum depth: 15
- Minimum samples split: 5
- Minimum samples leaf: 2
- Random state: 42
- Class weight: Balanced

Categorical features are processed using One-Hot Encoding.

Numerical features are passed through without categorical encoding.

The dataset is divided using:

- Training data: 80%
- Testing data: 20%
- Random state: 42
- Stratified split

Final split:

- Training samples: **4,045**
- Testing samples: **1,012**

---

## Model Performance

The final Random Forest model achieved:

| Metric | Result |
|---|---:|
| Accuracy | **77.37%** |
| Macro F1 Score | **0.494** |
| Weighted F1 Score | **0.785** |

The weighted F1 score is higher than the macro F1 score because the dataset contains class imbalance and the model performs much better on some classes than others.

The model performs particularly well for the `No Defect` and `Minor Damage` classes, while minority classes such as `Unknown`, `Scrap`, and `Major Damage` remain more difficult to predict.

---

## Critical Model Errors

The project gives additional attention to high-risk inspection outcomes.

### Major Damage

- Correct predictions: 23
- Total major damage cases: 49
- Misclassified cases: **26**

### Scrap

- Correct predictions: 13
- Total scrap cases: 38
- Misclassified cases: **25**

These errors are important because incorrectly identifying severe outcomes can have greater operational consequences than errors involving lower-risk classes.

---

## Model Feature Importance

The most influential features in the final Random Forest model include:

- Severity Score
- Resale Before ₹
- Condition Hint
- Value ₹
- Severity
- Transit Days
- Condition Risk Score

Feature importance is used to understand which available pre-inspection signals contribute most to the model's predictions.

Feature importance should be interpreted as a model-level signal and not as proof of direct causation.

---

## Trade-off Analysis

The project also evaluates operational trade-offs related to return prioritization.

The analysis considers:

- Priority distribution
- Product value
- SLA urgency
- Transit duration
- Safety risk
- Severity risk
- Condition risk
- Illustrative holding cost
- Operational exposure

The holding-cost analysis uses an **illustrative assumption** and is not presented as an actual company cost.

The trade-off analysis is intended to support operational decision-making rather than provide an exact financial forecast.

---

## Business Insights

The analysis provides several useful business insights:

1. A relatively small group of returns receives High priority, allowing inspection resources to focus on more critical cases.

2. Product value is an important consideration when deciding which returns may require faster attention.

3. Severity and safety-related signals are important for identifying potentially critical returns.

4. Transit duration and SLA urgency can contribute to prioritization and model prediction.

5. Condition-related information provides useful signals before inspection.

6. The machine learning model can support inspection planning, but it should not completely replace human inspection decisions.

7. Minority outcomes such as Scrap and Major Damage remain challenging for the model and require additional monitoring.

---

## Business Recommendations

Based on the analysis, the following recommendations are proposed:

### 1. Prioritize High-Risk Returns

High-priority returns should receive earlier inspection attention when operational capacity is limited.

### 2. Use Safety and Severity Signals

Safety and severity indicators should receive strong consideration because they can represent higher operational risk.

### 3. Consider Product Value

Higher-value products can be prioritized when inspection resources are limited.

### 4. Monitor SLA Urgency

Returns approaching their SLA deadline should receive appropriate attention to reduce operational delays.

### 5. Use ML as Decision Support

The Random Forest model should be used as a supporting tool rather than as a replacement for human inspection decisions.

### 6. Monitor Critical Classes

Major Damage and Scrap predictions should be monitored carefully because misclassification of these classes can have higher operational consequences.

### 7. Improve Minority-Class Data

Additional examples and better-quality information for minority outcomes may help improve model performance.

---

## Project Limitations

The project has several limitations:

1. The dataset may not represent all real-world furniture return scenarios.

2. The machine learning model predicts inspection outcomes based on the available historical data and may not generalize perfectly to new situations.

3. Minority classes such as Scrap and Unknown have relatively fewer examples, which affects model performance.

4. The illustrative holding-cost assumption should not be treated as an actual company financial estimate.

5. Model predictions can be affected by the quality and completeness of pre-inspection information.

6. Feature importance represents model behavior and should not be interpreted as causal relationships.

7. Human inspection remains important for final operational decisions.

---

## Project Workflow

The project is organized into eight analytical notebooks.

### Notebook 01 — Data Quality

Analyzes:

- Dataset structure
- Data types
- Missing values
- Duplicate records
- Basic data quality issues

### Notebook 02 — Data Cleaning

Performs:

- Blank-row removal
- Duplicate identification and removal
- Data type conversion
- Categorical standardization
- Missing-value handling
- Cleaning validation

### Notebook 03 — Feature Engineering

Creates:

- Value Risk Score
- Severity Score
- Safety Score
- Condition Risk Score
- Transit Risk Score
- SLA Urgency Score
- Priority Score
- Priority
- Priority Evidence

### Notebook 04 — Baseline Prioritizer

Builds the weighted rule-based prioritization system and ranks returns according to inspection priority.

### Notebook 05 — Machine Learning Model

Builds and trains the Random Forest model for inspection outcome prediction.

### Notebook 06 — Model Evaluation

Evaluates the model using:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix
- Major Damage errors
- Scrap errors
- Cost-weighted error analysis
- Model confidence
- Feature importance

### Notebook 07 — Trade-off Analysis

Analyzes:

- Priority distribution
- Product value
- SLA urgency
- Transit duration
- Safety risk
- Severity risk
- Condition risk
- Illustrative holding cost
- Operational exposure

### Notebook 08 — Business Insights

Generates:

- Overall return statistics
- High-priority return profile
- Product-level analysis
- Return-reason analysis
- Inspection outcome analysis
- Model feature importance
- Model performance summary
- Critical model errors
- Business insights
- Business recommendations
- Project limitations

---

## Project Structure

```text
Furniture-Return-Prioritizer/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── Raw/
│   └── Processed/
│
├── models/
│   └── random_forest_inspection_model.pkl
│
└── Notebooks/
    ├── 01_data_quality.ipynb
    ├── 02_data_cleaning.ipynb
    ├── 03_feature_engineering.ipynb
    ├── 04_baseline_prioritizer.ipynb
    ├── 05_ml_model.ipynb
    ├── 06_model_evaluation.ipynb
    ├── 07_tradeoff_analysis.ipynb
    └── 08_business_insights.ipynb