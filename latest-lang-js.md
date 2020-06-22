---
tags: [js, latest/js]
title: latest-lang-js
created: '2019-10-15T12:20:05.196Z'
modified: '2020-06-22T13:16:27.627Z'
---

# latest-lang-js

- react
  - defaultProps可能废除 https://github.com/reactjs/rfcs/pull/107
  - swr基于hooks的请求库，设计思想是stale-while-revalidate，先用缓存再请求


- htm
  - Hyperscript Tagged Markup: JSX alternative using standard tagged templates, with compiler support
  - 使用标签模版字符串取代jsx

- 201907-Hermes JS Engine
  - a new js engine optimized for running React Native on Android
  - JavaScriptCore最初是为桌面浏览器端设计，相较于桌面端，移动端能力有太多的限制，为了能从底层对移动端进行性能优化，Facebook团队选择自建JavaScrip引擎，设计了Hermes，限于iOS AppStore审核限制，目前仅用于Android平台
  - 在移动应用开发中，首次加载启动、内存大小和应用大小都是衡量应用好坏的重要指标
  - Hermes现在并没有JIT编译器
  - Hermes编译的字节码文件比纯文本js文件增大100%


## solutions
- tree shaking
  - Tree shaking is a term commonly used in the JavaScript context for dead-code elimination. 
  - It relies on the static structure of ES2015 module syntax, i.e. import and export
  - example
  ```
  import * as Foo from './foo';             // namespace import
  import { bar, bar2, bar3 } from './foo';  // named import
  ```
  - with a modern webpack setup, the two will generate the same compiled/transpiled JS
  - ref
    - https://medium.com/unsplash/named-namespace-imports-7345212bbffb
