---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Optimization in Neural Networks
description: Quick reference about how to optimize neural networks
headline: Optimization Algorithms in Neural Networks
categories:
  - Calculus
  - NeuralNetworks
  - MachineLearning
tags: coursera neuralnetwork machinelearning calculus
---
>&quot;Do not worry about your difficulties in Mathematics. I can assure you mine are still greater.&quot;
><small><cite title="Einstein">Einstein</cite></small>

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

### Shuffling
![mb_shuffling.png]({{site.baseurl}}/images/posts/NeuralNetwork_OptimizationAlgorithms/mb_shuffling.png)

### Partition
![mb_partition.png]({{site.baseurl}}/images/posts/NeuralNetwork_OptimizationAlgorithms/mb_partition.png)

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

## Gradient Descent With Momentum
Used to prevent diverting and/or overshooting gradient descent. The goal is to achieve a specific gradient descent faster in broader elipses and slower in narrower elipses

### Average Steps
$$On\, iteration\, t:$$ <br>
$$\,\,\,\, Compute\, dW,\, db\ on\, current\, mini batch$$ <br>
$$\,\,\,\, V_{dW} = \beta V_{dW} + (1-\beta)dW$$ <br>
$$\,\,\,\, V_{db} = \beta V_{db} + (1-\beta)db$$ <br>
$$\,\,\,\, W = W - \alpha V_{dW}; b = b - \alpha V_{db}$$<br>

### Physical Description
Look at it as a ball is rolling down a bowl, where $$V_{dW}$$ and $$V_{db}$$ are the velocities, the derivatives the gaining acceleration and $$\beta$$ the friction. It is easy to imagine how the ball is rolling down.

### Hyperparameters
This introduces a new hyperparameter $$\beta$$ to the existing $$\alpha$$. Normally start with $$\beta = 0.9$$.

## RMSprop
![RMSprop.png]({{site.baseurl}}/images/posts/NeuralNetwork_OptimizationAlgorithms/RMSprop.png)

$$On\, iteration\, t:$$ <br>
$$\,\,\,\, Compute\, dW,\, db\ on\, current\, mini batch$$ <br>
$$\,\,\,\, S_{dW} = \beta S_{dW} + (1-\beta)dW^2$$ <br>
$$\,\,\,\, S_{db} = \beta S_{db} + (1-\beta)db^2$$ <br>
$$\,\,\,\, W = W - \alpha \frac{dW}{\sqrt{S_{dW}}}; b = b - \alpha \frac{db}{\sqrt{S_{db}}}$$<br>

Element-wise squaring of the acceleration.

## Adam Optimization Algorithm
Adam := Adaptive Moment Estimation

This is a combination of gradient descent with momentum and RMSprop. 

### Implementation
1. It calculates an exponentially weighted average of past gradients, and stores it in variables $$v$$ (before bias correction) and $$v^{corrected}$$ (with bias correction).
2. It calculates an exponentially weighted average of the squares of the past gradients, and stores it in variables $$s$$ and $$s^{corrected}$$.
3. It updates parameters in a direction based on combining information from "1" and "2".

The update rule is: <br>

$$V_{dW} = 0, S_{dW} = 0, V_{db} =, S_{db} = 0$$ <br>
$$On\, iteration\, t:$$ <br>
$$\,\,\,\, Compute\, dW,\, db\ using\, current\, mini batch$$ <br>
$$\,\,\,\, V_{dW} = \beta_1 V_{dW} + (1-\beta_1)dW$$ <br>
$$\,\,\,\, V_{db} = \beta_1 V_{db} + (1-\beta_1)db$$ <br>
$$\,\,\,\, S_{dW} = \beta_2 S_{dW} + (1-\beta_2)dW^2$$ <br>
$$\,\,\,\, S_{db} = \beta_2 S_{db} + (1-\beta_2)db^2$$ <br>
$$\,\,\,\, V_{dW}^{corrected} = \frac{V_{dW}}{(1 - \beta_1^t)}, V_{db}^{corrected} = \frac{V_{db}}{(1 - \beta_1^t)}$$ <br>
$$\,\,\,\, S_{dW}^{corrected} = \frac{S_{dW}}{(1 - \beta_2^t)}, \,\,\,\, S_{db}^{corrected} = \frac{S_{db}}{(1 - \beta_2^t)}$$ <br>
$$\,\,\,\, W = W - \alpha \frac{V_{dW}^{corrected}}{\sqrt{S_{dW}^{corrected}} + \epsilon}, b = b - \alpha \frac{V_{db}^{corrected}}{\sqrt{S_{db}^{corrected}} + \epsilon}$$ <br>

