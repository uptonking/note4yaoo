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
  - node内置模块打包到浏览器环境下fallback库的实现不够成熟
  - 对客户端开发环境的支持，如electron/react-native
# rspack-dev-xp
- Rsbuild 应用不能使用 Rspack 的 devServer 配置项。你可以通过 Rsbuild 的 dev 和 server 配置 Server 的行为

- monorepo中包的入口要指定后缀，要用 `"main": "dist/index.mjs"`，而不是 `"main": "dist/index"`.
  - 否则会出现异常 Failed to resolve @your/pkg in builtin:swc-loader??

- 将swc-loader react.runtime 改为classic，可解决react组件打包产物的异常

## legacy-issues

- Uncaught SyntaxError: Cannot use 'import.meta' outside a module
  - 定位到原因是 `outputModule: true`， 而不是 `newTreeshaking: true`
# more
