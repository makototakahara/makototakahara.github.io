---
layout: post
author: Makoto Takahara
tags: [project]
include_in_list: false
---

# Project Overview
For this project, I predicted whether a patient has a heart disease or not.

I used classification using logistic regression based on information such as a patient's age, sex, cholesterol levels, and resting blood pressure. 

---

# Project Content

## Introduction

This project aims to develop a predictive model for detecting the presence of heart disease, utilizing key factors such as age, maximum heart rate, and cholesterol levels. Beyond its significance in advancing public health and cardiovascular research, the impact of detecting heart disease extends to individuals' well-being on a micro level. Our exploration of various factors relies on data from the UCI Heart Disease Dataset, with the goal of developing a robust model for this purpose.

Logistic regression, a foundational statistical method in binary classification, plays a pivotal role in this project. By fitting a sigmoid function to the data, it transforms a combination of features into a probability scale ranging from 0 to 1. Typically, a threshold of 0.5 is set to predict whether an observation indicates the presence (1) or absence (0) of heart disease. The relative simplicity and interpretability of logistic regression make it a powerful and reliable tool for binary classification tasks.

## Data

The data was split into training and testing datasets with 643 and 275 observations respectively by the Hackathon facilitators. Here is a look at the variables:

 - `Age`: age of the patient [years]
 - `Sex`: sex of the patient [M: Male, F: Female]
 - `ChestPainType`: chest pain type [TA: Typical Angina, ATA: Atypical Angina, NAP: Non-Anginal Pain, ASY: Asymptomatic]
 - `RestingBP`: resting blood pressure [mm Hg]
 - `Cholesterol`: serum cholesterol [mm/dl]
 - `FastingBS`: fasting blood sugar [1: if FastingBS > 120 mg/dl, 0: otherwise]
 - `RestingECG`: resting electrocardiogram results [Normal: Normal, ST: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV), LVH: showing probable or definite left ventricular hypertrophy by Estes' criteria]
 - `MaxHR`: maximum heart rate achieved [Numeric value between 60 and 202]
 - `ExerciseAngina`: exercise-induced angina [Y: Yes, N: No]
 - `Oldpeak`: oldpeak = ST [Numeric value measured in depression]
 - `ST_Slope`: the slope of the peak exercise ST segment [Up: upsloping, Flat: flat, Down: downsloping]
 - `HeartDisease`: output class [1: heart disease, 0: Normal]

![Heart Disease Variables](/images/Screenshot-2024-01-21-at-12.07.17.png)

From this, we observe that there is a undocumented `Unnamed: 0` variable that contains 0 in all observations. We disregard this variable in our analysis.

## Exploratory Data Analysis
### Univariate Analysis

First, we explore the distribution of numerical variables. 

![Heart Disease Histograms](/images/Screenshot-2024-01-21-at-12.13.21.png)

Upon visual inspection, there seem to be odd characteristics in some of the variables. For example, there is an empty bin in `Age` at 53. We also obvseve possibly unnatural peaks at 0 in Cholesterol and Oldpeak. 0 for `Oldpeak` seems to be plausible given that it is a value relative to `RestingECG`. On the other hand, we found that 0 mg/dl of cholesterol is not within a realistic range, as values below 70 mg/dl are reported as “abnormally low” even under the secondary prevention settings (https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7355098/). We suspect that there may have been measurement error or missing values.

However, given that 121 out of 643 observations in the training dataset has 0 for `Cholesterol`, it is difficult to remove these observations altogether. Furthermore, the testing dataset also contains a high proportion of observations with 0 for `Cholesterol`, so we note this abnormality as we go forward with our analysis. 

We also observe some outliers from these histograms, so we will identify them using z-scores with a threshold of 3. We have 13 outliers, which we will remove from the analysis. Before removal, our training dataset had 643 observations. After the removal of 13 outliers, we now have 630 observations in our dataset. 

Next, we explore the distribution of categorical variables. 

![Heart Disease Histograms](/images/Screenshot-2024-01-21-at-12.27.19.png)

We note that there are more males than females in the training dataset. There are also more people with heart disease than not, which raises concerns about the representativeness of this dataset. 

### Multivariate Analysis

We explore the correlation between each numerical predictor variable, using a scatter matrix and correlation heatmap. 

![Heart Disease Scatter Matrix](/images/output.png)
![Heart Disease Correlation Heatmap](/images/output11.png)

In general, we cannot observe correlation between most ofthe predictors. We may be concerned about the negative correlation between `Age` and `MaxHR`.

Next, we check for multicollinearity using Variance Inflation Factors (VIF). We use a cutoff of 10 to determine whether the factor should be removed from our logistic regression model.

![Heart Disease VIF1](/images/Screenshot-2024-01-21-at-12.46.07.png)

We see that `RestingBP` has a VIF of nearly 42, so we remove it an check again.

![Heart Disease VIF2](/images/Screenshot-2024-01-21-at-12.46.11.png)

We see that `Age` and `MaxHR` both have VIF around 13.  We have a choice of which variable to remove, though both are associated with heart disease.  We choose to remove `MaxHR` because of its slightly higher VIF and check for multicollinearity again. 

![Heart Disease VIF3](/images/Screenshot-2024-01-21-at-12.46.15.png)

We see that all numerical variables now have VIF under 5. This significant decrease in VIF for `Age` is in line with our concern of mild correlation between `Age` and `MaxHR`.

Finally, we encode for qualitative features before fitting a logistic regression model. 

## Logistic Regression
