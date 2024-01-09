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

Addressing these challenges is crucial to ensure our predictions accurately reflect the opinions of all Canadians. To address these potential biases, we employ a regression model with post-stratification (MRP). MRP is a statistical method that combines detailed demographic data from a census dataset with survey data to enhance the precision of predictions (Holt & Smith, 1979). Our data is sourced from two key providers: the General Social Survey (GSS), a comprehensive national survey by Statistics Canada, and the 2021 Canadian Election Study (CES), a specialized study focusing on Canadian federal elections. The GSS serves the census dataset, and offers insights into various aspects of Canadians' lives, such as employment, education, and family, enabling us to create a representative survey sample. The CES, on the other hand, serves as the survey data, and delves into voter behavior, party preferences, and policy concerns following the 2021 federal election. 

By combining census data with survey data, MRP can address some of the challenges by using detailed demographic information from sources like the General Social Survey (GSS) to make the survey data more representative and precise. It helps compensate for non-response bias, sampling bias, and other biases by incorporating additional information to create more accurate predictions, ensuring that the survey results better reflect the diverse opinions of the Canadian population (Holt & Smith, 1979).

In terms of overall relevance of the analysis, our research question delves into the core of democracy's functioning in our nation. Canadian federal elections determine governance, policy, and citizens' daily lives. Our methodology, utilizing regression with post-stratification, addresses limitations in traditional polling, offering more accurate and nuanced election predictions through data-driven approaches. If we can make a good prediction, it helps politicians plan better and allows people to make informed choices when they vote (Northcott, 2015). In this analysis, we'll explore factors like where people live, their education, and their age to understand who's likely to win in 2025. 

We hypothesize that the incumbent Liberal Party is more likely to secure victory in the next Canadian federal election in 2025. This hypothesis is based on historical patterns of incumbents often benefiting from the advantages of name recognition, established infrastructure, and the ability to campaign on their record of governance (Lucas et al., 2021). Additionally, the Liberal Party's historical performance and policy positions may position them favorably with the electorate. 

## Data
### Datasets
The General Social Survey (GSS) in 2016 used a two-stage sampling design to collect data from households across Canada. The sampling units were groups of telephone numbers, and the final stage units were individuals within the identified households. The survey employed a stratified sampling method, dividing the ten provinces into 27 strata based on geographic areas, including Census Metropolitan Areas (CMAs) and non-CMA regions. Minimum sample sizes were determined for each stratum to ensure acceptable sampling variability, and the remaining sample was allocated to balance the precision of national and stratum-level estimates. The GSS randomly selected one eligible member aged 15 or older from each sampled household to complete the questionnaire. Approximately 43,000 units were included in the field sample, with around 35,000 invitation letters sent to selected households, and an expected completion of 20,000 questionnaires. Data collection was voluntary and direct from survey respondents (Statistics Canada, n.d.). 

The Canadian Election Study (CES) data collection process for the 2021 election involved a two-wave panel. The Campaign Period Survey (CPS) gathered a sample of 20,968 members of the Canadian population through the Leger Opinion panel, stratified by region and balanced for gender and age within each region. The CPS consisted of three waves, collecting data from August to September 2021. After the election, 15,069 respondents completed the Post-Election Survey (PES) from late September to early October 2021, resulting in a return rate of 72%. Data quality checks were applied to remove incomplete, duplicate, or low-quality responses (Stephenson et al., 2022).

### Data Cleaning 
#### Census Dataset
1. Selecting columns that will be used for the model
We selected specific variables (columns) that will be included in the model. Specifically, the selected variables are 'age', 'marital_status', 'citizenship_status', 'province', 'education', and 'pop_center'. These variables are selected based on a study from Statistics Canada which shows significant variables in determining voter decisions. It shows marginal effects from a probit model of voting, which provides insights into how changes in the independent variables affect the probability of an individual voting in a particular election or engaging in a binary outcome, such as "voting" or "not voting." (Statistics Canada, 2015)

2. Mutating the categorical column so that each column has a numerical value
A new variable 'cps21_marital' is created, representing marital status. It is recoded based on the 'marital_status' variable. The recoding assigns numerical values 1 to 7 for various marital status categories, with 1 representing "Married," 2 for "Living common-law," 3 for “Divorced,” 4 for “Separated,” 5 for “Widowed,” 6 for “Single, never married,” and 7 for any other status. A new variable 'cps21_bornin_canada' is created to represent citizenship status. It is recoded based on the 'citizenship_status' variable, with 1 for "By birth," 2 for "By naturalization," and 3 for "Don't know." A new variable 'cps21_province' is created to represent the province of residence. It is recoded based on the 'province' variable. Each province is assigned a unique numeric value from 1 to 13, with 1 representing “Alberta,” 2 for “British Columnia,” 3 for “Manitoba,” 4 for "New Brunswick," 5 for "Newfoundland and Labrador," 6 for "Northwest Territories," 7 for "Nova Scotia," 8 for "Nunavut," 9 for “Ontario,” 10 for "Prince Edward Island," 11 for “Quebec,” 12 for "Saskatchewan," 13 for “Yukon.” A new variable 'cps21_education' is created to represent the level of education. It is recoded based on the 'education' variable. Numeric values are assigned to different education categories, with 5 for "High school diploma," 7 for "Trade certificate or diploma" and "College, CEGEP or other non-university certificate or diploma," 9 for "Bachelor's degree (e.g. B.A., B.Sc., LL.B.)," 4 for "Less than high school diploma or its equivalent," 8 for "University certificate or diploma below the bachelor's level," 9 for "University certificate, diploma or degree above the bachelor's level," and NA (representing missing values) if none of the above conditions are met. A new variable 'pes21_rural_urban' is created to represent the population center. It is recoded based on the 'pop_center' variable. Values 5 and 3 are assigned to "Larger urban population centres'' and "Rural areas and small population centres," respectively. 
Other values are set as missing (NA).

3. Column Removal
Columns 'marital_status', 'citizenship_status', 'province', 'education', 'pop_center', and ‘age’ are removed from the dataset as they are no longer needed.

4. Filtering
Rows in which the 'cps21_age' variable is less than 18 are filtered out because the model is trained on individuals aged 18 and above.

5. Removing Missing Values
Any rows with missing values (NA) are dropped from the dataset.

#### Survey dataset:
1. Variable Selection
We selected specific columns in the survey_data dataset for inclusion in the model_data dataset. These selected columns are:

- 'cps21_votechoice': Represents the respondent's vote choice.
- 'cps21_age': Represents the respondent's age.
- 'cps21_marital': Represents the respondent's marital status.
- 'cps21_bornin_canada': Represents the respondent's citizenship status (whether born in Canada or not).
- 'cps21_province': Represents the respondent’s province of residence.
- 'cps21_education': Represents the respondent's level of education.
- 'pes21_rural_urban': Represents the respondent’s area of residence, indicating whether it is within a population center and its urban/rural designation.
Similar to the census dataset, the selection is based on the study from Statistics Canada which shows significant variables in determining voter decisions (Statistics Canada, 2015). 

2. Removing Missing Values
The drop_na() function is used to remove rows with missing values from the model_data dataset. This step ensures that only complete cases with data in all selected columns are retained in the final dataset.

The result is a cleaned and filtered dataset named model_data that includes the specified variables for further analysis. Then, for census data, we cleaned it so that it matches the inputs as the survey data.
