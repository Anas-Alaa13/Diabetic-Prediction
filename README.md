# Diabetes Readmission Prediction Analysis and Modeling Report

## 1. Introduction
This report presents a comprehensive analysis of a diabetes readmission prediction project, utilizing a dataset containing patient records to predict hospital readmissions within 30 days.

The analysis includes:
- Data preprocessing  
- Exploratory Data Analysis (EDA)  
- Feature selection  
- Model development  
- Model comparison  

The goal is to identify key factors influencing readmission and develop a predictive model to assist healthcare providers in risk assessment.

---

## 2. Data Preprocessing

### 2.1 Initial Data Loading
The dataset contains **101,766 patient records** with **50 features**, including:
- Demographic details  
- Medical history  
- Hospital stay information  

Key steps:
- Imported libraries: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`
- Loaded dataset using `pandas.read_csv`

---

### 2.2 Missing Value Handling
- Dropped:
  - `max_glu_serum` (94,420 missing)
  - `A1Cresult` (84,748 missing)
- Replaced `'?'` with `NaN`
- Dropped rows with missing target (`readmitted`)

---

### 2.3 Feature Engineering
- Created binary target:
  - `1` → readmitted within 30 days (`<30`)
  - `0` → otherwise
- Identified:
  - **Numeric features**: `time_in_hospital`, `num_lab_procedures`
  - **Categorical features**: `race`, `gender`

---

### 2.4 Feature Selection
Used **SelectKBest (ANOVA F-test)** to select top 5 features:

- `number_inpatient`
- `discharge_disposition_id`
- `time_in_hospital`
- `num_medications`
- `number_diagnoses`

---

## 3. Exploratory Data Analysis (EDA)

### 3.1 Key Insights
- **Class imbalance**: ~11% readmitted within 30 days  
- Important features:
  - `number_inpatient` → strongest correlation  
  - `time_in_hospital` → longer stay = higher risk  
  - `discharge_disposition_id` → certain categories increase risk  

---

### 3.2 Visualizations
- Histograms (numeric features)
- Bar plots (categorical features)
- Correlation matrix:
  - strongest positive correlation → `number_inpatient`

---

## 4. Model Development

### 4.1 Models Implemented
- Logistic Regression (`max_iter=1000`)
- Support Vector Machine (SVM)
- Random Forest (`n_estimators=100`)
- XGBoost
- Decision Tree (`criterion='entropy'`)

---

### 4.2 Data Preparation
- Encoding → `LabelEncoder`
- Scaling → `StandardScaler`
- Train/Test Split:
  - 80% training
  - 20% testing
  - `random_state=42`

---

### 4.3 Model Evaluation
- Decision Tree:
  - Accuracy: **89.50%**
  - F1-score: **0.89**
- Other models:
  - Random Forest & XGBoost outperformed linear models

---

## 5. Model Comparison and Tuning

### 5.1 Comparison

| Model                | Accuracy | Notes |
|---------------------|----------|------|
| Decision Tree       | 89.50%   | Balanced but may overfit |
| Logistic Regression | ~85%     | Simple, interpretable |
| SVM                 | ~83%     | Computationally expensive |
| Random Forest       | ~87%     | Robust, handles non-linearity |
| XGBoost             | ~88%     | High performance |

---

### 5.2 Tuning Strategies
- **Decision Tree**
  - Tune: `max_depth`, `min_samples_leaf`

- **Logistic Regression**
  - Tune: `C` (regularization)

- **SVM**
  - Tune: `kernel`, `C`

- **Random Forest**
  - Tune: number of trees, depth

- **XGBoost**
  - Tune:
    - learning rate
    - max depth
    - subsampling

---

## 6. Final Summary and Insights

### 6.1 Key Outcomes
- Decision Tree achieved strong performance (**89.5%**)
- Best predictors:
  - `number_inpatient`
  - `time_in_hospital`
  - `discharge_disposition_id`
- Tkinter app enables:
  - Model training
  - Prediction interface

---

### 6.2 Insights
- **Clinical impact**
  - Helps identify high-risk patients
  - Enables targeted interventions

- **Model recommendation**
  - Use **Random Forest** or **XGBoost** in production

- **Future improvements**
  - Hyperparameter tuning
  - Handle imbalance (e.g., SMOTE)
  - Add external data

---

### 6.3 Conclusion
The project successfully developed a high-accuracy predictive model with actionable insights.

The Tkinter application enhances usability, enabling healthcare providers to make data-driven decisions and reduce readmission rates.
