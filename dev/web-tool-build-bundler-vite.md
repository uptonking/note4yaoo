---
title: web-tool-build-bundler-vite
tags: [bundler, tool, vite, web]
created: 2021-01-10T16:18:22.283Z
modified: 2021-01-10T16:24:19.787Z
---

# web-tool-build-bundler-vite

# guide

# discuss

 

- ## 

- ## 

- ## 

- ## [聊一聊Vite - 掘金 _202208](https://juejin.cn/post/7137873906748096525)
- Vite 相较于传统的 Webpack、Rollup 的编译方式，采用的是 ESM 混合编译。即在开发环境，使用 Server 动态编译 + 浏览器的 ESM ，实现了开发环境 “0编译”。在生产环境时，采用了 Rollup 进行打包编译。
- Vite 以原生 ESM 方式服务源码，当 import 模块时，浏览器通过 http 请求下载导入的模块。启动开发服务器，代码执行到页面对应的模块时自动请求模块文件，实现自动按需加载。
  - 不需要打包过程
  - 自动按需处理
  - 可利用浏览器缓存
  - 可实现高效的热更新
- 什么是依赖预构建？
- vite将代码分为两部分：
  - 依赖：例如react、antd，纯JS在开发中不会变动的部分
  - 源码：业务代码，非纯JS代码（需要转换JSX/LESS）并不是所有都需要被加载，开发时经常变化
  - 在首次启动 Vite 时，会使用 Esbuild 将依赖重新构建一遍并缓存在 node_modules。
  - 构建的依赖缓存到 node_modules/.vite，解析后的依赖会设置 HTTP 头 max-age=31536000, immutable进行强缓存

- Vite 3.0 在冷启动阶段进行了优化。
  - 3.0 通过延迟预构建的过程来实现，当浏览器请求第三方依赖时， dev server 会将首屏期间所有涉及到的所有模块依赖关系全部解析完后，才给浏览器发送 response。因此，如果发现有未预构建的第三方依赖，这个第三方依赖的请求会阻塞直到预构建完成。本质上是通过消耗首屏性能交换 reload 交互体验。

- Vite 的缺点
- 首屏性能
  - Vite 把 Webpack 的 dev Server 启动过程中完成的工作放在了 dev server 和响应浏览器请求中，不过即使额外做了这些工作，首屏渲染时间相较于 Webpack 的构建时间依旧有着极大的优势
- Dev 和生产不一致
  - Vite 在开发环境使用 Esbuild 对代码进行构建，但是生产环境使用的却是 Rollup。
  - Esbuild 在以下几个场景难以处理： 自动 CSS 代码分割, 对异步懒加载请求自动优化, 手动的代码分割控制
  - 生产环境依赖处理规则和开发环境一致，也使用 Esbuild 进行打包，目前该 feature 已经实现，并且在 Vite 3.0 版本作为一个实验性功能上线，可以通过添加optimizeDeps.disabled: false 配置开启。

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
