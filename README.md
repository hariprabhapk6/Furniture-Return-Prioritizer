# Furniture Return Prioritizer

## Return-to-Inspection Prioritization Based on Value Loss and Product Condition Risk

## 📌 Project Overview

Furniture companies receive a large number of returned products with different levels of damage, value loss, safety concerns, transit duration, and inspection urgency.

Treating every returned product with the same inspection priority can lead to inefficient use of inspection resources and delays in handling critical returns.

This project develops a data-driven system to analyze furniture returns, prioritize them based on risk, and predict inspection outcomes using Machine Learning.

---

## 🎯 Objectives

- Analyze the quality of furniture return data.
- Clean inconsistent and missing data.
- Engineer meaningful risk-based features.
- Develop a rule-based baseline prioritization system.
- Rank furniture returns based on inspection priority.
- Predict inspection outcomes using Machine Learning.
- Support better decision-making for inspection teams.

---

## 🔄 Project Workflow

Raw Furniture Return Data  
↓  
Data Quality Analysis  
↓  
Data Cleaning  
↓  
Feature Engineering  
↓  
Rule-Based Baseline Prioritization  
↓  
Machine Learning Model  
↓  
Inspection Outcome Prediction

---

## 📂 Project Structure

```text
Furniture-Return-Prioritizer/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── Raw/
│   │   └── Raw furniture return dataset
│   │
│   └── Processed/
│       ├── Processed CSV files
│       ├── Cleaned dataset
│       ├── Feature-engineered dataset
│       └── Prioritized / ML-ready dataset
│
├── models/
│   └── random_forest_inspection_model.pkl
│
└── Notebooks/
    ├── 01_data_quality.ipynb
    ├── 02_data_cleaning.ipynb
    ├── 03_feature_engineering.ipynb
    ├── 04_baseline_prioritizer.ipynb
    └── 05_ml_model.ipynb
```

---

## 📊 Dataset

The dataset contains furniture return records with information related to product value, condition, return reasons, safety risks, and inspection outcomes.

### Main Features

| Feature | Description |
|---|---|
| Return ID | Unique identifier for each return |
| Product | Type of furniture product |
| Value ₹ | Original product value |
| Transit Days | Number of days required for transit |
| Return Reason | Reason for product return |
| Condition Hint | Description of product condition |
| Severity | Damage severity |
| Safety | Safety risk level |
| SLA hrs | Required processing time |
| Inspection Outcome | Final inspection result |
| Resale Before ₹ | Product resale value before inspection |
| Resale After ₹ | Product resale value after inspection |

---

## 🔍 1. Data Quality Analysis

The dataset was analyzed for:

- Missing values
- Duplicate records
- Data type inconsistencies
- Invalid numeric values
- Categorical inconsistencies
- Dataset structure and column validation

**Notebook:** `01_data_quality.ipynb`

---

## 🧹 2. Data Cleaning

The following preprocessing steps were performed:

- Converted numeric columns into appropriate numeric formats.
- Standardized categorical values.
- Removed unnecessary spaces.
- Converted text values to lowercase.
- Handled missing categorical values using `unknown`.
- Handled missing numeric values.
- Checked duplicate records.
- Corrected inconsistent categorical values.

Example:

`Minor Damage → MINOR DAMAGE → minor damage`

**Notebook:** `02_data_cleaning.ipynb`

---

## ⚙️ 3. Feature Engineering

Several risk-based features were created to support prioritization and Machine Learning.

### Engineered Features

- Value Loss ₹
- Value Loss %
- Value Loss Risk Score
- Severity Score
- Safety Score
- Condition Risk Score
- Transit Risk Score
- SLA Urgency Score

These features convert business and product risks into numerical values for decision-making and model training.

**Notebook:** `03_feature_engineering.ipynb`

---

## 📈 4. Rule-Based Baseline Prioritizer

A weighted scoring system was developed to prioritize furniture returns.

### Priority Factors and Weights

| Factor | Weight |
|---|---:|
| Value Loss Risk Score | 30% |
| Severity Score | 20% |
| Safety Score | 20% |
| Transit Risk Score | 15% |
| SLA Urgency Score | 10% |
| Condition Risk Score | 5% |

Returns are categorized into:

- 🔴 High Priority
- 🟡 Medium Priority
- 🟢 Low Priority

### Baseline Prioritization Results

**Total Returns: 5,058**

| Priority | Number of Returns |
|---|---:|
| Low | 3,136 |
| Medium | 1,525 |
| High | 397 |

**Notebook:** `04_baseline_prioritizer.ipynb`

---

## 🤖 5. Machine Learning Model

### Algorithm Used

**Random Forest Classifier**

The model predicts the inspection outcome based on product information, value loss, severity, safety, condition, resale values, and engineered risk features.

### Dataset Split

| Dataset | Samples |
|---|---:|
| Training Data | 4,046 |
| Testing Data | 1,012 |

### Target Classes

- major damage
- minor damage
- no defect
- repairable
- scrap
- unknown

### Model Performance

🎯 **Accuracy: 89.43%**

### Top Important Features

1. Value Loss %
2. Severity Score
3. Resale After ₹
4. Severity
5. Condition Hint
6. Resale Before ₹
7. Value Loss Risk Score

The trained model is saved as:

`models/random_forest_inspection_model.pkl`

**Notebook:** `05_ml_model.ipynb`

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Joblib
- Jupyter Notebook
- Matplotlib
- OpenPyXL

---

## 📦 Installation

Clone the repository:

```bash
git clone <repository-url>
```

Navigate to the project directory:

```bash
cd Furniture-Return-Prioritizer
```

Install required libraries:

```bash
pip install -r requirements.txt
```

---

## ▶️ How to Run

Run the notebooks in the following order:

1. `01_data_quality.ipynb`
2. `02_data_cleaning.ipynb`
3. `03_feature_engineering.ipynb`
4. `04_baseline_prioritizer.ipynb`
5. `05_ml_model.ipynb`

---

## 📈 Current Results

The project currently demonstrates:

- ✅ Data quality analysis
- ✅ Data cleaning and standardization
- ✅ Feature engineering
- ✅ Risk-based scoring
- ✅ Rule-based prioritization
- ✅ Inspection ranking
- ✅ Machine Learning classification
- ✅ Random Forest model with 89.43% accuracy
- ✅ Saved trained ML model

---

## 🚀 Future Improvements

- Hyperparameter tuning
- Comparison with additional ML models
- Explainable AI for prediction reasoning
- Cost and service trade-off analysis
- Emission-aware prioritization
- Interactive dashboard
- Real-time prioritization
- Model deployment

---

## 👩‍💻 Author

**Hariprabha**

Computer Science and Engineering