where: <br>
- $$t$$ counts the number of steps taken of Adam
- $$\beta_1$$ and $$\beta_2$$ are hyperparameters that control the two exponentially weighted averages
- $$\alpha$$ is the learning rate
- $$\epsilon$$ is a very small number to avoid diving by zero

### Hyperparameters Choice
$$\alpha$$ := needs to be tuned <br>
$$\beta_1 := 0.9$$ <br>
$$\beta_2 := 0.999$$ <br>
$$\epsilon := 10^{-8}$$ <br>

## Learning Rate Decay
One epoch is 1 pass through the data.

$$ \alpha = \frac{1}{1 + decayRate * epochNum} * \alpha_0$$ <br>

$$Epoch \to \alpha$$ <br>
$$ 1 \to 0.1$$ <br>
$$ 2 \to 0.067$$ <br>
$$ 3 \to 0.05$$ <br>
$$ 4 \to 0.04$$ <br>

### Other Methods
$$\alpha = 0.95^{epochNum} * \alpha_0$$ <br>
$$\alpha = \frac{k}{\sqrt{epochNum}} * \alpha_0$$ <br>

## Problem of Local Optima
![local_optima.png]({{site.baseurl}}/images/posts/NeuralNetwork_OptimizationAlgorithms/local_optima.png)

Other possiblities are sattel point, meaning it is shaped as a horse sattel and therefore zero points are no always local or global minimas.
![sattle.png]({{site.baseurl}}/images/posts/NeuralNetwork_OptimizationAlgorithms/sattle.png)

Platforms can make learning very slow and then ADAM and likewise can really help to speed up the training.

## Tuning Process
- The following hyperparameters can be tuned: $$\alpha$$, $$\beta$$, #layers, #hidden units, learning rate decay, mini-batch size.
- It is better to try random values instead of using a parameter grid.
- We should use a coarse to fine sampling scheme

### Appropriate Scale To Pick Hyperparameters
- Use a logarthmic scale to chose from for the learning rate $$\alpha$$.

Possible implementation in Python:
{% highlight python linenos %}
# Values between 0.0001 and 1
def scaleLearningRate:
   r = -4 * np.random.rand()	
   learning_rate = np.power(10, r)
{% endhighlight %}

In pratice, hyperparameters can be tuned by means of Pandas or Caviar. It's good pratice to re-evaluate the parameters every month or so. 

During development a model can be *babysit one model*. Another approach would be to train many models in parallel. The first *babysitting* approach is callend Panda and the second is the Caviar approach.

This mainly depends on the resources we have at hand and the size of data to be processed.

There is a another approach which not always fits the problem we are facing. It is possible to normalize the activations in a network.

#### Batch Normalization
Batch normalization allows to train deeper neural networks, makes the hyperparameter search more easier
and the network much more robust.
Usually it is used with mini-batches. Batch norm are used per first mini-batch, then second and so on.

##### Idea
Normalized inputs speed up learning. The question is *can we normalize* $$a^{[2]}$$ *so as to train *$$W^{[3]}$$, $$b^{[3]}$$ *faster*? This is what Batch Normalization is doing.

##### Implementation
Given some intermediate values in my NN $$z^{(i)}, ..., z^{(m)}$$ <br>
$$\mu = \frac{1}{m}\sum_i z^{(i)}$$ <br>
$$\sigma^2 = \frac{1}{m}\sum_i(z_i - \mu)^2$$ <br>
$$Z_{norm}^{(i)} = \frac{z^{(i)} - \mu}{\sqrt{\sigma^2 + \epsilon}}$$ <br>
$$\tilde{z}^{(i)} = \gamma z_{norm}^{(i)} + \beta$$<br>

where
- $$\gamma$$ and $$\beta$$ are learnable hyperparameters of the model
- $$ \gamma = \sqrt{\sigma^2 + \epsilon}$$
- $$\beta = \mu$$
- Use $$\tilde{Z}^{[l](i)}$$ instead of $$Z^{[l](i)}$$

{% highlight python linenos %}
for t = 1 ... numMiniBatches
	Compute forward prop on X_T
    	In each hidden layer, use N to replace z_l with zTilde_l
    Use back prop to compute dW_l, db_l, dBeta_l, dGamma_l
    Update the parameters 
    	W_l = W - alpha * dW_l
        beta_l = beta_l - alpha * dBeta_l
        gamma_l = gamma_l - alpha * dGamma_l    
{% endhighlight %}


