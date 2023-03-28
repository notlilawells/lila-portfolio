---
date: '2023-03-15T23:13:03.369Z'
title: Exploring Diabetic Readmissions
tagline: Data Science
preview: >-
  Modeling and regression to explore the relationship between the factors
  associated with a patient's initial hospital stay and their likelihood of
  readmission. 
image: 'https://source.unsplash.com/ne2mqMgER8Y'
---
# Overview

A hospital’s ability to release healthier patients is an established metric for its success. More recently, a hospital’s success has also been measured by its readmission rate – or the extent to which patients are being retreated within 30 days of their initial inpatient stay. Readmissions signal a breakdown in care that negatively impact a patient’s health and wallet, as well as hospital finances. Thus, patients, healthcare providers, and healthcare administrators have an interest in decreasing readmissions. 

By analyzing data compiled from 130 U.S. hospitals between 1999 and 2008, we explore the relationship between the factors associated with a patient’s initial hospital stay and their likelihood of readmission. We implement several techniques (SMOTENC, undersampling, OLS, cross-validation) and logistic regression to answer this question–optimizing model recall, precision, and False Negative Rate. We find that a patient’s age, time spent in hospital, and number of inpatient visits increase their odds of readmission. Additionally, patients with many medication changes have decreased odds of readmission. Thus, We recommend that our stakeholders be hyper-vigilant with patients who are older, spend significant time in the hospital, and have frequent inpatient stays, as these patients have the highest odds of being readmitted to hospital..

_Project Team: Lila Wells, Amy Wang, Anastasia Wei, Kaitlyn Hung_

# Key Links 
> 1. [Download the project report](http://www.google.com) 
> 2. [View the project code](http://www.google.com)
> 3. [Explore the full GitHub repository](http://www.google.com)


# Problem Statement

To approach our analysis, we first articulated a question to guide our modeling process: **What is the relationship between the different factors associated with a patient’s hospital stay and their likelihood of being readmitted to that hospital within 30 days?**


In this question, we are most interested in identifying the relationship between predictors (here, factors associated with a patient’s hospital stay) and a response (whether a patient is readmitted or not). Thus, our model is mainly concerned with inference.

# Data Source

In our project, we used a dataset entitled “Diabetes 130-US hospitals for years 1999-2008 dataset” from the UCI Machine Learning Repository. The dataset can be accessed [here](https://archive.ics.uci.edu/ml/datasets/Diabetes+130-US+hospitals+for+years+1999-2008#).

All data was collected between 1999 and 2008 from over 130 US hospitals and related care centers. The dataset contains over 10,000 entries, each corresponding to a patient with either Type 1 or Type 2 diabetes.

Observations had to satisfy the following criteria to be included in this dataset:

- The patient must have had an inpatient encounter (i.e., they must have been admitted to the hospital)
- The incident must have been a diabetic encounter (i.e., the patient had to have been a diabetic)
- The length of the patient’s hospital stay had to have been between 1 and 14 days
- Laboratory tests had to have been administered during the patient’s initial hospital stay
- The patient must have received medications during their hospital stay

We chose to use this dataset because it contains our variable of interest (whether a patient was readmitted or not) along with ~46 potential predictors to use to fit the model. This dataset is extremely robust and comprehensive, including information on over 10,000 patients in the US across a decade. This broad and comprehensive data increases the generalizability of our study’s findings. Its number of predictors also allows us to approach our problem from multiple perspectives: (1) the patient’s characteristics, (2) their hospital stay and medical history, and (3) the treatments administered to them.

# Stakeholders

XXX

# Finalized Model

XXX

# Recommendations

XXX