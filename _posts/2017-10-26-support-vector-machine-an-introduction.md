---
layout: post
published: false
mathjax: true
featured: false
comments: true
title: Support Vector Machine - An Introduction
description: An introduction to SVM
headline: Support Vector Machine - An Introduction
categories:
  - MachineLearning
tags: Coursera MachineLearning
---
>&quot;Imagination is more important than knowledge. Knowledge is limited. Imagination encircles the world.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Support Vector Machine
SVM is an alternative view for logistic regression. Starting from logistic regression we can derive a good understanding of basic SVM.

![svm_formula.png]({{site.baseurl}}/images/posts/SupportVectorMachine_AnIntroduction/svm_formula.png)

Also helpfull is the concept of **large margins** or **decision boundaries** to help understand what SVM's are doing under the hood.

### SVM Decision Boundary
$$min C \sum_{i=1}^{m}\left y^{(i)} cost_1(\theta^T x^{(i)}) + (1-y^{(i)} cost_0(\theta^T x^{(i)})\right + \frac{1}{2}\sum_{i=1}^n \theta_j^2$$

## Kernels

