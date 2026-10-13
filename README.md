#DATA CLEANSER PR 2
# Data Cleaning & Imputation Project

## Overview
This project cleans and prepares a 500-record patient health dataset for analysis. The dataset contains patient information and health measurements including age, gender, region, BMI, blood pressure, cholesterol, glucose, and disease risk.

## Dataset
- Rows: **500**
- Columns: **9 original columns**
- Main numerical variables: Age, BMI, Blood Pressure, Cholesterol, Glucose
- Categorical variables: Gender, Region
- Target/indicator: Disease Risk

## Missing-Value Analysis
Initial missing values were:

| Column | Missing | Percentage |
|---|---:|---:|
| patient_id | 0 | 0.0% |
| age | 12 | 2.4% |
| gender | 10 | 2.0% |
| region | 15 | 3.0% |
| bmi | 18 | 3.6% |
| blood_pressure | 14 | 2.8% |
| cholesterol | 16 | 3.2% |
| glucose | 20 | 4.0% |
| disease_risk | 0 | 0.0% |

## Imputation Methods Tested
The notebook tested:
1. Mean imputation for BMI
2. Median imputation for BMI
3. Most-frequent imputation for Region and Gender
4. Missing-indicator + random-sample imputation for BMI
5. KNN imputation for numerical health variables
6. MICE / Iterative Imputer for Blood Pressure, Cholesterol, and Glucose

### Most Effective Imputation Strategy
**KNN Imputation was the most effective in the notebook for numerical completeness.** It simultaneously imputed Age, BMI, Blood Pressure, Cholesterol, and Glucose, reducing missing values in all five selected numerical columns to **0**.

MICE also successfully reduced missing values to 0 for Blood Pressure, Cholesterol, and Glucose, but the notebook applied it only to those three columns. Therefore, based on the demonstrated coverage in this notebook, KNN provided broader numerical imputation.

> Note: The notebook does not calculate an independent validation metric such as RMSE/MAE on artificially masked values, so "most effective" here means best demonstrated completeness/coverage, not proven prediction accuracy.

## Outlier Handling
The notebook compared:
- Z-score method on Cholesterol
- IQR method on BMI
- Percentile filtering on Glucose
- Winsorization on Cholesterol

### Best Data-Preservation Method
**Z-score filtering provided the strongest data-preservation result among the demonstrated methods.**

- Original records: **500**
- Z-score result: **498**
- Records retained: **99.6%**
- Cholesterol mean: **196.02 → 195.17**
- Cholesterol standard deviation: **38.58 → 36.22**

The IQR method retained 495 records (99.0%) and produced a smaller change in BMI statistics. Percentile filtering retained only 450 records (90.0%), so it removed substantially more observations.

The Winsorization result in the notebook should be interpreted cautiously because the code used glucose percentile limits to cap cholesterol, which is not a valid same-variable comparison.

## How Data Cleaning Improved Usability
Data cleaning improved the dataset by:
- Identifying missing values and quantifying their percentages.
- Applying suitable numerical and categorical imputation methods.
- Reducing missing values in selected health variables to zero.
- Detecting and treating extreme observations.
- Comparing dataset shape, mean, and standard deviation before and after outlier treatment.
- Making the numerical health variables more complete and suitable for downstream analysis and machine-learning workflows.

## Final Conclusion
The project shows that **KNN imputation** gave the broadest demonstrated numerical missing-value coverage, while **Z-score outlier filtering** preserved the largest proportion of records among the tested outlier-removal methods.

The notebook's final displayed dataset still contains missing values in **Age, Gender, Region, and BMI** because the MICE section reloads the original CSV and only imputes Blood Pressure, Cholesterol, and Glucose. For a truly final clean dataset, these remaining columns should also be imputed before saving the final file.

## Tools Used
- Python
- Pandas
- NumPy
- Scikit-learn
- Google Colab / Jupyter Notebook

- AUTHOR
- PATHAN SAHIL
