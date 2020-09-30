---
title: latest-js-web
tags: [js, latest]
created: '2019-10-15T12:20:05.196Z'
modified: '2020-09-26T12:52:33.493Z'
---

# latest-js-web

## ui-framework

### react

- defaultProps可能废除 https://github.com/reactjs/rfcs/pull/107
- swr基于hooks的请求库，设计思想是stale-while-revalidate，先用缓存再请求
- https://github.com/mohebifar/vidact
  - /671Star/MIT/202004
  - Vidact compiles your React source codes to VanillaJS code with No Virtual DOM
  - It is similar to Svelte, but unlike Svelte, Vidact does not introduce a new syntax. 
  - It takes in pure React-compatible JavaScript (JSX) and outputs plain JavaScript.
  - Vidact is a babel-plugin that scans your source code to find what parts of the UI need to be updated in response to a prop or state change and generates a plain JavaScript code that should have the same DOM result as the equivalent React code. 
  - Note that all of this is done in build time! Whereas React does the bulk of its work in runtime in the browser by leveraging Virtual DOMs to determine what needs to be updated in the actual DOM.
- https://github.com/sokra/rawact
  - /2.5kStar/MIT/201812
  - A babel plugin which compiles React.js components into native DOM instructions to eliminate the need for the react library at runtime.
- webcomponents的看法
  - web-component本身就是一个 runtime，特别适合替代 vue/react runtime
  - web components很可能无法替代其他框架，因为这些框架的目标不止浏览器环境，还支持native、ssr


- htm
  - Hyperscript Tagged Markup: JSX alternative using standard tagged templates, with compiler support
  - 使用标签模版字符串取代jsx

- Hermes JS Engine /201907
  - a new js engine optimized for running React Native on Android
  - JavaScriptCore最初是为桌面浏览器端设计，相较于桌面端，移动端能力有太多的限制，为了能从底层对移动端进行性能优化，Facebook团队选择自建JavaScrip引擎，设计了Hermes，限于iOS AppStore审核限制，目前仅用于Android平台
  - 在移动应用开发中，首次加载启动、内存大小和应用大小都是衡量应用好坏的重要指标
  - Hermes现在并没有JIT编译器
  - Hermes编译的字节码文件比纯文本js文件增大100%

## engineering

- 低代码平台
  - 阿里、百度都在研发
- vite
  - [如何看待 Web 开发构建工具 Vite？](https://www.zhihu.com/question/394062839/answers/updated)
    - vite不需要打包工具参与，利用浏览器对模块化的支持，实现vue的热更新
    - 利用 `<script type='module'>`
    - vite vs snowpack
      - Vite handles both dev and bundle in the same package, using Rollup. 
      - Snowpack delegates to plugins using webpack/parcel.
      - The advantage is that Vite produces smaller bundles and makes it easier for plugins to tweak dev and build at the same time.

- tree shaking
  - Tree shaking is a term commonly used in the JavaScript context for dead-code elimination. 
  - It relies on the static structure of ES2015 module syntax, i.e. import and export
  - example

``` js
  import * as Foo from './foo'; // namespace import
  import { bar, bar2, bar3 } from './foo'; // named import
```

  - with a modern webpack setup, the two will generate the same compiled/transpiled JS
  - ref
    - https://medium.com/unsplash/named-namespace-imports-7345212bbffb
