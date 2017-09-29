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

### How It Works
$$ for \, t = 1, ..., 500 $$<br>            $$ \,\,\,\,$$ Forward-Prop on $$X^{\{t\}}$$ <br>
$$ \,\,\,\,\,\,\,\, Z^{[1]} = W^{(1)}X^{\{t\}} + b^{[1]}$$ <br>
$$\,\,\,\,\,\,\,\, A^{[1]} = g^{[1]}(Z^{[1]})$$<br> $$ \,\,\,\, ... $$ <br> $$\,\,\,\,\,\,\,\, A^{[l]} = g^{[l]}(Z^{[l]}) $$ <br>
$$ \,\,\,\,$$ Compute Cost $$ J = \frac{1}{1000}\sum_{i=0}^l\mathcal{l}(\hat{y}^{(i)}, y^{(i)}) + \frac{\lambda}{2*1000}\sum_l\Vert{W^{[l]}}\Vert_F^2$$ <br>
$$\,\,\,\, $$ Backprop to compute gradients cost $$ J^{\{t\}} $$ (using ($$(X^{\{t\}}, Y^{\{t\}}))$$) <br>
$$\,\,\,\, W^{[l]} = W^{[l]} - \alpha\,dW^{[l]}$$<br>
$$\,\,\,\, b^{[l]} = b^{[l]} - \alpha\,db^{[l]}$$ <br>

### Mini-batch Size
![mini-batch_size.png]({{site.baseurl}}/images/posts/MachineLearning_AnIntroduction/mini-batch_size.png)

Make sure that the mini-batch fits in the CPU/GPU memory (64, 128, 256, 512). 

## Exponentially Weighted Averages
$$ V_t = \beta\, V_{t-1} + (1 - \beta)\theta_t$$ <br>
While $$\beta \to 1$$ we are averaging over larger data. 
$$\beta$$ is a hyperparameter.

### How It Works
$$ V_t = \beta\, V_{t-1} + (1 - \beta)\theta_t$$ <br>
$$ V_100 = 0.1 * \theta_{100} + 0.1 * 0.9 * \theta_{99} + 0.1 * (0.9)^2 * \theta_{98} + 0.1 * (0.9)^3 * \theta_{97} + ...$$ <br>
This is an exponentially decaying function and this becomes to $$V_{100}$$.

### Implementation Notes
$$ Repeat $$ <br>
$$ \,\,\,\, Get\, next\, \theta_t$$ <br>
$$ \,\,\,\, V_{\theta} = \beta V_{\theta} + (1-\beta) \theta_t $$ <br>

### Bias Correction in Exponentially Weighted Average
The curve from the above equation starts very low due to the initialization of $$V_0$$ with 0.

$$\frac{V_t}{1-\beta^t}$$ is used for bias correction. But bias correction is not applied very often.
