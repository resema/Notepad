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
>&quot;Do not worry about your difficulties in Mathematics. I can assure you mine are still greater.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Steps
1. Define the neural network structure (\# of input units, \# of hidden units, etc)
2. Initialize the model's parameters
3. Loop:
- Implement forward propagation
- Compute loss
- Implement backward propagation to get the gradients
- Update parameters (gradient descent)
