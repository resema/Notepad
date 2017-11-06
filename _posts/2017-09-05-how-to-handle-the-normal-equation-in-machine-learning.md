---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: How to handle the Normal Equation in Machine Learning
tags: MachineLearning Calculus
description: Computing parameter analytically in the normal equation
headline: Normal Equation
categories:
  - Calculus
  - MachineLearning
  - Mathematics
---
>&quot;God does not care about our mathematical difficulties. He integrates empirically.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Normal Equation
The normal equation solves without iterating for the minima of the cost function. As a result it returns the $$\theta$$ where the cost function is at its minimum.

$$ \theta = (X^TX)^{-1}X^Ty $$

## Comparison with Gradient Descent

### Normal Equation
- No need to choose $$\alpha$$
- Don't need to iterate
- Need to compute $$(X^TX)^{-1}$$
- Slow if $$n$$ is very large

### Gradient Descent
- Need to choose $$\alpha$$
- Needs many iterations
- Works well even when $$n$$ is large
