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
  - 难以打包包含二进制的包，如leveldown
  - 对客户端开发环境的支持，如electron/react-native
  - ✅ node内置模块打包到浏览器环境下fallback库的实现不够成熟

- [Bundler的设计取舍 · web-infra-dev · Discussion](https://github.com/orgs/web-infra-dev/discussions/4)
  - Vite 在大型项目中的性能表现不够理想，一方面一些业务首屏有几千个模块，因此带来几千个网络请求
  - Rollup 对 CommonJS 的支持问题有很多，或者说在 Rollup 目前的架构下（将 CommonJS 转换成 ESM），实现对 CommonJS 的完全兼容几乎是一个不可能的事情
  - Rollup 本身不支持 Persistent Cache，因此二次冷启动的性能相比 Webpack 更差，同时 Rollup 并不支持 HMR
  - esbuild 解决了 Rollup 的 CommonJS 和性能两个最大的问题，插件化问题： 众所周知，esbuild 的 API 极为精简，应用构建相比库构建需要更强的插件扩展能力，而 esbuild 难以满足这个需求，如缺失 onTransform hook 导致不同 transform 的扩展组合很难进行
# rspack-dev-xp
- Rsbuild 应用不能使用 Rspack 的 devServer 配置项。你可以通过 Rsbuild 的 dev 和 server 配置 Server 的行为

- monorepo中包的入口要指定后缀，要用 `"main": "dist/index.mjs"`，而不是 `"main": "dist/index"`.
  - 否则会出现异常 Failed to resolve @your/pkg in builtin:swc-loader??

- 将swc-loader react.runtime 改为classic，可解决react组件打包产物的异常

## legacy-issues

- Uncaught SyntaxError: Cannot use 'import.meta' outside a module
  - 定位到原因是 `outputModule: true`， 而不是 `newTreeshaking: true`
# more
