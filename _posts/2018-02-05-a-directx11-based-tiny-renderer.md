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

### Basic Initialization Of DirectX11
{% highlight c++ linenos %}
// COM interface object used to change the back to the front buffer
IDXGISwapChain* SwapChain;
// interface, which represents our hardware device (GPU)
ID3D11Device* d3d11Device;
//  2nd part of device interface, used to call rendering methods
ID3D11DeviceContext* d3d11DevCon;
// interface object which is the render target view
//  we write into this 2D texture and this texture is sent to the pipeline
ID3D11RenderTargetView* renderTargetView;
{% endhighlight %}

Create the **Swap Chain**, the **Back Buffer** and the **Render Target View**. Actually we write into the 2D texure of the Render Target View and send this to the pipeline to be rendered. Then bind them to the **Output-Merger State** of the pipeline.

{% highlight c++ linenos %}
// Create SwapChain
hr = D3D11CreateDeviceAndSwapChain(
  NULL,                     // pAdapter
  D3D_DRIVER_TYPE_HARDWARE, // DriverType
  NULL,                     // Software
  NULL,                     // Flags
  NULL,                     // pFeatureLvls
  NULL,                     // FeatureLvls
  D3D11_SDK_VERSION,        // SDK Version
  &swapChainDesc,           // pSwapChainDesc
  &SwapChain,               // ppSwapChain Interface
  &d3d11Device,             // ppDevice
  NULL,                     // pFeatureLvls
  &d3d11DevCon              // ppImmediateContext
  );
  
// Create BackBuffer
ID3D11Texture2D* BackBuffer;
hr = SwapChain->GetBuffer( 
  0,                            // first buffer 
  __uuidof( ID3D11Texture2D ),  // ref ID to type of interface
  (void**)&BackBuffer           // ptr to buffer
  );

// Create Render Target
hr = d3d11Device->CreateRenderTargetView(
  BackBuffer,        // pResource
  NULL,              // pDesc
  &renderTargetView  // pRTView
  );
// we don't need the backbuffer anymore
BackBuffer->Release();

// Bind  Render Target to Output-Merger state
d3d11DevCon->OMSetRenderTargets(
  1,                 // NumViews of render target views
  &renderTargetView, // ppRenderTargetViews
  NULL               // pDepthStencilView
  );
{% endhighlight %}

### Rendering A Scene
{% highlight c++ linenos %}
void DrawScene()
{
  // clear backbuffer to color
  D3DXCOLOR bgColor(red, green, blue, 1.f);
  
  d3d11DevCon->ClearRenderTargetView(
    renderTargetView,  // pRenderTargetView
    bgColor            // ColorRGBA
    );
    
  // present backbuffer to screen
  SwapChain->Present(
    0,                 // SyncInterval
    0                  // Flags
    );
}
{% endhighlight %}

### Spaces

#### Local Space
Local space is the space relative to an object.

#### World Space
World space is used to position each object relative to eatch other, in the world space.

#### View Space
The view space is basically the camera's space.

#### Projection Space
The space that, if objects are in, they are rendered to the screen, and if objects are out, they are discarded. It is defined by six planes, the near plane, far plane, top, left, bottom and right planes.

#### Screen Space
The last space is basicallz the x and y values in pixels of the backbuffer, where $$(0,0)$$ marks the top left of the space. This is the 2D space thats actually displayed on the monitor.

### Matrices
The rendering pipeline uses three spaces: World, View and Projection. To transform them from one to the other, we will multiply them together.

#### World Matrix
This matrix is used to **convert the vertices of our objects into vertices in the 3D scene**.

#### View Matrix
The view matrix is used to **calculate the position of where we are looking at the scene from**.

#### Projection Matrix
The projection matrix is used to **translate the 3D scene into the 2D viewport space**.

#### Orthographic Projection Matrix
This matrix is used for **rendering 2D element like user interfaces on the screen** allowing us the skip the 3D rendering.

### Buffers

#### Vertex Buffer
An objects is composed of hundreds of triangles. Each of the triangles in the model has three points to it, they re called vertices. To render the object we need to put all vertices into a special array that we call **vertex buffer**.

