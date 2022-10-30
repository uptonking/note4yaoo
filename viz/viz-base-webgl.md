---
title: viz-base-webgl
tags: [viz, webgl]
created: 2019-07-06T12:36:53.822Z
modified: 2020-12-21T07:47:02.451Z
---

# viz-base-webgl

# guide

- tips
  - 基于webgl实现数据可视化的重点在处理空间数据，然后渲染
  - 关注点可放在mapbox-gl、deck.gl，而不是threejs、babylonjs

- 👉🏻 webgl vs canvas
- webgl-pros
  - canvas可以使用webgl实现，使用webgl可以定制计算和优化细节
- webgl-cons
  - 基于webgl的开发更依赖图形学和数学知识，canvas被封装得更好，canvas开发更容易

- [cesium大牛-四季留歌-小结](https://www.zhihu.com/question/457815533/answer/2611385063)
  - 喜欢手撸原生但是懒得封装基本过程用 twgl
  - 不想写原生的过程式代码用 regl
  - 不想接触底层api用 threejs
  - 不想关注渲染知识用基于 threejs 之上的 ifc.js
  - 想深入定制长期发展的有时间研究的用 bbl
  - 有地理数据业务用 cesium

- [吴多益-webgl小结](https://zhuanlan.zhihu.com/p/162878354)
  - 对于一般WebGL开发，推荐使用 Babylon.js。
  - 如果要支持微信小程序，最好用国内的 LayaAir 和 Cocos，但需要注意它们只是源码开放，并不是无条件免费使用，需要仔细阅读使用协议。
  - 如果只想写原生WebGL特效，建议用 regl。
  - 如想支持大量光源和后期特效，又不需要支持iOS，用 Claygl。
  - 如果熟悉 Unity，直接用它导出 WebGL 也是可行的。
# faq

## webgl vs regl

- https://twitter.com/h_i_g_s_c_h/status/1370086897142337545
  - Maybe teaching webgl just using regl? That might be a good compromise between a heavy framework and the nitty gritty shader details.
    - I know and I love your notes on regl! I‘m actually using it here and there and for me it‘s a bit the D3 of webgl.

## webgl vs canvas 2d

### [Is there any reason for using WebGL instead of 2D Canvas for 2D games/apps?](https://stackoverflow.com/questions/21603350)

- WebGL is unusable without a GPU.
  - This hardware dependency is not a big problem because most systems have GPUs, but if GPU or CPU architectures ever evolve, preserving webgl content by emulation may be challenging. Running it on old (virtualized) computers is problematic.
  - But "Canvas vs WebGL" does not have to be a binary choice. 
    - I actually prefer using webgl for effects, but doing the rest in canvas. 
    - When I run it in a VM, it still works nicely and fast, just without the effects.
- "WebGL is unusable without a GPU" is false. It might be slow but it is not unusable.

- If you write code from zero, the canvas API is much easier to learn and understand. It requires minimal math knowledge, and development is fast and straightforward.
- Working with the WebGL API requires strong math skills and a full understanding of the rendering pipeline. People with these skills are harder to find, production is slower (due to the size and complexity of such a code base), and therefore it costs more.

## [Why isn't canvas 2D context using WebGL under the hood?](https://stackoverflow.com/questions/61698902)

- In theory, I believe everything in canvas 2D context could be emulated in WebGL, resulting in large performance gains. So why isn't it?

- Canvas2D does use the GPU under the hood using basically the same API as WebGL.
  - It's likely that if you implement the entire Canvas 2D spec in WebGL it will be a similar speed. 
  - Canvas supports things like drawing with patterns, drawing with gradients, clipping paths, lines with arbitrary widths, ends, joins, etc... 
  - Add all those features into your Canvas implemented in WebGL and it might a similar speed.
- The **reason WebGL can be faster** is (a) because you can choose not to implement the features you are not going to use and (b) because you can optimize knowing you're only going to use certain features.
- As a simple example, in canvas you can draw an image with drawImage(someImageElement, x, y). 
  - In WebGL you first have to create a texture from the image, then draw using the texture so you manually manage that texture. 
  - Canvas actually has to do the same thing. 
  - It had to load the image into a texture in order to draw it (assuming it's GPU based which canvas usually is). 
  - But, it has no idea if you're going to draw the image again so it can't keep that image as a texture forever. 
  - The simplest implementation would be to copy the image to a texture, draw, then delete the texture. I doubt that is what canvas does, I'm guessing it has some cache of textures it has made from images. 
  - But, the point is, it's management of textures is implicit where as in WebGL it's explicit, you have to manually manage the textures yourself.
- Another example is drawing shapes. 
  - In WebGL you generally decide what shapes to draw at init time, setup all the data needed to draw them, then at render time you just use the shapes you already setup. 
  - In Canvas it's more common to draw shapes on the fly meaning each time you want to draw the shape you use moveTo and lineTo commands to plot out the shape, which is effectively doing all the work every time you render instead of like WebGL doing that work only at init time.
- It's differences like those that add up to canvas being easier and webgl being faster.
- some people have tried to implement canvas2d in WebGL here and here
  - https://github.com/play-co/webgl-2d
    - /489Star/MIT/201104/js
    - WebGL-2D is a work in progress and currently supports a very small subset of the Canvas2D API.
  - https://github.com/karellodewijk/canvas-webgl
    - /21Star/NALic/201611/js
    - A canvas2d api implementation using webgl and javascript
  - https://github.com/jagenjo/Canvas2DtoWebGL
    - /206Star/MIT/202008/js
    - ports almost all the methods from the regular Canvas2D context (CanvasRenderingContext2D) of HTML5 to WebGL
    - this allows to mix 3D in your 2D Canvas or the opposite 
    - It uses litegl.js as the base WebGL library.
    - To improve performance it doesn't generate garbage (reuses the same containers). It can work with non power of two textures (no mipmaps obviously).

## [WebGL VS Canvas 2D hardware acceleration](https://stackoverflow.com/questions/36908427)

- These days, I need to draw many images on a canvas.
  - First, if I use canvas 2D context, I can just use context.drawimage() method to put every image on the proper location of the canvas.
  - Another way, I use WebGL to draw these images on the canvas. I use the image as texture to fill it.
  - Then, I compare the performance of these two methods. Both of their fps will reach 60
  - I compare their CPU usage. I expect that when I use WebGL, the CPU will use less because GPU will assure many work of drawing. But the result is, the CPU usage looks almost the same.
  - By google, I found that browser such as Chrome, Firefox will enable Hardware acceleration by default
  - I try to close the hardware acceleration. Then the CPU usage of the first method becomes much higher. 
- So, my question is, since canvas 2D use GPU to accelerate, is it necessary for me to use WebGL just for 2D rendering? 
  - What is different between canvas 2D GPU acceleration and WebGL? They both use GPU. 

- Canvas 2D has better compatibility.
- Theoretically WebGL can be faster because the default for canvas 2d is that the drawingbuffer is preserved whereas for WebGL it's not. 
  - That means if you turn anti-aliasing off on WebGL the browser has the option to double buffer. 
  - Something it can't do with canvas2d. 
- Another optimization is in WebGL you can turn off alpha which means the browser has the option to turn off blending when compositing your WebGL with the page, 
  - again something it doesn't have the option to do with canvas 2d. 
  - (there are plans to be able to turn off alpha for canvas 2d but as of 2017/6 it's not widely supported)
- But, by option I mean just that. It's up to the browser to decide whether or not to make those optimizations.
  - Otherwise if you don't pick those optimizations it's possible the 2 will be the same speed. I haven't personally found that to be the case. I've tried to do some drawImage only things with canvas 2d and didn't get a smooth framerate were as I did with WebGL. It made no sense to be but I assumed there was something going on inside the browser I was un-aware off.

- I guess that brings up the final difference. WebGL is low-level and well known. There's not much the browser can do to mess it up. Or to put it another way you're 100% in control.
  - With Canvas2D on the other hand it's up to the browser what to do and which optimizations to make. They might changes on each release. 
- An example would be what the canvas does when drawing an image. 
  - In WebGL you make the texture. You decide how complicated your shader is. 
  - In Canvas you have no idea what it's doing.
  - Maybe it's using a complicated shader that supports all the various canvas globalCompositeOperation, masking, and other features. 
  - Maybe for memory management it splits images into chucks and renders them in pieces. 
  - For each browser as well as each version of the same browser what it decides to do is up to that team, where as with WebGL it's pretty much 100% up to you. 
  - There's not much they can do in the middle to mess up WebGL.

## [threejs目前有什么缺陷?](https://www.zhihu.com/question/308346610)

- 优点
- TS支持
  - 这一点可以去看看其他经常使用到的类库就明确了，人家ThreeJS自带d.ts描述文件甚至是example里面没有并入核心部分的类都具备描述文件。
- 完全面向对象
  - 这一点可以说是前端开发的一大福利了，基本上很少有js库能够做到全面对象化，学习上在掌握三维编程的基础之后简直不要太简单，至少从上手来说已经将门槛降低很多了。
- 行业认同
  - 基本上大部分其他库或平台只要有相关的需要都会提供ThreeJS的集成路径，比如Mapbox、Echart、D3这一类，这一点可以说是最大的优势了。甚至大部分项目都愿意使用ThreeJS作为底层三维框架，比如AR.js、vanta.js等等。
- 完整三维特性
  - 什么PBR、风格化渲染、后期效果、物理、动画、粒子。。。。基本上上三维程序常用的功能特性他都是支持的，夫复何求？
- 底层可用性
  - 大部分功能性类库一旦想要拓展什么功能上来就是改源码重编类库，但是一旦读过ThreeJS源码就会知道，这玩意做拓展根本不需要搞源码，一方面是对象化封装使得我们可以继承重写，另一方面他其实已经将部分底层基础也是对象化实现了出来（比如着色器、几何体等）开发者可以对任意实例的任意属性或函数进行重写，这部分JS简直完胜C++。

- 缺点
- 易用性
  - 上面说了这玩意学习成本不高、编码难度不大，但是易用性较差。
  - ThreeJS只能算是三维引擎它只是在提供基础三维能力，并没有说提供强大的引擎能力，和真正的游戏引擎相比他缺乏优质好用的资源管理器、场景编辑器等等组件。
  - 甚至连写一个点选高亮都需要射线扫描同时集成后期效果实现，可以说只是让你能实现功能但是不能简易的实现功能。
- 性能问题
  - 这里的性能一方面虽然受到浏览器WebGL的限制，但是我认为ThreeJS的渲染管线确实是存在冗余的，但是我确实也没有找到问题出在哪里。
  - 其实可以和真正意义上的WebGL高性能应用做一下比较比如说mapbox、deck.gl等，基于GPU实时将大规模的矢量数据网格化并且完成渲染，同等量级下对比ThreeJS别说实时解析了即便是静态模型性能差距都很大（感觉有好几倍），并且人家还实现了模拟的64位精度运算。

- 总结
- 其实真正我想说的是一个定位的问题，假设你说你要做网页游戏那么有unity3D、你要做GIS有mapbox。
- 在各个具体的领域总有更为成熟且全面的WebGL框架给你使用。
- 但是ThreeJS的定位不在行业应用上，它的目的很简单只是为了在保证应用场景广度与拓展性的情况下降低WebGL的上手难度（只要写过原生WebGL都知道我在说什么）。
- 这样的东西缺点显然很多我上面说的只是冰山一角但是这些缺点根本就不重要，试问任何三维Web所要求的任何功能难道ThreeJS不能满足吗？基本真的不能满足那么拓展一下不就可以了？

- 缺陷很明显，一个2G左右的模型，加载一下试试。
  - 这是浏览器的问题还是threejs的问题呢
# WebGL
- ref
  - [caniuse webgl2](https://caniuse.com/webgl2)
    - 不支持：ie 11
    - 支持：safari preview-only

## overview

- WebGL is a cross-platform, royalty-free web standard for a low-level 3D graphics API based on OpenGL ES, exposed to ECMAScript via the HTML5 Canvas element. 
- Developers familiar with OpenGL ES 2.0 will recognize WebGL as a Shader-based API using GLSL, with constructs that are semantically similar to those of the underlying OpenGL ES API. It stays very close to the OpenGL ES specification, with some concessions made for what developers expect out of memory-managed languages such as JavaScript.
- WebGL 1.0 exposes the OpenGL ES 2.0 feature set; 
- WebGL 2.0 exposes the OpenGL ES 3.0 API.
- WebGL brings plugin-free 3D to the web, implemented right into the browser. 
- Major browser vendors Apple (Safari), Google (Chrome), Microsoft (Edge), and Mozilla (Firefox) are members of the WebGL Working Group.
- https://www.khronos.org/webgl/

## tips

- WebGL 1.0是基于OpenGL ES 2.0的API
- WebGL 2.0是基于OpenGL ES 3.0的API
- 在浏览器中，WebGL属于前端的API，后端根据不同平台使用OpenGL/Vulkan/D3D/Metal进行渲染
- WebGL目前来说比较适合做页游、WebVR的游戏以及基于Web的图形交互应用
- opengl vs opencl vs opencv
  - OpenGL(Open Graphics Library)是个定义了一个跨编程语言、跨平台的应用程序接口（API）的规格，它用于生成二维、三维图像
    - 这个接口由近三百五十个不同的函数调用组成，用来从简单图形到特绘制复杂的三维景象
    - 而另一种程序接口系统是仅用于Microsoft Windows上的Direct3D
    - OpenGL常用于CAD、虚拟实境、科学可视化程序和电子游戏开发
    - Photoshop, autoCAD之类加速都是通过OpenGL
    - Vulcan作为OpenGL的替代者，兼容性应该不会有什么问题
  - OpenCL(Open Computing Language)是一个为异构平台编写程序的框架，此异构平台可由CPU，GPU或其他类型的处理器组成
    - OpenCL由一门用于编写kernels （在OpenCL设备上运行的函数）的语言（基于C99）和一组用于定义并控制平台的API组成
    - OpenCL提供了基于任务分区和数据分区的并行计算机制
    - OpenCL类似于另外两个开放的工业标准OpenGL(跨平台图形API)和OpenAL(跨平台音效API)，这两个标准分别用于三维图形和计算机音频方面
    - OpenCL扩充了GPU图形生成之外的能力
    - OpenCL由非盈利性技术组织Khronos Group掌管
    - OpenCL基本没人用，Nvidia用CUDA，苹果推Metal，Android不支持，现在高通 Adreno 和 ARM Mali GPU 都支持 OpenCL 了，Android 带上厂商的 runtime 就能支持
    - 移动端通用计算除了芯片厂自己加OpenCL库做一些私有的功能，实际广泛采用的GPGPU实现方式是用OpenGL ES 2.0
    - OpenCL能够运行在CPU上，CPU厂商目前对Vulkan基本没有兴趣
    - opencl有其他同类产品覆盖不到的地方，FPGA,DSP,GPU CPU之类的都是可以用的，相比之下CUDA只支持N卡
  - OpenCV(Open Source Computer Vision Library)是一个跨平台的计算机视觉库(主要操作对象是图像)
    - OpenCV是由英特尔公司发起并参与开发，以BSD许可证授权发行，可以在商业和研究领域中免费使用
    - OpenCV可用于开发实时的图像处理、计算机视觉以及模式识别程序。该程序库也可以使用英特尔公司的IPP进行加速处理
- webgl与vulkan
  - WebGL 1.0 pipeline doesn’t allow us to use Vertex shader and Fragment shaders separately. So, we can’t use GPU to apply a matrix to a set of vertices, and get a new set of vertices. It’s a design limitation of OpenGL ES 2.0 which is partly resolved by OpenGL ES 3.0 / WebGL 2.0
  - Sadly, iOS Safari decided not to implement WebGL 3.0, effectively killing it.
  - vulkan设计的时候并没有把javascript考虑进来，例如一个command queue，javascript就找不到很好的数据结构来支持，而且javascript本身也是单进程的，所以多个command queue也不能很好的发挥作用。什么？你说有webworker，可是webworker thread之间的数据交互似乎也不像c里面的共享内存那么方便。此外，从我维护的一个WebGL的产品的用户来看，大多数是在Intel的集成显卡上跑(很多Mac用户)，程序的瓶颈是在GPU，而不是在于CPU。所以Javascript虽然慢，driver stack虽然厚，但是现在优化这些(Vulkan的主要提升点）并没有太多好处。不过我希望vulkan的stateless还是可以引入到webGL 3.0中。很多state management的事情引擎会作，就不需要driver再去做。

## 其他方案

- Vulkan
  - Vulkan最早是2015年由Khronos Group发布的一个低负载、多平台3D图形和运算API接口，当时被称为下一代OpenGL项目GLNext，但在这一名字发布后项目就被中止
      - Vulkan是OpenGL 5.0，也就是OpenGL 4.5的继任者
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
      - ANGLE是一个在Vulkan API基础上构建的 OpenGL ES 驱动。在Android Q上，开发者和手机厂商可以选择让某些应用使用 ANGLE 驱动，这可以让一些应用在不同设备上获得更为一致的特性。
  - 问题
      - Vulkan is not supported on Apple platform 201810
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
# 计算机图形学
- 选择参考
  - DX用作Windows平台的底层支持，最好能上个DX12
  - OpenGL、OpenGL ES作为Linux、Android、IOS等等其他平台的基础支持。如果需要更强的性能和更好的效果就上个Vulkan
  - 关于Metal，怕不是IOS独占，略过~略过~
  - 移动平台近年来对Vulkan的努力和对OpenGL的鄙视有目共睹，那最后你只能选择Vulkan
  - 移动桌面都能（除了苹果系），windows/linux/android都已经有vulkan的实现
- 案例参考
  - GODOT is moving to VULKAN (AND ES 2.0) instead of OPENGL ES 3.0 in 201802
  - notes
    - macOS 10.14 将逐渐淘汰 OpenGL和 OpenCL
    - OpenGL早期一直是由ARB (OpenGL Architecture Review Board，成员包括Nvidia, ATI, Intel, Apple, IBM, SGI等等）成员共同维护。每个成员可以为了支持自己硬件新的feature来开发OpenGL enxtension, 所有成员一致通过的extension才能加入到下个版本OpenGL核心中。这就造成了不同成员为了各自利益互相斗争，拖慢了开发进度。微软曾经也是ARB的成员之一，后来因为受不了这种机制退出专心搞自己的DirectX去了
    - OpenGL只是一个单纯的图形库，而DirectX是包含图形(Direct3D), 声音(DirectSound), 输入(DirectInput), 网络(DirectPlay)的一整套游戏开发解决方案。对开发者来说使用DirectX显然要方便的多。
    - ogl一直保持向后兼容，支持跨平台，就没什么其他优点了
  - OpenGL is mostly used for computer graphics, it is a graphics API
  - OpenCL is mostly used for parallel computing, it is a computation API.
  - You may use OpenGL to solve some problems you usually solve with OpenCL but you will have to map your problem to the graphics context in order to get your computation going.
  - I think the main reason for you to pick OpenGL for non-rendering tasks is to support older hardware that can't run OpenCL.
# game

## libgdx

- libGDX is a cross-platform Java game development framework based on OpenGL (ES) that works on Windows, Linux, Mac OS X, Android, your WebGL enabled browser and iOS.
  - https://github.com/libgdx/libgdx
  - https://libgdx.badlogicgames.com/
  - libGDX is licensed under the Apache 2 License.
  - source code based on GWT
# ref
- [How to animate WebGL with GSAP](https://www.reddit.com/r/webdev/comments/j7t271/best_way_how_to_animate_webgl_with_gsap/)
