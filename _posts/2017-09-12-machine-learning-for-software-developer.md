---
layout: post
published: true
mathjax: true
featured: false
comments: false
title: Machine Learning for Software Developer
description: Introduction to Machine Learning for SW Developers
headline: Machine Learning for Software Developer
categories:
  - interesting
  - machinelearning
tags: chOpen MachineLearning
---
## Different categories for ML

### Supervised Learning
An example with the housing prices and the known prices for a cluster of houses. This can be used to predict the housing price of a new house.

### Unsupervised Learning
Examples are clustering of e.g. flowers.

### Reinforcement Learning
Characterised with missing classical inputs and outputs.
Examples are Alpha Go, Robotic control, ...

### Semi-Supervised Learning
Labeling, which is generally expensive and/or time consuming, is reduced to a small set.

### Recommender Systems
Used when existing data is extrem sparse. Cold-start.
Examples are Amazon as seller.


## Algorithms

### KMeans
Example in SciPy "iris"

#### Pseudo Code
```
Create k points for starting centroids (often randomly)
While any point has changed cluster assignment
	for every point in our dataset:
		for every centroid
			calculate the distance between the centroid and point
		assign the point to the cluster with the lowest distance
	for every cluster calculate the mean of the points in that cluster
		assign the centroid to the mean
```

## General Approach
Check follow-along.ipynb file.


## Libraries
- face_recognition 0.1.13, Python, https://face-recognition.readthedocs.io/en/latest/face_recognition.html
- Dlib, C++, www.dlib.net


## Personalities
- Tom Mitchell
- Jason Brownlee
- Brian D. Ripley


## Links
- www.kaggle.com