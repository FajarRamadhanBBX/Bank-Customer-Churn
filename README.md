# Customer Churn Prediction 📊

This project aims to analyze customer data to identify key factors leading to churn and to build a predictive model to detect at-risk customers. The primary goal is to provide actionable insights that can help in developing effective customer retention strategies.

## 🎯 Business Problem

The project addresses two business questions:
1.  **What causes customers to churn?**
2.  **How can we improve customer retention?**

## 📈 Key Findings from Exploratory Data Analysis (EDA)

The initial analysis of the dataset revealed a critical insight: **customer complaints are the single strongest predictor of churn.**

* **Complaints and Churn Correlation:** There is a near-perfect correlation between a customer making a complaint (`Complain` = 1) and the customer churning (`Exited` = 1).
* **Statistical Significance:** An astonishing **99.51%** of customers who file a complaint end up churning. Conversely, **99.95%** of customers who do not complain remain with the bank.
* **Other Factors:** Other features such as *Credit Score*, *Card Type*, and *Satisfaction Score* showed no significant difference between customers who churned and those who did not. Interestingly, customers who churned tended to have a **higher average account balance**.

Based on these findings, the core business strategy should be to **proactively prevent and resolve customer complaints**.

## ⚙️ Methodology

Given the strong link between complaints and churn, the modeling approach was pivoted. Instead of predicting churn directly, the model is trained to **predict the likelihood of a customer filing a complaint**. This serves as an early warning system.

### 1. Data Preprocessing

* **Feature Removal:** Dropped irrelevant columns (`RowNumber`, `CustomerId`, `Surname`).
* **Categorical Encoding:**
    * **One-Hot Encoding** was applied to nominal features like `Gender` and `Geography`.
    * **Label Encoding** was used for ordinal features like `Card Type`.
* **Numerical Scaling:** The `RobustScaler` was used to scale numerical features, minimizing the impact of outliers.

### 2. Modeling

* **Algorithm:** An **XGBoost Classifier** was chosen for its performance and robustness in classification tasks.
* **Target Variable:** `Complain`.
* **Hyperparameter Tuning:** `GridSearchCV` was used to find the optimal parameters for the model, which were determined to be `{'criterion': 'gini', 'max_depth': 3}`.
* **Data Split:** The dataset was split into 80% for training and 20% for testing.

## 🚀 Results & Evaluation

The model's performance was evaluated on its ability to predict whether a customer would file a complaint.

The classification report is as follows:
          precision    recall  f1-score   support

     0.0       0.88      0.95      0.91      1568
     1.0       0.73      0.51      0.60       432

accuracy                           0.85      2000

### Interpretation

* The model achieves an overall **accuracy of 85%**.
* However, the **recall for the 'Complain' class (1.0) is 0.51**. This indicates that the model correctly identifies only 51% of the customers who will actually complain. The high number of False Negatives means that the model still misses about half of the at-risk customers.
* While the model is a good starting point, further improvements are needed to increase the recall rate and reduce False Negatives.

## 💡 Conclusion & Recommendations

The analysis conclusively shows that **customer complaints are the primary driver of churn**. Therefore, the most effective retention strategy is to minimize customer dissatisfaction.
