---
title: Accessing Model Accuracy
desc: “There is no free lunch in statistics!” For a particular dataset, one specific method may work best, but some other method may work better on a similar but different data set. So, it is very important to decide which method gives the best results for the data. Selecting the best approach is one of the most challenging tasks in machine learning. Measuring data accuracy hence is vital for any data scientist.
author: ashmin
tags: Fit Bias Variance Trade-Off KNN Bayes
image: model_accuracy.png
layout: post
mathjax: true
permalink: /accessing-model-accuracy/
---

* Do not remove this line (it will not be displayed) 
{:toc}

## Measuring quality of fit

In order to evaluate the performance of a statistical learning method on a given data set, its essential to measure how well the predictions actually match the observed data, so its necessary to quantify the extent to which the predicted response value for a given observation is close to the true response value for that observation. For regressions, the most common measurement used is mean square error (MSE).

$MSE = \frac{1}{n}\sum_{i=1}^n (y_i - \hat{f}(x_i))^2$

where $\hat{f}(x_i)$ is the prediction that $\hat{f}$ gives for the *i*th observation. The MSE is small if the prediction responses are very close to the true responses and will be large if the differences between predicted responses and true responses is high.

The MSE calculated using the training data used to fit the model is called the training MSE but it is not very important as accuracy of predictions obtained for unseen test data is key for any problem rather than the accuracy of the method used for training data.

e.g. An algorithm being used to forecast stock prices on previous stock returns should be able predict future prices of stocks with high accuracies rather than accuracies of the historical data.

For a large number of test observations, the average squared prediction error is used for measurement of accuracy given by the formula:

$Ave(y_0 - \hat{f}(x_0))^2$

where (*x*<sub>0</sub>,*y*<sub>0</sub>) is a previously unseen test observation. The average value of the test MSE is desired to be kept as low as possible.

In scenarios where test data is available, the best model is the one which gives the lowest test MSE. But in cases where test observations are not available, the best model would be the one which gives the lowest training MSE. But in such cases, there is no surety that a model with lowest training MSE would give the lowest test MSE. Methods where training MSE is low but test MSE is high are said to be overfitting the data. In such cases, the methods tend to work hard to find patterns in the training data and might pick up patterns that are cause because of a random value or an outlier rather than the true properties of the data. The test MSE would be high in such cases as the supposed patterns found in the training data doesn’t exist for in the test data. Regardless of the data, training MSE is always expected to be smaller as the learning methods tend to minimize the training MSE.

## Bias-Variance Trade-Off

Bias is the difference between the expected value and the true value of the predicted response. 

Variance on the other hand is the squared deviation of a random variable from its mean and it measures how far a set of numbers are spread out from their mean.

The expected test MSE for a given value *x*<sub>0</sub> is mathematically proved to be the sum of the variance of $\hat{f}(x_0)$, the squared bias of $\hat{f}(x_0)$ and the variance of the error term.

$E(y_0-\hat{f}(x_0))^2 = Var(\hat{f}(x_0)) + [Bias(\hat{f}(x_0))]^2 + Var(ϵ)$

where $E(y_0-\hat{f}(x_0))^2$ is the average test MSE obtained if f is repeatedly estimated using a large number of training sets and tested each at *x*<sub>0</sub>.

The overall expected test MSE is computed by averaging $E(y_0-\hat{f}(x_0))^2$ over all the possible values of *x*<sub>0</sub> in the test data set. The above equation tells that in order to minimize the expected test error, a learning method with low variance and low bias needs to be achieved and the test MSE can never go down below the variance of the irreducible error term.

Here variance refers to the amount by which $\hat{f}$ would change if estimated using a different training data set. Different training data sets will result in different $\hat{f}$. If a method has high variance then, minor changes in the training data can result in large changes in $\hat{f}$.

Bias refers to the error that is introduced by approximating a complicated real-life problem by a simple model. Linear regression for example assumes that there is a linear relationship between the predictors and the response which is not possible in real life so there is always some bias in the estimation of f while using linear regression. More flexible methods result in low bias.

In more flexible methods the variance increases while the bias reduces. The relative change of these quantities determines whether test MSE increases or decreases. If we increase flexibility of a method then the bias tends to initially decrease faster than the variance increases and the test MSE reduces. But after a point, if flexibility is increased then the bias doesn’t change much but the variance increases and consequently the test MSE increases.

A good performing model requires low variance and low squared bias. This relationship between bias, variance and test MSE is called as the bias-variance trade-off. This is called trade-off as it is easy to obtain a method with extremely low bias but high variance or a method with low variance yet high bias. Finding a method in which both variance and squared bias is low is quite a challenge for a data scientist.

In a classification problem, the most common approach for quantifying the accuracy of the prediction is the training error rate which is the proportion of mistakes made if apply the predictions to the training observations. It is given by the formula:

$\frac{1}{n} \sum_{i=1}^n I(y_i \ne \hat{y_i})$

where $\hat{y_i}$ is the prediction for the *i*th observation using $\hat{f}$. 

$I(y_i \ne \hat{y_i})$ equals 1 if $y_i \ne \hat{y_i}$ and 0 if $y_i = \hat{y_i}$. A zero value indicates correct classification.

The above equation is called training error rate as if uses data which was used to train the classifier. Similarly, the test error rate is given as

$Ave(I(y_i \ne \hat{y_i}))$ where $\hat{y_0}$ is the predicted label from the classifier being used to the test observation with predictor *x*<sub>0</sub>. A good classifier has small test error.

## Bayes Classifier

The test error rate can be theoretically minimized, on average, by a simple classifier that assigns each observation to the most likely class given its predictor values. This means that we should simply assign a test observation with predictor vector *x*<sub>0</sub> to the class *j* for which <code>Pr(Y = <i>j</i>|X = <i>x</i><sub>0</sub>)</code> is largest. This is called conditional probability which means it’s the probability of Y = *j* for a given predictor vector *x*<sub>0</sub>. This simple classifier is called as Bayes classifier. If in a problem there are two possible response values a and b, then the Bayes classifier corresponds to predicting class a if <code>Pr(Y = 1| X = <i>x</i><sub>0</sub>) > 0.5 </code> or class b otherwise. If the probability is exactly 50% for a prediction, then it is called the Bayes decision boundary.

Bayes classifier produces the lowest possible test error rate which is called the Bayes error rate which is given by <code>1 – E(max<sub>j</sub> Pr(Y = <i>j</i>|X))</code> where the expected value averages the probability over all the possible values of X. The Bayes error rate is analogous to the irreducible error.

## K-Nearest Neighbors (KNN)

For real data, the conditional distribution of response for the given qualitative predictors is impossible. So what can be done in turn is classify a given observation to the class with highest estimated probability. One of such methods is K-Nearest Neighbors classifier.

The K in the KNN is any positive integer. For a test observation x<sub>0</sub>, the KNN classifier first identifies the K points in the training data that are closest to x<sub>0</sub> and then estimates the conditional probability for class <i>j</i>  as a fraction of the points in N<sub>0</sub> whose response values equals *j* as:

$Pr(Y = j \| X = x_0) = \frac{1}{K} \sum_{i \in N_0} I(y_i = j)$

KNN simply applies Bayes rules and classifies the test observation x<sub>0</sub> to the class with largest probability. The value of K is important for the KNN classifier. If K = 1, the training error rate is 0 but the test error rate may be quite high. Low K values give more flexible methods and the flexibility decreases with increasing K. Choosing the level of flexibility is hence critical to the success of a statistical learning method.



## References

- James G., Witten D., Hastie T., Tibshirani R. (2013). An introduction to Statistical Learning. New York, NY: Springer