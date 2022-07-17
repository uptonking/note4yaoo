---
title: note-react-extensions
tags: [extensions, react]
created: 2020-11-07T17:57:09.108Z
modified: 2020-11-19T12:44:05.442Z
---

# note-react-extensions

# react-renderer

- https://github.com/pmndrs/react-three-fiber
  - a React renderer for threejs on the web and react-native.
  - Everything that works in threejs will work here.

- https://github.com/diegomura/react-pdf
  - React renderer for creating PDF files on the browser and server
  - This package is used to create PDFs using React. 
    - If you wish to display existing PDFs, you may be looking for https://github.com/wojtekmaj/react-pdf

- https://github.com/ReactUnity/core
  - https://reactunity.github.io/
  - React renderer for building user interfaces in Unity UI
  - React Unity is a way to build interactive UI in Unity3D using React.
  - It can be used together with packages like Typescript, redux, i18next, react-router and more. 
  - It also supports a subset of CSS features and Flex layout system.

- https://github.com/raphamorim/react-ape
  - a react renderer to build UI interfaces using canvas/WebGL. 
  - React Ape was built to be an optional React-TV renderer. 
  - It's mainly a renderer focused on creating things for TV, PS4, Nintendo Switch, PS Vita, PS3 and low memory devices.
  - https://github.com/raphamorim/react-tv
    - deprecated for react-ape

- https://github.com/clayrisser/react-ast
  - render abstract syntax trees with react
  - React AST is the ultimate meta programming tool that uses react to render abstract syntax trees. 
  - It can be used to build powerful unopinionated code generators and babel plugins that are easy to read and can scale without creating a rats nest of unreadable code.

 

- https://github.com/react-figma/react-figma
  - A React renderer for Figma. 
  - Use React components as a source for your designs.
  - Compatible with react-native, react-sketchapp, react-primitives API.
- https://github.com/airbnb/react-sketchapp
  - render React components to Sketch; tailor-made for design systems

- https://github.com/nitin42/Making-a-custom-React-renderer
  - a small tutorial on how to build your custom React renderer and render the components to the host environment you need. 

# starter-boilerplate

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
