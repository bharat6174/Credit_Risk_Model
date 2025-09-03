# Credit_Risk_Model

## Project Objective
To predict the probability that somebody will experience financial distress(serious delinquency) in the next two years.

## Dataset used
- Dataset: <a href="https://github.com/bharat6174/Credit_Risk_Model/blob/main/Give%20me%20some%20credit%20dataset.csv">Give me some credit</a> (open it, then click on _**View raw**_ to download the excel file)
## Process
The project covers data cleaning, feature engineering, handling class imbalance, model training with XGBoost, and threshold selection strategies.<br>

1. **Data Cleaning & Validation**
- **Step:** Checked dataset for duplicates, missing values, and outliers.  
- **Problems:**  
  - Missing `MonthlyIncome` and `NumberOfDependents`.  
  - Extreme outliers in `DebtRatio` and `RevolvingUtilizationOfUnsecuredLines`.  
- **Solutions:**  
  - Dropped duplicates.  
  - Imputed `NumberOfDependents` with **mode**.  
  - Imputed `MonthlyIncome` using **grouped median** (by age groups & dependents) as it ensures comparable values in respective groups.  
  - Capped extreme `MonthlyIncome` values at **99th percentile**.
  - Managed all other variables' possible problems.

2. **Feature Engineering**
- **Step:** Created additional informative features.  
- **Problems:** DebtRatio > 1 and zero income cases created anomalies, Number of delinquencies in 3 columns and their effect on target variable
- **Solutions:**  
  - Checked for disturbances due to zero income (found none).
  - Created a capped and transformed (log(1+x) transformation) version of `Debt Ratio` to handle wide unrealistic range and skewness.
  - Capped all 3 Number of delinquencies columns at `10` & Created `TotalDelinquencies` by aggregating delinquency counts.

3. **Handling Class Imbalance**
- **Step:** Default rate was ~7%, leading to highly imbalanced target variable.  
- **Problems:** Standard training biased towards majority (non-defaulters).  
- **Solutions Evaluated:**  
  - Random Oversampling (risk of overfitting).  
  - Random Undersampling (loss of majority data).  
  - SMOTE (synthetic data → risk of unrealistic borrowers).  
  - **Final Choice:** Algorithm-level handling with **XGBoost `scale_pos_weight`**, set to the ratio of non-defaulters/defaulters.  

4. **Model Selection**
- **Baseline:** Logistic Regression with `class_weight='balanced'`.  
  - **Problem:** Linear, struggled to capture non-linear interactions, underfit complex features.  
- **Final Choice:** **XGBoost** because:  
  - Captures **non-linear feature interactions**.  
  - Robust to skewed distributions and outliers.  
  - Built-in **regularization and early stopping**.
  - High **ROC-AUC score of 0.8648**

5. **Threshold Selection**
- **Step:** Default threshold = 0.5 was not suitable for imbalanced data especially in Credit Risk Models.  
- **Strategies Applied:** Business-driven cutoffs
    - **High Precision:** "Don’t reject too many good customers".  
    - **High Recall:** "Better safe than sorry" → catch most defaulters.
- **Evaluation by:** Confusion Matrix, Precision, Recall, F1-score at chosen thresholds.  

## Conclusion and Key Learnings
- **Groupwise imputation** captures richer patterns than global median.  
- **Capping + log-transform** stabilizes skewed financial ratios.  
- **Class imbalance** with skewed features is best handled at the algorithm level in XGBoost (vs. resampling).  
- **Threshold choice** is as important as the model itself, it must align with business objectives.  
