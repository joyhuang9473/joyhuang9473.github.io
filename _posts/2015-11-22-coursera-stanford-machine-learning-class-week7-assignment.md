---
layout: post
title: 'Standord Machine Learning Class: Week7 Assignment'
date: 2015-11-22 12:00
comments: true
tags: [machine-learning, Coursera, Stanford]
categories: [post-machine-learning]
---

## ex6.m

> you will be using support vector machines (SVMs) with various example 2D datasets.

- Plot Data (in ex6data1.mat)

![ex6_plotting_ex6data1.png](http://imgur.com/RDBi7t4.png)

- Plott decision boundary (ex6data1.mat)

SVM with Linear Kernel

> try using different values of the C parameter with SVMs. Informally, the C parameter is a positive value that controls the penalty for misclassified training examples.

![ex6_plotting_decision_boundary_with_C_1.png](http://imgur.com/wyWKeEQ.png)

![ex6_plotting_decision_boundary_with_C_100.png](http://imgur.com/eaTHemS.png)

- Plot Data (in ex6data2.mat)

![ex6_plotting_ex6data2.png](http://imgur.com/3dM01Ya.png)

- Train SVM with RBF Kernel and plot decision boundary (in ex6data2.mat)

C: 1, sigma: 0.1

![ex6_plotting_decision_boundary_with_rbf_kernel.png]()

- Plot Data (in ex6data3.mat)

![ex6_plotting_ex6data3.png](http://imgur.com/UWTOjjx.png)

- Try different SVM Parameters to train SVM with RBF Kernel

> Automatically choose optimal C and sigma based on a cross-validation set.

C list: [0.01 0.03 0.1 0.3 1 3 10 30]

sigma list: [0.01 0.03 0.1 0.3 1 3 10 30]

=> optimal C = 1 and sigma = 0.1

<script src="https://gist.github.com/joyhuang9473/073c860c60c72c235b24.js"></script>

![ex6_plotting_decision_boundary_with_optimal_svm_parameters.png](http://imgur.com/VrmJdJU.png)

## ex6_spam.m

> you will be using support vector machines to build a spam classifier.

> For the purpose of this exercise, you will only be using the body of the email (excluding the email headers).

- Preprocess sample email (in emailSample1.txt, vocab.txt)

> convert each email into a vector of features

> Given the vocabulary list, we can now map each word in the preprocessed emails into a list of word indices that contains the index of the word in the vocabulary list.

Lower-casing, Stripping HTML, Normalizing URLs, Normalizing Email Addresses, Normalizing Numbers, Normalizing Dollars, Word Stemming, Removal of non-words

vocabulary list: a list of 1899 words

<script src="https://gist.github.com/joyhuang9473/2e5a31ab1507978cc391.js"></script>

- Extracte Features from Emails (in emailSample1.txt)

> the feature xi ∈ {0, 1} for an email corresponds to whether the i-th word in the dictionary occurs in the email. That is, xi = 1 if the i-th word is in the email and xi = 0 if the i-th word is not present in the email.

<script src="https://gist.github.com/joyhuang9473/e8b8e53cdb221f4833de.js"></script>

- Train Linear SVM for Spam Classification (in spamTrain.mat, spamTest.mat)

> train a SVM to classify between spam (y = 1) and non-spam (y = 0) emails.

spamTrain.mat: 4000 training examples of spam and non-spam email

spamTest.mat: 1000 test examples

<script src="https://gist.github.com/joyhuang9473/9f26dadcca367c6b2643.js"></script>

## Trouble shooting:

- error on plotting the decision boundary of SVM with RBF Kernel

<script src="https://gist.github.com/joyhuang9473/3c6f97b25b70c1059425.js"></script>

Solution:

rewrite visualizeBoundary.m line 21:

=> contour(X1, X2, vals, [1 1], 'LineColor', 'b');

[related discussions](https://www.coursera.org/learn/machine-learning/programming/e4hZk/support-vector-machines/discussions/WCwK_XwqEeWb4g4qCdqdUQ)

## Reference

[黄海广: 斯坦福大学机器学习课程个人笔记完整版](http://wenku.baidu.com/view/99b86f70650e52ea54189862.html###)

[知乎: 机器学习有很多关于核函数的说法，核函数的定义和作用是什么？](http://www.zhihu.com/question/24627666)

[Quora: What are Kernels in Machine Learning and SVM?](https://www.quora.com/What-are-Kernels-in-Machine-Learning-and-SVM)
