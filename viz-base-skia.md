---
title: viz-base-skia
tags: [canvas, skia, viz, webgl]
created: '2021-05-19T17:46:51.794Z'
modified: '2021-05-19T17:48:06.572Z'
---

# viz-base-skia

# guide

- 技术选型
  - 全局canvas自绘制，还是部分自绘制+部分现有框架/dom绘制
  - 比如，基于canvas的data-grid很多只有行列部分是canvas，其余部分是基于dom实现
# faq

## skia vs canvas2d

- 对canvas的优化由浏览器决定，浏览器可能会选择它认为快的方式，如GPU
  - 使用skia由开发者决定什么时候使用何种方式
  - skia作为底层渲染工具库，提供了更底层的api，可以实现canvas api没有的功能
# discuss-stars
- ## 

- ## 
# discuss
- ## 

- ## 

- ## skia official: CanvasKit – Skia and WebAssembly
- https://news.ycombinator.com/item?id=20478860
- Skia is a 2d graphics engine developed in C++. 
  - Think of it as the building block for graphical interfaces, animations and everything else that involves displaying some 2D data on a screen, specially vectorial data.
  - For example, Flutter uses it to draw its UIs and Chrome uses it for almost everything, including rendering text parsed from HTML. Sublime Text, Firefox, Xamarin and many other projects also rely on Skia for the same sort of thing.
  - However, unlike, let's say, Qt or GTK+, Skia does not provide already done widgets (i.e., drop-in buttons, windows, text inputs etc.). It's like the fundamental building block on top of which you can create your buttons, animations and everything else and then display it on screen.
  - Now, CanvasKit is Skia ported to the browser via WebAssembly. Since Skia is a mature project and very performant (as you can guess from who is using it), it's now an alternative to Canvas API and DOM to render things on websites and will also let existing native applications to be ported to the web more easily.
- Skia is just a 2D drawing API, like Cairo. 
  - It's what Chrome uses under the hood to render their whole UI I think, including (non-WebGL) HTML5 canvas stuff.
  - Why you would want to use this over HTML5 canvas? 
  - Good question. Maybe you want some features in Skia that aren't in the canvas API? Maybe you have a Skia app that you want to port to the web?
- Any browser already includes the very same set of graphic primitives that Skia provides. Just to render what you see on the screen right now. Why not just to expose all that as API for WASM or whatever?
  - HTML canvas is incredibly slow and just a generally bad API. Using it from WASM is a mistake. It uses strings for everything and has a particularly slow imperative API, and the spec/de-facto-spec behaviors perform very slowly even on high-end hardware. I've seen relatively simple 2D canvas-based games drop frames in chrome on a GTX 2080ti because canvas is that bad.
  - **There is no guarantee that canvas is hardware accelerated, or how whatever they are optimized, so a low level software rendering library might turn out to execute faster, regardless of the browser**.
  - This is not about Canvas but rather set of primitives that browser uses for rendering web pages.

- ## Skia-canvas, a browserless implementation of the Canvas API for Node.js 
- https://news.ycombinator.com/item?id=24364656
- I'm curious, what if anything is different from node-canvas? 
  - This uses the Skia backend instead of Cairo. 
  - It will give results closer to Chrome's Canvas implementation.
  - It also doesn't appear to support Windows yet, whereas node-canvas does.
  - There's probably other differences, e.g. performance, size, etc. but you'd have to measure them.
- What are the differences between this and canvaskit, the official wasm version (?) of skia?
  - This is a native dependency where that's compiling skia itself to wasm. 
  - The native dependency should be able to be faster by a wide margin by taking advantage of hardware acceleration but it's not obvious if it does (similarly skia compiled to wasm must be much slower than using the proper canvas API in the browser)
- Skia itself has multiple backends, including CPU and GPU implementations. 
  - The wasm one must use the CPU path, where Skia in your browser can use a CPU or GPU path based on whatever is fastest. So already **wasm is necessarily equal-or-slower**.
  - Wasm also does have some overhead too; some of that will get better with upcoming changes; at least wasm-SIMD support and threads are both only available in some environments.
  - But don't get me wrong, I'm certainly not suggesting the skia-wasm project is pointless, there's just trade-offs here.
- Usually wasm is twice slower than native code
  - WebAssembly is essentially a bytecode that needs to be JITted before running. That's pretty much the same situation as with Java, you may have comparable performance but usually comparable Java code runs slower that native.

- ## Fast UI Draw is a library that provides a higher performance Canvas interface
- https://news.ycombinator.com/item?id=25079266
  - https://github.com/intel/fastuidraw
  - /inactive--201912/MPLv2
- Note that this has been practically unmaintained since Kevin Rogovin (fastuidraw's principal author) left Intel. It's also very suspect from testing 
- What is "Canvas interface" referring to here? I thought it was about the browser Canvas API 
  - The general 2D drawing API you'll find basically everywhere. 
  - So eg Skia's SkCanvas, QT's QPainter, Cairo's whatever, HTML5's `<canvas>` , etc... 
  - The basic 2D drawing "thing" (drawGlyphs, drawRect, drawImage, etc...)
  - It's referring to that broad concept, not a specific Canvas interface.
  - Vector graphics: drawing stuff by issuing commands to render specific simple geometric elements (lines, rects, triangles, circles)
  - Canvas: a context in which to place "objects" in 3 dimensions (x, y and z), and have them appropriately re-rendered when necessary (motion, object addition/removal)
- The standard Canvas API is probably your best option. 
  - So if some library claims to have better performance than Canvas 2D, I would love to see a benchmark on that. 
  - Anyone would assume WebGL is faster, but as you know "assumption is the mother of all fuckups". Let me explain.
  - A year ago, I had to make a proof of concept for drawing Gantt charts on a Canvas. 
  - Coming from a game development background, my assumption was that some things would be too slow on a canvas
  - rotating graphics
  - drawing an insane amount of rectangles
  - filling surfaces with a certain repeating texture
  - So I also included a benchmark of Canvas vs WebGL. 
  - The conclusion was that for most things, Canvas was faster:
  - rotating graphics
  - texturizing
  - etc.
  - This really amazed me, because as an old school game developer, I know all limitations of 2D rendering. 
  - The thing is, **all modern browsers heavily optimize their Canvas to the GPU**. Even the older Edge. Do some heavy Canvas 2D drawing, and see your GPU usage spikes.
  - Plus, rendering text on WebGL is not as straightforward.
  - However, there was a tipping(引爆点；临界点) point when drawing an insane amount of rectangles (which basically become dots), where WebGL would take over.
  - So for this project, the simplicity of the Canvas API, the text rendering, and the performance were definitely a sure way to use that one instead of a more complex, slower WebGL.
