---
layout: post
title: 'Standord Machine Learning Class: Week4 Assignment'
date: 2015-11-01 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## ex3.m

> implement one-vs-all logistic regression and neural networks to recognize hand-written digits.

- Plot Data (in ex3data1.mat)

![ex3_plotting_data.png](http://imgur.com/huVH9AS.png)

- Training One-vs-All Logistic Regression

hypothesis function: 1./(1+e.^(-1*(X*theta)))

K = 10 (0 to 9)

Iteration: 50

<script src="https://gist.github.com/joyhuang9473/0ca0a82a0b2616759a7e.js"></script>

- Predict for One-Vs-All

<script src="https://gist.github.com/joyhuang9473/8a964d894e25dc3aa1c4.js"></script>

## ex3_nn.m

>  implement a neural network to recognize handwritten digits using the same training set as before.

> provided with a set of network parameters (Θ(1),Θ(2)) already trained (in ex3weights.mat)

- Feedforward Propagation and Prediction

Loading Saved Neural Network Parameters in ex3weights.mat

<script src="https://gist.github.com/joyhuang9473/bc9786e6cb0ed377dc1f.js"></script>
