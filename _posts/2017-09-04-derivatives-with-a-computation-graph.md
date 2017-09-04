---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: Derivatives with a Computation Graph
categories:
  - Mathematics
tags: 'Calculus, Mathematics, Coursera'
description: Notes to the Coursera courser "DeepLearning.ai"
headline: What to remember from Calculus
modified: ''
imagefeature: ''
---
What to keep in mind regarding Calculus.

## Introduction
To compute derivates in Neural Networks a Computation Graph can help. It contains both a forward and a back propagation.

Back propagation contains Calculus, or more specific we have to take different Derivatives. Look at it as a computation from right to left.

## Chain Rule
u = bc --> v = a + u --> J = 3v

dJ/dv = 3
dJ/da = dJ/dv x dv/da = 3 x 1
dJ/du = dJ/dv x dv/du = 3 x 1
dJ/db = dJ/du x du/db = dJ/dv x dv/du x du/db = 3 x 1 x c

