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

#### Choosing The Number Of Clusters
There is not a perfect approach to choose the correct number of clusters. But there is the **Elbow Method** which can help. 

To use the **Elbow** method, we have to iterate over the number of clusters and calculate the cost function for each of them. We then choose the elbow of this curve as our number of clusters.

Sometimes, we are running k-Means to get clusters to use for some later or downstream purpose. In those cases we evaluate K-Means based on a metric for how well it performs for later purpose.

#### Local Optima
![k-means_localoptima.png]({{site.baseurl}}/images/posts/UnsupervisedLearning_AnIntroduction/k-means_localoptima.png)

Due to various initializations the algorithm can be stucked in local optimas. To not get stuck in such a local optima, run the algorithm between 50 to 1000 times and take the parameter which create the lowest cost.

{% highlight cpp %}
for i = 1 to 100 {
    Randomly initialize K-means
    Run K-Means. Get c^(i), ..., c^(m), mu_1, ..., mu_K.
    Compute cost function (distorsion) 
        J(c^(i), ..., c^(m), mu_1, ..., mu_K)
}

Pick clustering that gave lowest cost 
    J(c^(i), ..., c^(m), mu_1, ..., mu_K)
{% endhighlight %}

### Principal Component Analysis
PCA helps us to reduce multi-dimensional data to 2 or 3d data. It searches for a sub-structure in our data set and our data is projected onto this structure.

#### PCA Problem Formulation
![PCA_problemformulation.png]({{site.baseurl}}/images/posts/UnsupervisedLearning_AnIntroduction/PCA_problemformulation.png)

Reduce from n-dimenisional to k-dimenstional: Find *k* vectors $$u^{(1)}, u^{(2)}, ..., u^{(k)}$$ onto which to project the data, so as to minimize the projection error.

*Remember:* PCA is not linear regression! It projects **orthogonal** onto the sub-strucure!

#### Data Pre-Processing
We pre-process the training set by feature scaling and mean normalization: $$\mu_j = \frac{1}{m}\sum_{i=1}^m x_j^{(i)}$$. Then we replace each $$x_j^{(i)}$$ with $$x_j - \mu_j$$. If different features on different scales (eg. $$x_1$$ = size of house, $$x_2$$ = number of bedrooms), we should scale features to have **comparable** range of values.

### PCA Algorithm
Our goal is to reduce from *n*-dimensions to *k*-dimensions.

For that we have to compute the **covariance matrix**: <br>
$$\Sigma = \frac{1}{m}\sum_{i=1}^n(x^{(i)})(x^{(i)})^T$$ <br>
Then we have to compute the **eigenvectors** of the matrix $$\Sigma$$ (Sigma): <br>

{% highlight python %}
[U,S,V] = svd(Sigma); 
    #svd := single value decomposition
{% endhighlight %}

#### Matrices Dimensions
![singlevaluedecomposition.png]({{site.baseurl}}/images/posts/UnsupervisedLearning_AnIntroduction/singlevaluedecomposition.png)

{% highlight matlab %}
[U,S,V] = svd(Sigma); 
U_reduce  =U(:,1:k);
z = U_reduce' * x;
{% endhighlight %}
