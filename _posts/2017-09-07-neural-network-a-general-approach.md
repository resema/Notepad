---
layout: post
published: true
mathjax: true
featured: false
comments: false
title: Neural Network - A General Approach
description: General methodology to build a Neural Network
headline: Basic Approach
categories:
  - personal
  - neuralnetworks
tags: NeuralNetworks Methodology
---
>&quot;Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## General Steps
Applied deep learning is a very empirical process. From an idea, code a solution and test it on an experiment.
1. Define the neural network structure (\# of input units, \# of hidden units, etc)
2. Initialize the model's parameters
3. Loop:
  - Implement forward propagation
  - Compute loss
  - Implement backward propagation to get the gradients
- Update parameters (gradient descent)

### Forward Propagation
Calculate the weigths $$Z^{[i]} = W^{[i]}A^{[i]} + b^{[i]}$$ and the activations $$A^{[i]} = g^{[i]}(Z^{[i]})$$. In a neural network with n-layer, there will be a for-loop for calculating this values. 

It's completely okay to use a for-loop at this point.

#### Vectorized Parameters
$$W^{[l]}$$ is a $$(n^{[l]}, n^{[l-1]}$$-matrix.<br>
$$b^{[l]}$$ is a $$(n^{[l]}, 1)$$-matrix. <br>
$$Z^{[l]}$$ is a also a $$(n^{[l]}, m)$$-matrix. $$m$$ is the amount of features. The addition of b is made by means of Python's broadcasting.<br>

## Intuition about Deep Representation
Example:
Image input --> Edge detection --> Face subparts --> Faces

### Circuit Theory and Deep Learning
Informally: There are functions you can compute with a "small" L-layer deep neural network that shallower networks require exponentially more hidden units to compute.
![ex_deep-shallow_neural_network.png]({{site.baseurl}}/images/posts/ex_deep-shallow_neural_network.png)

## Gradient Descent in Neural Network
The following image shows a single step in gradient descent. It's important to see that some values are cached.
![one_iteration_of_gradient_descent.png]({{site.baseurl}}/images/posts/one_iteration_of_gradient_descent.png)

### Forward Propagation

### Backward Propagation

### Parameters and Hyperparameters
#### Parameters
$$W^{[1]}$$, $$b^{[1]}$$, $$W^{[2]}$$, $$b^{[2]}$$, $$W^{[3]}$$, $$b^{[3]}$$

#### Hyperparameters
- Learning rate $$\alpha$$
- Numbers of iterations
- Number of hidden layers
- Number of hidden units $$n^{[1]}$$, $$n^{[2]}$$, ...
- Choice of activation function
- Momentum
- Minibatch size
- Regularization