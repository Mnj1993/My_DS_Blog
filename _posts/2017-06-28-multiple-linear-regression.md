---
title: Multiple Linear Regression
desc: Multiple linear regression is the most common form of linear regression analysis. As a predictive analysis, the multiple linear regression is used to explain the relationship between one dependent variable and two or more independent variables.
author: ashmin
tags: multiple regression linear
image: multiplelineareregression.png
layout: post
mathjax: true
permalink: /multiple-linear-regression/
---

* Do not remove this line (it will not be displayed) 
{:toc}

## Multiple Linear Regression

Simple linear regression is useful to predict a response on the basis of a single predictor variable but in real world data, more than one predictors are always found.

It is possible to find the simple linear regression of the response with each of the predictors individually but that would ignore the effect of other predictors while forming the regression coefficients. So, the simple linear regression should be extended to accommodate multiple predictors. If there are p distinct predictors, then the multiple linear regression would take the form:

$Y = β_0 + β_1X_1 + β_2X_2 + ... + β_pX_p + ϵ$

where $X_j$ represents the jth predictor and $β_j$ quantifies the association between the variable and the response. $β_j$ is the average effect on Y on a one unit increase in $X_j$ keeping all the other predictors fixed.

The least square approach can be used to estimate the regression coefficients and is given by

$RSS = \sum_{i=1}^n (y_i - \hat{β_0} - \hat{β_1}x_{i1} - \hat{β_2}x_{i2} - ... - \hat{β_p}x_{ip})^2$

The regression coefficients are complicated in comparison to the simple linear regression and are usually represented by matrix algebra.

In order to determine if there is relationship between the response and the predictors, F statistics is used. It is given by $F = \frac{(TSS-RSS)/p}{RSS/(n-p-1)}$.

A F value closer to 1 tells that there is no relationship between the response and the predictors. For F greater than 1, the vice versa is true.

It is very possible that all of the predictors are associated with the response but more often its just a subset of the predictors that is related. The task of determining which predictors are associated with the response in order to fit a single model involving only those predictors is called as variable selection.

There are $2^p$ models to be considered for p variables in each case. For bigger values of p, it is impossible to consider all the models. There are few methods which can be used to choose a smaller set of models for consideration.

* Forward selection: This is begun with a null model with no predictors but an intercept. Then p simple linear regressions are fitted and then the variable that results in the lowest RSS is added to the null model. This is continued till some stopping rule is satisfied.
    
* Backward selection: In this approach, all the variables in the model are selected and then the one with maximum p-value (least significant variable) is removed. The model is then fit with the existing variables and again the variable with largest p-value is removed. This is continued until all the variables have a p-value below some threshold or some stopping rule is reached.
    
* Mixed selection: This is a combination of forward and backward selection. It is started with no variables in the model and then the variable that provides best fit is added as in forward selection. More variables are kept on adding one by one. If at one point the p-value of certain variable goes beyond a threshold, then that variable is removed like backward selection. These forward and backward steps are continued until all the variables have low p-values.
    
Model fit is measured using RSE and $R^2$ statistics. A $R^2$ value close to 1 indicates that the model explains a large portion of the variance in the response variable. But adding of more variables always lead to an increase in the $R^2$ value even if the variables are not associated or correlated with the response variable. This is because adding a variable makes the model fit the training data more accurately though it might lead to overfitting.

## Extension of Linear Models

The standard linear regression model provides interpretable results and works quite well on many real-world problems but it makes several restrictive assumptions that are often violated in practice. Two of the most important assumptions state that the relationship between the predictors and the response are additive and linear. The additive assumption means that the effect of changes in a predictor on the response is independent on the values of other predictors. The linear assumption states that the change in response due to a one-unit change in the predictor is constant regardless its value. 

Adding interaction terms to a regression model can make the relationships between the variables in the models more interpretable. It can be done when the number of predictors is more than one. It can be as simple as the multiplication of the predictors. But if an interaction term is being added to the model, it is essential to include the main effects also even if their p-values are low or are not significant.

## References

- James G., Witten D., Hastie T., Tibshirani R. (2013). An introduction to Statistical Learning. New York, NY: Springer