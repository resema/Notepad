---
layout: post
published: false
mathjax: true
featured: false
comments: false
title: Machine Learning - An Introduction
description: General Introduction to use Machine Learning
headline: Introduction
categories:
  - personal
  - calculus
  - machinelearning
tags: MachineLearning Introduction Coursera
---
>&quot;Imagination is more important than knowledge. Knowledge is limited. Imagination encircles the world.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Introduction

### Multiclass Classification

#### One-vs-All
![multiclass_classification.png]({{site.baseurl}}/images/posts/multiclass_classification.png)

### Problem of Overfitting
If we have too many features, the learned hypthesis may fit the training set very well ($$J(\theta) = \frac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})^2 = 0$$), but fail to generalize to new examples (predict prices on new examples).

The two terms of Bias and Variance are important for solving this issue.