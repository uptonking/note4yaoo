---
title: web-latest-industry
tags: [latest, web]
created: '2021-01-01T20:52:04.258Z'
modified: '2021-01-01T20:52:42.088Z'
---

# web-latest-industry

# guide

- watching
  - render
  - 华为鸿蒙os的app开发基于js

- new
  - react server components
  - lowcode/nocode
  - webpack module federation
  - faas

- still
  - 小程序
  - hybrid
  - flutter
  - 微服务
  - serverless
  - webrtc
  - browser as os, pwa

- engineering
  - 前后端一体化/BFF：blitz, redwood

- css
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

- ## [Serverless 能取代微服务吗？](https://www.zhihu.com/question/335301678/answers/updated)
- serverless是一种概念，serverless的目的是让开发者能更专注于逻辑的开发。
  - 云函数是一种可以直接使用的工具。也可以说是 serverless 的一种实现方式（虽然并不完美）
  - 云函数可以用来直接跑主要业务服务吗？看云商的支持力度。
- 微服务是分布式架构, 服务是网状 p2p 通讯, 是比较底层的概念.
  - 云函数是具体实现, 强调 轻量级服务+ serverless(弹性调用), 云函数必然是微服务架构, 而且是 弹性微服务容器架构, 已经是一种 saas 产品形态了.
  - 历史经验告诉我们, 场景复杂了, 就没有万能的架构, 总是要根据实际情况做取舍.
  - 应用领域有很多复杂的状态问题, 应用冷启动, jit, 状态迁移, 缓存, session , 都制约了应用的弹性
  - serverless目前是云厂商售卖的概念。需要解决的体验问题很多。

- ## [2020 国内公司前端团队都在搞些什么?](https://www.zhihu.com/question/398940598/answers/updated)
- 我的前端工程化突破点是 webpack5 的 module federation
- 得物作为最近两年的黑马，前端团队也在不断探索新的技术疆域：
  - “no code”、“low code”、“数据可视化”、“前端微服务”、“设计素材中心”、“性能异常监控”、“动画库”、“可视化埋点”、“一站式服务”、“组件 Hub”、“H5 游戏”、“Mock Server”、“前端质量诊断系统”、“BFF”、“前端行为回放”
- 2020年前端团队的新挑战和方向
  - H5(HTML5)+ 原生 ( Cordova、 Ionic、微信小程序)
  - Javascript 开发 + 原生渲染 ( React Native、Weex、快应用)
  - 自绘 U+ 原生 ( QT Mobile、 Flutter)
  - uniApp / Taro
