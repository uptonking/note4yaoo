---
title: lang-js-webpack-rspack
tags: [devtools, rspack, toolchain, webpack]
created: 2020-11-20T19:29:35.880Z
modified: 2024-01-02T07:53:22.956Z
---

# lang-js-webpack-rspack

# guide
- 推迟迁移到rspack的原因
  - 难以迁移lib打包用到的第三方plugin
  - 难以迁移lib打包用到的第三方loader，如fonts/svg/img
  - 难以打包包含二进制的包，如leveldown/sqlite
  - 难以打包包含二进制的文件，如png，特别是在esm的环境下
  - 对客户端开发环境的支持，如electron/react-native
  - ✅ node内置模块打包到浏览器环境下fallback库的实现不够成熟
# [Bundler的设计取舍 · web-infra-dev · Discussion _202309](https://github.com/orgs/web-infra-dev/discussions/4)
- Vite在大型项目中的性能表现不够理想，一方面一些业务首屏有几千个模块，因此带来几千个网络请求
  - Rollup 的产物优化能力相比弱了不少，尤其是缺失 Bundle Splitting 等能力导致业务很难做精细的优化，
  - 因此内部有不少业务是 dev 下运行 Vite，生产环境用 Webpack，这导致开发和生产存在着较大的差异。
- Rollup 对 CommonJS 的支持问题有很多，或者说在 Rollup 目前的架构下（将 CommonJS 转换成 ESM），实现对 CommonJS 的完全兼容几乎是一个不可能的事情
  - Rollup 本身不支持 Persistent Cache，因此二次冷启动的性能相比 Webpack 更差，
  - 同时 Rollup 并不支持 HMR
- esbuild 解决了 Rollup 的 CommonJS 和性能两个最大的问题，
  - 插件化问题： 众所周知，esbuild 的 API 极为精简，应用构建相比库构建需要更强的插件扩展能力，而 esbuild 难以满足这个需求，如缺失 onTransform hook 导致不同 transform 的扩展组合很难进行
  - 产物性能问题： 在 C 端的场景下，对 chunk 数目和大小很敏感，大量的小 chunk 可能导致很差的加载性能，esbuild 缺乏像 webpack 对 chunk 的深度定制的能力
  - esbuild 并没内置支持HMR的能力，因此如果要支持 HMR，就需要自行在 Load 阶段注入 HMR 的 runtime
- 上述的这些问题，导致我们渐渐放弃了 esbuild 的方案，专向自研 Rust Bundler 的之路。

- 我们自研 Rust Bundler 并不是一开始就选择走 Rust Webpack 这条路，实际上我们最开始的路径更加简单，解决 esbuild 的目前的一些问题，因此最开始的路径其实是 Rust 版本的 esbuild | rollup 加上内置 HMR、CommonJS 和 Bundle splitting 的支持
  - Rspack 的 legacy 分支仍然保留了当初兼容 esbuild 接口的设计。
- Rollup 的核心架构是只支持 ESM 作为一等公民，其他的模块系统（CommonJS）或者非 JS 模块系统都需要转换成 ESM 才能工作，这导致了非常多的问题，
  - 一个最为常见的问题就是不同的模块系统的 resolve 逻辑是不一致的（还有更多的不一致，如 sideEffects 的默认值，chunk 的生成逻辑等），在 Rollup下并不能很好的感知到不同模块的差异（因为所有的模块都被转换成了 ESM 模块），
  - 因为 Rollup 在核心层并没对不同模块进行区分，这导致只能依赖在插件侧依赖非常的 hack 逻辑来实现该功能（每个 CommonJS 转换成 ESM 的时候需要给对应模块标注原始的 CommonJS 标记，以便于后续的 resolve 逻辑进行区分。
- 与很多人的直觉可能相违背的是，Webpack 和 Parcel一样都是 language agnostic，而 Rollup 则是只有 Javascript 才是一等公民。这可能也是 Webpack 5 最为人忽视的一点，Webpack 5 支持了更多的一等公民模块。
- Rust Bundler 自从立项开始，自始至终就有一个核心需求，那就是支持通过 JavaScript 写Plugin，这点始终未变，因为我们在业务支持中，深知业务的扩展性是非常必要的，一个业务不可扩展的 Bundler 是难以落地的，因此如何设计插件 API 就成了我们的一个核心问题。

- 另一个对性能影响很大的设计就是如何在不同的模块转换之间复用AST，因为 parse 的开销通常非常巨大且常常成为性能的瓶颈，如果能尽可能的复用 AST 则可以大大的优化性能。我们看看各个工具是如何处理 AST的复用的。
  - 首先webpack里返回的AST只能是符合ESTree标准的AST，但是不幸的是，社区的各种JS转换的loader返回的基本都不是标准的ESTree AST，包括 babel-loader 和 swc-loader
  - 另一个问题是 webpack 虽然内部 parser 支持多种AST(CSS AST和 JavaScript AST)，但是 webpack 目前也只支持JavaScript的AST，这导致虽然 Webpack 支持这个功能很长时间，但是其实也没有大规模应用。

- 虽然我们整体路线上决定采用了 Webpack 的架构，但是在实施过程中还是走了很多弯路，
  - 我们在早期开发过程中，一方面收到了 esbuild 的影响，另一方面则是当时的 loader 尚未完全支持，因此我们决定扩展了对一等公民的支持（如支持 jsnext、ts、tsx、jsx 等 js 扩展语言作为一等公民），这虽然帮助我们快速的在业务侧进行了落地，但是也导致了较多问题
  - bundle splitting 的结果不够准确，因为 AST 转换后没有立即进行 codegen 导致无法拿到转换后的代码
  - 默认对 ts 和 js 文件使用 swc 进行转换，导致一些不能进行 transform 的模块会出错（如core.js
- 因此在未来 Rspack 考虑放弃对 ts、tsx、jsx 等模块的一等公民支持，而让用户通过 swc-loader 来进行编译处理，这保证了一等公民的处理和 Webpack 对齐，同时保障核心层的稳定。

- 👥

- 分布式构建是未来的规划之一，我们持续关注

- 
- 
- 

# rspack-dev-xp
- Rsbuild 应用不能使用 Rspack 的 devServer 配置项。你可以通过 Rsbuild 的 dev 和 server 配置 Server 的行为

- monorepo中包的入口要指定后缀，要用 `"main": "dist/index.mjs"`，而不是 `"main": "dist/index"`.
  - 否则会出现异常 Failed to resolve @your/pkg in builtin:swc-loader??

- 将swc-loader react.runtime 改为classic，可解决react组件打包产物的异常

## legacy-issues

- Uncaught SyntaxError: Cannot use 'import.meta' outside a module
  - 定位到原因是 `outputModule: true`， 而不是 `newTreeshaking: true`
# changelog

## v2023

- [feat: electron support _202306](https://github.com/web-infra-dev/rspack/pull/3414)
# more
