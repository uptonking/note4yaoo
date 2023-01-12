---
title: web-fwk-dev-solutions-frontend
tags: [framework, frontend, solutions, web]
created: 2020-11-01T09:48:26.955Z
modified: 2023-01-12T10:24:40.550Z
---

# web-fwk-dev-solutions-frontend

- 技术选型时，参考知名项目或大公司项目的选择

# faq-not-yet

- scrolling滚动时的样式
  - 不同浏览器的滚动条样式不一致
  - 难以实现sticky，滚动的是body还是div
  - 移动端地址栏显示与隐藏
- component-to-thumbnail-image
  - repng
- 中文字体体积大的问题
  - 静态网页可通过腾讯开源的font-spider删除字体库中未使用的字符数据
  - 动态中文web字体暂无解决方案
- css模块化方案选择的问题
  - 基于Shadow DOM标准的局部css尚未流行
  - 可以参考ant-design等大型项目的选择，直接使用css或scss
  - 要考虑如何将依赖的第三方样式集成到本项目，如何将本项目的样式提供给第三方用
  - 要考虑如何与具体框架结合，更方便实现国际化RTL、语言和样式主题切换
  - 考虑在特殊情况下如何覆盖组件的样式

# guide

- 选用现有框架，还是自己实现框架
  - 现有框架的生态系统若十分丰富，则就用现有框架
    - 如koa的架构虽比express更好，但用户太少，插件没有express丰富，恶性循环
    - 优秀的第三方库如redux会帮你处理伴随依赖的更新和修bug，不用自己花精力兼容concurrent mode
  - 自己的时间和精力有限
  - 知名框架一般有大公司或商业公司推广，小项目资源有限
  - react的挑战者需要：丰富功能、生态、大公司支持

# frontend-solutions

- 组件层 components
  - 要素：dom、样式、交互
  - i18n
  - theming
  - css样式及布局
  - icon
  - animation
  - drag-layout-events
  - layer
  - more
    - design-tokens
    - live-playground
    - starter

- 视图层 view layer
  - MVC/MVVM
  - VDOM结构
  - DOM更新及操作
  - 生命周期
  - 模版
    - ejs, pug, nunjucks, mustache, handlebars, swig, art, lodash template

- 状态管理 state management
  - single vs multi store
  - 发布订阅模式 vs 观察者模式
  - 优化：拆分合并，子树更新

- 路由管理 routing
  - dynamic routing
  - file based routing

- 网络请求
  - fetch
  - observable

- io
  - file-uploader
  - image-optimization

- ssr/universal/isomorphic
  - 核心优势：加快首屏显示、seo友好
  - 实例：next.js、razzle、beidou、react-server

- functional
  - React tries/trying to move towards functional programming more these days with the advent of hooks etc 
  - angular doesn't by default having components as classes. 

- extensions/middleware
  - log
  - cache
  - graphics
  - immutable
  - geo

- packages
  - ui
  - form
  - grid

- scaffolder
  - create-react-app
  - tutorials: counter, todo, data-fetching, realworld
  - books/online courses
  - showcase(made with fwk)
  - storybook, online demo
  - live docs

- tooling
  - devtools: hmr，flash-updates
  - ide: react-ide, spring-tools
  - cli
    - easy to create and develop starter project
  - framework playground
  - testing

- integration/wrapper
  - baas: firebase、LeanCloud、bomb
  - animations
  - charts
  - maps
  - material components
  - framework implementation of X/Carbon/Ant Design System
  - graph

- cross-platform/devices
  - deno
  - renderer for terminal/repl
  - react-native
  - electron
  - ar/vr

- community
  - site + github repo
  - official blog
  - documentation
  - catalog-list
  - experts on Twitter
  - changelog, roadmap
  - forum discussion posts, github issues, discord chats
  - meetup, conference, youtube  series

- more-frontend-dev
  - type safety
  - AOT编译
  - template
    - html模版, js in html element
  - 静态资源处理
    - webpack-loader
  - keyboard shortcuts

- 前后端一体化
  - 优点
    - 高效快速
  - 缺点
    - 若前后台耦合过多，如去掉api服务层，则难以支持不同的前端如android、ios

- JAMStack
  - 最适合一些内容更新不太频繁的网站（比如新闻、电商、文档）
  - 不适合Feeds流、聊天室、论坛、个性化推荐这样高度动态化的网站，以及邮箱、编辑器这样偏重型的Web应用。
  - 是类似WordPress建站
- tree-shaking
  - 各工具库的编译方式不同，webpack各版本支持程度不同
  - webpack v4不支持，v5支持

