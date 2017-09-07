---
layout: post
published: true
mathjax: true
featured: false
comments: false
title: 'Backpropagation: Derivatives with a Computation Graph'
categories:
  - Mathematics
  - Calculus
  - Neural Network
tags: Calculus Mathematics Coursera
description: Notes to the Coursera courser "DeepLearning.ai"
headline: What to remember from Calculus in Backpropagation
---
>&quot;Do not worry about your difficulties in Mathematics. I can assure you mine are still greater.&quot;
><small><cite title="Einstein">Einstein</cite></small>

What to keep in mind regarding Calculus for Back Propagation.

## Introduction
To compute derivates in Neural Networks a Computation Graph can help. It contains both a forward and a back propagation.

Back propagation contains Calculus, or more specific we have to take different Derivatives. Look at it as a computation from right to left.

## Chain Rule
u = bc --> v = a + u --> J = 3v

>dJ/dv = 3 <br>
>dJ/da = dJ/dv x dv/da = 3 x 1 <br>
>dJ/du = dJ/dv x dv/du = 3 x 1 <br>
>dJ/db = dJ/du x du/db = dJ/dv x dv/du x du/db = 3 x 1 x c <br>

## Wording
$$a_j^{[2](i)} $$ := layer 2, example i, neuron j

## Formulas for Forward and Back Propagation
Estimation function $$Z^{[i]} = W^{[i]}X + b^{[i]}$$ <br>
Sigmoid function $$g^{[i]} = 1/1+e^{-z}$$<br>
Node $$a^{[i]} = g^{[i]}(z^{[i]})$$<br>
Loss (error) function $$ \mathcal{L}(\hat{y}, y) = -(y log \hat{y} + (1-y) log(1-\hat{y}))$$<br>
Cost Function $$J(w,b) = 1/m * \sum_{i=1}^m \mathcal{L}(\hat{y}^{[i]}, y^{[i]}) = - 1/m * \sum_{i=1}^m y^{(i)} log(\hat{y}^{[i]}) + (1-y^{[i]}) log(1-\hat{y}^{[i]})$$

### Summary of gradient descent (Backpropagation)
$$dz^{[2]} = a^{[2]} - y$$ <br>
$$dW^{[2]} = dz^{[2]}a^{[1]^T}$$ <br>
$$db^{[2]} = dz^{[2]}$$ <br>
$$dz^{[1]} = W^{[2]^T}dz^{[2]} * g^{[1]}(z^{[1]})$$ <br>
$$dW^{[1]} = dz^{[1]}x^T$$<br>
$$db^{[1]} = dz^{[1]}$$ <br>

#### Vectorized implementation
$$dZ^{[2]} = A^{[2]} - Y$$ <br>
$$dW^{[2]} = 1/m dZ^{[2]}A^{[1]^T}$$ <br>
$$db^{[2]} = 1/m np.sum(dZ^{[2]}, axis=1, keepdims=True)$$<br>
$$dZ^{[1]} = W^{[2]^T}dZ^{[2]} * g^{[1]}'(Z^{[1]})<br>
$$dW^{[1]} = 1/m dZ^{[1]}X^T$$<br>
$$db^{[1]} = 1/m np.sum(dZ^{[1]}, axis=1, keepdims)True)$$<br>

### Calculation Problem with Zero Matrix
Initialize weights with a 2x2 zero matrix is a problem. The computed a's will be the same. And the dW rows will also be the same. This is independent how many cycles are be computed.

#### Random Initialization
We should initialize the parameters randomly. The parameters are $$n_x := n\, of\, input\, layer$$, $$n_h := n\, of\, hidden\, layer$$ and $$n_h := n\, of\, output\, layer$$<br>
$$W^{[1]} = np.random.randn(n_h,n_x) * 0.01$$<br>
$$b^{[1]} = np.zeros((n_h,1))$$ <br>
$$W^{[2]} = np.random.randn(n_y,n_h) * 0.01$$ <br>
$$b^{[2]} = np.zeros((n_y,1))$$ <br>

Where does the constant 0.01 comes from? We prefer to use very small initialization values. This means we will not start at the flat parts of the curve.
