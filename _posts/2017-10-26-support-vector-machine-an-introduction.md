---
layout: post
published: true
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
$$min C \sum_{i=1}^{m}\left y^{(i)} $$

## Kernels
![kernel_landmarks.png]({{site.baseurl}}/images/posts/SupportVectorMachine_AnIntroduction/kernel_landmarks.png)