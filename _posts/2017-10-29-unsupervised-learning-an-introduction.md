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

## K- Means Algorithm,
{% highlight %}
Input:
	*N* number of clusters
    Training set x^1, x^2, ... x^m
	drop x_0 =1 convention

Randomly initialize N cluster centroids mu_1, \mu_2, ..., \mu_N
Repeat {
	for i = 1 to m
    	c^(i) := index (from 1 to N) of cluster centroid closest to x^(i)
    for k = 1 to N
    	mu_k := average (mean) of points assigned to cluster *k*
}
{% endhighlight %}
