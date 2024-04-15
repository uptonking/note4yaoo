---
title: toc-devtools-webpack
tags: [bundler, compiler, devtools, toc, webpack]
created: 2023-12-26T19:10:24.000Z
modified: 2023-12-26T19:10:48.719Z
---

# toc-devtools-webpack

# guide

# popular

# plugins

- https://github.com/godaddy/radpack /js
  - Radpack fuses the best of both worlds by taking advantage of build-time bundling, with graph-based run-time loading to prevent wasteful waterfalls.

## webpack-rewrite

- https://github.com/JinJieTan/mini-webpack
  - 本文会先介绍webpack的打包流程，运行原理，然后去实现一个简单的webpack

- https://github.com/yangyfeng/mypack
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
  - https://github.com/dykily/simple_webpack /js
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
# used-loaders
- https://github.com/Epimodev/svg-sprite-html-webpack /202301/js/inactive
  - Webpack loader and plugin to generate a SVG sprite with `<symbol>` elements and inject it in html built by `html-webpack-plugin`
# used-plugins

# more
