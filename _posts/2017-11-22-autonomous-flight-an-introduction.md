---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Autonomous Flight - An Introduction
headline: Autonomous Flight - An Introduction
categories:
  - Engineering
  - Robotics
tags: Coursera Aerial Robotics
description: Introduction to Aerial Robotics
---
>&quot;It’s not that I’m so smart, it’s just that I stay with problems longer.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Key Components Of Autonomous Flight
- State Estimation
- Control
- Mapping
- Planning

### State Estimation
**SLAM** = **S**imultaneous **L**ocalization **A**nd **M**apping

![SLAM.png]({{site.baseurl}}/images/posts/AerialRobotics/SLAM.png)

### Dynamical Systems
Systems where the effects of actions do not occur immediately.
Every dynamical system is defined by its states: a collection of vairables that completely characterizes the motion of a system.
Evoluton of these states over time is often given by a set of governing ordinary differential equations. 
- Example 1: Mass-Spring System
  $$m\ddot{y}(t) + ky(t) = u(t)$$
- Example 2: Quadrotor (facilitate)
  
#### Control Of Height
$$\sum_{i=1}^4 k_F\omega_i^2 + mg = ma$$ <br>
where $$ a = \frac{d^2x}{dt^2} = \ddot{x}$$ <br>
becomes:
$$ u = \frac{1}{m} \left[ \sum_{i=1}^4 k_F\omega_i^2 + mg\right] $$
where $$ u =\ddot{x}$$ a **second order dynamic system**.