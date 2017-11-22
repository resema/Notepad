---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Object Detection By Means Of Neural Networks
headline: Object Detection By Means Of Neural Networks
description: Localize and detect objects in a picture
categories:
  - NeuralNetworks
  - MachineLearning
  - ComputerVision
tags: Coursera ML NN ComputerVision BoundingBox
---
>&quot;I have no special talent. I am only passionately curious.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Object Localization
A Convolution Network can output a softmax layer to indicate if an object, such as a car, is present in the image. We call this **Class Label**. Furthermore it can also output a **Bounding Box** (defined by $$b_x, b_y, b_h, b_w$$) around the object.

## Landmark Detection
For an example we'd like to find all the corners of the eyes on an image showing a face. The approach is similiar by outputting a vector with the parameter $$p_{face}, l_x, l_y, ...$$ with *l* as landmark parameter.