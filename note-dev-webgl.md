---
tags: [dev/webgl]
title: note-dev-webgl
created: '2019-07-06T12:36:53.822Z'
modified: '2019-08-21T10:38:16.676Z'
---

# note-dev-webgl

## WebGL

### overview
- WebGL is a cross-platform, royalty-free web standard for a low-level 3D graphics API based on OpenGL ES, exposed to ECMAScript via the HTML5 Canvas element. 
- Developers familiar with OpenGL ES 2.0 will recognize WebGL as a Shader-based API using GLSL, with constructs that are semantically similar to those of the underlying OpenGL ES API. It stays very close to the OpenGL ES specification, with some concessions made for what developers expect out of memory-managed languages such as JavaScript.
- WebGL 1.0 exposes the OpenGL ES 2.0 feature set;
- WebGL 2.0 exposes the OpenGL ES 3.0 API.
- WebGL brings plugin-free 3D to the web, implemented right into the browser. 
- Major browser vendors Apple (Safari), Google (Chrome), Microsoft (Edge), and Mozilla (Firefox) are members of the WebGL Working Group.
- https://www.khronos.org/webgl/

### tips
- WebGL 1.0是基于OpenGL ES 2.0的API
- WebGL 2.0是基于OpenGL ES 3.0的API
- 在浏览器中，WebGL属于前端的API，后端根据不同平台使用OpenGL/Vulkan/D3D/Metal进行渲染
- WebGL目前来说比较适合做页游、WebVR的游戏以及基于Web的图形交互应用

- 问题
    - WebGL 1.0 pipeline doesn’t allow us to use Vertex shader and Fragment shaders separately. So, we can’t use GPU to apply a matrix to a set of vertices, and get a new set of vertices. It’s a design limitation of OpenGL ES 2.0 which is partly resolved by OpenGL ES 3.0 / WebGL 2.0
    - Sadly, iOS Safari decided not to implement WebGL 3.0, effectively killing it.
    - vulkan设计的时候并没有把javascript考虑进来，例如一个command queue，javascript就找不到很好的数据结构来支持，而且javascript本身也是单进程的，所以多个command queue也不能很好的发挥作用。什么？你说有webworker，可是webworker thread之间的数据交互似乎也不像c里面的共享内存那么方便。此外，从我维护的一个WebGL的产品的用户来看，大多数是在Intel的集成显卡上跑(很多Mac用户)，程序的瓶颈是在GPU，而不是在于CPU。所以Javascript虽然慢，driver stack虽然厚，但是现在优化这些(Vulkan的主要提升点）并没有太多好处。不过我希望vulkan的stateless还是可以引入到webGL 3.0中。很多state management的事情引擎会作，就不需要driver再去做。

### 挑战方案
- Vulkan
    - Vulkan最早是2015年由Khronos Group发布的一个低负载、多平台3D图形和运算API接口，当时被称为下一代OpenGL项目GLNext，但在这一名字发布后项目就被中止
    - 2016年2月16日，Khronos Group发布了Vulkan API的首个正式版本。从此，数字图形技术产业诞生了一个真正意义上能与OpenGL、Direct3D分庭抗礼的全新图形接口项目
    - Vulkan的目的是全面优于OpenGL等老的API，特点包括
        - Vulkan提供更低的运行开销、更直接的GPU控制和较低的CPU负载。通过批处理方式减少CPU的负载，将CPU从额外的运算和渲染中解放出来去执行别的任务
        - Vulkan原生支持多线程并发处理，而OpenGL是面向CPU单核的设计
        - Vulkan将计算任务和图形着色渲染统一管理，无需使用单独的计算API和图形API进行连接
        - 为移动设备和高端显卡提供跨平台的API接口支持
        - API的系统无关性提高了应用的可移植性
    - OpenGL使用高级语言GLSL（OpenGL Shading Language，OpenGL着色语言，常用于OpenGL的3D实时渲染的高级特效，如体积光、光线遮蔽阴影等效果）编写的着色器，它迫使每个OpenGL驱动必须为了GLSL运行自己的编译器将运行的程序解释成目标平台的可执行代码。
    - Vulkan提供了一种被成为SPIR-V[Standard Portable Intermediate Representation，轻量化标准中间件的二进制中间层格式，类似于HLSL(High-Level Shading Language，高级着色语言，在DirectX中的作用类似GLSL)着色器在DirectX中被编译的二进制代码。它减轻了显卡驱动方的负担，着色器可预编译，并允许程序开发者使用GLSL以外的语言编写着色器。
    -nvk:  Vulkan API for JavaScript/TypeScript
    - 案例
        - ANGLE是一个在 Vulkan API 基础上构建的 OpenGL ES 驱动。在 Android Q上，开发者和手机厂商可以选择让某些应用使用 ANGLE 驱动，这可以让一些应用在不同设备上获得更为一致的特性。
    - 问题
        -  Vulkan is not supported on Apple platform 201810
            - https://community.khronos.org/t/why-vulkan-is-not-supported-on-apple-platform/7577
            - the OS owns the GPU and the driver. The user can only communicate with the graphics driver to the extent that the OS allows them to. 
            - Windows had a channel to allow direct communication; MacOS never did. 
            - Without such direct communication mechanisms, it is not possible to build a Vulkan implementation directly.
            - You have to build it on top of MacOS’s graphics API: Metal.
            - Vulcan是Khronos Group（开发 OpenGL 的行业机构）开发的开放式跨平台 GPU API，可以在 Windows、Linux、Android、Nintendo Switch 和云系统上使用，但唯独缺少苹果的平台。macOS 上用的是又老又慢的 OpenGL 驱动，而 iOS 支持 OpenGL ES（OpenGL 子集，为嵌入式系统设计）。迄今为止，苹果并没有表现出对现代 Vulkan API 有任何兴趣，而是选择推出了自己的专属 Metal API。
            - MoltenVK（使用 Metal 实现的 Vulkan API 子集）允许开发者能够为苹果平台构建Vulkan应用程序
- WebGPU
    - Unlike WebGL, WebGPU is not a direct port of any existing native API. 
    - It is based on concepts in Vulkan, Metal, and Direct3D 12 and is intended to provide high performance on these modern graphics APIs across mobile and desktop platforms

## 计算机图形学

- 选择参考
    - DX用作Windows平台的底层支持，最好能上个DX12
    - OpenGL、OpenGL ES作为Linux、Android、IOS等等其他平台的基础支持。如果需要更强的性能和更好的效果就上个Vulkan
    - 关于Metal，怕不是IOS独占，略过~略过~
    - 移动平台近年来对Vulkan的努力和对OpenGL的鄙视有目共睹，那最后你只能选择Vulkan
    - 移动桌面都能（除了苹果系），windows/linux/android都已经有vulkan的实现
- 案例参考
    - GODOT is moving to VULKAN (AND ES 2.0) instead of OPENGL ES 3.0 in 201802
    



## game

### libgdx
- libGDX is a cross-platform Java game development framework based on OpenGL (ES) that works on Windows, Linux, Mac OS X, Android, your WebGL enabled browser and iOS.
- https://github.com/libgdx/libgdx
- https://libgdx.badlogicgames.com/
- libGDX is licensed under the Apache 2 License.
- source code based on GWT
