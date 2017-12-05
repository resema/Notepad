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
where **second order dynamic system** $$ u =\ddot{x}$$

##### Control Of A Linear Second-Order System
###### Problem
Find a control input function $$u(t)$$ so that $$x(t)$$ follows the desired trajectory $$x^{des}(t)$$
###### General Approach
Define error $$e^{(t)} = x^{des}(t) - x(t)$$ <br>
We want $$e(t)$$ to converge exponentially to zero
###### Strategy
Find $$u(t)$$ such that<br>
$$\ddot{e} + K_v \dot{e} + K_pe = 0$$ <br>
where $$K_p, K_v > 0$$<br>
and $$K_v$$ is the **Derivative Gain** <br>
and $$K_p$$ is the **Proportional Gain**

##### Proportional-Derivative Controller (PD)

$$u(t) = \ddot{x}^{des}(t) + K_v \dot{e}(t) + K_p e(t)$$ <br>
- Proportional control acts like a spring (capacitance) response
- Derivative control is a viscous dashpot (resistance) response
- Large derivative gain makes the system overdamped and the system converges slowly

##### Proportional-Integral-Derivative Controller (PID)
In the presence of disturbances (e.g. wind) or modeling errors (e.g. unkown mass), it is often advantageous to use PID control:

$$u(t) = \ddot{x}^{des}(t) + K_v \dot{e}(t) + K_p e(t) + K_i \int_0^t e(\tau)d\tau$$ <br>

**PID** control generates a **third-order** closed-loop system. Integral control makes the steady-state error go to zero.

#### Agility And Maneuverability
Let's look at the situation from **Maximum Velocity to Rest**. Max deceleration is achieved by tilting the robot. But in this case the robot will also lose height.

##### Agility
Two key ideas:
- Accelerate quickly by maximizing $$a_{max}$$ <br>
  $$\text{maximize}\frac{u_{1,max}}{W}$$
- Roll/Pitch quickly by maximizing $$\alpha_{max}$$ <br>
  $$\text{maximize}\frac{u_{2,max}}{I_{xx}}$$

#### Effects Of Size
![effectSize.png]({{site.baseurl}}/images/posts/AerialRobotics/effectSize.png)

- Froude scaling <br>
  $$v \approx \sqrt{l}$$<br>
  $$F \approx l^3$$<br>
  $$ a \approx 1, \alpha \approx \frac{1}{l}$$
- Mach scaling <br>
  $$ v \approx 1$$<br>
  $$ F \approx l^2$$<br>
  $$a \approx \frac{1}{l}, \alpha \approx \frac{l}{l^2}$$