---
layout: post
published: true
mathjax: true
featured: false
comments: false
title: 'chOpen2017: Machine Learning for Software Developer'
description: Introduction to Machine Learning for SW Developers
headline: 'chOpen2017: Machine Learning for Software Developer'
categories:
  - interesting
  - machinelearning
  - chOpen
tags: chOpen2017 MachineLearning
---
## Different categories for ML

### Supervised Learning
An example with the housing prices and the known prices for a cluster of houses. This can be used to predict the housing price of a new house.
The every data feature has a clear label.

### Unsupervised Learning
Examples are clustering of e.g. flowers, customer segmetation.
The data features have no clear label at the beginning. Cluster can become labels.

### Reinforcement Learning
Characterised with missing classical inputs and outputs.
Examples are Alpha Go, Robotic control, ...
Labels are completely unclear.

### Semi-Supervised Learning
Labeling, which is generally expensive and/or time consuming, is reduced to a small set.

### Recommender Systems
Used when existing data is extrem sparse. Cold-start.
Examples are Amazon as seller.


## Preconditions for Supervised Learning
- Useful topic
  - Automated decision taking in a process
  - Operative decision
  - Repeated, time consuming or difficult decisions
  - **Non-deterministic** probleme
  - Root and cause
- Data
  - Relevant data
  - Correct data
  - Enough data (depending also on algorithm)
  - Unaggregated data (better to have atomic data)
  - Data with labels
- Feedback loop
  - **Prediction** of algorithm has value or not
  - **Controlling** of estimation
  - Adapt the model
 
## Process Steps for Supervised Learning
Check follow-along.ipynb file.

- Domain knowledge and data
- Data preparation, clearing and correction
- Feature engineering
- Validation methodology
- Training and model building
  - Hyperparams optimize
- Ensembling (Combine multiple algorithms)
- Prediction

### Feature Engineering
Needs a lot of domain knowledge to create set of features. Has a big impact on performance. A neural network handles the feature generation by itself. 

Possible steps:
- Extraction
- Construction
- Selection


## SW Developpers
A pyramide shows the needs on the SW devs:
- predict
- report & visualize
- process & query
- measure, structure & store


## Algorithms

### Extreme Gradient Boosting

### Neural Networks
Is a universal function approximator. Used for supervised and unsupervised learning.

#### Deep Learning
Is a deep neural network, meaningly a higher number of hidden layers.

- CNN: Convolutional Neural Network
- RNN: Recurrent Neural Network

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

### Random Forest


## Libraries
- face_recognition 0.1.13, Python, https://face-recognition.readthedocs.io/en/latest/face_recognition.html
- Dlib, C++, www.dlib.net


## Personalities
- Tom Mitchell
- Jason Brownlee
- Brian D. Ripley


## Links
- www.kaggle.com
- www.datarobot.com
