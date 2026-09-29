# Customer Churn Prediction – Supervised Learning

## Project Overview

This project is a hands-on supervised learning project focused on **Customer Churn Prediction** using a messy real-world customer dataset.

A subscription-based company is experiencing customer churn and wants to identify customers who are likely to leave so that the retention team can take preventive action.

As a Junior Data Scientist, the objective was to clean the raw customer data, explore churn patterns, build multiple classification models, compare their performance, and select a suitable final model based on business requirements.

---

## Business Objective

Build a supervised machine learning solution that predicts whether a customer is likely to churn (**Churn = Yes/No**) and evaluate the model on unseen data.

The project also aims to identify customer characteristics associated with higher churn and provide actionable recommendations for the retention team.

---

## Dataset

**Dataset:** Supervised_Learning_Messy_Customer_Churn.csv

* Original records: 184
* Records after removing exact duplicates: 180
* Target variable: `Churn`
* Problem type: **Binary Classification**

The dataset contains customer information related to:

* Demographics
* Usage
* Billing
* Services
* Contract type
* Satisfaction
* Customer support interactions

The dataset intentionally contains common real-world data-quality issues.

---

## Data Cleaning

The following data-quality issues were investigated and handled:

* Missing values
* Duplicate records
* Invalid numerical values
* Outliers
* Inconsistent categorical labels
* Capitalization and whitespace inconsistencies
* Placeholder values such as `N/A`, `NA`, and `?`
* Unrealistic or impossible numerical values

Cleaning decisions were made based on the context of the data rather than simply deleting unusual records.

`Customer_ID` was not used as a predictive feature because it is an identifier rather than a meaningful customer characteristic.

---

## Exploratory Data Analysis

The analysis investigated relationships between customer characteristics and churn, including:

* Contract type vs. churn
* Satisfaction vs. churn
* Tenure vs. churn
* Monthly charge vs. churn
* Support interactions vs. churn
* Data usage vs. churn

### Key Business Insights

1. **Contract type is strongly associated with churn.**
   Monthly-contract customers had an observed churn rate of **62.50%**, compared with **20.83%** for 2-year contracts.

2. **Customer satisfaction is associated with churn.**
   Customers with a satisfaction score of 10 had an observed churn rate of **29.41%**, compared with **69.23%** at a score of 3.

3. **Frequent support interactions are associated with higher churn.**
   Customers with 6 or more support calls in the last three months had an observed churn rate of **78.57%**.

4. **Higher data usage was associated with higher churn.**
   The highest data-usage quartile had an observed churn rate of **62.22%**, compared with **44.44%** in the lowest quartile.

These findings represent observed associations in the dataset and should not be interpreted as proof of causation.

---

## Machine Learning Models

Four supervised classification models were implemented and evaluated:

* Logistic Regression
* K-Nearest Neighbors (KNN)
* Decision Tree
* Random Forest

The models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Cross-validation F1-score

---

## Model Comparison

| Model                   | Test Accuracy | Test Precision | Test Recall |    Test F1 | Mean CV F1 | CV-Test F1 Difference |
| ----------------------- | ------------: | -------------: | ----------: | ---------: | ---------: | --------------------: |
| **Logistic Regression** |    **0.6111** |     **0.6667** |  **0.5263** | **0.5882** | **0.6507** |            **0.0625** |
| KNN                     |        0.4444 |         0.4667 |      0.3684 |     0.4118 |     0.6025 |                0.1907 |
| Decision Tree           |        0.5000 |         0.5333 |      0.4211 |     0.4706 |     0.5838 |                0.1132 |
| Random Forest           |        0.5556 |         0.6000 |      0.4737 |     0.5294 |     0.5674 |                0.0380 |

---

## Final Model – Logistic Regression

**Logistic Regression** was selected as the final model based on the overall evaluation results.

It achieved:

* **Test Accuracy:** 61.11%
* **Test Precision:** 66.67%
* **Test Recall:** 52.63%
* **Test F1-score:** 58.82%
* **Mean Cross-Validation F1-score:** 65.07%

