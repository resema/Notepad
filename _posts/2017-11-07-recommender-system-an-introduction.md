---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Recommender System - An Introduction
description: A short introduction to Recommender Systems
headline: Recommender System - An Introduction
categories:
  - MachineLearning
tags: Coursera MachineLearning
---
>&quot;Try not to become a man of success, but rather try to become a man of value.&quot;
><small><cite title="Einstein">Einstein</cite><small>
  
### Example: Predicting Movie Ratings
- User rates movies using zero to five stars
- 5x movies and 4x persons
- $$n_u$$ is no. of users
- $$n_m$$ is no. of movies
- $$r(i,j)$$ is 1 if user *j* has rated movie *i*
- $$y^{(i,j)}$$ is rating given by user *j* to movie *i* (defined only *r(i,j) = 1*)

## Content Based Recommendations

### Problem Formulation
$$r(i,j)$$ is 1 if user *j* has rated movie *i*
$$y^{(i,j)}$$ is rating given by user *j* to movie *i* 

$$\theta^{(i)}$$ = parameter vector for user *j*
$$x^{(i)}$$ = feature vector for movie *i*
For user *j*, movie *i*, predicted rating: $$(\theta^{(j)})^T \cdot (x^{(i)})$$ <br>

$$m^{(j)}$$ = no. of movies rated by user *j*

To learn $$\theta^{(j)}$$:
Use linear regression with some simplifications

![recommender_system.PNG]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/recommender_system.PNG)

![recommender_update.PNG]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/recommender_update.PNG)

## Collaborative Filtering
We have no information about the classification of our movies. So what do we do? How to we calculate $$\theta^{(j)}$$?

From the data of our user we can get the parameters for the $$\theta$$ vectors.

### Learn The Feature Vector *x*
Given $$\theta^{(1)},...,\theta^{(n_u)}$$ to learn $$x^{(1)},..., x^{(n_m)}$$

![collaborative_filtering.png]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/collaborative_filtering.png)

### How To Solve The Chicken Or Egg Problem
Both $$x^{(i)}$$ and $$\theta^{(i)}$$ can be extracted from the data set.
Guess $$\theta \to x \to \theta \to x \to ...$$ <br>

![collaborative_filtering_optimization1.png]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/collaborative_filtering_optimization1.png)

This going back and forth to estimate the two parameters is not the fastest approach. There are also others as the proposed simultanous approach:

![collaborative_filtering_optimization_simultanously.png]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/collaborative_filtering_optimization_simultanously.png)

### How To Apply The Algorithm
![collaborative_filtering_algorithm.png]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/collaborative_filtering_algorithm.png)

### Low Rank Matrix Factorization
Stacking all movie ratings into matrix *X* with each movie per row (transposed) and all user ratings into matrix $$\theta$$ with each user per row (transposed), the resulting matrix is called a **Low Rank Matrix**.

![low_rank_matrix.png]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/low_rank_matrix.png)

#### Finding a Feature Vector
For each product *i*, we learn a feature vector $$x^{(i)} \in \mathbb{R}^n$$.

How to find movies *j* related to movie *i* ?<br>
5 most similiar movies to movie *i* : <br>
Find the 5 movies *j* with the smallest $$\Vert x^{(i)} - x^{(j)}\Vert$$.

### Mean Normalization
What if a user has not rated any movies? The first term in the minimization algorithm therefore doesn't play any role and the $$\theta^{(5)}$$ is a zero vector for this user.

**BUT** this above described approach doesn't seem to be a good way...

We should apply a **mean normalization** to get the initial ratings for a user without any ratings:

![collaborative_filtering_mean_normalization.png]({{site.baseurl}}/images/posts/RecommenderSystems_AnIntroduction/collaborative_filtering_mean_normalization.png)
