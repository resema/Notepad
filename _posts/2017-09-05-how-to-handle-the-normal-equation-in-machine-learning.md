---
layout: post
published: true
mathjax: true
featured: false
comments: false
title: How to handle the Normal Equation in Machine Learning
categories:
  - calculus
  - machinelearning
  - mathematics
tags: MachineLearning Calculus
description: Computing parameter analytically in the normal equation
headline: Normal Equation
---
>&quot;God does not care about our mathematical difficulties. He integrates empirically.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Normal Equation

$$ \theta = (X^TX)^{-1}X^Ty $$

## Comparison with Normal Equation

### Normal Equation
- No need to choose \\(\alpha)\\
- Don't need to iterate
- Need to compute $$(X^TX)^{-1}$$
- Slow if $$n$$ is very large

### Gradient Descent
- Need to choose $$\alpha$$
- Needs many iterations
- Works well even when $$n$$ is large
