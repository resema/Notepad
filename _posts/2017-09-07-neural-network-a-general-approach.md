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
  - neuralnetworks
tags: NeuralNetworks Methodology
---
>&quot;Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Steps
1. Define the neural network structure (\# of input units, \# of hidden units, etc)
2. Initialize the model's parameters
3. Loop:
- Implement forward propagation
- Compute loss
- Implement backward propagation to get the gradients
- Update parameters (gradient descent)
