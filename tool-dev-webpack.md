---
title: tool-dev-webpack
tags: [tool, engineering, webpack]
created: '2020-11-20T19:29:35.880Z'
modified: '2020-11-20T19:30:56.804Z'
---

# tool-dev-webpack

## guide

- Webpack Incremental Builds
  - Use webpack's watch mode. Don't use other tools to watch your files and invoke webpack. 
  - The built-in watch mode will keep track of timestamps and passes this information to the compilation for cache invalidation.
  - In some setups, watching falls back to polling mode. 
    - With many watched files, this can cause a lot of CPU load. 
    - In these cases, you can increase the polling interval with watchOptions.poll.
  - 可实现类似ts project references的快速增量编译
  - The following utilities improve performance by compiling and serving assets in memory rather than writing to disk:
    - webpack-dev-server/webpack-hot-middleware/webpack-dev-middleware

## webpack-config

## webpack-dev-server

## webpack-extensions

- https://github.com/etsy/kevin-middleware
  - Kevin is an Express-style middleware that makes developing with Webpack in a monorepo a lot simpler. 
  - It's loosely based off of Webpack's dev middleware, and it is intended to be used as a replacement for it.
  - Using Webpack in development in a monorepo can be challenging because, by default, it will try to keep your entire JavaScript codebase in memory.
    - Kevin addresses this problem by allowing you to create separate Webpack configs for different parts of your codebase; 
    - it then manages these configs by having Webpack only watch and build relevant files.

## repos-monorepo

- https://github.com/carlosnakane/monorepo-react-webpack
  - /ts/基于tsc且无babel
  - configure a monorepo for a modular React App and use webpack to generate a single chunk for each package and lazy load them.
  - React, Webpack 4, yarn workspaces, Styled Components, TS
- https://github.com/dan-kez/lerna-webpack-example
  - /ts/基于babel
  - an example configuration for a monorepo using lerna
- https://github.com/rtivital/react-monorepo-starter
  - /js
  - all building and starting scripts run from root and share the same webpack configuration.
  - [Working with React in monorepository](https://dev.to/rtivital/working-with-react-in-monorepository-o0b)
- https://github.com/serhii-havrylenko/monorepo-babel-ts-lerna-starter
  - /ts/基于babel
- https://github.com/Hy-Vee/lerna-yarn-workspaces-monorepo
  - /js/

## ref

- [Cutting our webpack build times in half_201905](https://www.cargurus.dev/Cutting-our-webpack-build-time-in-half/)
  - We use yarn workspaces, and whats known as a mono-repo. 
  - Essentially our entire codebase is in one git repo, divided into npm packages that all resolve in a single filesystem. 
  - In the past developers had to compile the entire codebase when changes were made. 
  - We created our own webpack plugin that detects which files have changed and only recompile the bundles specific to what has changed. 
  - Our plugin is a lot like the Hard Source plugin, which you can use to do the same thing. 
  - By detecting what has changed, and only recompiling the changed files, we cut many of our builds from 7+ minutes to 30 seconds.
- [Developing in a Monorepo While Still Using Webpack: kevin-middleware_202004](https://codeascraft.com/2020/04/06/developing-in-a-monorepo-while-still-using-webpack/)
- [webpack扩展插件](https://www.timsrc.com/article/45/extending-with-plugins)
