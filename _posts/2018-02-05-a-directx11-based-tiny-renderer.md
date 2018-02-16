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
{% highlight c++ linenos %}
// COM interface object used to change the back to the front buffer
IDXGISwapChain* SwapChain;
// interface, which represents our hardware device (GPU)
ID3D11Device* d3d11Device;
//  2nd part of device interface, used to call rendering methods
ID3D11DeviceContext* d3d11DevCon;
// interface object which is the render target view
//  we write into this 2d texture and this texture is sent to the pipeline
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
d3d11DevCon->OMSetRenderTargets( 1, &renderTargetView, NULL );
{% endhighlight %}

#### Projection Matrix
The projection matrix is used to **translate the 3D scene into the 2D viewport space**.

#### World Matrix
This matrix is used to **convert the vertices of our objects into vertices in the 3D scene**.

#### View Matrix
The view matrix is used to **calculate the position of where we are looking at the scene from**.

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
