---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Anomaly Detection By Means Of Machine Learning
description: Using Machine Learning for Anomaly Detection
headline: Anomaly Detection
categories:
  - MachineLearning
---
>&quot;I very rarely think in words at all. A thought comes, and I may try to express in words afterwards.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Anomaly Detection
$$x$$ is distributed Gaussian with mean $$\mu$$ and variance $$\sigma^2$$. Also called the normal distribution.

![gaussian_distribution.png]({{site.baseurl}}/images/posts/Anomaly Detection/gaussian_distribution.png)

$$\sigma$$ is the with of the Gaussian curve and $$\mu$$ is where the Gaussian curve is centered.

### Parameter Estimation
$$\mu _j= \frac{1}{m}\sum_{i=1}^m x_j^{(i)}$$<br>
$$\sigma_j^2 = \frac{1}{m}\sum_{i=1}^m(x_j^{(i)} - \mu_j)^2$$<br>

This is called **Maximum Likely-Hood Estimation** in statistics.

### Density Estimation
By using the Gaussian distribution to estimate the density of our samples.

$$p(x) = p(x_1; \mu_1,\sigma_1^2)*p(x_2; \mu_3,\sigma_2^2)*...*p(x_n; \mu_n,\sigma_n^2)$$ <br>
$$p(x) = \prod_{j=1}^n p(x_j; \mu_j, \sigma_j^2)$$ <br>

### Detection Algorithm
![AnomalyDetection.png]({{site.baseurl}}/images/posts/Anomaly Detection/AnomalyDetection.png)

### Developing and Evaluating An Anomaly Detection System
When we develope a learning algorithm (choosing features, etc.), making a decision is much easier if we have a way of **evaluating our learning algorithm**.

Assume we have some labeled data of anomalous (*y = 1*) and non-anomalous (*y = 0* if normal) examples.

We have a larger number of normal examples and some anomalous examples. We divide them as usual into train, cross-validation and test set.

#### Algorithm Evaluation
Possible evaluation metrics:
- True positive, false positive, false negative, true negative
- Precision/Recall
- $$F_1$$ Score

##### Anomaly Detetion
- Fraud detectino
- Manufacturing (e.g. aircraft engines)
- Monitoring machines in a data center

##### Supervised Learing
- Email spam classification
- Weather prediction (sunny, rainy, etc.)
- Cancer classification
