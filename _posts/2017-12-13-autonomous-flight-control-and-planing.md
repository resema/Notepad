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

## 2-D Quadrotor Control

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
and $$e_v = \ddot{\mathbf{r}}_T(t) - \ddot{\mathbf{r}}$$<br>

### Nested Control Structure
![nestedCtrlStructure.png]({{site.baseurl}}/images/posts/AerialRobotics_ControlAndPlaning/nestedCtrlStructure.png)

If we are following non-aggressive trajectories where the snap is small, we may approximate this as $$\ddot{\phi}_c = 0$$. Furthermore, we may "absorb" $$\mathbf{I}_{xx}$$ into the proportional and derivate gains. This gives us a new, **simplified** equation: <br>
$$u_2 = k_{p,\phi}(\phi_c - \phi) + k_{d,\phi}(\dot{\phi}_c - \dot{\phi})$$<br>

### Control Equations
So these are the three equations we can use to drive a quadrotor that is close to the operating point and stays on the y-z-plane.

$$u_1 = m(g + \ddot{z}_{des} + k_{d,z}(\dot{z}_des - \dot{z}) + k_{p,z}(z_{des} - z))$$<br>
$$u_2 = k_{p,\phi}(\phi_c - \phi) + k_{d,\phi}(\dot{\phi}_c - \dot{\phi})$$<br>
$$\phi_c = -\frac{1}{g}(\ddot{y}_{des} + k_{d,y}(\dot{y}_{des} - \dot{y}) + k_{p,y}(y_{des} - y))$$<br>

## 3-D Quadrotor Control

### Trajectory Tracking
For the 2D quadrotor our trajectories were specified as a 2D vector $$[y(t), z(t)]^T$$. In the case of 3D the trajectories are specified as a **4D vector** consisting of **desired trajectory (position, yaw angle)**:

$$\mathbf{r}_T(t) = \left[\begin{matrix}x(t)\\y(t)\\z(t)\\\psi(t)\end{matrix}\right]$$ <br>

The desired trajectory $$r(t)$$ with the corresponding position, velocity and acceleration can be achieved by the **commanded acceleration**, calculated by the controller using: <br>
$$(\ddot{r}_T(t) - \ddot{r}_c= + \mathbf{K}_de_v + \mathbf{K}_pe_p = 0$$<br>
with $$e_p = \mathbf{r}_T(t) - \mathbf{r}$$<br>
and $$e_v = \ddot{\mathbf{r}}_T(t) - \ddot{\mathbf{r}}$$<br>

### Nested Control Structure
![nestedCtrlStrct3d.png]({{site.baseurl}}/images/posts/AerialRobotics_ControlAndPlaning/nestedCtrlStrct3d.png)

Please keep in mind that the **angular velocity components** in body frame are as followed: <br>
$$\left[\begin{matrix}p\\q\\r\end{matrix}\right] = \left[\begin{matrix}
\cos\theta & 0 & -\cos\theta \\
0 & 1 & \sin\varphi \\
\sin\theta & 0 & \cos\varphi\cos\theta
\end{matrix}\right]  \left[\begin{matrix}\dot{\varphi} \\ \dot{\theta} \\ \dot{\psi} \end{matrix}\right]$$ <br>

#### Control For Hovering
Let's look at it in a special case, the **hovering**.

We will now **linearize** the dynamics at the hover configuration:
![hovering3D.png]({{site.baseurl}}/images/posts/AerialRobotics_ControlAndPlaning/hovering3D.png)

By means of these linearized equations we go further and look at the **nested control structure**.
![nCtrlStructHover.png]({{site.baseurl}}/images/posts/AerialRobotics_ControlAndPlaning/nCtrlStructHover.png)