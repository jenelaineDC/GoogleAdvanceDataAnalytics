# 💼 Employee Attrition Prediction – Salifort Motors

## 🧠 Introduction
In today’s competitive business landscape, retaining skilled employees is vital for operational efficiency and company culture. Salifort Motors began exploring ways to improve employee satisfaction and reduce turnover but lacked the analytical insight to interpret their internal HR data. This project bridges that gap with data-driven solutions.

## 📊 Business Scenario
The HR department collected comprehensive employee data and posed a key question:  
**What factors are most likely to influence an employee’s decision to leave the company?**

Given the costs associated with recruitment, onboarding, and training, the ability to forecast resignations is an invaluable asset. I was approached as a Data Analytics professional to analyze patterns in employee satisfaction and deliver strategic insights that enhance retention efforts.

## 🎯 Project Overview & Deliverables

This project aimed to transform raw employee data into actionable insights for Salifort Motors’ HR department. By applying data cleaning, exploratory analysis, and predictive modeling, I built a machine learning solution to help identify employees most at risk of resignation.

Key deliverables include:
- 📊 A cleaned and well-documented dataset ready for analysis
- 📈 Visualizations of critical attrition patterns to support HR strategies
- 🤖 A predictive model to classify high-risk employees using classification algorithms
- 📝 Data-driven recommendations for improving retention and employee satisfaction

## 📚 Data Dictionary

This project uses a dataset called `HR_capstone_dataset.csv`, which contains self-reported data from employees of a fictitious multinational vehicle manufacturing corporation.

- 🧾 **Total rows:** 14,999 (each row = one employee)
- 📊 **Total columns:** 10

| **Column Name**           | **Data Type** | **Description**                                                                 |
|---------------------------|---------------|---------------------------------------------------------------------------------|
| `satisfaction_level`      | int64         | Employee’s self-reported satisfaction level (range: 0–1)                        |
| `last_evaluation`         | int64         | Score of employee's last performance review (range: 0–1)                        |
| `number_project`          | int64         | Number of projects employee contributes to                                     |
| `average_monthly_hours`   | int64         | Average number of hours worked per month                                       |
| `time_spend_company`      | int64         | Number of years the employee has worked at the company                         |
| `work_accident`           | int64         | Indicates if the employee has had a workplace accident                         |
| `left`                    | int64         | Indicates if the employee left the company (1 = yes, 0 = no)                   |
| `promotion_last_5years`   | int64         | Indicates if employee was promoted in the past five years                      |
| `department`              | str           | The employee's department within the company                                   |
| `salary`                  | str           | The employee’s salary bracket (`low`, `medium`, or `high`)                     |


## 📝 Project Workflow Summary

This notebook outlines a complete data science pipeline applied to employee attrition data. Below are the key stages and techniques explored:

### 📦 1. Data Cleaning
- Checked for missing values, dropping duplicate entries and checking data types
- Performed outlier detection and treatment
- Remove Personally Identifiable Information (PII) from the dataset.
- Encoded categorical variables for modeling

### 📊 2. Exploratory Data Analysis (EDA)
- Visualized feature distributions and correlations
- Analyzed patterns in attrition-related variables
- Highlighted trends using histograms, boxplots, and heatmaps
- Three new features were introduced
  - `overworked` — defined as monthly hours > 160
  - `satisfaction_cat` — categorized into detractors, neutral, promoters based on satisfaction_level
  - `evaluation_cat` — grouped into low, medium, high based on last-evaluation
- The `department` and `work_accident` columns were dropped to streamline the dataset.

### 🤖 3. Modeling
- Applied train-test split with stratified sampling to address class imbalance
- Trained classification models (Logistic Regression, Random Forest, XGBoost, CatBoost)
- Performed hyperparameter tuning and model optimization using GridSearchCV

### 📈 4. Evaluation
- Assessed model performance using metrics such as Accuracy, Precision, Recall, F1 Score, ROC_AUC
- Compared multiple models to select the champion
- Provided interpretation and HR-facing insights

## 🔍 Exploratory Data Analysis (EDA)

