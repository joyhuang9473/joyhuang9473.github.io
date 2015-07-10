---
layout: post
title: '演算法 Algorithms : Homework 05'
date: 2013-10-30 16:40
comments: true
tags: [Algorithms]
---
1 . Exercises 15.1‐2
Show, by means of a counterexample, that the following "greedy" strategy does not always determine an optimal way to cut rods. Define the density of a rod of length i to be pi / i, that is, its value per inch. The greedy strategy for a rod of length n cuts off a first piece of length i, where 1 ≤ i ≤ n, having maximum density. It then continues by applying the greedy strategy to the remaining piece of length n‐i.

2 . Exercises 15.1‐3
Consider a modification of the rod‐cutting problem in which, in addition to a price pi for each rod, each cut incurs a fixed cost of c. The revenue associated with a solution is now the sum of the prices of the pieces minus the costs of making the cuts. Give a dynamic‐programming algorithm to solve this modified problem.

3 . Exercises 15.1‐4
Modify MEMORIZED‐CUT‐ROD to return not only the value but the actual solution, too.

4 . Exercises 15.2‐1
Find an optimal parenthesization of a matrix‐chain product whose sequence of dimensions is《5, 10, 3, 12, 5, 50, 6》.

5 . Exercises 15.2‐4
Describe the subproblem graph for matrix‐chain multiplication with an input chain of length n. How many vertices does it have? How many edges does it have, and which edges are they?

6 . Exercises 15.3‐1
Which is a more efficient way to determine the optimal number of multiplications in a matrix‐chain multiplication problem: enumerating all the ways of parenthesizing the product and computing the number of multiplications for each, or running RECURSIVE‐MATRIX‐CHAIN? Justify your answer.

7 . Problems 15‐3 Bitonic Euclidean traveling‐salesman problem
(Page 405)