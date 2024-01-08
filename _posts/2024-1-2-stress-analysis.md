---
layout: post
author: Makoto Takahara
tags: [project]
include_in_list: false
---

# Project Overview
For this project, I worked in a group to investigate the relationship between subjective stress levels and various lifestyle factors.

We used a multiple linear regression to model this relationship with data from Kaggle. This project places an emphasis on testing the assumptions of linear regression, correcting and mitigating violated assumptions, model selection, and analysis of variance (ANOVA). 

# Project Content
## Introduction
This study aims to investigate the association between subjective stress levels and various factors among individuals aged 21 to 35. Our research question focuses on understanding how sleep habits, social interaction levels, meditation, passions, and gender collectively influence the subjective stress experienced by this age group. Employing a multiple linear regression model, we examine lifestyle factors as independent variables and gender as an independent categorical variable, considering literature highlighting its impact on subjective stress (APA, 2012). The linear model evaluates the significance of predictors on stress levels, with positive coefficients for numerical variables indicating increased stress with higher values, and vice versa for negative coefficients. For gender, a positive coefficient implies higher stress for males compared to females, and vice versa for negative coefficients. Statistically significant relationships, determined by p-values below 0.05, are identified, providing a comprehensive and nuanced exploration of how lifestyle factors and gender influence stress levels in individuals aged 21-35.

The existing literature on stress factors offers valuable insights, with Jin's exploration emphasizing therapeutic activities like meditation and walking, albeit overlooking crucial lifestyle factors such as sleep habits, social interaction, and gender (Jin, 1992). Nollet et al.'s neuroscientific perspective delves into the sleep-stress relationship, but their focus on neurochemistry neglects an examination of sleep's impact on subjective stress levels (Nollet et al., 2020). In contrast, Cacioppo and Hawkley (2003) touch upon stress within the context of social isolation, yet stress plays a peripheral role in their broader health proxies. Our research model aims to fill this gap by explicitly investigating the association between social interactions and stress, offering a more direct analysis of their relationship. Building upon existing studies, our research addresses the need for a holistic investigation into how a combination of lifestyle factors and individual characteristics collectively influences subjective stress levels.

## Methods
### Assessing Model Assumptions
Our initial linear regression model takes daily stress as the response variable and a number of lifestyle
factors and gender as predictors, presented below:

$$
\begin{align*}
Daily\ Stress &= \beta_0 + \beta_1 Social\ Network \\
&\quad + \beta_2 Daily\ Steps + \beta_3 Daily\ Sleeping \\
&\quad + \beta_4 Sleep + \beta_5 Screen\ Time\ for\ Passion \\
&\quad + \beta_6 Meditation + \beta_7 Gender + \varepsilon
\end{align*}
$$

**Daily Stress:** Likert scale ranging from 1 to 5 (weak to strong)  
**Social Network:** Number of people individuals interact with in a day.  
**Daily Steps:** Number of steps (in thousands) individuals typically walk every day.  
**Daily Shouting:** Number of times individuals shout at somebody in a week.  
**Sleep:** Hours individuals typically sleep.  
**Time for Passion:** Hours individuals spend every day doing what they are passionate about.  
**Meditation:** Number of times individuals think about themselves in a week.  
**Gender:** Categorical variable (1 indicating male and 0 indicating female).

To assess assumptions in our multiple linear regression analysis, we employ a side-by-side boxplot for gender (categorical) and histograms for lifestyle factor predictors and daily stress. Skewness in response histograms or asymmetry in predictors' boxplots may indicate violations of linearity or normality assumptions. For the conditional mean response, we inspect a "response vs fitted value" scatter plot for daily stress, aiming for a random diagonal scatter to satisfy this condition. The conditional mean predictor is assessed through pairwise scatterplots for numerical predictors, meeting the condition if residual plots exhibit no curve or non-linear trend. Violation of these conditions implies that future residual plots cannot pinpoint specific assumption violations. After assessing conditions, we generate residual plots ("residual vs fitted" & "residual vs each predictor") and a side-by-side boxplot for "Gender." To check the uncorrelated error assumption, we scan for large clusters in residual plots, as their presence would render the model inappropriate. If absent, we proceed to assess linearity, identifying violations through systematic patterns in residual plots. Box-cox transformations on corresponding predictors follow, involving maximum likelihood estimation for lambda and selecting a simple power. After transforming predictors, we refit the model and reevaluate conditions until linearity improves. Once achieved, we check the normality assumption using a QQ plot, applying box-cox transformations to the response variable as needed. This process repeats until normality is improved. Subsequently, we examine the constant variance assumption by scrutinizing the fanning spread of data points in residual plots. Violations prompt variance stabilizing transformations on the response variable, and we iterate through conditions until constant variance is enhanced. Ensuring all assumptions are met, we conduct an ANOVA test on the model, evaluating the null hypothesis of no statistically significant linear relationship between all predictors and daily stress. A p-value exceeding 0.05 deems the linear regression model inappropriate; otherwise, further testing is pursued. Individual T-tests are then performed on all predictors, assuming no linear relationship with daily stress. If all p-values are below 0.05, the full model is finalized. Otherwise, predictors with p-values above 0.05 are removed to create a reduced model, followed by a partial F-test. A p-value below 0.05 retains the original full model, while a higher p-value designates the reduced model as final, indicating no significant linear relationship between daily stress and the removed predictors.

### Diagnostics
We employ the variance inflation factor (VIF) to assess multicollinearity by calculating VIF values for each predictor. A VIF value below 5 indicates no significant multicollinearity in our model. Should any predictor exhibit a VIF value exceeding 5, we address multicollinearity by removing the predictor with the highest VIF and constructing a reduced model. Subsequently, we reassess the assumptions and conditions for the refined model. To identify potential outliers or influential points, we calculate tool values for each observation, acknowledging values surpassing a predetermined cutoff as limitations in our analysis rather than removing the corresponding observations. This approach aligns with our objective of drawing generalizable conclusions from the model while considering ethical considerations.

Table 1: Tools to Detect Problematic Points and Their Cutoff Values

|Problematic Point Type| Tool          | Cutoff  |
|:-:|:-:|:----------:|
|Leverage points       | Leverage      | $\frac{2(p+1)}{n}$, where $p$ is the number of predictors in our model and $n=6108$ is the total number of observations in our dataset.|
|Outliers              | Absolute value of standardized residuals of each observation     | $4$ |
|Observations influential on all fitted values|Cook’s distance      |Median of the F-distribution $F(p+1, n-p-1)$. |
|Observations influential on their own fitted values|Absolute value of “difference in fitted values” (DFFITS)| $2\sqrt{\frac{2(p+1)}{n}}$.|
