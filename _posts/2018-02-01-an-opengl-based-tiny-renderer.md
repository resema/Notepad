---
layout: post
published: true
mathjax: true
featured: false
comments: true
title: An OpenGL Based Tiny Renderer
description: A Tiny Renderer based on OpenGL
headline: Llet's use OpenGL to renderer!
categories:
  - Mathematics
  - C++
  - Programming
tags: 3DGraphics Tutorial OpenGL
---
>&quot;It’s not that I’m so smart, it’s just that I stay with problems longer.&quot;<small><cite title="einstein">Einstein</cite></small>

## Tiny Real OpenGL Application
After completing the tutorial about building my own graphics pipeline. I will continue my journey to trully understand 3D graphics by looking at OpenGL.

### OpenGL Toolkit
I'm using GLFW v3.2.1 as a toolkit to manage windows and user inputs. It has been installed by means of Home Brew.

### Shaders
Shaders have to be compiled at runtime. This usually happens at startup. 

{% highlight cpp lineos %}
// if only one src code then sz=1 and length omitted
glShaderSource(id, sz, ptr_to_code, length);
// compile the src
glCompileShader(id);
// to check for invalid values or errors
glGetShaderiv(id, flag, ptr_to_buffer);
glGetShaderInfoLog(id, log_length, msg_length /*NULL*/, ptr_to_msg);
{% endhighlight %}

After compiling the shader code, they have to be linked to a created programm.
{% highlight cpp lineos %}
GLuint program_id = glCreateProgram();
glAttachShader(program_id, vertex_shader_id);
glAttachShader(program_id, fragment_shader_id);
glLinkProgram(program_id);
{% endhighlight %}