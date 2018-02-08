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
>&quot;The engines don’t move the ship at all. The ship stays where it is and the engines move the universe around it.&quot;<small><cite title="futurama">Futurama</cite></small>

## Tiny Real OpenGL Application
After completing the tutorial about building my own graphics pipeline. I will continue my journey to trully understand 3D graphics by looking at OpenGL.

### OpenGL Toolkit
I'm using GLFW v3.2.1 as a toolkit to manage windows and user inputs. It has been installed by means of Home Brew.

### Shaders
Shaders have to be compiled at runtime. This usually happens at startup. 

{% highlight c++ lineos %}
// if only one src code then sz=1 and length omitted
glShaderSource(id, sz, ptr_to_code, length);
// compile the src
glCompileShader(id);
// to check for invalid values or errors
glGetShaderiv(id, flag, ptr_to_buffer);
glGetShaderInfoLog(id, log_length, msg_length /*NULL*/, ptr_to_msg);
{% endhighlight %}

After compiling the shader code, they have to be linked to a created programm.
{% highlight c++ lineos %}
GLuint program_id = glCreateProgram();
glAttachShader(program_id, vertex_shader_id);
glAttachShader(program_id, fragment_shader_id);
glLinkProgram(program_id);
{% endhighlight %}

#### GL Shader Language (GLSL)

##### Vertex Shader

{% highlight glsl lineos %}
// version description
#version 330 core
// location: buffer we use for the variable
// in: input data (corresponding out)
// vec3: data type
layout(location = 0) in vec3 variable_name;

// main
void main()
{
  //  gl_Position: built-in variable 
  gl_Position.xyz = variable_name;
  gl_Position.w = 1.0;
}
{% endhighlight %}

##### Fragment Shader
{% highlight glsl lineos %}
// version description
#version 330 core
// out: output data
// vec3; data type
out vec3 variable_name;
// main
void main()
{
  variable_name = vec3(1,0,0);
}
{% endhighlight %}

### Homogeneous Coordinates
Remember for ever:
- if $$w == 1$$, then the vector $$(x,y,z,1)$$ is a **position in space**
- if $$w == 0$$, then the vector $$(x,y,z,0)$$is a **direction in space**
