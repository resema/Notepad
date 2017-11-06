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
modified: ''
tags: ''
imagefeature: ''
---
>&quot;I very rarely think in words at all. A thought comes, and I may try to express in words afterwards.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Anomaly Detection
$$x$$ is distributed Gaussian with mean $$\mu$$ and variance $$\sigma^2$$. Also called the normal distribution.

![gaussian_distribution.png]({{site.baseurl}}/images/posts/Anomaly Detection/gaussian_distribution.png)

$$\sigma$$ is the with of the Gaussian curve and $$\mu$$ is where the Gaussian curve is centered.

### Parameter Estimation
$$\mu = \frac{1}{m}\sum_{i=1}^m x^{(i)}$$<br>
$$\sigma^2 = \frac{1}{m}\sum_{i=1}^m(x^{(i)} - \mu)^2$$<br>

This is called **Maximum Likely-Hood Estimation** in statistics.
