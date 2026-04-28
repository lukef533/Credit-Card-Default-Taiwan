# 💳 Credit Card Default Prediction

Using Machine Learning to Identify High-Risk Borrowers

## 📌 Table of Contents

* [Overview](#overview)
* [Project Objective](#project-objective)
* [Dataset](#dataset)
* [Repository Contents](#repository-contents)
* [Project Workflow](#project-workflow)
* [Models Used](#models-used)
* [Model Performance](#model-performance)
* [Key Findings](#key-findings)
* [Conclusions](#conclusions)
* [Limitations](#limitations)
* [Future Improvements](#future-improvements)
* [Tools & Libraries](#tools--libraries)
* [Author](#author)

---

## 📖 Overview

This project explores how machine learning can be used to predict whether a credit card client will default on their next month’s payment. Using the **Default of Credit Card Clients Dataset (Taiwan, 2005)** from the UCI Machine Learning Repository, the goal was to identify high-risk borrowers early so lenders can reduce financial losses and improve credit risk decision-making.

The project compares multiple classification models and evaluates their ability to distinguish likely defaulters from non-defaulters using financial history, payment behavior, and demographic information.

---

## 🎯 Project Objective

**Research Question:**
Can machine learning predict which credit card customers will default before they miss a payment?

### Why This Matters

Credit card defaults cost financial institutions billions annually. Traditional credit scoring methods such as FICO scores and rule-based lending decisions often miss early warning signs. Machine learning models can detect complex behavioral patterns across many variables simultaneously, enabling earlier and more accurate intervention.

---

## 📊 Dataset

**Source:** UCI Machine Learning Repository
**Dataset:** Default of Credit Card Clients Dataset (Taiwan, 2005)

### Dataset Summary

* **30,000 customer records**
* **25 total features** (after preprocessing and feature engineering)
* **22% default rate**
* Binary target variable: **Default next month (Yes/No)**

### Key Feature Groups

#### Demographics

* Age
* Sex
* Education
* Marital Status

#### Credit Information

* Credit limit (`LIMIT_BAL`)
* Payment history across 6 months (`PAY_0`–`PAY_6`)

#### Financial Activity

* Bill statement amounts (`BILL_AMT1`–`BILL_AMT6`)
* Previous payment amounts (`PAY_AMT1`–`PAY_AMT6`)

#### Target Variable

* `DEFAULT` → whether the client defaulted the following month

---

## 📁 Repository Contents

```text
├── dataset/
│   └── default_of_credit_card_clients.csv
│
├── notebook/
│   └── INBM300_Taiwan_Credit_Card_Default.ipynb
│
├── poster/
│   └── INBM300 Credit Card Default Poster.pdf
│
├── proposal/
│   └── INBM300 Credit Default Proposal.pdf
│
└── README.md
```

### Included Files

* **Dataset** – raw project dataset used for analysis
* **Jupyter Notebook** – complete workflow including cleaning, EDA, feature engineering, modeling, and evaluation
* **Final Poster** – presentation-ready summary of findings
* **Original Proposal** – initial project scope, research question, and methodology plan

---

## ⚙️ Project Workflow

### 1. Data Loading & Inspection

* Loaded and reviewed dataset structure
* Checked dimensions, data types, and missing values
* Verified class imbalance in target variable

### 2. Data Cleaning

* Renamed columns for clarity
* Removed **35 duplicate records**
* Standardized unusual category values in Education and Marital Status
* Encoded categorical variables for modeling

### 3. Exploratory Data Analysis (EDA)

* Visualized target imbalance
* Examined default behavior across demographics
* Analyzed credit limits, payment status, and payment trends
* Investigated feature correlations

### 4. Feature Engineering

Created four summary features to better capture repayment behavior:

#### Average Payment Status

Average payment delay across all six months

#### Total Bill Amount

Total outstanding balance across all statements

#### Total Payment Amount

Total amount repaid by the client

#### Payment Ratio

Fraction of total bill actually paid

A lower payment ratio often indicates higher default risk.

### 5. Modeling & Evaluation

Three classification models were trained using a **70/30 train-test split**.

To address class imbalance, all models used:

```python
class_weight='balanced'
```

---

## 🤖 Models Used

### Logistic Regression

Interpretable baseline model that works like a weighted scoring system.

### Random Forest

Ensemble of decision trees capable of capturing non-linear relationships.

### LightGBM

Gradient boosting framework optimized for speed and predictive performance.

This model produced the strongest overall results.

---

## 📈 Model Performance

| Model               | Accuracy | Precision | Recall | F1 Score |   ROC-AUC |
| ------------------- | -------: | --------: | -----: | -------: | --------: |
| Logistic Regression |    0.814 |     0.727 |  0.253 |    0.376 |     0.719 |
| Random Forest       |    0.811 |     0.639 |  0.339 |    0.443 |     0.755 |
| **LightGBM** ⭐      |    0.760 |     0.467 |  0.594 |    0.523 | **0.767** |

### Why ROC-AUC Matters

Accuracy alone can be misleading with imbalanced datasets. ROC-AUC better measures how well a model separates defaulters from non-defaulters.

LightGBM achieved the highest ROC-AUC and the best balance between recall and precision.

---

## 🔍 Key Findings

### Strongest Predictor: Payment History

Clients with delayed or missed payments were significantly more likely to default.

### Lower Credit Limits = Higher Risk

Customers with lower credit limits showed higher default rates.

### Bill and Payment Amounts Were Highly Correlated

Feature engineering helped summarize these relationships more effectively.

### Demographics Were Less Predictive

Age, sex, education, and marital status showed weaker predictive power compared to payment behavior.

---

## ✅ Conclusions

**LightGBM was the best-performing model** for predicting credit card default.

It provided the strongest ROC-AUC score and the best balance of identifying actual defaulters without generating excessive false positives.

This supports the broader conclusion that machine learning can outperform traditional linear methods when predicting borrower risk, especially when recent payment behavior is included.

---

## ⚠️ Limitations

### Dataset Age

The dataset is from Taiwan in 2005. Lending behavior and credit markets have changed significantly since then.

### Geographic Generalization

Results may not directly transfer to modern U.S. borrowers or other lending environments.

### Class Imbalance

Only 22% of customers defaulted, making minority class prediction more difficult.

### Interpretability vs Accuracy

More powerful models like LightGBM improve performance but are harder to explain compared to logistic regression.

---

## 🚀 Future Improvements

Potential next steps for expanding this project:

* Hyperparameter tuning for LightGBM
* Cross-validation for stronger model validation
* SHAP values for model explainability
* Threshold optimization based on business risk tolerance
* Testing modern lending datasets for stronger real-world relevance

---

## 🛠 Tools & Libraries

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* LightGBM
* Jupyter Notebook

---

## 👤 Author

**Luke Finkielstein**
INBM300 – Data Analytics / Machine Learning Project
