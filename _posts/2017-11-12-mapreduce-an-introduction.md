---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: MapReduce - An Introduction
description: Using MapReduce Pattern in Machine Learning
headline: MapReduce - An Introduction
categories:
  - MachineLearning
  - Mathematics
tags: Coursera MachineLearning MapReduce
---
>&quot;Small is the number of people who see with their eyes and think with their minds.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## MapReduce
Split the data set in multiple pieces of data sets. Then multiple machines will execute such a piece of data.

Batch gradient descent: <br>
$$\theta_j := \theta_j - \alpha \frac{1}{400}\sum_{i=1}^{400}(h_{\theta}(x^{(i)}) - y^{(i)})\,x_j^{(i)}$$ <br>

Machine 1: Use $$(x^{(1)}, y^{(1)}), ... ,(x^{(100)}, y^{(100)})$$ <br>
$$temp_j^{(1)} = \sum_{i=1}^{100}(h_{\theta}(x^{(i)}) - y^{(i)})\,x_j^{(i)}$$ <br>

Machine 2: Use $$(x^{(101)}, y^{(101)}), ... ,(x^{(200)}, y^{(200)})$$ <br>
$$temp_j^{(2)} = \sum_{i=101}^{200}(h_{\theta}(x^{(i)}) - y^{(i)})\,x_j^{(i)}$$ <br>

Machine 3: Use $$(x^{(201)}, y^{(201)}), ... ,(x^{(300)}, y^{(300)})$$ <br>
$$temp_j^{(201)} = \sum_{i=201}^{300}(h_{\theta}(x^{(i)}) - y^{(i)})\,x_j^{(i)}$$ <br>

Machine 4: Use $$(x^{(301)}, y^{(301)}), ... ,(x^{(400)}, y^{(400)})$$ <br>
$$temp_j^{(301)} = \sum_{i=301}^{400}(h_{\theta}(x^{(i)}) - y^{(i)})\,x_j^{(i)}$$ <br>