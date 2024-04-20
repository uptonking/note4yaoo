---
title: lang-js-webpack-rspack-issues
tags: [bundler, issues, rspack, webpack]
created: 2024-01-03T16:13:51.139Z
modified: 2024-01-03T16:14:25.702Z
---

# lang-js-webpack-rspack-issues

# guide

# issues-esm 📦
- 变通方案
  - 开发时热加载需关闭esm, 否则问题太多
  - app打包时优先cjs，然后尽量支持esm
  - lib打包时优先esm，特别是不依赖二进制包或文件时

- esm模式，不支持修改文件后热加载

- 🐛❓ 对 .png 打包会出现异常, Cannot use 'import.meta' outside a module
  - 异常信息是 // webpack/runtime/auto_public_path
  - if (typeof import.meta.url === "string") scriptUrl = import.meta.url
  - 注释掉产物中异常的代码，图片依然无法显示
  - 但 .svg 能正常打包
# issues-not-yet
- rspack.v0.6在打包yjs时，YDoc的random未使用打包模块
# discuss-not-yet
- ## 

- ## 

- ## [support webpack5 new library type 'module' · webpack-contrib/webpack-bundle-analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer/discussions/587)
- 未实现

- ## 🐛 [HookWebpackError: HMR is not implemented for module chunk format yet [webpack 5] · Issue #17636 · webpack/webpack](https://github.com/webpack/webpack/issues/17636)
- 202312: It is still under development and in our roadmap, sorry for delay, we have an issue for full compatibility ES modules

- 🧐 rspack的esm模式也不支持热加载

- https://discord.com/channels/977448667919286283/1080692512068481084/1192058459580022804
  - webpack esm支持hmr吗? 这个比较复杂，我们可能需要等webpack侧先实现
# discuss-stars
- ## 

- ## 

- ## 
# issues-done
- ## 

- ## 

- ## [[Bug]: Default identifiers not transformed in constructor parameters ](https://github.com/web-infra-dev/rspack/issues/6197)
  - Identifiers that are used as default values of a constructor's parameters are not being transformed properly.
