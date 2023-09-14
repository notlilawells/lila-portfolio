---
date: '2023-09-14T20:45:17.459Z'
title: Nonlinear Modeling to Predict Wine Quality
tagline: Data Science / Machine Learning
preview: >-
  Nonlinear modeling to predict wine quality in the Vinho Verde region.
image: 'https://images.unsplash.com/ckjuMXBLu7o'
---
# Overview

A wine’s quality is an established metric for its price. Yet determining wine quality has largely been a subjective practice—determined by oenologists and sommeliers. 

However, a new method is emerging in the industry to reduce the human error and subjectivity of wine quality determination -- evaluating quality based on a wine’s physical and chemical attributes. As quality equates to price, wine producers, mass consumers (like restaurants and bars), and wine evaluators like oenologists and sommeliers all have a vested interest in furthering this new mathematical method to avoid subjective error. 

By analyzing data compiled from over 6,000 wines in the Vinho Verde region from 2004 to 2007, we build 3 linear and 9 nonlinear machine learning, tree-based, and boosting models to predict wine quality based on a wine’s physical and chemical attributes. We implement several techniques (rigorous hyperparameter tuning, cross-validation, voting and stacking ensemble methods) to answer this question—optimizing Root Mean Squared Error (RMSE). 

Our finalized ensemble yields RMSE of 0.642. This translates to the ability to correctly predict quality scores on a scale from 1 to 10 with a ±1 error. Thus, our ensemble offers our stakeholders a robust method to determine, validate, and standardize wine quality scores.

# Models Developed 

> 1. Intercept base model
> 2. Ridge & lasso regression 
> 3. MARS
> 4. Decision trees
> 5. Bagging decision trees
> 6. Random forest
> 7. AdaBoost
> 8. Gradient Boost 
> 9. XGBoost
> 10. CatBoost
> 11. LightGBM

# Data Source

We elected to use data set entitled "Wine Quality Data Set" from the UCI Machine Learning Repository. The dataset can be accessed [here](https://archive.ics.uci.edu/dataset/186/wine+quality). This dataset helped us to address our project by comprehensively cataloging the different qualities of over 6,000 red and white variants of Portuguese "Vinho Verde" wine from 2004 to 2007. A wine's quality is based on its physicochemical properties, and this data set included 10 of such properties - thus reinforcing its use in our goal to predict wine quality.

Our response variable here was wine quality, represented by the variable quality in this dataset. This value ranged from 1 to 10. The predictors we used included physicochemical attributes of wine such as pH, density, fixed and volatile acidity, citric acid content, residual sugars, chlorides, free sulfur dioxides and total sulfur dioxides, sulphates, alcohol quality, and wine type (red or white). There are 11 total predictors in the dataset: 10 continuous predictors one categorical predictor. There are 6,497 total observations in this dataset, and each observation represents a different wine sample.

# Conclusions & Recommendations

From the development of our ensemble model, we conclude that our model can predict wine quality based on physicochemical properties with an RMSE of 0.642. This translates to the ability to correctly predict quality score with a  error when considering rounding.

While there remains much room for improvement, we posit that our model is and will be still generally useful for the wine industry, where expert but subjective opinions currently determine quality. There are many use cases where we recommend that our stakeholders implement our model.

For wine producers, our model can help inform which grape strains to grow in order to produce the highest quality wines. Wine producers can analyze the physicochemical makeup of high quality wines, and grow new strains that with properties that emulate those wines. In addition, wine producers can use the model to determine wine quality before undergoing the certification process. If a certain wine is predicted to be of poor quality, it would be beneficial for wine producers to focus on other wines.

For restaurant and bar owners, the objective measure of quality can give a metric to determine appropriate pricing of the wines they purchase from producers. If able to obtain physicochemical properties independently of wine producers, restaurant owners can confirm the validity of wine quality reported by wine producers or sommeliers.

Finally, our model can assist oenologists and sommeliers make quicker, more standardized assessments of wine quality. The model's assessment serves as an auxilliary mechanism, another datapoint upon which these experts can weigh to determine the quality of wines.

Our model is currently limited to predicting the quality of wines in the Vinho Verde region. Wines from different regions have distinct flavor profiles based on environmental and procedural factors determining wine production. This leads to distinct assignments of quality between different regions of the world. If the climate of the Vinho Verde region changes significantly in the future, we would need to obtain updated datapoints to retrain our model. In addition, we need to obtain more samples of wines that span the entire numerical range of quality 0-10, so that the model can directly learn from samples with qualities at the ends of the spectrum.

# Key Links 
> 1. [Download the project report](https://github.com/notlilawells/Saturn-303-3/blob/main/Project-Report/Project_Report_Saturn.ipynb) 
> 2. [View the project code](https://github.com/notlilawells/Saturn-303-3/blob/main/Project-Report/Project_Code_Saturn.ipynb)
> 3. [Explore the full GitHub repository](https://github.com/notlilawells/Saturn-303-3)
