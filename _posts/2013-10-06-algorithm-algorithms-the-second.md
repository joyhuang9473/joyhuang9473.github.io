---
layout: post
title: '演算法 Algorithms : Homework 02'
date: 2013-10-06 09:14
comments: true
tags: 
---
1 . Describe a θ( nlgn ) ‐time algorithm that, given a set S of n integers and anotherinteger x, determines whether or not there exist two elements in S whose sum is exactly x.


2 . Although merge sort runs in θ( nlgn ) worst‐cast time and insertion sort runs in θ( n^2 ) worst‐cast time, the constant factors in insertion sort make it faster for small n. Thus, it makes sense to use insertion sort within merge sort when sub‐problems become sufficiently small. Consider a modification to merge sort in which n/k sub‐lists of length k are sorted using insertion sort and then merged using the standard merging mechanism, where k is a value to be determined.

- a. Show that the n/k sub‐lists, each of length k, can be sorted by insertion sort in θ(nk) worst‐case time.
- b. Show that the sub‐lists can be merged in θ( nlg(n/k) ) worst‐case time.
- c. Given that the modified algorithm runs in θ( nk+nlg(n/k) ) worst‐case time, what is the largest asymptotic (θ‐notation) value of k as a function of n for which the modified algorithm has the same asymptotic running time as standard merge sort?
- d. How should k be chosen in practice?

3 . Let A[1..n] be an array of n distinct numbers. If i < j and A[i] > A[j], then the pair (i,j) is called an inversion of A.

- a. List the five inversions of the array 〈2, 3, 8, 6, 1〉.
- b. What array with elements from the set {1, 2, ⋯, n} has the most inversions? How many does it have?
- c. What is the relationship between the running time of the insertion sort and the number of inversions in the input array? Justify your answer.
- d. Give an algorithm that determines the number of inversions in any permutation on n elements in θ( nlg(n) ) worst‐case time. (Hint: Modify merge sort.)

4 . Given two non‐negative function f, g (i.e. f, g : N → R*) such that f≠O(g), f≠θ (g), and f≠Ω(g).

5 . Problem 3‐3 Ordering by asymptotic growth rates

- a. Rank the following functions by order of growth; that is, find an arrangement g1, g2, …, g30 of the functions satisfying g1 = Ω(g2), g2 = Ω(g3), …, g29 = Ω(g30). Partition your list into equivalence classes such that functions f(n) and g(n) are in the same class if and only if f(n) = Ѳ( g(n) ).

(pic)

- b. Give an example of a single nonnegative function f(n) such that for all functions gi(n) in part (a), f(n) is neither O( gi(n) ) nor Ω( gi(n) ).