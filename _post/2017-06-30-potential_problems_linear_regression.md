---
title: Potential Problems of Linear Regression
desc: Linear Regression is one of the most basic and most commonly used prediction techniques known to humans, with applications in diverse fields. Unfortunately, the technique is frequently misused and misunderstood. Part of the difficulty lies in the fact that a great number of people using linear regression have just enough training to be able to apply it, but not enough to training to see why it often shouldn’t be applied. 
author: ashmin
tags: linear regression problems collinearity correlation outlier
image: potential_problems.png
layout: post
mathjax: true
permalink: /potential_problems_of_linear_regression/
---

* Do not remove this line (it will not be displayed) 
{:toc}

## Potential Problems

When a linear regression model is fit to a particular data set, many problems might occur. 

Few of the most common problems are:

* **Non-Linearity of the data:** The linear regression assumes that there is a straight-line relationship between the predictors and the response. If the true relationship is not linear then all the conclusions made from the model are invalid and the prediction accuracy isn’t even great. In such cases a residual plot should be drawn to find if the relationships are non-linear in nature and if so, then the non-linear transformations of the predictors like $log X, X^2 or \sqrt{X}$ can be used in the regression model.

* **Correlation of error terms:** Linear regression is based on assumption that the error terms are uncorrelated and the regression coefficients are based on these uncorrelated regression coefficients. If the error terms are correlated then the estimated standard errors will underestimate the true standard errors so the confidence interval would be narrower than they should be and the p-values associated with the model would be lower than they should be making some predictors as significant though they are not. Correlation in error terms is frequently found in time series data. Data at discrete points in time would have positively correlated errors. To determine correlation in error terms for such cases, the residuals from the model as a function of time should be plotted. If there is no correlation among the error terms then there would be not visible pattern else adjacent residuals would have similar values.

* **Non-constant variance of error terms:** Another important assumption of the linear regression model is that error terms have a constant variance. But often it is the case that they are not. Non-constant variances in the errors (heteroscedasticity) can be found from the presence of a funnel shape in the residual plot. Such problems can be tackled by transforming the response using any concave function such as log or square-root. Such a transformation results in a great amount of shrinkage of the larger responses resulting in the reduction of heteroscedasticity. 

* **Outliers:** It is an observation point that is distant from other observations. It can arise from reasons like incorrect recording of an observation during data collection. Outliers can affect the RSE which in turn is used to compute confidence intervals, p-values and R2 values. Residual plots can be used to identify outliers but it is a difficult task to determine how large a residual needs to be in order to be considered as an outlier. Studentized residuals can be plotted in such cases as it the division of each residual by its estimated standard error. Observations with studentized residuals greater than 3 in absolute values are possible outliers. If error in data collection results in the outlier then that observation should be removed but it is also possible that a missing predictor variable resulted in outliers.

* **Points with high leverage:** In contrast to the outliers, there are observations with high leverage. Removing such points has a significant impact on the regression line. If couple of such observation make the entire model biased and invalidate true observations. So it is essential to identify such observations with high leverage. For a simple linear regression, observations with high leverage are easy to identify as such observations which lie outside the normal range of observations can be simply looked up. In multiple linear regression, there may be observations which lie well within the range of each individual predictor values but become unusual for the full set of predictors. To quantify an observation’s leverage, the leverage statistic is calculated. A high value of this statistic indicates an observation with high leverage. If the data has p predictors and a sample size of n, then the average leverage of all the observations is always equal to (p+1)/n. Any observation with value higher than this can be considered to have high leverage.

* **Collinearity:** This is the situation where two or more predictor variables are closely related to each other. As the predictors tend to increase or decrease simultaneously, it is difficult to find out the individual effects of the collinear variables on the response. These leads to large uncertainty in the coefficient estimates and a small change in data can lead to drastic changes in predictions. The correlation matrix of the predictors can be used to detect collinearity in most of the cases. In rare cases, collinearity exists between the predictors even if there is no correlation between them. This situation is called multicollinearity which can be assessed using variance inflation factor(VIF). VIF ranges from 1 upwards. The numerical value of VIF tells what percentage of variance is inflated for each coefficient. A VIF of 1.9 for example tells that the variance of a particular coefficient is 90% more than what can be expected in absence of multicollinearity. As a rule of thumb, when VIF is 1, it tells that there is a complete absence of collinearity while a value greater than 5 tells that the collinearity among the predictors is problematic. When collinearity is an issue while modelling then either the collinear variables can be dropped or they can be combined to form a single predictor (taking average or any other similar approach to combine them). Doing so won’t affect the regression fit.

## References

- James G., Witten D., Hastie T., Tibshirani R. (2013). An introduction to Statistical Learning. New York, NY: Springer