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

Linearized dynamics by replacing $$\sin\phi$$ by $$\phi$$ and $$\cos\phi$$ by 1: <br>
$$\ddot{y} = -g\phi$$<br>
$$\ddot{z} = -g + \frac{u_1}{m}$$ <br>
$$\ddot{\phi} = \frac{u_2}{I_{xx}}$$<br>

### Trajectory Tracking
$$r_T(t) = \left[\begin{matrix}y(t) \\ z(t)\end{matrix}\right]$$<br>

The desired trajectory $$r(t)$$ with the corresponding position, velocity and acceleration can be achieved by the **commanded acceleration**, calculated by the controller using: <br>
$$(\ddot{r}_T(t) - \ddot{r}_c= + \mathbf{K}_de_v + \mathbf{K}_pe_p = 0$$<br>
with $$e_p = \mathbf{r}_T(t) - \mathbf{r}$$<br>
and $$e_v = \mathbf{\ddot{r}}_T(t) - \mathbf{\ddot{r}}<br>

### Nested Control Structure
![nestedCtrlStructure.png]({{site.baseurl}}/images/posts/AerialRobotics_ControlAndPlaning/nestedCtrlStructure.png)

If we are following non-aggressive trajectories where the snap is small, we may approximate this as $$\ddot{\phi}_c = 0$$. Furthermore, we may "absorb" $$\mathbf{I}_{xx}$$ into the proportional and derivate gains. This gives us a new, **simpliefied** equation: <br>
$$u_2 = k_{p,\phi}(\phi_c - \phi) + k_{d,\phi}(\dot{\phi}_c - \dot{\phi})$$<br>

### Control Equations
$$u_1 = m(g + \ddot{z}_{des} + k_{d,z}(\dot{z}_des - \dot{z}) + k_{p,z}(z_{des} - z))$$<br>
$$u_2 = k_{p,\phi}(\phi_c - \phi) + k_{d,\phi}(\dot{\phi}_c - \dot{\phi})$$<br>
$$\phi_c = -\frac{1}{g}(\ddot{y}_{des} + k_{d,y}(\dot{y}_{des} - \dot{y}) + k_{p,y}(y_{des} - y))$$<br>
