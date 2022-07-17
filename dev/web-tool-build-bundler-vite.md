---
title: web-tool-build-bundler-vite
tags: [bundler, tool, vite, web]
created: 2021-01-10T16:18:22.283Z
modified: 2021-01-10T16:24:19.787Z
---

# web-tool-build-bundler-vite

# guide

# discuss

 

- ## Vite now supports glob imports  (think webpack context) 
- https://twitter.com/youyuxi/status/1348077806723485699
- https://github.com/kentcdodds/import-all.macro
  - A babel-macro that allows you to import all files that match a glob
  - It's relevant - the thing with Vite is that all built-in transforms are done without the need for full AST parses so it's super fast
- webpack has require.context but no import based equivalent. 
  - The glob syntax is a Vite-specific feature (and in fact a fairly straightforward transform)

- ## [如何看待 Web 开发构建工具 Vite？](https://www.zhihu.com/question/394062839/answers/updated)
- vite不需要打包工具参与，利用浏览器对模块化的支持，实现vue的热更新
- 利用 `<script type='module'>`
- vite vs snowpack
  - Vite handles both dev and bundle in the same package, using Rollup. 
  - Snowpack delegates to plugins using webpack/parcel.
  - The advantage is that Vite produces smaller bundles and makes it easier for plugins to tweak dev and build at the same time.
