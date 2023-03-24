---
title: toc-viz-base-webgl
tags: [lib, toc, viz, webgl]
created: 2020-07-17T13:33:55.480Z
modified: 2020-10-05T06:18:29.671Z
---

# toc-viz-base-webgl

# popular

- red-otter /83Star/MIT/202303/ts/NoDeps
  - https://github.com/tchayen/red-otter
  - https://red-otter.dev/
  - Self-contained WebGL flexbox layout engine
  - Canvas-like WebGL renderer which supports text rendering and arbitrary polygons (by triangulating them).
  - Text rendering is based on a font atlas texture that uses SDF (signed distance field).
  - Layout engine which resembles Facebook Yoga
  - JSX support with DOM-like elements
  - In terms of software philosophy, think about products such as Warp or Zed. They are extremely fast programs which implement their own GPU rendering.

- deck.gl /10.3kStar/MIT/202210/ts
  - https://github.com/visgl/deck.gl
  - https://deck.gl/
  - a WebGL2-powered framework for visual exploratory data analysis of large data sets
  - 依赖luma.gl、probe.gl
  - Use deck.gl layers as custom mapbox-gl-js layers
    - mapbox扩展模块依赖mapbox-gl.v2

- kepler.gl /9kStar/MIT/202210/ts
  - https://github.com/keplergl/kepler.gl
  - http://kepler.gl/
  - a data-agnostic, high-performance web-based application for visual exploration of large-scale geolocation data sets
  - Built on top of Mapbox GL and deck.gl, kepler.gl can render millions of points
  - 依赖deck.gl、mapbox、redux-toolkit、turf、d3、pbf、react-map-gl(依赖mapbox-gl.v2)、react-vis、supercluster

- streetscape.gl /573Star/MIT/202005
  - https://github.com/uber/streetscape.gl
  - http://www.streetscape.gl/
  - a toolkit for visualizing autonomous and robotics data in the XVIZ protocol. 
  - built on top of React and Uber’s WebGL-powered visualization frameworks
- https://github.com/Harmoware/Harmoware-VIS
  - Spatial-Temporal Visualization Library using Deck. GL

- spritejs /4.5kStar/MIT/202105/js/inactive/周边项目都没有更新了
  - https://github.com/spritejs/spritejs
  - https://spritejs.org/#/zh-cn/index
  - 依赖 gl-matrix、sprite-animator
  - OffscreenCanvas and Web Worker.
  - Work with d3.
  - It is renderer agnostic enabling the same api to render in multiple contexts: webgl2, webgl, and canvas2d.
  - Manipulate the sprites in canvas as you do with the DOM elements.
  - https://github.com/qcharts/core
    - https://github.com/spritejs/q-charts
    - 基于 spritejs 封装的图表库

- two.js /7.1kStar/MIT/202105/js
  - https://github.com/jonobr1/two.js
  - https://two.js.org/
  - A renderer agnostic two-dimensional drawing api for the web.
  - It is renderer agnostic enabling the same api to render in multiple contexts: webgl, canvas2d, and svg.
  - 依赖 Underscore.js(以前也依赖raf、@codemirror/next)
  - Focus on Vector Shapes: aims to make the creation and animation of flat shapes easier and more concise.
  - At its core two.js relies on a scenegraph.
    - This means that when you draw or create an object (a Two.Path or Two.Group), two actually stores and remembers that. 
  - Two.js has a built in animation loop. 
  - Two.js features a Scalable Vector Graphics Interpreter
# gl-utils
- luma.gl /1.7kStar/MIT/202009
  - https://github.com/visgl/luma.gl
  - https://luma.gl/
  - High-performance Toolkit for WebGL-based Data Visualization
  - While generic enough to be used for general 3D rendering, luma.gl's mandate(指令、契约) is primarily to support GPU needs of data visualization frameworks in the vis.gl suite
# threejs
- https://github.com/mrdoob/three.js
  - /63.7kStar/MIT/202009/js
  - The aim of the project is to create an easy to use, lightweight, cross-browser, general purpose 3D library. 
  - The current builds only include a WebGL renderer but WebGPU (experimental), SVG and CSS3D renderers are also available as addons.

- https://github.com/RenaudRohlinger/three-material-editor
  - https://z59h4.csb.app/
  - A GLSL editor for Threejs materials. 
  - Automatically detect the WebGL programs and provide live edit for the shaders. 
  - Easily edit the materials in your beautifully crafted threejs scene. Compatible vanilla and react.
# webgl-animation
- https://github.com/scottstensland/webgl-3d-animation
  - An interactive 3D animation using WebGL to depict a 2D predator prey ecology on a grid real-time mapped onto the surface of a 3D torus. 
# examples
- https://github.com/swift502/Sketchbook
  - https://jblaha.art/sketchbook/latest
  - 3D playground built on three.js and cannon.js
# webgl-canvas-interoperable
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

- https://github.com/pixijs/pixijs
  - PixiJS is a rendering library that will allow you to create rich, interactive graphics and cross-platform applications and games without having to dive into the WebGL API or deal with browser and device compatibility.
  - PixiJS has full WebGL support and seamlessly falls back to HTML5's canvas if needed.
# webgpu
- https://gitlab.com/unconed/use.gpu
  - https://usegpu.live/
  - Use. GPU / Live - react-without-react for WebGPU
# more-repos
