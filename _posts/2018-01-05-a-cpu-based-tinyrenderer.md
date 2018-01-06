---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: A CPU Based TinyRenderer
description: TinyRenderer based on the Tutorial by Jofrey Luc
headline: A CPU Based TinyRenderer
categories:
  - Mathematics
  - C++
  - Programming
tags: Renderer Graphics
---
>&quot;It’s not that I’m so smart, it’s just that I stay with problems longer.&quot;<small><cite title="einstein">Einstein</cite></small>

## Graphic Pipeline - An Introduction
Back in 2016 I found this little tutorial about the programming of a renderer. Due to other projects I could fullfil this one. And this is why I'm back on it.

I love seeing computer creating virtual worlds and therefore I want to now what are the basics of it.

With this little tutorial created by Jofrey Luc I try to fill this mind gap. The goal is to build a small "tiny" renderer powered by the CPU.

I will document my humble opinion and what I learnt from it here in this posts. 

### Modelview Matrix
Due to the camera position the new coordinate system of the objects has to be calculated.

#### LookAt Method
The **lookAt** method calculates the **ModelView** matrix by means of the eye, its up vector and the center coordinates. With this three vectors we can calculate the inverse transformation matrix from the initial coordinate system to the model coordinate system.

{% highlight cpp linenos %}
void lookat(Vec3f eye, Vec3f center, Vec3f up) {
    Vec3f z = (eye-center).normalize();
    Vec3f x = cross(up,z).normalize();
    Vec3f y = cross(z,x).normalize();
    Matrix Minv = Matrix::identity();
    Matrix Tr   = Matrix::identity();
    for (int i=0; i<3; i++) {
        Minv[0][i] = x[i];
        Minv[1][i] = y[i];
        Minv[2][i] = z[i];
        Tr[i][3] = -center[i];
    }
    ModelView = Minv*Tr;
}
{% endhighlight %}
