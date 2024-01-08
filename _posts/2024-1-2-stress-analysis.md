---
layout: post
author: Makoto Takahara
tags: [about me]
include_in_list: false
---

# Project Overview
For this project, I worked in a group to investigate the relationship between subjective stress levels and various lifestyle factors.

We used a multiple linear regression to model this relationship with data from Kaggle. This project places an emphasis on testing the assumptions of linear regression, correcting and mitigating violated assumptions, model selection, and analysis of variance (ANOVA). 

# Project Content
## Introduction
This study aims to investigate the association between subjective stress levels and various factors among individuals aged 21 to 35. Our research question focuses on understanding how sleep habits, social interaction levels, meditation, passions, and gender (categorical) collectively influence the subjective stress experienced by this age group. Employing a multiple linear regression model, we examine lifestyle factors as independent variables and gender as an independent categorical variable, considering literature highlighting its impact on subjective stress (APA, 2012). The linear model evaluates the significance of predictors on stress levels, with positive coefficients for numerical variables indicating increased stress with higher values, and vice versa for negative coefficients. For gender, a positive coefficient implies higher stress for males compared to females, and vice versa for negative coefficients. Statistically significant relationships, determined by p-values below 0.05, are identified, providing a comprehensive and nuanced exploration of how lifestyle factors and gender influence stress levels in individuals aged 21-35.

The existing literature on stress factors offers valuable insights, with Jin's exploration emphasizing therapeutic activities like meditation and walking, albeit overlooking crucial lifestyle factors such as sleep habits, social interaction, and gender (Jin, 1992). Nollet et al.'s neuroscientific perspective delves into the sleep-stress relationship, but their focus on neurochemistry neglects an examination of sleep's impact on subjective stress levels (Nollet et al., 2020). In contrast, Cacioppo and Hawkley (2003) touch upon stress within the context of social isolation, yet stress plays a peripheral role in their broader health proxies. Our research model aims to fill this gap by explicitly investigating the association between social interactions and stress, offering a more direct analysis of their relationship. Building upon existing studies, our research addresses the need for a holistic investigation into how a combination of lifestyle factors and individual characteristics collectively influences subjective stress levels.

## Methods
### Assessing Model Assumptions
Our initial linear regression model takes daily stress as the response variable and a number of lifestyle
factors and gender as predictors, presented below:

$$
Daily\ Stress = \beta_0 + \beta_1 Social\ Network + \beta_2 Daily\ Steps + \beta_3 Daily\ Sleeping + \beta_4 Sleep + \beta_5 Screen\ Time\ for\ Passion + \beta_6 Meditation + \beta_7 Gender + \varepsilon
$$

**Daily Stress:** Likert scale ranging from 1 to 5 (weak to strong)  
**Social Network:** Number of people individuals interact with in a day.  
**Daily Steps:** Number of steps (in thousands) individuals typically walk every day.  
**Daily Shouting:** Number of times individuals shout at somebody in a week.  
**Sleep:** Hours individuals typically sleep.  
**Time for Passion:** Hours individuals spend every day doing what they are passionate about.  
**Meditation:** Number of times individuals think about themselves in a week.  
**Gender:** Categorical variable (1 indicating male and 0 indicating female).

