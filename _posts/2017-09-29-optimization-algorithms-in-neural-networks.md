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
Mini-batch i $$= X^{\{i\}}$$ <br>
