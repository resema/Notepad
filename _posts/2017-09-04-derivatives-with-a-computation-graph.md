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
>dz<sup>[2]</sup> = a<sup>[2]</sup> - y <br>
>dW<sup>[2]</sup> = dz<sup>[2]</sup>a<sup>[1]<sup>T</sup> </sup> <br>
>db<sup>[2]</sup> = dz<sup>[2]</sup> <br>
dz<sup>[1]</sup> = W<sup>[2]<sup>T</sup></sup>dz<sup>[2]</sup> * g<sup>[1]</sup>'(z<sup>[1]</sup>) <br>
dW<sup>[1]</sup> = dz<sup>[1]</sup>x<sup>T</sup> <br>
db<sup>[1]</sup> = dz<sup>[1]</sup> <br>

#### Vectorized implementation
>dZ<sup>[2]</sup> = A<sup>[2]</sup> - Y <br>
>dW<sup>[2]</sup> = 1/m dZ<sup>[2]</sup>A<sup>[1]<sup>T</sup></sup> <br>
db<sup>[2]</sup> = 1/m np.sum(dZ<sup>[2]</sup>, axis=1, keepdims=True)<br>
dZ<sup>[1]</sup> = W<sup>[2]<sup>T</sup></sup>dZ<sup>[2]</sup> * g<sup>[1]</sup>'(Z<sup>[1]</sup>)<br>
dW<sup>[1]</sup> = 1/m dZ<sup>[1]</sup>X<sup>T</sup><br>
db<sup>[1]</sup> = 1/m np.sum(dZ<sup>[1]</sup>, axis=1, keepdims)True)<br>

### Calculation Problem with Zero Matrix
Initialize weights with a 2x2 zero matrix is a problem. The computed a's will be the same. And the dW rows will also be the same. This is independent how many cycles are be computed.

#### Random Initialization
We should initialize the parameters randomly. The parameters are $$n_x := n\, of\, input\, layer$$, $$n_h := n\, of\, hidden\, layer$$ and $$n_h := n\, of\, output\, layer$$<br>
$$W^{[1]} = np.random.randn(n_h,n_x) * 0.01$$<br>
$$b^{[1]} = np.zeros((n_h,1))$$ <br>
$$W^{[2]} = np.random.randn(n_y,n_h) * 0.01$$ <br>
$$b^{[2]} = np.zeros((n_y,1))$$ <br>

Where does the constant 0.01 comes from? We prefer to use very small initialization values. This means we will not start at the flat parts of the curve.
