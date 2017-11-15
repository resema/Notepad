---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Convolutional Neural Networks - An Introduction
description: 'Convolution neural networks '
headline: Convolutional Neural Networks - An Introduction
categories:
  - NeuralNetworks
  - MachineLearning
  - ComputerVision
tags: >-
  Coursera MachineLearning NeuralNetworks ConvolutionNeuralNetwork
  ComputerVision Edge Detection
---
>&quot;A person who never made a mistake never tried anything new.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Convolutional Neural Network
In real word examples computer vision has to work on images with a size of 1000x1000x3 pixels. This becomes a huge matrix, if e.g. the first layer has 1000 knots. This results in a matrix dimension of (1000, 3M). To solve this kind of problems, we introduce **convolutional neural networks**.

Classical problem fields are **computer vision** or **edge detection**.

### Edge Detection
![vertEdgeDetection.png]({{site.baseurl}}/images/posts/ConvolutionalNN/vertEdgeDetection.png)