The model also showed a relatively smaller difference between its cross-validation and test F1-score compared with KNN and Decision Tree.

Since the business wants to identify customers who may churn, **recall is particularly important** because missing a genuine churner can result in a lost customer.

An exploratory threshold of **0.30** increased recall to **73.68%**, showing that the model can identify more potential churners when the business prioritizes reducing missed churn cases. However, this can also increase false-positive alerts.

---

## Business Recommendations

### 1. Focus on Monthly-Contract Customers

Monthly-contract customers showed a substantially higher observed churn rate.

The company can consider:

* Targeted retention offers
* Contract upgrade options
* Incentives for longer-term plans

### 2. Proactively Engage Customers with Frequent Support Interactions

Customers with 6 or more support calls showed substantially higher observed churn.

The retention team can prioritize these customers for:

* Service-quality reviews
* Proactive follow-up
* Issue resolution

### 3. Monitor Customers with Low Satisfaction

Lower satisfaction was generally associated with higher churn.

The company can use:

* Customer feedback
* Service recovery
* Satisfaction-improvement initiatives

to address potential churn risks.

### 4. Use Churn Predictions for Retention Prioritization

The Logistic Regression model can be used as a **screening tool** to identify customers with a higher predicted probability of churn.

A lower classification threshold can be considered when the business wants to identify more potential churners, while accepting that this may generate more false-positive alerts.

### 5. Continuously Evaluate the Model

The current dataset is relatively small. The model should be monitored and retrained as more customer data becomes available.

Future performance should be validated on genuinely unseen and more recent customer data before operational deployment.

---

## Limitations

### Small Dataset

After removing exact duplicate records, the dataset contains only **180 customer records**. A larger dataset would provide more reliable estimates of model performance.

### Data Quality

The original dataset contained missing values, inconsistent categorical labels, placeholders, and unusual numerical values. These were investigated and cleaned, but some unusual observations were retained when they were not clearly invalid.

### Limited Generalization

The evaluation is based on one held-out test set and cross-validation on the training data. Performance on a different customer population may vary.

### Preprocessing Limitation

Missing values were imputed before the train-test split during the cleaning stage.

For a fully leakage-free production workflow, imputation should be performed inside a preprocessing pipeline using statistics learned only from the training data.

### Threshold Analysis Limitation

The classification threshold comparison was performed on the held-out test set for exploratory purposes.

A final production threshold should be selected using validation data and business costs before deployment.

### Association Does Not Imply Causation

The EDA findings show relationships between customer characteristics and observed churn, but they do not establish that these factors directly cause customers to churn.

### Further Validation Required

Before operational use, the model should be tested on a larger and more recent dataset and monitored over time.

---

## Project Workflow

```text
Raw Customer Dataset
        ↓
Initial Data Inspection
        ↓
Data Cleaning
        ↓
Exploratory Data Analysis
        ↓
Feature Engineering
        ↓
Train-Test Split
        ↓
Model Training
        ↓
Cross-Validation
        ↓
Model Comparison
        ↓
Final Model Selection
        ↓
Business Insights & Recommendations
```

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook
* VS Code

---

## Project Files

| File                                    | Description                                                          |
| --------------------------------------- | -------------------------------------------------------------------- |
| `Business_Use_Case.pdf`                 | Original business use case and project requirements                  |
| `supervised_learning.ipynb`             | Complete data analysis, preprocessing, model building and evaluation |
| `cleaned_dataset.csv`                   | Cleaned customer churn dataset                                       |
| `Supervised_Learning_Presentation.pptx` | Project presentation                                                 |
| `README.md`                             | Project documentation                                                |

---

## Conclusion

This project demonstrates the complete application of supervised machine learning to a real-world customer churn problem.

Multiple classification models were implemented and compared using test-set metrics and cross-validation. **Logistic Regression** was selected as the final model based on its overall performance and relatively stable validation results.

The model can be used as a screening tool to help the retention team prioritize customers who may be at higher risk of churn. However, due to the small dataset and preprocessing limitations, further validation on a larger and more recent dataset is required before production deployment.
