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

### Splitting Data
In the old days it has been normal to split data to 
70% train and 30% test or 60% train, 20% dev and 20% test. 
But in modern times where we might have millions examples in our sets. Then it has become common to split into 98% train, 1%dev and 1% test set. 
The rule of thumb is to set our test set to be big enough to give high confidence in the overall performance of our system.
There are possibilities where we don't need a test set and we can split only into train/dev set. The purpose of the test set is to help us evaluate our final cost buys of the system.

### Human-Level Performance
Human-Level Performance is a approximation to **Bayes** error. It helps to decide if Bias or Variance has to be optimized.

#### Reducing (Avoidable) Bias and Variance
![human_level_performance.png]({{site.baseurl}}/images/posts/StructuringMLProjects/human_level_performance.png)

### Approach
We should build our system quickly and the iterate over it.

### Training And Testing On Different Distributions
More and more teams are using different data sets for training and testing ML algorithms.
Mix the images from the different sources and shuffle it. Then take as usual a train/dev/test data from this dataset.

## Bias And Variance With Mismatched Data Distributions

### Cat Classifier Example
Assume humans get $$\approx 0%$$ error 

Training error .... *1%*
Dev error      .... *10%*

Training-dev set: Same distribution as training set, but not used for training


Training error     .... *1%*   .... *1%*
Training-dev error .... *9%*   .... *1.5%*
Dev error          .... *10%*  .... *10%*

This tells us that we have a **variance** problem.

The second column is a second example and it shows a **data mismatch** problem.