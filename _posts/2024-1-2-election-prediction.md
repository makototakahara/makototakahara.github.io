---
layout: post
author: Makoto Takahara
tags: [project]
include_in_list: false
---

# Project Overview
For this project, I worked in a group to predict the proportion of votes each party will recieve in the 2025 Canadian Federal Election. 

We used multilevel regression with poststratification with data from the General Social Survey (GSS), a comprehensive national survey by Statistics Canada, and the 2021 Canadian Election Study (CES), a specialized study focusing on Canadian federal elections. This project placed an emphasis on considering both individual-level and group-level variations in hierarchical data and adjusting for population characteristics through post-stratification.

---

# Project Content
## Introduction

With the next Canadian federal election on the horizon in 2025, we will predict the party that will obtain the highest proportion of the popular vote. Predicting election outcomes helps people anticipate or prepare for potential policy changes, shifts in government priorities, and the overall political landscape. Businesses, investors, and even individuals may adjust their strategies based on these predictions. 

The challenge in answering this research question lies in obtaining an accurate representation of the diverse Canadian population's political preferences, especially considering the potential bias arising from survey data. There is a risk of non-response bias, where the characteristics of individuals who choose not to participate in a survey differ systematically from those who do. This can potentially skew the study's findings and compromising its representativeness. Social desirability bias is also a concern, as participants may provide socially acceptable answers instead of their true beliefs, especially regarding sensitive topics. In surveys, sampling bias may arise when the group surveyed doesn't represent the full diversity of the population, potentially skewing the results (Mayer, 2021). Additionally, question wording and framing can influence how participants respond to the survey, so survey questions must be carefully worded to avoid bias. 

Addressing these challenges is crucial to ensure our predictions accurately reflect the opinions of all Canadians. To address these potential biases, we employ a "regression model with post-stratification," a statistical method that combines detailed demographic data from a "census" dataset with survey data to enhance the precision of predictions (Holt & Smith, 1979). Our data is sourced from two key providers: the General Social Survey (GSS), a comprehensive national survey by Statistics Canada, and the 2021 Canadian Election Study (CES), a specialized study focusing on Canadian federal elections. The GSS serves the census dataset, and offers insights into various aspects of Canadians' lives, such as employment, education, and family, enabling us to create a representative survey sample. The CES, on the other hand, serves as the survey data, and delves into voter behavior, party preferences, and policy concerns following the 2021 federal election. It helps to refine our predictions for the 2025 Canadian federal election by examining the influence of political beliefs, party affiliations, and regional variations. These data sources are important in our data-driven approach to understanding the upcoming election.

Multilevel Regression and Poststratification (MRP) can help address some of the challenges by using detailed demographic information from sources like the General Social Survey (GSS) to make the survey data more representative and precise. It helps compensate for non-response bias, sampling bias, and other biases by incorporating additional information to create more accurate predictions, ensuring that the survey results better reflect the diverse opinions of the Canadian population (Holt & Smith, 1979).

In terms of overall relevance of the analysis, our research question delves into the core of democracy's functioning in our nation. Canadian federal elections determine governance, policy, and citizens' daily lives. Our methodology, utilizing regression with post-stratification, addresses limitations in traditional polling, offering more accurate and nuanced election predictions through data-driven approaches. If we can make a good prediction, it helps politicians plan better and allows people to make informed choices when they vote (Northcott, 2015). In this analysis, we'll explore factors like where people live, their education, and their age to understand who's likely to win in 2025. 

We hypothesize that the incumbent Liberal Party is more likely to secure victory in the next Canadian federal election in 2025. In this context, incumbent refers to the political party that is currently in power and holds the majority of seats in the government. This hypothesis is based on historical patterns of incumbents often benefiting from the advantages of name recognition, established infrastructure, and the ability to campaign on their record of governance (Lucas et al., 2021). Additionally, the Liberal Party's historical performance and policy positions may position them favorably with the electorate. Please get ready for a data-driven adventure that will provide insights into the forthcoming Canadian election!

## Data
### Datasets
The General Social Survey 
