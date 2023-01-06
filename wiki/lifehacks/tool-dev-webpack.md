---
title: tool-dev-webpack
tags: [devtools, engineering, tool, webpack]
created: 2020-11-20T19:29:35.880Z
modified: 2020-12-08T14:05:41.408Z
---

# tool-dev-webpack

# guide

- 仅支持webpack v4的项目
  - ckeditor 5
  - atlaskit editor

- Webpack Incremental Builds
  - Use webpack's watch mode. Don't use other tools to watch your files and invoke webpack. 
  - The built-in watch mode will keep track of timestamps and passes this information to the compilation for cache invalidation.
  - In some setups, watching falls back to polling mode. 
    - With many watched files, this can cause a lot of CPU load. 
    - In these cases, you can increase the polling interval with watchOptions.poll.
  - 可实现类似ts project references的快速增量编译
  - The following utilities improve performance by compiling and serving assets in memory rather than writing to disk:
    - webpack-dev-server/webpack-hot-middleware/webpack-dev-middleware

- [How Webpack decides what entry to load from a package.json](https://www.jonathancreamer.com/how-webpack-decides-what-entry-to-load-from-a-package-json/)
  - If the `target` of your app is `web` or a few others (which is default). 
  - It will look first at the `browser` field, and if it doesn't exist, it'll look for the `module`, and lastly `main`.
  - 可查看源码 WebpackOptionsDefaulter.js
  - if your Webpack target is `node`, it looks at the `module` and `main` for entry. Otherwise, it goes to the `browser`, then `module`, then `main`.
  - 技巧：module可指向源码，main指向转义后的es5代码
# Module Federation
- [Module Federation原理剖析](https://zhuanlan.zhihu.com/p/296233114)
  - https://github.com/efoxTeam/emp
    - [基于Webpack 5 & Module Federation的微前端解决方案](https://github.com/efoxTeam/emp/blob/main/README-zh_CN.md)
# webpack-config

# webpack-dev-server

- webpack
  - https://github.com/webpack/webpack
  - a module bundler
  - it bundles various module formats primarily so they can be run in a browser. 
  - It offers both a CLI and Node API.

- webpack-dev-server
  - https://github.com/webpack/webpack-dev-server
  - 命令行会执行 `bin/webpack-dev-server.js` 的startDevServer()方法
  - Webpack Dev Server is itself an express server which uses `webpack-dev-middleware` to serve the latest bundle and additionally handles hot module replacement (HMR) requests for live module updates in the client.

- webpack-dev-middleware
  - https://github.com/webpack/webpack-dev-middleware
  - Webpack Dev Middleware is middleware which can be mounted in an express server to serve the latest compilation of your bundle during development. 
  - This uses webpack's Node API in watch mode and instead of outputting to the file system it outputs to memory.
  - For comparison, you might use something like express.static instead of this middleware in production.
  - webpack-dev-middleware is a wrapper that will emit files processed by webpack to a server. 
  - This is used in webpack-dev-server internally, however it's available as a separate package to allow more custom setups if desired.
  - No files are written to disk, rather it handles files in memory
  - If files changed in watch mode, the middleware delays requests until compiling has completed

- webpack-hot-middleware
  - https://github.com/webpack-contrib/webpack-hot-middleware
  - Actually making your application capable of using hot reloading to make seamless changes is out of scope, and usually handled by another library. 
  - This allows you to add hot reloading into an existing server without webpack-dev-server.
  - This module is only concerned with the mechanisms to connect a browser client to a webpack server & receive updates. 
  - It will subscribe to changes from the server and execute those changes using webpack's HMR API.
  - Actually making your application capable of using hot reloading to make seamless changes is out of scope, and usually handled by another library. 

- webpack-hot-server-middleware
  - https://github.com/60frames/webpack-hot-server-middleware
  - designed to be used alongside webpack-dev-middleware and webpack-hot-middleware to handle hot module replacement of server rendered apps.

- koa-webpack
  - https://github.com/shellscape/koa-webpack
  - Development and Hot Module Reload Middleware for Koa2, in a single middleware module.
  - This module wraps and composes webpack-dev-middleware and webpack-hot-client into a single middleware module, allowing for quick and concise implementation.
  - it'll also use the installed webpack module from your project, and the webpack.config.js file in the root of your project
  - 作者会等webpack 5稳定后才会升级到webpack 5
  - webpack-dev-server基于express，非常受欢迎
  - 还要考虑是否支持框架层的插件，如react-fast-refresh
# webpack-extensions
- https://github.com/etsy/kevin-middleware
  - Kevin is an Express-style middleware that makes developing with Webpack in a monorepo a lot simpler. 
  - It's loosely based off of Webpack's dev middleware, and it is intended to be used as a replacement for it.
  - Using Webpack in development in a monorepo can be challenging because, by default, it will try to keep your entire JavaScript codebase in memory.
    - Kevin addresses this problem by allowing you to create separate Webpack configs for different parts of your codebase; 
    - it then manages these configs by having Webpack only watch and build relevant files.
# repos-monorepo
- 在子repo中共用webpack配置的示例
  - monorepo-react-webpack-ts
    - 创建了一个单独的dev-tools包
    - 基于webpack-merge根据common创建dev、prod、server的配置
  - monorepo-webpack-babel-example-js
    - 创建了单独的文件webpack.shared.js
    - 但未使用webpack-dev-server
  - https://github.com/DoSomething/webpack-config
    - 自己封装了createConfig方法，需要查阅api

- https://github.com/Quramy/lerna-yarn-workspaces-example
  - /ts/基于tsc
  - https://github.com/Quramy/npm-ts-workspaces-example
- https://github.com/carlosnakane/monorepo-react-webpack
  - /ts/基于tsc
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
- https://github.com/shnydercom/lerna-typescript-cra-uilib-starter
  - /ts/基于cra

- https://github.com/react-workspaces/react-workspaces-playground
  - /js/基于cra
  - 依赖Create React App 3(React 16.8)，Storybook 5，Yarn Workspaces，Host Multiple CRA Apps，Hot Reload all Apps

- more-monorepos
  - https://github.com/korfuri/awesome-monorepo
  - https://github.com/Thinkmill/monorepo
    - Thinkmill's Monorepo Style Guide
  - https://github.com/LukasBombach/webpack5-monorepo-test
    - 依赖next
  - https://github.com/jimmy-james/fm-monorepo-poc
    - PoC in js, ts, react, redux for Webpack Federated Modules and monorepo project structure
    - https://github.com/carlosnakane/webpack-module-federation-typescript
  - https://github.com/jeremy-coleman/monorepo-starterkit
    - use rollup for bundles and webpack for apps, hmr works
  - https://github.com/flegall/monopack
    - A JavaScript bundler for node.js monorepo-codebased applications.
  - https://github.com/lucasgdb/monorepo-react-node-postgres-ts
# ref
- [webpack: Choosing a Development Tool](https://webpack.js.org/guides/development/ )
- [Cutting our webpack build times in half_201905](https://www.cargurus.dev/Cutting-our-webpack-build-time-in-half/)
  - We use yarn workspaces, and whats known as a mono-repo. 
  - Essentially our entire codebase is in one git repo, divided into npm packages that all resolve in a single filesystem. 
  - In the past developers had to compile the entire codebase when changes were made. 
  - We created our own webpack plugin that detects which files have changed and only recompile the bundles specific to what has changed. 
  - Our plugin is a lot like the Hard Source plugin, which you can use to do the same thing. 
  - By detecting what has changed, and only recompiling the changed files, we cut many of our builds from 7+ minutes to 30 seconds.
- [Developing in a Monorepo While Still Using Webpack: kevin-middleware_202004](https://codeascraft.com/2020/04/06/developing-in-a-monorepo-while-still-using-webpack/)
- [webpack扩展插件](https://www.timsrc.com/article/45/extending-with-plugins)
- [Webpack vs webpack-dev-server vs webpack-dev-middleware vs webpack-hot-middleware](https://stackoverflow.com/questions/42294827/webpack-vs-webpack-dev-server-vs-webpack-dev-middleware-vs-webpack-hot-middlewar)

- [How does the CodeSandbox browser-side webpack work? ](https://developpaper.com/how-does-the-codesandbox-browser-side-webpack-work-part-one/)
