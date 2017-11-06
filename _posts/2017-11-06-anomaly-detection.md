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

