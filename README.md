### Diabetes Risk Prediction from Dietary Habits and Lifestyle Factors

**Author:** Nireshwalia

#### Executive Summary
This project uses data from the CDC's National Health and Nutrition Examination Survey (NHANES) 2017-2018 to predict diabetes risk based on dietary habits, body composition, physical activity, and demographic factors. A baseline logistic regression model achieved an AUC-ROC of 0.806 and a recall of 0.80 for the diabetic class, meaning the model correctly identifies 80% of diabetic individuals. Key findings from exploratory data analysis reveal that age, waist circumference, and weight are the strongest predictors of diabetes risk, while dietary variables alone show surprisingly little separation between diabetic and non-diabetic groups.

#### Rationale
Over 38 million Americans have diabetes and another 98 million have prediabetes — most of whom are undiagnosed. Current diagnosis requires clinical blood tests, meaning the disease is often already progressing by the time it is detected. If behavioral and lifestyle risk factors can reliably predict diabetes risk, it becomes possible to identify at-risk individuals earlier through simple screening tools — enabling preventive intervention before clinical onset. This analysis aims to identify which modifiable behaviors are the strongest drivers of diabetes risk and translate those findings into actionable public health intelligence.

#### Research Question
Can dietary habits and lifestyle factors — such as physical activity, BMI, and nutritional intake — reliably predict whether an individual is at risk for diabetes, and which of these modifiable behaviors are the strongest drivers of that risk?

#### Data Sources
Primary dataset: NHANES 2017-2018 (National Health and Nutrition Examination Survey), published by the CDC and freely available at [nhanes.cdc.gov](https://wwwn.cdc.gov/nchs/nhanes/).

Five files were merged on the respondent ID (SEQN):
- **DEMO_J.XPT** — Demographics (age, gender, ethnicity, education, income)
- **DIQ_J.XPT** — Diabetes questionnaire (target variable: diabetes diagnosis)
- **DR1TOT_J.XPT** — Dietary intake (calories, macronutrients, sugar, fiber, sodium, alcohol)
- **BMX_J.XPT** — Body measures (BMI, waist circumference, weight, height)
- **PAQ_J.XPT** — Physical activity (vigorous/moderate activity, sedentary time)

Final dataset after cleaning: 4,966 adults with 28 features and zero missing values.

#### Methodology
1. **Data Cleaning** — merged 5 NHANES files, filtered to adults (18+), recoded diabetes target variable (combined prediabetic and diabetic into positive class), imputed missing body measures with median, dropped rows with missing dietary data, replaced NHANES coding errors (9999) in activity columns, and capped dietary outliers at the 99th percentile.

2. **Exploratory Data Analysis** — visualized diabetes prevalence by age group, BMI distributions by diabetes status, dietary variable comparisons, physical activity levels, and a full feature correlation matrix.

3. **Baseline Model** — logistic regression with `class_weight='balanced'` to handle class imbalance (82% non-diabetic, 18% diabetic). Features scaled using StandardScaler. 80/20 train/test split with stratification.

4. **Planned improvements (Module 24)** — Random Forest and XGBoost classifiers for improved accuracy and feature importance rankings; K-Means clustering for behavioral profiling.

#### Results
The baseline logistic regression model achieved the following results on the held-out test set:

| Metric | Score |
|--------|-------|
| AUC-ROC | 0.806 |
| Recall (diabetic class) | 0.80 |
| Precision (diabetic class) | 0.35 |
| Overall Accuracy | 0.70 |

Key findings from EDA:
- Diabetes prevalence increases sharply with age: 1.9% in 18-30 year olds vs 35.1% in 71-80 year olds
- Diabetic individuals have a higher mean BMI (32.5) compared to non-diabetic individuals (29.1)
- Dietary variables alone show little separation between groups, suggesting diabetes risk is driven by the interaction of multiple factors
- Age, waist circumference, and weight are the strongest predictors; vigorous physical activity has a modest protective effect

#### Next Steps
- Implement Random Forest and XGBoost models to improve predictive accuracy and generate more robust feature importance rankings
- Apply K-Means clustering to identify distinct behavioral risk profiles in the data
- Address multicollinearity between BMI, waist circumference, and weight through feature selection
- Consider adding sleep and mental health data (NHANES SLQ and DPQ files) as additional predictors
- Translate findings into a non-technical report for public health communication (Module 24)

#### Outline of Project

- [Link to notebook - diabetes_analysis.ipynb]()

##### Contact and Further Information
For questions about this project, please reach out via the GitHub repository.
