---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: A DirectX11 Based Tiny Renderer
description: An Introduction into DirectX11
headline: A DirectX11 Based Tiny Renderer
categories:
  - Mathematics
  - C++
  - Programming
---
>&quot;Everybody is a genius. But if you judge a fish by its ability to climb a tree, it will live its whole life believing that it is stupid.&quot;<small><cite title="einstein">Einstein</cite></small>

## Tiny DirectX11 Application
I'm extending my journey into graphics renderering by DirectX11. I found this larger collection of [tutorials](http://www.rastertek.com/tutindex.html) and I will go through them as far as possible.
I'll report here my findings and the most important points IMHO.

### Creating A Framework and Window
Missing description of long intialization.

### Initialize DirectX11
Even longer description is missing.

#### Projection Matrix
The projection matrix is used to **translate the 3D scene into the 2D viewport space**.

#### World Matrix
This matrix is used to **convert the vertices of our objects into vertices in the 3D scene**.

#### View Matrix
The view matrix is used to **calculate the position of where we are looking at the scene from**.

#### Orthographic Projection Matrix
This matrix is used for **rendering 2D element like user interfaces on the screen** allowing us the skip the 3D rendering.