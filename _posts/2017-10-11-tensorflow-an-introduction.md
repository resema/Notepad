---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: TensorFlow - An Introduction
description: An introduction to programming frameworks
headline: TensorFlow - An Introduction
categories:
  - NeuralNetworks
  - MachineLearning
tags: coursera NeuralNetworks MachineLearning TensorFlow
---
>&quot;Optimization limits the evolution.&quot;
><small><cite title="unknown">unkown</cite></small>

## TensorFlow
As an example we start by using the following simple cost function $$J(w) = w^2 - 10w + 25$$.

Let us look at a simple example works in Python:

{% highlight python linenos %}
import numpy as np
import tensorflow as tf

w = tf.Variable(0,dtype=tf.float32)
%cost = tf.add(tf.add(w**2,tf.multiply(-10,w)),25)
cost = w**2 - 10*w + 25 % Possible due to overloading
train = tf.train.GradientDescentOptimizer(0.01).minimize(cost)

init = tf.global_variables_inittializer()
session = tf.Session()
session.run(init)
print(session.run(w))	% Output: 0.0

session.run(train)
print(session.run(w))	% Output: 0.1

for i in range(1000):
	session.run(train)
print(session.run(w))	% Output: 4.99999
{% endhighlight %}

Now we extend the example:
```python
coefficient = np.array([1.], [-20], [100.]])
w = tf.Variable(0,dtype=tf.float32)
% Placeholder are variables in TF you provide later
x = tf.placeholder(tf.float32, [3,1])

% replace the coefficient by data
cost = x[0][0]*w*2 + x[1][0]*w + x[2][0]
train = tf.train.GradientDescentOptimizer(0.01).minimize(cost)

init = tf.global_variables_inittializer()
session = tf.Session()
session.run(init)
print(session.run(w))	% Output: 0.0

session.run(train, feed_dict=(x:coefficients))
print(session.run(w))	% Output: 0.2

for i in range(1000):
	session.run(train, feed_dict=(x:coefficients))
print(session.run(w))	% Output: 9.99998
```