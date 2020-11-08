---
title: latest-js-web
tags: [js, latest]
created: '2019-10-15T12:20:05.196Z'
modified: '2020-09-26T12:52:33.493Z'
---

# latest-js-web

- To make vanillajs great again

## dilemma

- [是否应该在production里使用typescript的decorator？](https://www.zhihu.com/question/404724504)
  - decorator提案到现在为止已有三版草案，尤其第三版是对前两版的推倒重来
  - 前两版是类似于 python decorator 的语义，第三版是静态语义，类似于弱化的宏
  - 但是这三版都无法推进到 stage 3（主要的障碍来自于引擎厂商）
  - 现在TypeScript所实现的 decorator，基于第一版的草案
    - 现在TS团队拒绝投入精力到与 decorator 相关的任何改进。
    - Vue 3放弃了class component而转向 composition API，也有部分原因源于 decorator 前景不明
  - [TypeScript装饰器(Decorators)具体做了什么工作）](https://www.zhihu.com/question/68257128)
    - Angular使用的根本不是装饰器（Decorator），而是注解（Annotation）
    - 装饰器的定位是通过对应的装饰函数，修改内容本身的定义，从而实现不同的行为。
    - 而注解并不产生任何行为，仅仅添加附加内容，需要相应的Scanner读取并识别其中的内容，从而使得Scanner自身产生不同的行为。
    - Angular是通过装饰器来模拟了注解的功能

## latest-web

- jspm
  - jspm provides a module CDN allowing any package from npm to be directly loaded in the browser and other JS environments as a fully optimized native JavaScript module.
  - esm是未来的趋势，随着http3（quic）普及，或许web应用将脱离打包工具和node_modules ”黑洞“。
    - Vite 以及 snowpack 在开发者模式是用的就是浏览器原生ESM语法，体验相当的棒。
    - 以及之前大家喊“学不动”的 Deno 也表示拥抱 ESMA，这是前端开发者对统一标准的需要。
    - jspm.io 试图将npm的生态搬到浏览器环境，类似的还有 skypack.dev 以及 esm.sh ，以及unpkg也在实验性提供对esm的支持。

``` html
<script type="module">
  // Statically:
  import babel from 'https://jspm.dev/@babel/core';
  console.log(babel);

  // Dynamically:
  (async () => {
    console.log(await import('//jspm.dev/lodash@4/clone'));
  })();
</script>
```

- [2020年前端最火的技术是什么](https://www.zhihu.com/question/365588457/answers/updated)
- As browsers are adding support for debugging the CSSOM, there should be no need to resort to slower DOM-based solutions.
- Right now, bundling JS is required for loading performance, but practically kills caching...
  - WebBundles will enable us to have both!! 

## ui-framework

- 最新的web components和stencil再等等看，思路是framework as compiler
  - web components本身使用浏览器标准的runtime，特别适合替代vue/react的runtime
  - web components难以替代其他框架，因为这些框架的目标不止浏览器环境，还支持native、ssr
  - 在其他框架中使用w-c组件，无需w-c框架层的依赖，这是通用组件重要的优势
  - 但在w-c中使用其他框架组件，则需组件源码加上框架runtime的依赖，并且每次导入组件都会导入一次框架层的依赖
  - stencil vs svelte
    - stencil编译到w-c，svelte还能编译到framework-less的纯js
    - stencil组件基于vdom，svelte组件会编译到js代码
    - stencil的状态管理更类似react
    - stencil的dom模版使用jsx，svelte使用的是自定义指令
    - svelte暂不支持ts
    - stencil的css基于shadow dom，且写在单读文件，svelte的css写在style块

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

- 微前端
  - 阿里乾坤，目的是解决遗留应用的管理问题
    - 基于single-spa，具备js沙箱、样式隔离、HTML Loader、预加载 等微前端系统所需的能力
    - qiankun可以用于任意js框架，微应用接入像嵌入一个iframe系统一样简单。
    - qiankun 2.0带来的最大变化便是定位将由 微前端框架 转变为 微应用加载器。
- 低代码平台
  - 阿里、百度都在研发，如百度开源的AMIS、阿里formily
- 编辑器解决方案参考
  - 文本编辑器：slate、editor
  - 拖拽搭建：craft.js、react-page
  - 产品搭建：react-chart-builder、amCharts-editor、alibaba-formily-editor
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
