---
title: web-latest-trending
tags: [latest, web]
created: '2021-01-01T20:52:04.258Z'
modified: '2021-01-01T20:52:42.088Z'
---

# web-latest-trending

# guide
- watching
  - ssr
  - cjs to esm
  - ~~renderer using sika like flutter~~
  - 华为鸿蒙os的app开发基于js
  - [Technology Preview: Jetpack Compose for Web](https://blog.jetbrains.com/kotlin/2021/05/technology-preview-jetpack-compose-for-web/)
# topics
- viewpoints
  - Payments are moving from batch processing to realtime processing. this changes everything

- new-infra
  - webpack module federation
    - deno url import
  - faas/serverless
  - esbuild/vite bundler

- new-framework-app
  - react server components
  - component story format
  - lowcode/nocode

- hot-now
  - 小程序
  - hybrid
  - flutter
  - 微服务
  - serverless
  - webrtc
  - browser as os, pwa

- engineering
  - 前后端一体化/BFF：blitz, redwood

- animation
  - web animations api

- css
  - CSS Painting API／CSS Layout API／CSS Typed OM
  - css typed om
    - firefox和safari均不支持(202001)
  - css in js依然活跃

- js
  - webgl > webgpu
  - v8 > wasm

- web components
  - react + hooks

- classic
  - viz
  - animation
  - gaming
  - auto testing/monitoring
    - puppeteer
  - compiler

- more
  - WebGL 2
  - Push Notifications
  - anything based on Worklets
  - WebRTC
  - WebP/VP8/VP9
  - WebXR
  - CSS Typed OM
  - Offscreen Canvas
  - ImageBitmap (quickly draw programmatically created images)
  - CSS Typed OM (fast CSS updates from JS)
  - requestIdleCallback
  - ResizeObserver
  - scroll-snap
  - :focus-within
  - new media query options (OS settings personalization)
  - logical properties (block & inline)
  - Sticky Situations
  - backdrop-filter
  - :is()
  - FlexBox gap
  - Houdini
  - Custom properties
  - Paint API
  - Animation Worklet

- ios-missing
  - No Service Worker
  - Can't print or save as PDF
  - No support for GetUserMedia
  - Web Push Notifications (ZOMFG)
  - Audio Worklet
  - Custom Paint
  - Web Animations API
  - Pointer Events
  - CSS Typed OM
  - Web Bluetooth
# products
- natto
  - https://natto.dev/
  - a canvas for JavaScript
# discuss
- ## techs to look out for in the javascript world in 2021
- https://twitter.com/KerryRitter/status/1344039489123934209
  - @stenciljs - web components compiler
  - @tailwindcss - design system toolkit
  - @rustlang - language for wasm
  - @nestframework - 2020s fastest rising framework
  - @deno_land - new JS/TS runtime
- Tanner Linsley 2021 Goals
  - XState
  - Serverless
  - Improve @nozzleio sales
  - 2 years worth of @nozzleio updates
  - React Query Essentials v3
  - React Table v8 (TS rewrite)
  - React Table Essentials
  - React Table/Grid Pro
  - Hopes: Physically attend a JS/React conference
  - There's a good chance this year that I will reimplement React-Charts with airbnb/visx
    - and a slightly smaller chance that React Charts goes away all together.
    - I need more chart types @nozzleio, and not enough time to build essentially what visx has already built.

- ## [Web development and designing trends in 2021](https://twitter.com/Prathkum/status/1347779080259715073)
  - Progressive Web Apps
  - Single Page Websites
  - Accelerated Mobile Pages
  - Voice-Enabled eCommerce apps
  - API-first development
  - Parallax animation
  - Glass and Neumorphism
    - 也称为soft ui，是一种类似于浮雕的效果，有的人说这是新的拟物风格（New Skeuomorphism）
  - Abstract art compositions
  - 3D visuals

- ## [My bold two-year prediction](https://twitter.com/tylerlwsmith/status/1346282659484323841): 
  - 2021 will be the peak of JavaScript frameworks & compilers. 
  - In 2022, tools like Turbo, Laravel Livewire, . NET Blazor Pages and Alpine JS that allow interactivity with little custom JavaScript will become serious alternatives to React & friends.
  - Developers gravitate towards tools that let them build things fast, even if it means letting go of some control. 
    - Bootstrap and Tailwind caught on because they let developers build real apps without tediously writing their own CSS.
    - The same thing will happen to JavaScript.
  - Modern JavaScript is complicated. 
    - Webpack is a challenge for even experienced JS developers.
    - Tools like Create React App ease this pain, but they can force you to put your JS app in a different repo & on a different server, complicating development & deployment.
  - JavaScript is a challenging language. 
    - The "this" keyword, functions vs arrow functions, prototypical inheritance, bind vs call, and immediately-invoked function expressions can be hard to understand.
    - Developers coming from other languages would often rather not learn these.
  - JavaScript's ecosystem has an overwhelming number of choices.
    - React? Vue? Ember? Angular? Svelte?
    - Styled Components? CSS Modules? Emotion?
    - Redux? MobX? XState?
    - JavaScript fatigue can kick in before you write a single line of code. This slows down development.
  - I believe developers will begin to recognize the productivity benefits of writing less custom JavaScript, 
    - and developers with no JavaScript experience will be able to create meaningful interactive/real time web applications.
  - If you are a JavaScript developer and this sounds scary, let me reassure you: there will always be work for JavaScript developers. 
    - However, the tent of web development will become much bigger.
    - Here's to a democratized web

- ## [Serverless能取代微服务吗？](https://www.zhihu.com/question/335301678/answers/updated)
- serverless是一种概念，serverless的目的是让开发者能更专注于逻辑的开发。
  - 云函数是一种可以直接使用的工具。也可以说是 serverless 的一种实现方式（虽然并不完美）
  - 云函数可以用来直接跑主要业务服务吗？看云商的支持力度。
- 微服务是分布式架构, 服务是网状 p2p 通讯, 是比较底层的概念.
  - 云函数是具体实现, 强调 轻量级服务+ serverless(弹性调用), 云函数必然是微服务架构, 而且是 弹性微服务容器架构, 已经是一种 saas 产品形态了.
  - 历史经验告诉我们, 场景复杂了, 就没有万能的架构, 总是要根据实际情况做取舍.
  - 应用领域有很多复杂的状态问题, 应用冷启动, jit, 状态迁移, 缓存, session , 都制约了应用的弹性
  - serverless目前是云厂商售卖的概念。需要解决的体验问题很多。

- ## [2020年国内公司前端团队都在搞些什么?](https://www.zhihu.com/question/398940598/answers/updated)
- 我的前端工程化突破点是 webpack5 的 module federation
- 得物作为最近两年的黑马，前端团队也在不断探索新的技术疆域：
  - “no code”、“low code”、“数据可视化”、“前端微服务”、“设计素材中心”、“性能异常监控”、“动画库”、“可视化埋点”、“一站式服务”、“组件 Hub”、“H5 游戏”、“Mock Server”、“前端质量诊断系统”、“BFF”、“前端行为回放”
- 2020年前端团队的新挑战和方向
  - H5(HTML5)+ 原生 ( Cordova、 Ionic、微信小程序)
  - Javascript 开发 + 原生渲染 ( React Native、Weex、快应用)
  - 自绘 U+ 原生 ( QT Mobile、 Flutter)
  - uniApp / Taro
