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
- https://github.com/TanStack/devtools /65Star/MIT/202508/ts
  - https://x.com/AlemTuzlak/status/1954587606479487396
    - We've integrated an event bus which let you pipe the data from your libraries/app code into your devtools panel. You can set up custom devtools within minutes that help you ship faster.
  - https://x.com/AlemTuzlak/status/1950968833478467592 _20250801
    - I've been invited by the wonderful @tan_stack team to help them build out framework-agnostic devtools
    - the plugin system is the best part, it should be as easy as just plugging it in
    - Can't wait for the multi-tool view
    - take a look at the nuxt devtools, very nice things to take inspiration from
  - https://x.com/AlemTuzlak/status/1951292149204386082 _20250801
    - @tan_stack Devtools is officially in alpha
    - You mount a devtools shell into your app, then you give it the plugins as props, when you click on one of the tabs it calls the plugins render method and mounts the UI so you can see it. 
    - The core just gives you the DOM node where the adapters allow you to pass in JSX.
    - It's a panel that allows you to plug anything into it and show it inside of that panel via plugins. This allows you to have both the TanStack router/query devtools inside of here. 
    - For now, the biggest priority would be helping the tanstack ecosystem by providing tooling for easier integration of other potential devtools (think db, form etc)
    - In the long run when we enable server <> client communication things will get crazy

- https://github.com/google/zx /apache2/202309/ts
  - https://google.github.io/zx/
  - A tool for writing better scripts
  - The zx package provides useful wrappers around `child_process`, escapes arguments and gives sensible defaults.

- https://github.com/module-federation/core /2.1kStar/MIT/202508/ts
  - https://module-federation.io/
  - Module Federation is a concept that allows developers to share code and resources across multiple JavaScript applications
  - You can consider the module federation capabilities provided by this repository as "module federation 2.0".
  - "Module Federation 2.0" differs from the "Module Federation" built into Webpack 5 by offering not only the core features of module export, loading, and dependency sharing but also additional dynamic type hinting, a "Manifest", a "Federation Runtime", and a "Runtime Plugin System". 
  - These features make "Module Federation" more suitable for use as a micro-frontend architecture in large-scale web applications.
# nodejs
- https://github.com/poppinss/ts-exec /MIT/202512/ts
  - Execute TypeScript on Node using SWC
  - A JIT compiler for running TypeScript and JavaScript code in Node.js without compilation, built on top of SWC with full ESM support for Node.js 24 and above.
  - ts-exec is a TypeScript execution engine that lets you run `.ts` and `.tsx` files directly in Node.js without a build step. 
  - Unlike other popular solutions, ts-exec prioritizes compatibility with Node.js module resolution, ensuring that code running with ts-exec will work identically after compilation to JavaScript.
  - ts-node is no longer actively maintained and has become bloated over time. While tsx offers a modern alternative, it makes a critical compromise: it allows extension-less imports and directory imports during development. because Node.js strictly requires explicit file extensions and cannot resolve directory imports.
  - ts-exec takes a different approach. It provides the complete TypeScript feature set (including enums, legacy decorators, and JSX syntax) while strictly following Node.js file resolution rules. 
  - https://x.com/AmanVirk1/status/1997926011699450346
    - Node.js native support lacks JSX + decorators (table stakes for many). TSX has unsafe imports.
    - Node.js implementation not supporting tsconfig.json is such a pain

- https://github.com/swc-project/swc-node /MIT/202510/ts
  - Faster ts-node without typecheck
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
# mobile
- https://github.com/Tencent/vConsole /MIT/202306/svelte
  - A lightweight, extendable front-end developer tool for mobile web page
# devtools
- https://github.com/coryhouse/react-switchboard /MIT/202408/ts
  - Quickly create custom DevTools for your React app
  - https://x.com/housecor/status/1823182847902912730
    - Configure mock APIs
    - Simulate slowness for specific HTTP requests
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
