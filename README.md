# Credit_Risk_Model

## Project Objective
To predicting the probability that somebody will experience financial distress(serious delinquency) in the next two years.

## Dataset used
- Dataset: <a href="https://github.com/bharat6174/Credit_Risk_Model/blob/main/Give%20me%20some%20credit%20dataset.csv">Give me some credit</a> (open it, then click on _**View raw**_ to download the excel file)
## Process
1. Conducted rigorous data preprocessing, including duplicate removal, imputation of missing values using mode and median, and outlier treatment for features like _**Number of dependents, Monthly Income, Revolving Utilization Of Unsecured Lines, Debt Ratio**_ etc.
2. I used multiple **distributions** of feature like _**Monthly Income, Debt Ratio**_ and visualized some other variables using **histograms** and **boxplots** to guide data cleaning decisions.
3. Developed a credit risk prediction model using theXGBoost Classifier on the cleaned dataset, predicted the values, and achieved an **accuracy of _~94.6%_**.
4. Evaluation of the model was done using **_confusion matrix_** and classification report (precision, recall, F1-score), and **AUC Score**.
* This project demonstrates applied ML for real-world credit scoring and credit risk prediction.