- [2020年的React Hooks生态](https://juejin.im/post/6861055676652158990)
  - router: react-router, hookrouter
  - state: redux, mobx, unstated-next, recoil, use-immer, dva
  - components: antd, sunflower
  - hooks封装: react-use, ahooks, huse, react-adaptive-hooks
  - css-in-js: emotion, useTheme
  - i18n: react-intl, react-i18next
  - animation: react-spring
  - request: swr, react-query

- [2020年前端最火的技术是什么](https://www.zhihu.com/question/365588457/answers/updated)
  - As browsers are adding support for debugging the CSSOM, there should be no need to resort to slower DOM-based solutions.
  - Right now, bundling JS is required for loading performance, but practically kills caching...
    - WebBundles will enable us to have both!! 

## [下一代前端框架会去解决什么问题？](https://www.zhihu.com/question/433673833)

- 试图小结已有框架解决的问题：
  - jQuery解决DOM操作，浏览器兼容性
  - Backbone 解决数据与视图的耦合
  - React/Vue/Angular 解决DOM操作及数据与视图的耦合
  - Apollo/Relay 解决API与数据的割据
  - RN/Flutter/Taro/Uniapp 解决安卓苹果小程序的分裂

- 个人认为，前端~api~后端~数据库，这个链条上的类型安全，是个方向
  - 这条路要把现在很多crud后端的饭碗抢一半
  - 这很重要但我并不觉得这是前端框架该做的。
    - 后端重要的还是接口，后端应该通过标准化的方式向前端发布带类型的接口，而后端到数据
    - 类型在兼容不同语言的接口这个问题实在太必要了
    - 库也应该用带类型的结构定义来对应起来。
    - 这样的后端不**仅仅是对接js前端，其他client也可以对接**；
    - 这样的前端不仅仅对接node后端，任何能生成标准接口的后端都可以对接；
    - 这样的后端也可以对接任何能做ORM的数据库；
    - 这些方案其实都已经比较现成了，缺的就是一个组织起来的bootstrap吧
- 未来的一个方向与是提供完善且优秀的前后端一体化方案，并通过 SSR/SSG/Serverless 等多种方式提升研发体验与用户体验。
  - 类似的产品有我们最近开源的 Midway Hooks/Next.js/Nuxt/Blitz/Redwood.js
  - 基础框架（Vue/React/Angular/Svelte...），解决如何更好编写代码的问题，包括效率、质量等
  - 上层框架（Next.js/Nuxt/Midway Hooks 等），解决好特定领域的问题。
    - 例如经典的 Next.js 解决的就是 SSR 的问题，并开始引领 JAMStack 概念
- Midway Hooks
  - 前后端一体化，支持 React/Vue，使用API比blitz要简单，支持通过hooks创建后端api。
  - （和blitz的理念不太一样。他们希望做大而全，我们希望专注于前后端一体化与hooks的开发体验）
  - 希望通过函数+hooks的方式，统一前后端的写法。提供自然的调用体验。在这种情况下，你调用接口和调用普通函数是一模一样的，context 则是通过hooks拿到的
- 前端目前的主要矛盾，主要聚焦于跨端矛盾和前后端的矛盾！
  - 众所周知，RN 的很多苹果安卓不一致，有些像当年IE与网景之争，最后屈服于chrome的一统江湖。
  - 苹果与安卓怕是无解了，所以跨端长时间有市场。
  - 小程序界比苹果安卓好多了，但 Taro 还有很大的改善空间，即期待下一代的小程序跨端技术方案；
- BFF架构 - 服务于前端的后端
  - 前后端联调不好说，怕一石惊起千层浪，但实践中，大前端已润物细无声。
  - 作为一名前端，乐意看到 Backend For Frontend 的技术方案百花齐放。
- MVVM把组件内的状态都把握到很完美的样子，Redux/Mobx把共享的状态管理
- Apollo把网络层、数据缓存也是风风火火（就是有些复杂的样子，类似Angular的复杂），所以期待这一块有下一代的搅局者。
- 一个是以移动端为主的跨端方案，目标是将体验无限接近native，并且可以低成本的在各种平台上跑起来，作为人与设备交互的窗口。
  - 目前比较火的是RN，flutter这种。
- 另一个是浏览器操作系统化，通过云计算，将越来越多的场景放到浏览器上。
  - 这种场景下前端的业务场景会越来越复杂，类似的应用像微软的office，云管控平台，IDE等。
  - 前端如何处理这种超大复杂业务的开发，将是一个越来越需要解决的问题。
  - 目前的方案主要是微前端，但是现有的方案还不是很完美。
- web是不是未来
  - web 没有未来，自然不存在下一代前端框架
  - 如果你说的这个前端不是单指 web，那么下一代前端框架肯定是往嵌入式，小而美发展
  - 我倒是觉得5g 乃至 xg 的出现会让各个端变成显示器，而不是处理器，而 web 技术实际上是开发界面最方便的技术。
- 更成熟的web特性
  - 第一，充分利用worker，现在的框架还是在浏览器的主线程中做所有事情，对于UI的渲染多多少少都会有影响，可能会把一部分的计算放入到worker当中进行，通过异步通信方式交互实现更少的对UI阻塞。
  - 第二，可能会出现使用wasm的框架，其实微软已经有这样的框架了能够实现C#在浏览器上跑，不过wasm不能处理UI，对于js语言的框架来说似乎没有必要，不过vDom用wasm来计算的话可能效率会更好，但是wasm的标准和普及率目前还不能让主流框架趋之若鹜。
  - 第三，时间切片，这个现在react已经在做实践了，这个概念其实就是cpu的多任务运行方式，无论是概念还是技术都是很成熟的，就是不知道实际应用效果如何了
  - 第四，利用gpu来加速框架运算实现，这个目前还没有什么框架去实现，必经大多数是UI应用，假如有一个处理数据的框架的话这个就会比较实用
