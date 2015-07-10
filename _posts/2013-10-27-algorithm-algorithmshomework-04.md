---
layout: post
title: '演算法 Algorithms : Homework 04'
date: 2013-10-27 13:17
comments: true
tags: 
---
1 . Exercise 4.3‐9:
Solve the recurrence T(n) = 2T(n^(1/2)) +1 by making a change of variables. Your solution
should be asymptotically tight. Do not worry about whether values are integral.

2 . Problem 4‐1: Recurrence examples
Give asymptotic upper and lower bounds for T(n) in each of the following
recurrences. Assume that T(n) is constant for n≦2. Make your bounds as tight as
possible, and justify your answers.

a . T(n) = 2T(n/2)+n^4
b . T(n) = T(7n/10)+n
c . T(n) = 16T(n/4)+n^2
d . T(n) = 7T(n/3)+n^2
e . T(n) = 7T(n/2)+n^2
f . T(n) = 2T(n/4)+n^(1/2)
g . T(n) = T(n-2)+n^2

3 . Exercise 4.5‐4:
Can the master method be applied to the recurrence T(n) = 4T(n/2) + n^2 * lgn ? Why or why not? Give an asymptotic upper bound for this recurrence.

4 . Exercise 4.2‐3
How would you modify Strassen’s algorithm to multiply n * n matrices in which n is not an exact power of 2? Show that the resulting algorithm runs in time θ(nlg7).

5 . Exercise 4.2‐5
V. Pan has discovered a way of multiplying 6868 matrices using 132,464 multiplications, a way of multiplying 70 * 70 matrices using 143,640 multiplications, and a way of multiplying 72 * 72 matrices using 155,424 multiplications. Which method yields the best asymptotic running time when used in a divide‐and‐conquer matrix‐multiplication algorithm? How does it compare to Strassen’s algorithm?

6 . Exercise 4.2‐7
Show how to multiply the complex numbers a  bi and c  di using only three multiplications of real numbers. The algorithm should take a, b, c, and d as input and produce the real component ac  bd and the imaginary component ad - bc separately.

7 . Ext. 3‐1
在課本4.1 節中(p.68)作者將stock buying problem 轉成 maximum‐subarray problem 再用Divide‐and‐conquer 的概念來解此問題，請給一個O(n)執行時間的 Pseudo code algorithm 直接解stock buying problem ， 無需再做任何 transformation。

8 . Ext. 4‐1
The input is a sequence of n integers with many duplications, such that the number of distinct integers in the sequence is O(log n).
(a) Design a sorting algorithm to sort such sequences using at most O(n log log n)
comparisons in the worst case.
(b) Why is the lower bound of sorting (n log n) not satisfied in this case?