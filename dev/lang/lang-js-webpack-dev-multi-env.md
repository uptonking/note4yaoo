---
title: lang-js-webpack-dev-multi-env
tags: [bundler, toolchain, webpack]
created: 2023-12-25T19:39:38.656Z
modified: 2024-01-02T07:53:38.401Z
---

# lang-js-webpack-dev-multi-env

# guide

# roadmap/rfc
- [RFC-019: more target environments support_202209](https://github.com/web-infra-dev/rspack/discussions/648)
# examples
- 同时支持browser和nodejs的打包方式参考
  - 打包到node可基于tsc/babel，打包到browser可基于bundler
  - 还可用browserify将cjs代码直接转换到browser环境
  - 前端demo测试项目热加载可先watch某个或某些lib的output，再start测试项目
  - webpack
    - https://github.com/seald/nedb/blob/master/webpack.config.js /源码js默认可直接在nodejs使用，browser单独打包
    - https://github.com/fergiemcdowall/search-index/blob/master/webpack.config.js /js
  - rollup
    - https://github.com/lucaong/minisearch/blob/master/rollup.config.js /ts
    - https://github.com/isomorphic-git/isomorphic-git/blob/main/rollup.config.js /js
    - https://github.com/mongodb/js-bson/blob/main/rollup.config.mjs /ts
    - https://github.com/simple-statistics/simple-statistics/blob/main/rollup.config.mjs /js
    - https://github.com/axios/axios/blob/v1.x/rollup.config.js /js
    - https://github.com/foliojs/pdfkit/blob/master/rollup.config.js /js
  - esbuild/vite
    - https://github.com/jvilk/BrowserFS/blob/master/scripts/build.mjs /ts
    - https://github.com/unjs/ofetch/blob/main/build.config.ts
    - https://github.com/octokit/octokit.js/blob/main/scripts/build.mjs
    - https://github.com/metachris/typescript-boilerplate
  - browserify
    - pouchdb
    - https://github.com/appy-one/acebase-core
  - 多个入口
    - https://github.com/Level/browser-level
    - https://github.com/Level/memory-level

- https://github.com/dominicbirch/replace-resolve-webpack-plugin /202304/ts
  - a webpack resolve plugin which supports replacing imports in directory A, with any imports that exist at the same relative path in directory B (optional substitution by convention).
  - Tailoring libraries for multiple targets using the same source (react native maybe?)
  - While it makes sense in situations where you want to replace a lot of imports with different values, it's less convenient in cases where the intention is to redirect lots of modules to a small set of replacements; in such cases I would suggest leveraging either webpack's `alias` or `NormalModuleReplacementPlugin`.
  - Alternatively, in simple use cases where only module resolution precedence (no absolute, dot paths or imports with extensions are involved), it would probably be simpler to make use of `resolve.modules` in webpack's configuration rather than using this plugin.
# blogs

## [Recipes on how to create a library that supports both browser and Node.js - DEV Community_202002](https://dev.to/riversun/recipes-on-how-to-create-a-library-that-supports-both-browser-and-node-js-201m)

- There are two ways to create a library that supports both browser and node.js.
  - One bundle: build both browser and Node.js code with one bundle.
  - Two bundles: build libraries for browser and node.js separately

- https://github.com/riversun/making-library-with-webpack /202105/js
  - Introduces how to build a library that supports both browser and Node.js using webpack4 and ES6
# discuss-stars
- ## 

- ## 
# discuss
- ## 

- ## 

- ## [webpack - NormalModuleReplacementPlugin does not work when modifying resourceRegExp slightly - Stack Overflow](https://stackoverflow.com/questions/56741909/normalmodulereplacementplugin-does-not-work-when-modifying-resourceregexp-slight)
- `webpack.NormalModuleReplacementPlugin(regex, result => result.createData.resource = NEW_PATH)`

- ## [Add `target: "universal"` · webpack/webpack_201802](https://github.com/webpack/webpack/issues/6525)
- Another solution would be using the direct source of the `globalThis` implementation:
  - i tried these last solution of @simonwep and other solutions editing `globalThis` . I don't receive `window` is not defined anymore but my web worker does not work.  My application goes straight without throwing errors and get the workers

- ## [Provide a way to write a library that supports different dependencies on Node and the Browser · webpack/webpack_202109](https://github.com/webpack/webpack/issues/14314)
- multiple solutions:
  - universal, output with ecma modules/umd output, create protection for only Node.js packages (i.e. const chokidar = typeof window === 'undefined' ? require('chokidar') : null; as you written above), unfortunately it requires change logic on you side, no job for webpack here, some modules can be shimming
  - packages_conditional_exports, using multi compiler mode and create different files for Node.js and web target
  - avoid using Node.js modules, but it's not applicable for some cases
