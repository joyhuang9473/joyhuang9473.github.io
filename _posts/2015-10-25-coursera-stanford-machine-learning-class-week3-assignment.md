---
layout: post
title: 'Standord Machine Learning Class: Week3 Assignment'
date: 2015-10-25 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## ex2.m

> implement logistic regression and apply it to two different datasets (ex2data1.txt, ex2data2.txt)

- Plot Data (in ex2data1.txt)

![ex2_plotting_data.png](http://imgur.com/RXDSOwp.png)

- Compute Cost and Gradient

hypothesis function: 1./(1+e.^(-1*(X*theta)))

<script src="https://gist.github.com/joyhuang9473/8b2d74f94c2c072b413e.js"></script>

- Learning parameters using fminunc

initial theta: zeros, iteration: 400

<script src="https://gist.github.com/joyhuang9473/635f38f09e0d5236fafe.js"></script>

- Plot Decision Boundary

![ex2_plotting_decisionBoundary.png](http://imgur.com/OtGyVq8.png)

- Predict and Accuracies

> use the logistic regression model to predict the probability that a student with score 45 on exam 1 and score 85 on exam 2 will be admitted.

<script src="https://gist.github.com/joyhuang9473/3a36b3c1b4284f43f422.js"></script>

## ex2_reg.m

> The axes are the two test scores, and the positive (y = 1, accepted) and negative (y = 0, rejected) examples are shown with different markers.

- Plot Data (in ex2data2.txt)

![ex2_reg_plotting_data.png](http://imgur.com/paDbfw1.png)

- Add Polynomial Features and Compute Cost

original X: [X1 X2]

mapFeatured X: [X1 X2 (X1.^2) (X2.^2) (X1*X2) (X1*X2.^2) ...]

hypothesis function: 1./(1+e.^(-1*(X*theta)))

<script src="https://gist.github.com/joyhuang9473/ad85e427bdafc28dda0a.js"></script>

- Plot Decision Boundary with lambda 0

![ex2_reg_plotting_decisionBoundary_with_lambda_0.png](http://imgur.com/fi7SjLI.png)

<script src="https://gist.github.com/joyhuang9473/0b2386d4fd000c142537.js"></script>

- Plot Decision Boundary with lambda 1

![ex2_reg_plotting_decisionBoundary_with_lambda_1](http://imgur.com/zCFrSK8.png)

<script src="https://gist.github.com/joyhuang9473/d2a03915e1d5b7b3d7be.js"></script>

- Plot Decision Boundary with lambda 100

![ex2_reg_plotting_decisionBoundary_with_lambda_100](http://imgur.com/mBxdkwR.png)

<script src="https://gist.github.com/joyhuang9473/da48d195b70e123cb43d.js"></script>