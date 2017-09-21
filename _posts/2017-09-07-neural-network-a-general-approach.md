---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Neural Network - An Introduction
description: General methodology to build a Neural Network
headline: Introduction
categories:
  - calculus
  - neuralnetworks
tags: NeuralNetworks Introduction Coursera
---
>&quot;Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## General Steps
Applied deep learning is a very empirical process. From an idea, code a solution and test it on an experiment.	

![neural_network_overview.png]({{site.baseurl}}/images/posts/neural_network_overview.png)
The above figure gives an overview of a possible approach. This approach contains the following steps:
1. Define the neural network structure (\# of input units, \# of hidden units, etc)
2. Initialize the model's parameters
3. Loop:
  - Implement forward propagation
  - Compute loss
  - Implement backward propagation to get the gradients
- Update parameters (gradient descent)

### Formulas for Forward and Back Propagation
![forward_backward_propagation.png]({{site.baseurl}}/images/posts/forward_backward_propagation.png)

### Forward Propagation
Calculate the weigths $$Z^{[i]} = W^{[i]}A^{[i]} + b^{[i]}$$ and the activations $$A^{[i]} = g^{[i]}(Z^{[i]})$$. In a neural network with n-layer, there will be a for-loop for calculating this values. 

It's completely okay to use a for-loop at this point.

#### Vectorized Parameters
$$W^{[l]}$$ is a $$(n^{[l]}, n^{[l-1]}$$-matrix.<br>
$$b^{[l]}$$ is a $$(n^{[l]}, 1)$$-matrix. <br>
$$Z^{[l]}$$ is a also a $$(n^{[l]}, m)$$-matrix. $$m$$ is the amount of features. The addition of b is made by means of Python's broadcasting.<br>

### Rectified Linear Unit (ReLU)
In the context of artificial neural networks, the rectifier is an activation function defined as $$f(x) = x^+ = max(0,x)$$.

## Intuition about Deep Representation
Example:
Image input --> Edge detection --> Face subparts --> Faces

### Circuit Theory and Deep Learning
Informally: There are functions you can compute with a "small" L-layer deep neural network that shallower networks require exponentially more hidden units to compute.
![ex_deep-shallow_neural_network.png]({{site.baseurl}}/images/posts/ex_deep-shallow_neural_network.png)

## Gradient Descent in Neural Network
The following image shows a single step in gradient descent. It's important to see that some values are cached.
![one_iteration_of_gradient_descent.png]({{site.baseurl}}/images/posts/one_iteration_of_gradient_descent.png)

## Parameters and Hyperparameters
### Parameters
$$W^{[1]}$$, $$b^{[1]}$$, $$W^{[2]}$$, $$b^{[2]}$$, $$W^{[3]}$$, $$b^{[3]}$$

### Hyperparameters
- Learning rate $$\alpha$$
- Numbers of iterations
- Number of hidden layers
- Number of hidden units $$n^{[1]}$$, $$n^{[2]}$$, ...
- Choice of activation function
- Momentum
- Minibatch size
- Regularization

## Train, Dev and Test Sets
In the modern big data area the commonly used splitting of the data into 70/30 or 60/20/20 is not mostly used anymore. Instead the dev and test sets just have to be big enough, e.g. in case of 1'000'000 data samples, 10'000 examples for the dev set and 10'000 for the test set can be enough. This results into 98/1/1 or 99.5/0.4/0.1 division.

### Mismatched Train/Test Distribution
Different image resolution between train and test set can lead to a mismatch.
As a rule of thumb: "Make sure that dev and test sets come from the same distribution".

## Bias and Variance

### Bias
Bias refers to the tendency of a measurement process to over- or under-estimate the value of a population parameter.

### Variance
Variance is the expectation of the squared deviation of a random variable from its mean. Informally, it measures how far a set of (random) numbers are spread out from their average value.

### Examples
From an example "Cat Classification" you have an Train Set Error of 1% and a Dev Set Error of 11%. This would mean you are performing will in train set but poorly under dev set. This looks like you have overfit the train set.
So for the dev set it must be said that it has a high variance.

In a second example, we have a train set error of 15% and 16% under dev set. This means is has a high bias. It's not even fitting the train set.

In a third example, we have a train set error of 15% and 30% under the dev set. Here you have high bias as well as high variance.

In a last example, we have a train set error of 0.5% and 1% dev set error. Here we have low bias and low variance.

## Basic Recipe for Machine Learning
- High bias $$\Rightarrow$$ Bigger network, train longer, NN architecture
- High variance $$\Rightarrow$$ More data, regularization, NN architecture

## Regularizing Your Neural Network
Regularize the logistic regression cost function $$J(w,b)$$.
![L2_regularization.png]({{site.baseurl}}/images/posts/L2_regularization.png)

Frobenius norm used to regularize neural networks. Weight decay is also a key word in this field.
![NN_regularization.png]({{site.baseurl}}/images/posts/NN_regularization.png)

#### Implementation
$$J(w,b) = \frac{1}{2m}\sum_{i=1}^{n_x}\mathcal{L}(\hat{y}^{[i]}, y^{[i]}) + \frac{\lambda}{2m}\sum_l^L\Vert w^{[l]}\Vert_F^2$$

### Dropout
Go through all layers of the network, and flipping a coin if the node is going to be eliminated or not.
![dropout_regularization.png]({{site.baseurl}}/images/posts/dropout_regularization.png)

#### Basic Principles Why Dropout Works
Intuition: Can't rely on any one feature, so have to spread out weights. This shrinks the importance of single weights.
Keep-Probabilities "keep_probs" can vary for different layer. Usually larger layers have a smaller probability than smaller layers. The downside is that this increases the hyper-parameters of the network.
Dropout is mostly used in image recognition areas, where we always have to few data.
Downside: Cost function $$J$$ is less defined. 

#### Implementing Dropout
Illustrate with the layer l= 3. The keep_prob is 0.8 and d3 is the dropout matrix, with a 80% chance to be 1 and 20% to be 0 and therefore be eliminated.

Step 1: Create a random matrix if nodes be eliminated or not.
$$d3 = np.random.rand(a3.shape[0], a3.shape[1]) < keep\_prob$$ <br>
Step 2: Eliminated the nodes in the activation layer a3.
$$a3 = np.multiply(a3, d3)$$ <br>
Step 3: Scaling up the remaining values due to the loss by eliminating nodes.
$$ a3 /= keep\_prob$$ <br>

### Early Stopping
Stopping learning at the best point.
Downside is that it couples the optimizing and the not-overfitting tools. Relates to Orthogonalization.
![early_stopping.png]({{site.baseurl}}/images/posts/NeuralNetwork_AnIntroduction/early_stopping.png)

## Normalizing Input Data
