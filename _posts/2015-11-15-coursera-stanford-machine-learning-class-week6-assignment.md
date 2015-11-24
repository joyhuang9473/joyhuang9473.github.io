---
layout: post
title: 'Standord Machine Learning Class: Week6 Assignment'
date: 2015-11-15 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## ex5.m

> implement regularized linear regression and use it to study models with different bias-variance properties.

- Plot Data (in ex5data1.mat)

![ex5_plotting_data.png](http://imgur.com/93Cp93w.png)

- Compute Regularized Linear Regression Cost

lambda: 1, theta: [1 ; 1]

<script src="https://gist.github.com/joyhuang9473/49e4ec6b0893ea82a274.js"></script>

- Compute Regularized linear regression gradient

lambda: 1, theta: [1 ; 1]

<script src="https://gist.github.com/joyhuang9473/3494fcd5fde3f80b5728.js"></script>

- Train linear regression and plot fit over the data

lambda: 0

![ex5_trained_linear_regression.png](http://imgur.com/YtBL0Fk.png)

- Comput train error and cross validation error for linear regression

lambda: 0

training error: evaluate the training error on the first i training examples (i.e., X(1:i, :) and y(1:i))

cross-validation error: evaluate on the _entire_ cross validation set (Xval and yval).

<script src="https://gist.github.com/joyhuang9473/5540eaa4359125e88e5c.js"></script>

- Plot learning curve for linear regression

> Since the model is underfitting the data, we expect to see a graph with "high bias"

![ex5_learning_curve_for_linear_regression.png](http://imgur.com/KWK4kUN.png)

- Map X onto Polynomial Features and Normalize

X_poly(i, :) = [X(i) X(i).^2 X(i).^3 ...  X(i).^p]

<script src="https://gist.github.com/joyhuang9473/04f16509b897ed2ab102.js"></script>

- Train Polynomial regression and plot fit over the data

![ex5_trained_polynomial_regression.png](http://imgur.com/w8bsAlv.png)

- Comput train error and cross validation error for polynomial regression

lambda: 0

training error: evaluate the training error on the first i training examples (i.e., X(1:i, :) and y(1:i))

cross-validation error: evaluate on the _entire_ cross validation set (Xval and yval).

<script src="https://gist.github.com/joyhuang9473/1cbf0c9df2da3b667c8e.js"></script>

- Plot learning curve for polynomial regression

> Since the model is overfitting the data, we expect to see a graph with "high variance"

![ex5_learning_curve_for_polynomial_regression.png](http://imgur.com/WsiFwAP.png)

- Test various values of lambda and compute error

<script src="https://gist.github.com/joyhuang9473/4a642b25bd987c77a444.js"></script>

- Plot validation curve

> use validation curve to select the "best" lambda value

the best value of lambda is around 3

![ex5_validation_curve_for_polynomial_regression.png](http://imgur.com/887VVKb.png)
