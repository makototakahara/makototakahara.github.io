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

 - id = Object Identifier, the unique value that identifies the object in the image catalog used by the CAS.
 - alpha = Right Ascension angle (at J2000 epoch).
 - delta = Declination angle (at J2000 epoch).
 - u = Ultraviolet filter in the photometric system.
 - g = Green filter in the photometric system.
 - r = Red filter in the photometric system.
 - i = Near Infrared filter in the photometric system.
 - z = Infrared filter in the photometric system.
 - run_ID = Run Number used to identify the specific scan.
 - rerun_ID = Rerun Number to specify how the image was processed.
 - cam_col = Camera column to identify the scanline within the run.
 - field_ID = Field number to identify each field.
 - spec_obj_ID = Unique ID used for optical spectroscopic objects (this means that 2 different observations with the same spec_obj_ID must share the output class).
 - redshift = redshift value based on the increase in wavelength.
 - plate = plate ID, identifies each plate in SDSS.
 - MJD = Modified Julian Date, used to indicate when a given piece of SDSS data was taken.
 - fiber_ID = fiber ID that identifies the fiber that pointed the light at the focal plane in each observation.
 - class = object class [GALAXY: galaxy, STAR: star or QSO: quasar object].

![Celestial Variables](/images/Screenshot-2024-01-21-at-00.05.09.png)

All variables are currently numeric. However, some are not appropriate for predictive modelling as it is. For example, all of the variables with names ending in ID are categorical, using numbers as labels for each category. After research into the meaning of each variable, we convert `id`, `run_ID`, `rerun_ID`,`cam_col`, `field_ID`, `spec_obj_ID`, `fiber_ID`, `plate`, `MJD` to categocial variables.

Next, we explore the numerical variables.

![Celestial Numerical Variables](/images/Screenshot-2024-01-21-at-00.16.47.png)

We see that the minimum of `u`, `g`, `z` is -9999.000000, which we would not expect in this context. Flux values represent the amount of light detected from a celestial object in a specific wavelength range, and negative flux values would not have a physical interpretation in this context (CITE). We find that it is the same observation with these values, so we remove this observation from the training dataset. 


## Exploratory Data Analysis

We plot a kernel density estimate Plot to summarize the distribution of the numerical variables for each class of celestial object. 

![Celestial KDE Plot](/images/Screenshot-2024-01-21-at-00.37.37.png)

For all of the variables except for `redshift`, we can observe varying distributions for each class. The KDE plot for `redshift` looks pelicular, and we dig deeper to find that all 10703 observations of the star class has redshift between -0.0042 and 0.0042. We also find that within this range, 97.9% of observations are of the star class.

![Celestial Star redshift](/images/Screenshot-2024-01-21-at-00.48.50.png)

We also perform a Chi-squared test to determine if there is a statistically significant relationship between each categorical variable and the respone variable `class`.

![Chi-squared test](/images/Screenshot-2024-01-21-at-00.51.46.png)

We see that `spec_obj_ID` does not have a statistically significant relationship with the predictor variable. With this information in mind, we move onto fitting a model. 



https://skyserver.sdss.org/dr1/en/sdss/data/data.asp
