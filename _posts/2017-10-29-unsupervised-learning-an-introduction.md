---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Unsupervised Learning - An Introduction
description: An Introduction to Unsupervised Learning
headline: Unsupervised Learning
categories:
  - MachineLearning
tags: Coursera MachineLearning UnsupervisedLearning
---
>&quot;Not everything that can be counted counts, and not everything that counts can be counted.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Unsupervised Learning
Data sets which are not labeled or group are classified by means of unsupervised learning, e.g. market segmentation or social network analysis.

One such approach is **Clustering** and the most common used algorithm is k-Means.

### K- Means Algorithm
{% highlight cpp %}
Input:
    *K* number of clusters
    Training set x^1, x^2, ... x^m
    drop x_0 = 1 convention

Randomly initialize N cluster centroids mu_1, mu_2, ..., mu_K
Repeat {
    for i = 1 to m
        c^(i) := index (from 1 to N) of cluster centroid closest to x^(i)
    for k = 1 to K
    	mu_k := average (mean) of points assigned to cluster *k*
}
{% endhighlight %}

### Optimization Objective
$$c^{(i)}$$ = index of cluster (1,2,...,*K*) to which example $$x^{(i)}$$ is currently assigned <br>
$$\mu_k$$ = cluster centroid *k* ($$\mu_k \in \mathbb{R}^n$$) <br>
$$\mu_{c^{(i)}}$$ = cluster centroid of clluster to which example $$x^{(i)}$$ has been assigned

**Optimization objective:** <br>
$$J(c^{(1)},..., c^{(m)}, \mu_1,...,\mu_K) = \frac{1}{m}\sum_{i=1}^m\Vert x^{(i)} - \mu_{c^{(i)}}\Vert^2$$ <br>
$$min J(c^{(1)},..., c^{(m)}, \mu_1,...,\mu_K)$$ regarding $$c^{(i)}$$ and $$\mu_k$$<br>

### Random Initialization of K-Means
There are few different ways, but there is one method which is most often recommended.

- Should have *K* < *m*
- Randomly pick *K* training examples
- Set $$\mu_1, ..., \mu_K$$ equal to these *K* examples.

#### Local Optima
Due to various initializations the algorithm can be stucked in local optimas.

{% highlight cpp %}
for i = 1 to 100 {
    Randomly initialize K-means
    Run K-Means. Get c^(i), ..., c^(m), mu_1, ..., mu_K.
    Compute cost function (distorsion) 
        J(c^(i), ..., c^(m), mu_1, ..., mu_K)
}

Pick clustering that gave lowest cost J(c^(i), ..., c^(m), mu_1, ..., mu_K)
{% endhighlight %}