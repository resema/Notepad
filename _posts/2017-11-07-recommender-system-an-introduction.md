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
- $$\n_u$$ is no. of users
- $$n_m$$ is no. of movies
- $$r(i,j)$$ is 1 if user *j* has rated movie *i*
- $$y^{(i,j)}$$ is rating given by user *j* to movie *i* (defined only *r(i,j) = 1*)

## Content Based Recommendations

### Problem Formulation
$$r(i,j)$$ is 1 if user *j* has rated movie *i*
$$y^{(i,j)}$$ is rating given by user *j* to movie *i* 

$$\theta^{(i)}$$ = parameter vector for user *j*
$$x^{(i)}$$ = feature vector for movie *i*
For user *j*, movie *i*, predicted rating: $$(\theta^{(j)}^T(x^{(i)})$$ <br>

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

