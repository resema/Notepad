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

## Object Detection

### Car Detection Example
We train a **ConvNet** with data labeled if there is a car or not. While scanning an image we use a **Sliding Window Detection** by passing just a square part of the image to the **ConvNet** and slide it through every region of the image. Then we repeat this procedure with a different size of the sliding window.

#### Disadvantage Of Sliding Window Detection
Due to the huge number of the regions to check slows down the algorithm massively. Fortunately this problem of computational cost has a pretty good solution.
With the help of a **Convolutional Implementation** we can re-use different layer's output.

### Convolutional Implementation Of Sliding Windows
![convImplEx.png]({{site.baseurl}}/images/posts/ObjectDetection/convImplEx.png)

### Bounding Box Predictions
What if any of the BBox match with the object in the image? Is there a possibility to get the algorithm more accurate?

#### YOLO Algorithm
Divide the image with a grid and use the above mentioned algorithm in every grid cell.

