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

#### YOLO Algorithm (YOLO := You Only Look Once)
Divide the image with a grid and use the above mentioned algorithm in every grid cell.

![yoloEx.png]({{site.baseurl}}/images/posts/ObjectDetection/yoloEx.png)

### Intersection Over Union (IoU)
It computes the intersection over two bounding boxes.
$$ IoU = \frac{size\,of\,intersection}{size\,of\,area_{total}}$$ <br>
"Correct" if $$IoU \ge 0.5$$ <br>

More generally, IoU is a measure of the overlap between two bounding boxes.

### Non-max Suppression
If an object is not easily classified to belong to one single grid cell. Multiple grid cells will claim the center of object to their possession.

Cells with high IoU get darkened and the others highlighted. Then we suppress darkened cells and from the remaining we choose the cell with the highest probability.

- Each output prediction is a vector $$[p_c, b_x, b_y, b_h, b_w]^T
- Discard all boxes with $$p_c \le 0.6$$
  - Pick the box with the largest $$p_c$$ and output that as a prediction
  - Discard any remaining box with $$IoU \ge 0.5$$ with the box ourput in the previous step