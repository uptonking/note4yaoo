---
title: toc-devtools-compiler-bundler-toolchain
tags: [compiler, devops, devtools, engineering, toc]
created: 2020-10-05T08:14:22.192Z
modified: 2022-11-01T01:05:07.873Z
---

# toc-devtools-compiler-bundler-toolchain

# guide

- transpile
  - babel, swc

- compiler
  - esbuild, wmr

- dev-server
# popular
- https://github.com/google/zx /apache2/202309/ts
  - https://google.github.io/zx/
  - A tool for writing better scripts
  - The zx package provides useful wrappers around `child_process`, escapes arguments and gives sensible defaults.
# frontend-compiler

# dynamic-import

- https://github.com/Rich-Harris/shimport /js
  - A 2kb shim for import and export. Allows you to use JavaScript modules in all browsers, including dynamic import().
  - A 2kb shim for import and export. Allows you to use JavaScript modules in all browsers, including dynamic import().
  - if they are, just use the native module loader
  - if not, use Shimport
# npm
- [npmmirror 镜像站, 一个完整 npmjs.com 镜像](https://npmmirror.com/)

- https://github.com/pnpm/pacquet /MIT/rust
  - experimental package manager for node.js
  - A Rust rewrite of pnpm
# rollup
- https://github.com/rolldown-rs/rolldown_legacy /202304/rust/inactive
  - https://rolldown.rs/
  - Fast JavaScript/TypeScript bundler in Rust with Rollup-compatible API.
  - Currently we are targeting to pass the function tests of Rollup.
  - [尤雨溪：Vite 的现状与未来展望 - 知乎_202310](https://zhuanlan.zhihu.com/p/659714285)
    - 原始的 Rolldown 项目在很久之前就开始了，它或多或少是 Rspack 的前身
    - 正在从零开始重新编写 Rolldown 的新版本，并借鉴了以前迭代的知识和经验。
    - Rolldown 的重点将放在本地级别的性能上，同时尽可能与 Rollup 保持兼容。最终目标是在 Vite 中切换到 Rolldown，并对用户产生最小的影响。
    - Vite 团队将与 Rspack 团队合作开发一些共享的底层工具和功能，例如，都将建立在当前 Rust 中最快的 JS 解析器 OXC 的基础上，还将研究如何在 Rspack 和 Vite 之间实现模块联邦。
    - 第四阶段：使用 Rust 重构 Vite
  - [Is this project still under maintenance?](https://github.com/rolldown-rs/rolldown_legacy/issues/131)
    - 202308: We are refactoring the core architecture of current codebase under the hood. It's immature, so we don't made the process public.But yes, the project is still alive.
# bundler
- https://github.com/farm-fe/farm /rust
  - 基于 Rust 的极速 web 构建引擎
  - fast web-building tool written in Rust, like webpack and vite, but much faster.
  - [Farm v0.4：最快！增加与 rspack 和 turbopack 性能对比，支持大量新特性 - 知乎](https://zhuanlan.zhihu.com/p/613209716)

- https://github.com/slava-sh/rust-bundler /rust/inactive
  - Creates a single-source-file version of a Cargo package.
  - https://github.com/Endle/rust-bundler-cp
    - Creates a single-source-file version of a Cargo package. It's designed for Competitive Programming like Codeforces.

- https://github.com/kuretchi/cargo-simple-bundler
  - Packs only necessary modules of the crate into a single file automatically.

- https://github.com/devongovett/bundler-algorithm /rust/inactive
  - Experimenting with a faster bundling algorithm
# test
- https://github.com/YMFE/yapi
  - /18.1kStar/Apache2/202010
  - 依赖mongodb、axios、json5、jsonwebtoken、koa、markdown-it、mockjs
  - YApi是dd一个可本地部署的、打通前后端及QA的可视化接口管理平台
  - features
    - 基于 Json5 和 Mockjs 定义接口返回数据的结构和文档
    - 扁平化权限设计
    - 类似 postman 的接口调试
    - 支持 postman, har, swagger 数据导入
    - 免费开源，内网部署
  - [开发不活跃，YApi开源项目作者，目前在美团优选工作](https://github.com/YMFE/yapi/issues/1173)
- RAP 阿里
  - https://github.com/thx/rap2-delos
  - /6.4kStar/MIT/202009
  - 依赖Koa、MySQL
  - https://github.com/thx/rap2-dolores
  - 依赖react、@material-ui/core、chart.js、codemirror、formik、jquery、react-redux
  - 阿里妈妈前端团队出品的开源接口管理工具RAP第二代
- https://github.com/NEIAPI/nei
  - https://nei.netease.com/
  - NEI 网易接口管理平台 源代码
  - 前端依赖：网易自研开源nej、regularjs
  - 后端依赖：koa、mysql、redis、mongodb
- https://github.com/trueleaf/moyu
  - 基于 Vue 和 Electron 的在线协同api接口管理工具。
  - 接口文档管理工具、接口工具、接口文档、api文档、api工具、快乐摸鱼
# database-manager
- https://github.com/405go/pdman
  - 开源免费的数据库模型建模工具
  - 是PowerDesigner之外，更好的免费的替代方案
# site
- https://github.com/jbake-org/jbake
  - Java based open source static site/blog generator
# java
- https://github.com/alibaba/arthas
  - Alibaba Java Diagnostic Tool
- https://github.com/RohitAwate/Everest
  - cross-platform REST client.
- https://github.com/zxh0/classpy
  - GUI tool for investigating Java class files
- https://github.com/vanzin/jEdit
  - copy of jEdit's repository from jedit.sourceforge.net.
- https://github.com/JFormDesigner/markdown-writer-fx
  - open source Markdown editor written in JavaFX 8.
