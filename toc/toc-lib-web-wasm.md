---
title: toc-lib-web-wasm
tags: [toc, wasm, web, webassembly]
created: 2020-12-31T15:18:36.947Z
modified: 2020-12-31T15:19:37.542Z
---

# toc-lib-web-wasm

# js

- https://github.com/TheLartians/modern-wasm-starter
  - A starter template to easily create WebAssembly packages for npm using type-safe C++ code with automatic declarations. 

- https://github.com/finos/perspective
  - /3.1kStar/Apache2/202012/js/cpp
  - https://perspective.finos.org/
  - https://perspective.finos.org/docs/md/development.html
  - Streaming pivot visualization via WebAssembly
  - Perspective is an interactive visualization component for large, real-time datasets
    - Perspective makes it simple to build real-time & user configurable analytics entirely in the browser, or in concert with Python and/or Jupyterlab. 
    - Use it to create reports, dashboards, notebooks and applications, with static data or streaming updates via Apache Arrow.
  - A fast, memory efficient streaming query engine, written in C++ and compiled to WebAssembly, with read/write/stream support for Apache Arrow.
  - A framework-agnostic query configuration UI component, based on Web Components, and a WebWorker and/or WebSocket data engine host for stable interactivity at high frequency.
  - A customizable HTML Data Grid plugin, and a Chart plugin built on D3FC.
  - Integration with Jupyterlab, both natively in a Python kernel, and as a notebook Widget.
  - Cross-language streaming and/or virtualization to the browser via Apache Arrow.
  - Runtimes for the browser, Node.js, and Python.
  - Perspective uses both WebAssembly and Web Workers, each of which place constraints on how assets and scripts must be loaded
  - @finos/perspective modules has an additional, unmanaged dependency—the Emscripten compiler, 
    - which is used to compile the core C++ engine to WebAssembly, and must be installed independently.
- https://github.com/lume/glas
  - WebGL in WebAssembly with AssemblyScript.
  - This is a work-in-progress port of Three.js, a JavaScript 3D WebGL library, to AssemblyScript.

- https://github.com/ffmpegwasm/ffmpeg.wasm
  - FFmpeg for browser and node, powered by WebAssembly
- https://github.com/evgeny-nadymov/telegram-react
  - Experimental Telegram web client with tdlib, webassembly and react js under the hood
- https://github.com/jtenner/as-pect
  - fast testing with AssemblyScript
# cpp
- https://github.com/mbasso/asm-dom
  - A minimal WebAssembly virtual DOM to build C++ SPA (Single page applications)
  - You can write an entire SPA in C++ 
    - and compile it to WebAssembly (or asmjs as fallback) using Emscripten, 
    - asm-dom will call DOM APIs for you.
- https://github.com/timhutton/opengl-canvas-wasm
  - example of animating the HTML5 canvas from C++ using OpenGL through WebAssembly

 

- https://github.com/rsms/markdown-wasm
  - Markdown parser and HTML generator implemented in WebAssembly, based on md4c
  - Very fast Markdown parser & HTML renderer implemented in WebAssembly
  - Zero dependencies (31 kB gzipped)
  - Portable & safe (WASM executes in isolated memory and can run almost anywhere)
  - Based on md4c — compliant to the CommonMark specification

- https://github.com/mosra/magnum
  - modular C++11/C++14 graphics middleware for games and data visualization
- https://github.com/emscripten-core/emscripten
  - Emscripten: An LLVM-to-WebAssembly Compiler
- https://github.com/faasm/faasm
  - High-performance stateful serverless runtime based on WebAssembly
- https://github.com/wwwg/wasmdec
  - WebAssembly to C decompiler
# rust
- https://github.com/yewstack/yew
  - https://yew.rs/
  - /14.4kStar/MIT|Apache2/202012/rust
  - Rust/Wasm framework for building client web apps
  - modern Rust framework for creating multi-threaded front-end web apps with WebAssembly.
- https://github.com/seed-rs/seed
  - Rust framework for creating fast and reliable web apps with an elm-like architecture.
- https://github.com/fitzgen/dodrio
  - A fast, bump-allocated virtual DOM library for Rust and WebAssembly.
- https://github.com/koute/stdweb
  - The goal of this crate is to provide Rust bindings to the Web APIs and to allow a high degree of interoperability between Rust and JavaScript.
- https://github.com/38/plotters
  - A rust drawing library for high quality data plotting for both WASM and native, statically and realtimely
# wasm-toolchain
- https://github.com/WebAssembly/wabt
  - The WebAssembly Binary Toolkit
- https://github.com/iodide-project/pyodide
  - The Python scientific stack, compiled to WebAssembly.
  - Pyodide brings the Python 3.8 runtime to the browser via WebAssembly, 
    - along with the Python scientific stack including NumPy, Pandas, Matplotlib, parts of SciPy, and NetworkX
  - Pyodide provides transparent conversion of objects between Javascript and Python. 
    - When used inside a browser, Python has full access to the Web APIs.
  - Pyodide goes beyond running in a notebook environment. 
    - Pyodide may be used standalone in any context where you want to run Python inside a web browser.
- https://github.com/ballercat/walt
  - JavaScript-like syntax for WebAssembly text format
# wasm-java
- https://github.com/i-net-software/JWebAssembly
  - Java bytecode to WebAssembly compiler
- https://github.com/wasmerio/wasmer-java
  - WebAssembly runtime for Java
- https://github.com/leaningtech/cheerpj-meta
  - CheerpJ - convert Java bytecode to WebAssembly and JavaScript
# wasm-examples
- https://github.com/WordPress/wordpress-playground
  - https://developer.wordpress.org/playground/
  - WordPress Playground is an experimental in-browser WordPress that runs without a PHP server thanks to the magic of WebAssembly.
# more
