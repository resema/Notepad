---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: The Basic Formulas in Neural Networks
tags: calculus mathematics coursera
description: Notes to the Coursera courser "DeepLearning.ai"
headline: What to remember from Mathematics in Forward and Backpropagation
categories:
  - Calculus
  - NeuralNetworks
---
>&quot;Do not worry about your difficulties in Mathematics. I can assure you mine are still greater.&quot;
><small><cite title="Einstein">Einstein</cite></small>

What to keep in mind regarding Calculus for Back Propagation.

## Introduction
To compute derivates in Neural Networks a Computation Graph can help. It contains both a forward and a back propagation.

Back propagation contains Calculus, or more specific we have to take different Derivatives. Look at it as a computation from right to left.

## Chain Rule
$$u = bc \Rightarrow v = a + u \Rightarrow J = 3v$$

$$\frac{dJ}{dv} = 3$$ <br>
$$\frac{dJ}{da} = \frac{dJ}{dv} * \frac{dv}{da} = 3 * 1$$ <br>
$$\frac{dJ}{du} = \frac{dJ}{dv} * \frac{dv}{du} = 3 * 1$$ <br>
$$\frac{dJ}{db} = \frac{dJ}{du} * \frac{du}{db} = \frac{dJ}{dv} * \frac{dv}{du} * \frac{du}{db} = 3 * 1 * c$$ <br>

## Wording
$$a_j^{[2](i)} $$ := layer 2, example i, neuron j

## Formulas for Forward and Back Propagation
![forward_backward_propagation_formulas.png]({{site.baseurl}}/images/posts/forward_backward_propagation_formulas.png)

### Forward Propagation
Estimation function $$Z^{[i]} = W^{[i]}X + b^{[i]}$$ <br>
Sigmoid function $$g^{[i]} = 1/1+e^{-z}$$<br>
Node $$a^{[i]} = g^{[i]}(z^{[i]})$$<br>
Loss (error) function $$ \mathcal{L}(\hat{y}, y) = -(y\, log(\hat{y}) + (1-y) log(1-\hat{y}))$$<br>
Logistic Regression Cost Function $$J(w,b) = 1/m * \sum_{i=1}^m \mathcal{L}(\hat{y}^{[i]}, y^{[i]}) = - 1/m * \sum_{i=1}^m y^{(i)} log(\hat{y}^{[i]}) + (1-y^{[i]}) log(1-\hat{y}^{[i]})$$

#### Vectorized implementation
$$J(w,b) = -1/m * np.sum(np.multiply(Y, np.log(A^{[L]})) + np.multiply((1 - Y),np.log(1-A^{[L]})))$$

#### Forward Propagation with Dropout
Create matrix $$D^{[i]}$$ with the same dimension as the corresponding activation matrix $$A^{[i]}$$ and initialize it randomly. Then set all values to 0 or 1 regarding the *keep probability*. Then multiply the activation matrix with the dropout matrix and divide the remaining values by the *keep probability*.

### Backward Propagation
Suppose you have already calculated the derivative $$dZ{[l]} = \frac{\partial{\mathcal{L}}}{\partial{Z^{[l]}}} $$, then you want to get $$dW^{[l]}$$, $$db^{[l]}$$ and $$dA^{[l-1]}$$. <br>

$$dW^{[l]} = \frac{\partial{\mathcal{L}}}{\partial{W^{[l]}}} = \frac{1}{m} dZ^{[l]}A^{[l-1]T}$$ <br>
$$db^{[l]} = \frac{\partial{\mathcal{L}}}{\partial{W^{[l]}}} = \frac{1}{m} \sum_{i=1}^{m}dZ^{[l](i)}$$ <br>
$$dA^{[l-1]} = \frac{\partial{\mathcal{L}}}{\partial{A^{[l-1]}}} = W^{[l]T}dZ^{[l]}$$ <br>
where <br>
$$dZ^{[l-1]} = W^{[l]^T}dZ^{[l]} * g'^{[l-1]}(Z^{[l]})$$<br>
$$dZ^{[L]} = A^{[L]} - Y$$<br>


