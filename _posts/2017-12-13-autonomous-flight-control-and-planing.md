---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: Autonomous Flight - Control And Planing
description: Control and Planning of of Quadrotor
headline: Autonomous Flight - Control And Planing
categories:
  - Physics
  - MatlabOctave
  - Robotics
tags: Cousera Robotics
---
>&quot;It’s not that I’m so smart, it’s just that I stay with problems longer.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## 2D Quadrotor Control

### Equation Of Motion
![planarEquMotion.png]({{site.baseurl}}/images/posts/AerialRobotics_ControlAndPlaning/planarEquMotion.png)

Dynamics are non linear:<br>
$$\ddot{y} = -\frac{u_1}{m}\sin(\phi)$$<br>
$$\ddot{z} = -g + \frac{u_1}{m}\cos(\phi)$$<br>
$$\ddot{\phi} = \frac{u_2}{I_{xx}}$$<br>

Equilibrium hover configuration:<br>
$$y_0, z_0, \phi_0 = 0, u_{1,0} = mg, u_{2,0} = 0$$ <br>

Linearized dynamics by replacing $$\sin\phi$$ by $$\phy$$ and \cos\phi$$ by 1$$: <br>
$$\ddot{y} = -g\phi$$<br>
$$\ddot{z} = -g + \frac{u_1}{m}$$ <br>
$$\ddot{\phi} = \frac{u_2}{I_{xx}}$$<br>

