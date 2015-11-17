---
layout: post
title: 'Standord Machine Learning Class: Week5 Assignment'
date: 2015-11-08 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## ex4.m

> implement the backpropagation algorithm for neural networks and apply it to the task of hand-written digit recognition.

- Plot Data (in ex4data1.mat)

![ex4_plotting_data.png](http://imgur.com/tY8bXI9.png)

- Feedforward Using Neural Network and Compute Cost at parameters (loaded from ex4weights)

<script src="https://gist.github.com/joyhuang9473/790352737fe959821453.js"></script>

- Cost function with regularization

lambda: 1

<script src="https://gist.github.com/joyhuang9473/540e0b501c927f583a3f.js"></script>

- Random initialization weights

symmetry breaking: initialize weights

Theta(j, i) = RABD_NUM\*(2\*INIT_EPSILON) - INIT_EPSILON

RABD_NUM: between 0 to 1

- Complete backpropagation and check Neural Network Gradients

generate some 'random' test data and test

input_layer_size: 3

hidden_layer_size: 5

num_labels: 3

m: 5

<script src="https://gist.github.com/joyhuang9473/3fc1b204488622e9c307.js"></script>

- Regularized Neural Networks

lambda: 3

<script src="https://gist.github.com/joyhuang9473/d86452cbac7ee04a5380.js"></script>

- Training Neural Network

lambda: 1

<script src="https://gist.github.com/joyhuang9473/235a373f8de7658789a0.js"></script>

- Visualizing Weights

> displaying the hidden units to see what features they are capturing in the data.

displaying images of Theta1

![ex4_visualizing_nn.png](http://imgur.com/gLJ5kVf.png)
