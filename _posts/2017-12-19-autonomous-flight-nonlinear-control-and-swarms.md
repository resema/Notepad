---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Autonomous Flight - Nonlinear Control And Swarms
headline: Autonomous Flight - Nonlinear Control And Swarms
description: Aerial Robotics - Advanced Topics
categories:
  - MatlabOctave
  - Robotics
tags: Coursera EulerEquation Robotics
---
>&quot;It’s not that I’m so smart, it’s just that I stay with problems longer.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## On-Board Estimation, Nonlinear Control And Swarms

### Sensing And Estimation
#### SLAM - Simultaneous Localization And Mapping Problem

### Nonlinear Control
From the earlier posts we saw that we always granted that the movement of the robot is in linear boundaries. But now, we want to extend this assumption and take also high positions and attitude changes into our calculation.

#### Trajectory Planning
Trajectory planning helps us to plan complex paths in the planar space (projected into it) and then project it back to the 3-D space.

#### Differential Flatness
All state variables and the inputs can be written as smooth functions of **flat outputs** and their derivatives.

![differentialFlatness.png]({{site.baseurl}}/images/posts/AerialRobotics_NonlinearControl/differentialFlatness.png)

Or the other way around:
The flat outputs and their derivatives can be written as a function of the state, the inputs, and their derivatives.

![differentialFlatness2.png]({{site.baseurl}}/images/posts/AerialRobotics_NonlinearControl/differentialFlatness2.png)

