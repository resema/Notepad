---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Optimization Algorithms in Neural Networks
description: Quick reference about how to optimize neural networks
headline: Optimization Algorithms in Neural Networks
categories:
  - Calculus
  - NeuralNetworks
  - MachineLearning
tags: coursera neural network machinelearning calculus
---
>&quot;Do not worry about your difficulties in Mathematics. I can assure you mine are still greater.&quot;

## Mini-batch Gradient Descent
Looking back to Batch Gradient Descent, Vectorization allows us to efficiently compute on *m* examples. But if *m* is big it is still very slow because you have to train the complete training set.

Mini-batch Gradient Descent splits up the data samples into baby batches.
Mini-batch t $$= X^{\{t\}}$$ <br>

## How It Works
$$ for \, t = 1, ..., 500 $$<br>            $$ \,\,\,\, Forward\,Prop\, on\, X^{\{t\}}$$ <br>
$$ \,\,\,\,\,\,\,\, Z^{[1]} = W^{(1)}X^{\{t\}} + b^{[1]}$$ <br>
\,\,\,\,\,\,\,\, \,\,\,\,\,\,\,\, A^{[1]} = g^{[1]}(Z^{[1]})$$<br> $$ \,\,\,\,\,\,\,\, \,\,\,\,\,\,\,\, ... $$ <br> $$\,\,\,\,\,\,\,\, \,\,\,\,\,\,\,\, A^{[l]} = g^{[l]}(Z^{[l]}^) $$ <br>
$$ \,\,\,\,\,\,\,\, Compute Cost J = \frac{1}{1000}\sum_{i=0}^l\mathcal{L}(\hat{y}^{(i)}, y^{(i)}) + \frac{\lambda}{2*1000}\sum_l\Vert{W^{[l]}\Vert_F^2$$ <br>
$$\,\,\,\,\,\,\,\, $$ Backprop to compute gradients cost $$ J^{\{t\}} $$ (using ($$(X^{\{t\}}, Y^{\{t\}}))$$) <br>
$$\,\,\,\,\,\,\,\, W^{[l]} = W^{[l]} - \alpha\,dW^{[l]}$$<br>
$$\,\,\,\,\,\,\,\, b^{[l]} = b^{[l]} - \alpha\,db^{[l]}$$ <br>
