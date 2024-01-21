---
layout: post
author: Makoto Takahara
tags: [project]
include_in_list: false
---

# Project Overview
For this project, I classied celestial objects into galaxies, stars, and quasars. This was my submission to DS3 Datathon. 

I used machine learning techniques such as decision trees and random forests to make predictions about the class of celestial object given information about telescope angles, various photometric filters, redshift values, and more. A significant challenge in project was my lack of domain knowledge and I learned on the fly about new subjects to create models that are appropriate in both statistics and the domain. 


---

# Project Content

## Introduction
This project aims to develop a predictive model for the classification of celestial objects, a critical aspect of astronomical research. Leveraging data from the Sloan Digital Sky Survey, which includes measurements such as telescope angles, photometric filters, and redshift values, we aim to predict whether a celestial object is a star, galaxy, or quasar. Processing this information to make timely decisions is important because asstronomers need to configure their telescopes accordingly before the target objects become unobservable (SDSS). We will explore decision trees and random forests to make predictions. 


## Data

The data was split into training and testing datasets with 50,000 observations each by the Hackathon facilitators. Here is a look at the variables:

![Celestial Variables](/images/Screenshot-2024-01-21-at-00.05.09.png)

All variables are currently numeric. However, some are not appropriate for analysis as is.

For example, all of the variables with names ending in ID use numbers as 




https://skyserver.sdss.org/dr1/en/sdss/data/data.asp