This section outlines the exploratory techniques and feature engineering steps applied to understand patterns in employee attrition.

### 🧠 Key Insights
- The correlation analysis indicates that attrition does not have a strong relationship with any individual feature. However, a slight negative correlation was observed between employee satisfaction levels and attrition, indicating that lower satisfaction may contribute to employees leaving.
- Employees classified as detractors or neutral based on satisfaction scores exhibit a higher tendency to leave the company, highlighting the impact of employee engagement on retention.
- Attrition rates are notably higher among employees in their 2nd to 4th year of tenure compared to long-term employees. This group is also characterized by medium-to-low salaries and lower satisfaction ratings, suggesting a potential link between compensation, engagement, and retention.
- Salary does not demonstrate a clear proportional relationship with tenure, indicating that longer service does not necessarily correspond to higher compensation.
- Employees who exited the company were predominantly those with evaluation scores clustering around 0.9 and 0.5, which may suggest performance-related trends or inconsistencies in evaluation outcomes.
- The dataset exhibits class imbalance between employees who stayed and those who left. To address this, we applied stratification during the train-test split to ensure a balanced representation. Additionally, this imbalance necessitates careful model evaluation, as accuracy alone would not provide a meaningful assessment.

## 📈 Model Performance Summary

To determine the most effective model for predicting employee attrition, we evaluated four algorithms using key performance metrics: precision, recall, F1-score, accuracy, and ROC AUC. Due to class imbalance, **ROC AUC** was prioritized as our primary metric over raw accuracy.

![Model Evaluation Table](URL_TO_MODEL_EVALUATION_IMAGE)  
*Figure: Evaluation metrics for each model including precision, recall, F1-score, accuracy, and ROC AUC.*

![Confusion Matrix Plot](URL_TO_CONFUSION_MATRIX_IMAGE)  
*Figure: Confusion matrix visualizations across different classification models.*

### ⚙️ Modeling Insights:
- Our baseline model, **Logistic Regression**, struggled with classification. The confusion matrix revealed **495 false negatives** and **no true negatives**, highlighting low precision and recall.

- To improve performance, we explored three ensemble learning techniques:  
  **Random Forest**, **XGBoost**, and **LightGBM**

These models consistently outperformed Logistic Regression, with:  
- **F1-scores** around **0.87**  
- **ROC AUC scores** near **0.97**

The best-performing model was **Light Gradient Boosting (LightGBM)**, which achieved a **ROC AUC of 0.973** and demonstrated robust classification across both classes.

## 🧾 Conclusion, Recommendations & Next Steps

### ✅ Conclusion  

Key predictors of employee attrition were identified through feature importance analysis across ensemble models. The most impactful features include:  
- `time_spend_company` (Tenure)  
- `number_project`  
- `satisfaction_level`  
- `last_evaluation`  

These variables consistently ranked highest, offering strategic targets for HR intervention.  

![Feature Importance Plot](URL_TO_YOUR_IMAGE)

*Figure: Feature importance chart generated from ensemble models (e.g., Random Forest, LightGBM).*


### 💡 Recommendations
- Investigate why employees in their **2nd to 4th year** are more likely to leave, particularly those classified as **detractors or neutral** in satisfaction surveys.
- Address **potential mismanagement of project distribution**. As departing employees were assigned **4 to 7 projects** and working excessive hours, which may indicate burnout risks.
- Implement rules on working hours such as higher overtime pay or limit the number of working hours.
- Encourage balanced workload planning and regular check-ins on satisfaction levels to improve retention outcomes.

### 🔄 Next Steps
- Implement a more rigorous approach to outlier handling before fitting a Logistic Regression model. While we prioritized ensemble learning techniques due to their ability to manage outliers effectively, future iterations could benefit from refining preprocessing steps for improved evaluation metric.
- Expand the dataset to incorporate additional behavioral and engagement metrics (e.g. survey responses, peer feedback).
- Perform survival analysis as this models the timing of attrition, not just the likelihood. This will also help HR pinpoint windows of risk and intervene proactively


