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

{% highlight c++ linenos %}
// if only one src code then sz=1 and length omitted
glShaderSource(id, sz, ptr_to_code, length);
// compile the src
glCompileShader(id);
// to check for invalid values or errors
glGetShaderiv(id, flag, ptr_to_buffer);
glGetShaderInfoLog(id, log_length, msg_length /*NULL*/, ptr_to_msg);
{% endhighlight %}

After compiling the shader code, they have to be linked to a created programm.
{% highlight c++ linenos %}
GLuint program_id = glCreateProgram();
glAttachShader(program_id, vertex_shader_id);
glAttachShader(program_id, fragment_shader_id);
glLinkProgram(program_id);
{% endhighlight %}

#### GL Shader Language (GLSL)

##### Vertex Shader

{% highlight glsl linenos %}
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
{% highlight glsl linenos %}
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
Remember forever:
- if $$w == 1$$, then the vector $$(x,y,z,1)$$ is a **position in space**
- if $$w == 0$$, then the vector $$(x,y,z,0)$$is a **direction in space**

**Homogeneous coordinates** allow us to use a single mathematical formula to deal with these two cases.

#### Model Matrix
To go from **Model Space** (all vertices efined relatively to the cetner of the model) to **World Space** (all vertices defined relatively to the center of the world), we have to multiply all vertices by the Model Matrix.

#### View Matrix
To go from **World Space** (all vertices defined relatively to the center of the world) to **Camera Space** (all vertices defined relatively to the camera, we have to multiply all vertices in World Space by the View Matrix.

{% highlight c++ linenos %}
glm::mat4 CameraMatrix = glm::lookAt(
  cameraPosition, // the position of your camera, in world space
  cameraTarget,   // where you want to look at, in world space
  upVector        // probably glm::vec3(0,1,0)
);
{% endhighlight %}

#### Projection Matrix
In **Camera Space** a vertex that happens to have $$x==0$$ and $$y==0$$ should be rendered at the center of the screen. To take the depth into account we have to get into **Perspective Projection**. This is done by multiplying by the Projection Matrix.

{% highlight c++ linenos %}
// Generates a really hard-to-read matrix, but a normal, standard 4x4 matrix nonetheless
glm::mat4 projectionMatrix = glm::perspective(
  glm::radians(FoV), // The vertical Field of View, in radians: the amount of "zoom". 
  4.0f / 3.0f,       // Aspect Ratio. Depends on the size of your window. 
  0.1f,              // Near clipping plane. Keep as big as possible, or you'll get precision issues.
  100.0f             // Far clipping plane. Keep as little as possible.
);
{% endhighlight %}

#### Example Of Shaders
{% highlight glsl linenos %}
#version 330 core

// input vertex data, different for all executions of this shader
layout(location = 0) in vec3 vertexPosition_modelspace;
layout(location = 1) in vec3 vertexColor;

// values that stay constant for the whole mesh
uniform mat4 MVP;

// output data
out vec3 fragmentColor;

void main() 
{
  gl_Position = MVP * vec4(vertexPosition_modelspace, 1);
  fragmentColor = vertexColor;
}
{% endhighlight %}