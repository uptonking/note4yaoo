---
title: toc-devtools-webpack
tags: [bundler, compiler, devtools, toc, webpack]
created: 2023-12-26T19:10:24.000Z
modified: 2023-12-26T19:10:48.719Z
---

# toc-devtools-webpack

# guide

# popular

# bundler

- https://github.com/unjs/unbuild /MIT/202411/ts
  - A unified JavaScript build system
  - rollup based bundler that supports typescript and generates commonjs and module formats + type declarations
  - Automagically infer build config and entries from package.json.

- https://github.com/godaddy/radpack /MIT/202312/js
  - Radpack fuses the best of both worlds by taking advantage of build-time bundling, with graph-based run-time loading to prevent wasteful waterfalls.
  - Bundlers like Webpack do a great job at providing a toolset needed to deliver an optimal out-of-the-box delivery solution for your end-users. 
  - Most loaders on the other hand, are focused on delivering only the requested assets, as they are needed. 
  - Radpack fuses the best of both worlds by taking advantage of build-time bundling, with graph-based run-time loading.

## webpack-powered

- https://github.com/KidkArolis/jetpack
  - Replaced webpack with rspack in jetpack@3.0.0-0 

## webpack-rewrite

- https://github.com/hardfist/unpack /202410/rust
  - ⚖️ Unplugin API built on top of Webpack architecture
  - Unpack is a miniature model of the bundler, intended to teach the structure of the real bundler.
  - Crafting Bundler builds Unplugin API on top of Webpack architecture.
  - This is the repo used for the in-progress book "Crafting Bundler". It contains the markdown text of the book, full implementation of bundler(unpack).
  - Inspired by https://github.com/sandersn/mini-typescript and https://github.com/codecrafters-io/build-your-own-x and https://github.com/munificent/craftinginterpreters/tree/master
  - literally writing a mini rspack bundler implementation... as a way to teach and reference bundler design. "will contain 1/10th the functionality of rspack"

- https://github.com/JinJieTan/mini-webpack /201909/js
  - 本文会先介绍webpack的打包流程，运行原理，然后去实现一个简单的webpack
  - 识别入口文件，逐级递归识别依赖，构建依赖图谱，将代码转化成AST抽象语法树，把AST抽象语法树变成浏览器可以识别的代码， 然后输出

- https://github.com/romanticu/simple_webpack /201904/js
  - [理解webpack原理，手写一个100行的webpack - 知乎](https://zhuanlan.zhihu.com/p/58151131)

- https://github.com/yangyfeng/mypack /202012/js
  - 0、读取webpack.config.js
  - 1、解析文件依赖
  - 2、替换require为__webpack_require__
  - 3、本地使用{}存储所有的文件，然后通过使用为__webpack_require__获取文件内容，执行函数方式为eval的包裹代码字符串

- https://github.com/kakoc/myox_js_bundler /202012/rust/inactive
  - Let's implement JS bundler from scratch with Rust step by step
  - [MYOX: Javascript bundler](https://kakoc.blog/blog/myox-js-bundler/)

- https://github.com/goto-bus-stop/prototype-rs /201806/rust/inactive
  - A basic JS bundler in Rust, using esprit and node-resolve.
  - It's a bit similar to browserify but without all the features.
  - 不支持async

- https://github.com/Censkh/Maxwell /201708/rust/inactive
  - JS minifier and (soon to be) bundler. To compete with Webpack. WIP
  - The goal is to transform Javascript source files into a browser compatible format (Babel.js), minify them (uglify.js) and then bundle them for optimized use in the browser

- webpack
  - https://github.com/dykily/simple_webpack /201904/js
  - https://github.com/gracehui88/HMR
  - https://github.com/pmmmwh/react-refresh-webpack-plugin
- https://github.com/jgraph/drawio
  - online diagramming tool
- https://github.com/evolus/pencil
  - tool for making diagrams and GUI prototyping

- https://github.com/ramselgonzalez/bundler /js
  - A small bundler to service personal projects as an alternative to industry bundlers such as Webpack, Rollup, etc.
  - This was an experiment to better understand what the frontend ecosystem is built on top of.
  - parsed my source code into a single file. 
  - This was built using espree for AST generation, estraverse for AST traversal and editing, and a fork of escodegen for rebuilding the AST into javascript.

- https://github.com/matanbroner/JS-Bundler /rust
  - A project to learn Rust while also learning to build a Javascript bundler
  - Currently performs a "webpack" style bundling process that condenses all modules into a single file

- https://github.com/rmanoka/webundle /archived
  - Web bundler written in Rust
# loaders
- https://github.com/Epimodev/svg-sprite-html-webpack /202301/js/inactive
  - Webpack loader and plugin to generate a SVG sprite with `<symbol>` elements and inject it in html built by `html-webpack-plugin`
# plugins
- https://github.com/unjs/unplugin /ts
  - Unified plugin system for Vite, Rollup, Webpack, esbuild, and more
  - very high level to adapt plugins to bundlers
  - parsing/transforming is still babel
# more
