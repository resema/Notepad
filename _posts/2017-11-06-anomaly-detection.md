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
Possible evaluation metrics for a treshold $$\epsilon$$:
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

### Choosing What Features to Use
Arrange the data in a Gaussian bell like curve. Use different transformation to make the data more gaussian, e.g. $$log(x)$$ or $$log(x + c)$$ or $$x^{\frac{1}{3}}$$.

{% highlight matlab %}
% show the data as a histogram
hist(x);
{% endhighlight %}

### Error Analysis
We want *p(x)* to be large for normal examples *x* and *p(x)* small for anomalous examples *x*.

#### Common Problem
The most common problem to that is, that *p(x)* is comparable (say, both large) for nomal and anomalous examples.
A possible solution to this is trying to come up with more features to distinguish between the normal and the anomalous examples.

### Multivariate Gaussian Distribution
$$x \in \mathbb{R}^n$$ <br>
We don't model $$p(x_1), p(x_2), ...$$ separately, instead we model $$p(x)$$ all in one go.
Parameters: $$\mu \in \mathbb{R}^n, \Sigma \in \mathbb{R}^{n\,x\,n}$$ (covariance matrix).

![multivariante_gaussian_distr.png]({{site.baseurl}}/images/posts/Anomaly Detection/multivariante_gaussian_distr.png)

$$\vert\Sigma\vert$$ is the determinate and can be computed in Matlab/Octave by

{% highlight matlab %}
determinate = det(Sigma)
{% endhighlight %}

#### Shifting And Distorsion
![Gaussian_Distribution1.png]({{site.baseurl}}/images/posts/Anomaly Detection/Gaussian_Distribution1.png)

![Gaussian_Distribution2.png]({{site.baseurl}}/images/posts/Anomaly Detection/Gaussian_Distribution2.png)

![Gaussian_Distribution3.png]({{site.baseurl}}/images/posts/Anomaly Detection/Gaussian_Distribution3.png)

### Anomaly Detection With The Multivariate Gaussian
1. Fit model *p(x)* by setting
$$\mu = \frac{1}{m}\sum_{i=1}^m x^{(i)}$$ <br>
$$\Sigma = \frac{1}{m}\sum_{i=1}^m (x^{(i)} - \mu)(x^{(i)} - \mu)^T$$ <br>
2. Given a new example *x*, we compute *p(x)* 

![multivariante_gaussian_distr.png]({{site.baseurl}}/images/posts/Anomaly Detection/multivariante_gaussian_distr.png)

And flag an anomaly if $$p(x) \lt \epsilon$$.

### Original Model

$$p(x) = p(x_1; \mu_1,\sigma_1^2)*p(x_2; \mu_3,\sigma_2^2)*...*p(x_n; \mu_n,\sigma_n^2)$$

- Manually create features to cature anomalies where $$x_1$$, $$x_2$$ take unusual combinations of values.
$$x_3 = \frac{x_1}{x_2} = \frac{CPU\, load}{memory}$$ <br>

- Computationally cheaper ( alternatively, scales better to large *n*).

- OK even if *m* (trainings set size) is small

### Multivariate Gaussian
![multivariante_gaussian_distr.png]({{site.baseurl}}/images/posts/Anomaly Detection/multivariante_gaussian_distr.png)

- Automatically captures correlations between features.

- Computationally more expensive.

- Must have $$m \gt n$$, or else $$\Sigma$$ is non-invertible.
