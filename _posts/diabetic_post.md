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

By analyzing data compiled from 130 U.S. hospitals between 1999 and 2008, we explore the relationship between the factors associated with a patient’s initial hospital stay and their likelihood of readmission. We implement several techniques (SMOTENC, undersampling, OLS, cross-validation) and logistic regression to answer this question–optimizing model recall, precision, and False Negative Rate. **We find that a patient’s age, time spent in hospital, and number of inpatient visits increase their odds of readmission. Additionally, patients with many medication changes have decreased odds of readmission.** Thus, We recommend that our stakeholders be hyper-vigilant with patients who are older, spend significant time in the hospital, and have frequent inpatient stays, as these patients have the highest odds of being readmitted to hospital.

_Project Team: Lila Wells, Amy Wang, Anastasia Wei, Kaitlyn Hung_

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

# Finalized Model 

The finalized model is as follows: 

```py
readmitted = -1.9434 + (0.1791 * time_in_hospital) + (0.0296 * age) + (-0.0025 * time_in_hospital * age) + (-0.5601 * num_of_changes) + (0.1535 * number_inpatient)
```

Where `readmitted` is the binary response variable which takes on the value of zero when a patient is not readmitted within 30 days of their initial hospital stay, and 1 when the patient *is* readmitted in that time frame; `time_in_hospital` is the length of the patient's initial hospital stay (in days); `age` is the patient's age; `num_of_changes` is their humber of medication changes during their initial hospital stay; and `number_inpatient` is their number of previous inpatient hospital stays. 

# Findings at a Glance

1. A diabetic patient's odds of readmission increase by **22.29 %** with each additional day spent in the hospital during the patients initial hospital stay.

2. Their odds of readmission increase by **3.44 %** with each additional added decade in patient age (i.e., each decade-increase in a patient's age impacts these odds).

3. For a constant age **X**, the odds of readmission change by **0.1916 − X ∗ 0.0026** with each additional day spent in the hospital. In other words, as the decade of a patient's age increases, the additional day in the hospital will have a smaller effect in increasing the odds of readmission. We note, however, that conclusion (1) still holds. The reducing effect of age is small relative to the increase of readmission odds brought on by the additional day in the hospital, so the likelihood of readmission will overall still be increased.

4. A diabetic patient's odds of readmission decrease by **40.96 %** with each additional medication change.

5. Their odds of readmission increase by **16.65 %** with each additional inpatient hospital visit.

# Recommendations 

### Recommendation (1)

Regarding finding (1), it is imperative that healthcare providers be hyper-vigilant regarding the care of those who have long inpatient hospital stays. As the odds of being readmitted to the hospital within 30 days increases by 22.9% with each additional day spent in the hospital, patients with lengthy hospital stays are far more likely to have to go back to the hospital for further treatment. Per finding (3), the long hospital stay is caveated by how greater patient age slightly decreases the odds of returning to the hospital. According to the National Institute for Health, the average hospital stay in the U.S. is 5.5 days long. Thus, healthcare providers and patients alike should be notified if the patient's stay exceeds that average (as longer hospital stays may indicate that a patient is at a greater risk of readmission).

### Recommendation (2) 

Age is a large risk factor in determining hospital readmission, with the odds of readmission increasing 3.44% per decade increase of the patient's age (finding 2). We recommend that healthcare providers take additional measures to ensure diligent care for elderly patients. Specifically, readmission is often caused by poor transitions from the hospital to the next location of care and complications in the patient's illness. These causes may be countered, especially for elderly patients, by deliberately giving consultations to the patient's family and caregivers on care and reevaluating the patient's medication plan to ensure compliance.

### Recommendation (3)

As finding (4) notes, a patient’s odds of readmission decrease by 40.96% with every additional medication change during their initial hospital stay. Importantly, our population of interest is diabetic patients, whose variable blood sugar levels necessitate constant supervision and subsequent adjustments in insulin and related medications. As such, we recommend that, for diabetic patients undergoing an inpatient hospital stay, their medications be monitored and adjusted more frequently than that of non-diabetic patients. This may necessitate more frequent nurse visits to diabetic patients. For example, if nurses were to check on patients every 3 hours, we would recommend moving that interval up slightly (depending on hospital staffing) for diabetic patients (so instead of every 3 hours, diabetic patients are checked on and monitored every 1.5 to 2 hours). Increased monitoring may allow hospital staff to more accurately gauge a patient’s blood sugar levels and associated health risks (leading, thus, to an increased probability of medication or insulin adjustments that could decrease that diabetic patient’s risk of readmission).

### Recommendation (4) 

Inpatient hospital visits increase a patient's chance of readmission per finding (5). In light of this, we suggest that healthcare providers determine a patient's number of inpatient hospital visits while taking the patient's medical history. We suggest that patients be transparent about the number of their inpatient visits to the hospital. Healthcare administrators may assist the effort to obtain this information from each patient by supporting the implementation of a system that automatically tracks number of inpatient hospital visits, such as an electronic health record system.

# Key Links 
> 1. [Download the project report](https://github.com/AnastasiaKWei/Saturn/blob/main/Saturn_code.html) 
> 2. [View the project code](https://github.com/AnastasiaKWei/Saturn/blob/main/Saturn_code.html)
> 3. [Explore the full GitHub repository](https://github.com/AnastasiaKWei/Saturn)