##### Input Layout
Direct3D uses what is called an **input layout**. An input layout is the layout of the data containing the location and properties of a vertex.

Input layout let us select which information we want to use and send just that data. This enables us to send many more vertices between each frame.

#### Index Buffers
Index buffers are related to vertex buffers. Their purpose is to record the location of each vertex that is in the vertex buffer. They help find the vertex faster.

#### Vertex Shaders
Vertex shaders are small programms that are written maily for transforming the vertices from the vertex buffer into 3d space.

#### Pixel Shaders
Pixel shaders are small programs that are written for doing the coloring of the polygons that we draw. They are run by the GPU for every visible pixel.

### Shaders And HLSL
The vertex and pixel shader are **COM objects**.

{% highlight c++ linenos %}
// global
ID3D11VertexShader* pVS;
ID3D11PixelShader* pPS;

void InitPipeline()
{
  // load and compile the two shaders
  ID3D10Blob *VS, *PS;
  D3DX11CompileFromFile(L"shaders.shader", 0, 0, "VShader", "vs_4_0", 0, 0, 0, &VS, 0, 0);
  D3DX11CompileFromFile(L"shaders.shader", 0, 0, "PShader", "ps_4_0", 0, 0, 0, &PS, 0, 0);

  // encapsulate both shaders into shader objects
  dev->CreateVertexShader(VS->GetBufferPointer(), VS->GetBufferSize(), NULL, &pVS);
  dev->CreatePixelShader(PS->GetBufferPointer(), PS->GetBufferSize(), NULL, &pPS);

  // set the shader objects
  devcon->VSSetShader(pVS, 0, 0);
  devcon->PSSetShader(pPS, 0, 0);
}
{% endhighlight %}

### Programmable Graphics Rendering Pipeline
![RenderPipeline.PNG]({{site.baseurl}}/images/posts/DirectX11_AnIntroduction/RenderPipeline.PNG)

#### Input Assembler (IA)
The IA is a fixed function stage, which reads geometric data, vertices and indices. It uses the data to create primitives which will be fed into and used by other stages.
The two buffers used by the IA are the **vertex** and **index buffers**.

#### Vertex Shader (VS)
The VS is the first programmable shader, which means we have to program it ourselves.
The VS stage is what all the vertices go through after the primitives have been assembled in the IA. It allows transformation, scaling, lighting, displacement mapping for textures and stuff like that.

The vertex shader takes a single vertex as input and returns a single input.

#### Hull Shader (HS)
The HS is the first of the three optional stages added to graphics rendering pipeline. The three new stages , Hull Shader, Tessellator and Domain Shader, all work together to implement **tesselation**.

Tesselation takes a primitive object and divides it up into many smaller section to increase the detail of models. They are not saved to memory, so this saves much time in creating them on the CPU and memory.

The **Hull Shader**  calculates how and where to add new verties to a primitive to make it more detailed.

#### Tessellator (TS)
The TS is the second, fixed stage in the tessellation process and actually does the diving of the primitive.

#### Domains Shader (DS)
This programmable function stage transforms the vertices from the the tessellator stage to create the more detail.

#### Geometry Shader (GS)
Another optional pragrammable function stage. It is able to create or destroy primitives.

#### Stream Output (SO)
This stage is used to obtain Vertex data from the pipeline. Vertex data output from the SO are always sent out as lists, such as line lists or triangle list. Incomplete primitives are never sent out, they are just silently discarded.

#### Rasterization Stage (RS)
The RS stage takes the vector information sent to it and turns them into pixels by interpolating per-vertex values across each primitive.
It also handles the clipping.

#### Pixel Shader (PS)
This stage does calculations and modifies each pixel, such as lighting on a per pixel base. It is another programmable function and an optional stage.

The job of the pixel shader is to calculate the final color of each pixel fragment.

#### Output Merger (OM)
The final stage in the pipeline. This stage takes the pixel fragments and depth/stencil buffers and determines which pixels are actually written to the render target.

##### Depth/Stencil View
This lets the OM stage check all the pixel fragment's depth/stencil values on a render target.
The depth values are used to draw pixel which are in front and discard those in the back.
The stencila part of the depth view is for advanced techniques, such as mirrors.
