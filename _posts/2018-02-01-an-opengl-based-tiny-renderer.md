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
- if $$w == 0$$, then the vector $$(x,y,z,0)$$ is a **direction in space**

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
The input variable to the shaders have to be passed and/or to be en-/disabled in the C++ code as follows:
{% highlight c++ linenos %}
GLuint program_id = LoadShaders("path/filename.vs", "path/filename.fs");

// get a handle for our "MVP" uniform 
GLuint matrix_id = glGetUniformLocation(program_id, "MVP");
do {
  glUseProgram(program_id);
  
  // send uniform variable to the shader
  glUniformMatrix4fv(matrix_id, 1, GL_FALSE, pointer_matrix_begin);
  
  // enable connection
  glEnableVertexAttribArray(0);		// layout location 0
  glBindBuffer(GL_ARRAY_BUFFER, vertex_buffer);
  
  glVertexAttribPointer(
    0,          // attribute 0
    3,          // size
    GL_FLOAT,   // type
    GL_FALSE,   // normalized
    0,          // stride
    (void*)0    // array buffer offset
  );
  
  glDrawArrays(GL_TRIANGLES, 0, cnt);
  
  // disable connection
  glDisableVertexAttribArray(0);
  
} while (true);
{% endhighlight %}

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

{% highlight glsl linenos %}
#version 330 core

// input data
in vec3 fragmentColor;

// output data
out vec3 color;

void main()
{
  color = fragmentColor;
}
{% endhighlight %}

### Buffers And Textures
Creating textures is very similar to creating vertex buffers: **Create** a texture, **bind** it, **fill** it, and **configure** it.

In **glTexImage2D**, the GL_RGB indicates that we are talking about a 3-component color, and GL_BGR says how exactly it is represented in RAM. As a matter of fact, BMP does store $$\text{Blue}\to\text{Green}\to\text{Red}$$, and this has to be told to OpenGL.

{% highlight glsl linenos %}
// create an OpenGL texture
GLuint textureID;
glGenTextures(
  1,          // number of texture names to be generated
  &textureID  // array which stores the generated texture names
  );

// BIND the newly created texture: all future texture functions will modify texture
glBindTexture(
  GL_TEXTURE_2D,   // specify target
  textureID        // texture name
  );

// FILL the image and give it to OpenGL
glTexImage2D(
  GL_TEXTURE_2D,      // target texture
  0,                  // level of detail
  GL_RGB,             // internal format
  width, height,      // texture image
  0,                  // border
  GL_BGR,             // data format
  GL_UNSIGNED_BYTE,   // data type
  data                // ptr to image data
  );
  
// CONFIGURE it (poor filtering)
glTexParameteri(
  GL_TEXTURE_2D,          // target texture
  GL_TEXTURE_MAG_FILTER,  // symbolic name
  GL_NEAREST              // value of name
  );
glTexParameteri(
  GL_TEXTURE_2D,
  GL_TEXTURE_MAG_FILTER,
  GL_NEAREST
  );
{% endhighlight %}

#### Compressed Textures
A useful tool to create compressed textures, which are understood by the graphics hardware is [The Compressonator](https://gpuopen.com/gaming-product/compressonator/). It can produce mipmaps inthe formats DXT1, DXT3 or DXT5.
Your graphics card provides dedicated hardware to decompress such file formats. Therefor using texture compression yields a 20% increase in performance.

This [link](https://msdn.microsoft.com/en-us/library/bb943982.aspx) provides information about the file layout of a .dds file.

#### Texture Sampler
A texture sampler helps to access the color at a specific UV coordinate in a texture. This is done in the **fragment shader**.

{% highlight glsl linenos %}
// interpolated values from the vertex shaders
in vec2 UV;

// output data
out vec3 color;

// values that stay constant for the whole mesh
uniform sampler2D textureSampler;

void main()
{
  color = texture(textureSampler, UV).rgb;
}
{% endhighlight %}

### Basic Shading
This includes the following lighting effects which increase the realism of the scene: **ambient**, **diffuse** and **specular light**. 

#### Vertex Shader
The vertex shader is used to compute the **normal vectors**, the **eye point coordination** and **light direction vector**. All three must be in the same space.

{% highlight glsl linenos %}
//input vertex data
/* location 0 is used for vertex position */
layout(location = 1) in vec2 vertexUV;
layout(location = 2) in vec3 vertexNormal_modelspace;

// output data ; will be interpolated for each fragment
out vec2 UV;
out vec3 Position_worldspace;
out vec3 Normal_cameraspace;
out vec3 EyeDirection_cameraspace;
out vec3 LightDirection_cameraspace;

// values that stay constant for the whole mesh
uniform mat4 MVP;
uniform mat4 V;
uniform mat4 M;
uniform vec3 LightPosition_worldspace;

void main()
{
  /* output position of the vertex, in clip space : gl_Position */

  // position of the vertex, in worldspace : M * position
  Position_worldspace = (M * vec4(vertexPosition_modelspace, 1)).xyz;

  // vector that goes from the vertex to the camera, in camera space
    
  //  in camera space, the camera is at the origin (0,0,0)
  vec3 vertexPosition_modelspace = (V * M * vec4(vertexPosition_modelspace, 1)).xyz;
  EyeDirection_cameraspace = vec3(0,0,0) - vertexPosition_modelspace;

  // vector that goes from the vertex to the light, in camera space.
  //  M is ommited because it's identity
  vec3 LightPosition_cameraspace = (V * vec4(LightPosition_worldspace, 1)).xyz;
  LightDirection_cameraspace = LightPosition_cameraspace + EyeDirection_cameraspace;

  // normal of the vertex, in camera space
  Normal_cameraspace = (V * M * vec4(vertexNormal_modelspace, 0)).xyz; // generally use its inverse transpose

  // UV of the vertex. no special space for this one
  UV = vertexUV;
}
{% endhighlight %}

#### Ambient Light
This is most faked light in computer graphics. It is done by adding simply a fixed value in the shader.

{% highlight glsl linenos %}

{% endhighlight %}