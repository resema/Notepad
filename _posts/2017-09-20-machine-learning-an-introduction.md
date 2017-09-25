---
layout: post
published: false
mathjax: true
featured: false
comments: true
title: Machine Learning - An Introduction
description: General Introduction to use Machine Learning
headline: Introduction
categories:
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
If we have too many features, the learned hypthesis may fit the training set very well ( $$ J(\theta) = \frac{1}{2m}\sum_{i=1}^m(h_\theta(x^{(i)}) - y^{(i)})^2 = 0 $$ ), but fail to generalize to new examples (predict prices on new examples).

#### Adressing overfitting
Options:
1. Reduce number of features
  - Manually select which features to keep 
  - Model selection algorithm
2. Regularization
  - Keep all the features, but reduce magnitude/values of parameters $$\theta_j$$.
  - Works well when we have a lot of features, each of which contributes a bit to predicting $$y$$.

The two terms of Bias and Variance are important for solving this issue.

### Regularization
Small values for parameters $$\theta_0$$, $$\theta_1$$, ..., $$\theta_n$$
  - "simpler" hypothesis
  - less prone to overfitting

#### Implementation
$$J(\theta) = \frac{1}{2m} \[ \sum_{i=1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})^2 + \lambda \sum_{j=1}^n \theta_j^2 \]$$

```
for each i:
	dTheta_approx[i] = 1/2*Epsilon * ( J(theta_1, theta_2, ..., theta_i + Epsilon) - J(theta_1, theata_2, ..., theta_i - Epsilon) );
    CheckEuclideanDist((dTheta_approx - dTheta) / (dTheta_approx + dTheta))
```

Epsilon $$\epsilon$$ should be in the range of $$10^{-7}$$.

#### Additional Implementation Notes
- Don't use in training - only to debug
- If algorithm fails grad check, look at components to try to identify bug
- Remember regularization
- Doesn't work with dropout
- Run at random initialization; perhabs again after some training