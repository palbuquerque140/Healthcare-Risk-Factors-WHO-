# Healthcare Risk Factors Prediction

## Overview

This project aims to predict an individual’s health condition based on demographic, behavioral, and physiological factors using the Healthcare Risk Factors Dataset (a mix of WHO-inspired and synthetic data available on Kaggle).
The task is a multiclass classification problem, with the goal of identifying the likely health condition of each individual (e.g., diabetes, obesity, asthma, hypertension, cancer, etc.).

The project applies a full machine learning pipeline, from exploratory data analysis and preprocessing to model training, fine-tuning, and evaluation using Python’s data science stack.

## Summary of Insights

### Data Understanding & Insights

A thorough exploratory data analysis revealed several key trends and medically consistent patterns across demographic and health-related variables:

General Population Trends

- `Glucose` and HbA1C levels show a sharp **increase** between **ages 40–75**, suggesting a higher prevalence of diabetes or pre-diabetic conditions in middle-aged and older adults.
- `Blood Pressure and Cholesterol` both **increase** steadily **with age**, peaking among older individuals, consistent with cardiovascular risk accumulation.
- `BMI` **rises** rapidly between **25–30** years old, then **gradually decreases** in older age groups.
- `Triglycerides` follow a **similar** pattern to `cholesterol`, reflecting metabolic risk.
- `Physical Activity, Diet Score, and Sleep Duration` all **decline with age**, while `Stress Levels` exhibit a clear **upward trend**.
- `Smoking and Alcohol Consumption` showed **no significant relationship with age**, remaining relatively stable across groups.

Condition-Specific Insights

- `Diabetes`: Characterized by **elevated Glucose and HbA1C levels**, often accompanied by a **family history** of the disease, confirming its genetic predisposition.
- `Obesity`: Marked by **higher BMI and Triglycerides**, and frequently overlapping with `Hypertension and Elevated Cholesterol`.
- `Asthma`: Patients displayed noticeably **lower Oxygen Saturation** compared to others.
- `Hypertension`: Predominantly found among **older adults** with **high** `Cholesterol and Blood Pressure` readings.
- `Cancer`: Patients tended to have **longer hospital stays** and **higher** `stress levels`, indicating potential psychosomatic effects or treatment-related stress.
- `Arthritis`: **Similar** to `hypertension`, this condition was more prevalent in **older individuals**, aligning with age-related inflammatory risks.
- `Healthy individuals`: Exhibited the **lowest** values across `Glucose, HbA1C, Cholesterol, BMI, and Stress Levels`, and the **highest** values for `Physical Activity, Diet Score, and Sleep Duration.`

Demographic Distribution

- **No young patients** were identified with `diabetes or hypertension`.
- `Healthy` individuals ranged broadly from 20 to 70 years old.
- `Asthma` appeared across ages 10–60, indicating a more **evenly** distributed condition.
- `Obesity` was most frequent between **25–65 years old**.
- `Cancer` affected a **wide range**, from 30s to 80s, while `Arthritis and Hypertension` were concentrated in **older populations**.

**Feature Importance Insight:** Although "Length of Stay" showed the highest correlation with the target variable, it was deliberately **excluded from the model** to avoid data leakage, as this information would only be available after the outcome occurs. This decision highlights the importance of maintaining realistic and deployable predictive models.


## Modeling & Results

To handle class imbalance, Stratified K-Fold Cross-Validation was used throughout training.
Five models were initially benchmarked. Gradient Boosting and SVM were selected, based on performance and generalization, for fine-tuning using Randomized Search.

After retraining with optimal hyperparameters, both models achieved similar results on the test set:

Gradient Boosting → Accuracy: 0.87 • Macro Recall: 0.81 • Macro F1: 0.82 • Macro Precision: 0.84  
SVM               → Accuracy: 0.87 • Macro Recall: 0.80 • Macro F1: 0.82 • Macro Precision: 0.83

The confusion matrices for both models are shown below:

![Confusion Matix GB](Results/confusion_matrix_gb.png)

![Confusion Matix SVM](Results/confusion_matrix_svm.png)

Both models demonstrated consistent, balanced performance across classes, with Gradient Boosting slightly outperforming SVM in recall and F1-score, making it the preferred final model.


## Recommendations & Next Steps

- Feature Engineering: Introduce interaction terms (e.g., BMI × Age) or domain-informed derived features to capture more nuanced health patterns, potentially improving model discriminative power.

- Ensemble Methods: Experiment with model stacking or blending (e.g., combining GB and SVM outputs) to leverage complementary strengths of different algorithms.

- Hyperparameter Optimization: Extend search using GridSearch for finer tuning, aiming for improved predictive performance while avoiding overfitting.