#### Summary of gradient descent
$$dz^{[2]} = a^{[2]} - y$$ <br>
$$dW^{[2]} = dz^{[2]}a^{[1]^T}$$ <br>
$$db^{[2]} = dz^{[2]}$$ <br>
$$dz^{[1]} = W^{[2]^T}dz^{[2]} * g'^{[1]}(z^{[1]})$$ <br>
$$dW^{[1]} = dz^{[1]}x^T$$<br>
$$db^{[1]} = dz^{[1]}$$ <br>
$$dA^{[l-1]} = \frac{\partial{\mathcal{L}}}{\partial{A^{[l-1]}}} = W^{[l]^T}dZ^{[l]}$$<br>

#### Vectorized implementation example
$$dZ^{[2]} = A^{[2]} - Y$$ <br>
$$dW^{[2]} = \frac{1}{m} dZ^{[2]}A^{[1]^T}$$ <br>
$$db^{[2]} = \frac{1}{m} np.sum(dZ^{[2]}, axis=1, keepdims=True)$$<br>
$$dZ^{[1]} = W^{[2]^T}dZ^{[2]} * g'^{[1]}(Z^{[1]})$$<br>
$$dW^{[1]} = \frac{1}{m} dZ^{[1]}X^T$$<br>
$$db^{[1]} = \frac{1}{m} np.sum(dZ^{[1]}, axis=1, keepdims=True)$$<br>
$$dA^{[l-1]} = W^{[l]^T}dZ^{[l]}$$<br>
$$dA^{[l]} = -(np.divide(Y, A^{[L]}) - np.divide(1-Y, 1-A^{[L]}))$$ <br>
The derivative of cost with respect to $$A^{[L]}$$<br>

### Calculation Problem with Zero Matrix
Initialize weights with a 2x2 zero matrix is a problem. The computed a's will be the same. And the dW rows will also be the same. This is independent how many cycles are be computed.

#### Random Initialization
We should initialize the parameters randomly. The parameters are $$n_x$$ := n of input layer, $$n_h$$ := n of hidden layer and $$n_y$$ := n of output layer<br>
$$W^{[1]} = np.random.randn(n_h,n_x) * 0.01$$<br>
$$b^{[1]} = np.zeros((n_h,1))$$ <br>
$$W^{[2]} = np.random.randn(n_y,n_h) * 0.01$$ <br>
$$b^{[2]} = np.zeros((n_y,1))$$ <br>

Where does the constant 0.01 comes from? We prefer to use very small initialization values. This means we will not start at the flat parts of the curve.

##### Xavier or He Initialization
Xavier initialization uses the factor $$\sqrt{\frac{1}{n_x}}$$ instead of 0.01. And He et al. proposed the slightly adapted factor $$\sqrt{\frac{2}{n_x}}$$.

### General Gradient Descent Rule
$$\theta = \theta - \alpha\frac{\partial{J}}{\partial{\theta}}$$ <br>

#### Update Rule For Each Parameter
$$W^{[i]} = W^{[i]} - \alpha * dW^{[i]}$$ <br>
$$b^{[i]} = b^{[i]} - \alpha * db^{[i]}$$ <br>

### L2 Regularization
The standard way to avoid overfitting is called **L2 regularization**. It consits of appropriately modifying your cost function. <br>
$$J=-\frac{1}{m}\sum_{i=1}^m[y^{(i)}log(a^{[L](i)}) +(1-y^{(i)})log(1-a^{[L](i)})]$$ <br>
to: <br>
$$J_{regularized}=-\frac{1}{m}\sum_{i=1}^m[y^{(i)}log(a^{[L](i)}) +(1-y^{(i)})log(1-a^{[L](i)})] + \frac{1}{m}\frac{\lambda}{2}\sum_l\sum_k\sum_jW_{j,k}^{[l]2}$$ <br>
The first term is named **cross-entropy cost** and the second term **L2 regularization cost**.

#### Observations
- The value of $$\lambda$$ is a hyperparameter that you can tune using a dev set.
- L2 regularization makes your decision boundary smoother. If $$\lambda$$ is too large, it is also possible to *oversmooth*, resulting in a model with high bias.

#### Implementation Details
To calculate $$\sum_k\sum_j W_{k,j}^{[l]2}$$ use
```
np.sum(np.square(W1))
```
#### Backpropagation With Regularization
For each node we have to add teh regularization term's gradient $$(\frac{d}{dW}(\frac{1}{2}\frac{\lambda}{m}W^2) = \frac{\lambda}{m}W$$.

#### Backpropagation with Dropout
Multiply the derivative $$dA^{[i]}$$ with the corresponding droupout matrix cached in the forward propagation. Finally divide the remaining values in the activation matrix by the *keep probablity*.
