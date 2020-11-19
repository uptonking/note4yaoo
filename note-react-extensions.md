---
title: note-react-extensions
tags: [extensions, react]
created: '2020-11-07T17:57:09.108Z'
modified: '2020-11-19T12:44:05.442Z'
---

# note-react-extensions

## quick-dev

- create-react-app creates apps with one command and no build config
  - React, JSX, ES6(最新语法), TypeScript and Flow syntax support.
  - Autoprefixed CSS
  - A fast interactive unit test runner 
  - A live development server(使用的是webpack-dev-server)
  - A build script to bundle JS, CSS, and images for production
  - An offline-first service worker and a web app manifest for PWA
- dva是基于redux、redux-saga和react-router的轻量级前端框架，偏数据流
  - dva: react + redux + redux-saga + react-router + 其他
  - 相比于cra多了内置的redux、redux-saga、react-router
  - 仅有6个api(但有很多约定)
  - app = dva(opts)
  - app.use(hooks)
  - app.model(model)
  - app.unmodel(namespace)
  - app.replaceModel(model)
  - app.router(({ history, app }) => RouterConfig)
  - app.start(selector?)
- umi是插件化的企业级前端应用框架，偏构建工具，但支持很多插件引入框架
  - umi: react-router + webpack + babel
  - 内置了路由、构建、部署、测试等
