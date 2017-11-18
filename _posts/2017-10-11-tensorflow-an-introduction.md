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
tags: Coursera NeuralNetworks MachineLearning TensorFlow
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
# cost = tf.add(tf.add(w**2,tf.multiply(-10,w)),25)
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

Now we extend the example a little bit:
{% highlight python linenos %}
coefficient = np.array([1.], [-20], [100.]])
w = tf.Variable(0,dtype=tf.float32)
# Placeholder are variables in TF you provide later
x = tf.placeholder(tf.float32, [3,1])

# replace the coefficient by data
cost = x[0][0]*w*2 + x[1][0]*w + x[2][0]
train = tf.train.GradientDescentOptimizer(0.01).minimize(cost)

init = tf.global_variables_initializer()
# improve the session running
with tf.Session() as session:
	session.run(init)
	print(session.run(w))	% Output: 0.0

session.run(train, feed_dict={x:coefficients})
print(session.run(w))		% Output: 0.2

for i in range(1000):
	session.run(train, feed_dict={x:coefficients})
print(session.run(w))		% Output: 9.99998
{% endhighlight %}

What is this programm really doing?
TensorFlow is in this case calculating the forward calculation of the cost function $$cost$$. And the nice thing is that due to implementing forward propagation, TensorFlow has already build in the backward propagation. So you don't need to implement backprop. This makes the frameworks very powerful and helpful.

## Small API Outtakes
{% highlight python linenos %}
# constants, variable, placeholders
tf.constant(val,shape,name)
tf.Variable(val,shape,name)
tf.placeholder(tf.float32,shape,name)

# get an existing variable with these parameters or create a new one.
tf.get_variable(name, shape, initializer)

# creating and using a session
with tf.Session() as session:
	session.run([optimizer, func], feed_dict={x:data_x, y:data_y})

# create a hard max tensor
tf.one_hot(indices, depth, axis)

# initialize data for ML
tf.zeros_initializer()
tf.contrib.layers.xavier_initializer   # "Xavier" initialization for weights

# ReLU activation
tf.nn.relu(features, name)

# computes the cost using a sigmoid cross entropy
tf.nn.sigmoid_cross_entropy_with_logits(logit, labels)

# computes the cost using a softmax cross entropy
tf.nn.softmax_cross_entropy_with_logits(logit, labes)

# Compute mean of elements across a tensor.
tf.reduce_mean(tensor, axis, name)

# optimizer
tf.train.GradientDesentOptiizer(learning_rate).minimize(func)

# Convolution for NN
tf.nn.conv2d(Xnput, filter, strides, padding)

# Pooling
tf.nn.max_pool(input, window_shape, pooling_type, padding)

# Flattening
tf.contrib.layers.flatten(P)   # Can be used after convolution and before FC

# Fully Connected Layer
tf.contrib.layers.fully_connected(inputs, num_outputs)

{% endhighlight %}
