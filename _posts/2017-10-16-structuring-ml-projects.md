---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Structuring ML Projects
description: An introduction about structuring ML projects
headline: Structuring ML Projects
categories:
  - NeuralNetworks
  - MachineLearning
tags: Coursera NeuralNetwork MachineLearning
---
>&quot;Nothing that I can do will change the structure of the universe.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Orthogonalization
Knowing what to tune in order to try to achieve one effect. This is a process we call orthogonalization.
The different effects should be orthogonal to each other, meaning there should be NO interferences between different features.

## Evaluation Metric

### Single Number Evaluation Metric
$$F1_{score}$$ = *Average* of **P** and **R**
where P is **Precision** and R is **Recall**.

**Precision** is the % of correctly recognized entity out of % of entites in the set. **Recall** on the otherside is the % of actual entities of correctly recognized.

### Satisficing And Optimizing Metric
**Accuracy** is has to be optimized and **Running Time** has to be satisfied.

**False Positive** is the parameter of recognizing an entity even if it is not.

## Train/Dev/Test Distribution And Size
The distribution has a large impact on the project. The dev set is also called hold out cross validation set.
Dev and test set should come from the same distribution.

### Guideline
Choose a dev set and test set to reflect data you expect to get in the future and consider important to do well on.