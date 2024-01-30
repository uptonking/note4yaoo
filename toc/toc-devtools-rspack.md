---
title: toc-devtools-rspack
tags: [bundler, compiler, devtools, rspack, toc, webpack]
created: 2023-12-26T19:10:58.700Z
modified: 2023-12-26T19:11:22.389Z
---

# toc-devtools-rspack

# guide
- 推迟迁移到rspack的原因
  - 难以迁移lib打包用到的第三方plugin
  - 难以迁移lib打包用到的第三方loader，如fonts/svg/img
  - lang-js
    - json ✅
  - env
    - node内置模块打包到浏览器环境下fallback库的实现不够成熟
    - 对客户端开发环境的支持，如electron/react-native
  - monorepo
    - rspack不支持tsconfig.extends
  - to-test: dynamic import, hot reloading

- tips
  - 官方仓库提供了很多场景和框架的示例，不必在github找
# popular
- https://github.com/web-infra-dev/rspack /MIT/rust
  - https://rspack.dev/
  - A fast Rust-based web bundler 
  - Compatible with the architecture and ecosystem of webpack, no need to build the ecosystem from scratch.
  - 依赖oxc_resolver(解析js/ts)、nodejs-resolver、glob-match、petgraph、tokio、async-trait
  - With a built-in incremental compilation mechanism, HMR is extremely fast and fully capable of developing large-scale projects.
  - Batteries Included: Out-of-the-box support for TypeScript, JSX, CSS, CSS Modules, Sass, and more.
  - Framework Agnostic: Not bound to any frontend framework, ensuring enough flexibility.
  - 🍴 forks
  - https://github.com/Brooooooklyn/rspack

- https://github.com/rspack-contrib/performance-compare /202312/js
  - Performance compare for Rsbuild, Farm, Webpack, Rspack, Turbopack and Vite
  - Forked from farm-fe/performance-compare, thanks to the Farm team
  - Using Turbopack's bench cases (1000 React components), see https://turbo.build/pack/docs/benchmarks

- https://github.com/KyrieLii/webpack-to-rspack /md
  - Configuration mapping from webpack to rspack
# starter/web/client/nodejs
- resources
  - https://github.com/web-infra-dev/rspack-demo /js/react
  - https://github.com/rspack-contrib/rspack-examples /ts/arco-pro

- https://github.com/web-infra-dev/rspack-repro /202311/js
  - A GitHub template for creating a Rspack minimal reproducible example.
  - Webpack is included for comparing the outputs.

- https://github.com/yanhaijing/rspack-cra /202312/ts/svgr
  - create-react-app@5.0.1 脚手架创建的项目，接入了rspack@0.3.11，同时给 create-react-app 添加了测试环境的构建(build:test)

- https://github.com/2401345934/rspack-react-demo /202310/ts
  - rspack-react-starter
- https://github.com/everton-dgn/boilerplate_rspack /202310/ts
  - a complete React.js boilerplate
  - Styled-Components, vite, vitest

- https://github.com/ulivz/rspack-preact-example /202311/js
  - Minimal Rspack-powered preact example

- https://github.com/drafting-dreams/rspack-browser-extension-template /202310/ts
  - browser extension template

- https://github.com/RyanProMax/electron-react-rspack /202310/ts
  - Electron boilerplate including TypeScript, React, Rspack and ESLint.

- https://github.com/felixmosh/rspack-express-js /202309/ts
  - Express.js app bundled with Rspack with HMR
# examples
- https://github.com/tobua/rspack-react-pdf /202312/ts
  - rspack setup to generate PDFs in the Browser with @react-pdf/renderer
# integrations
- https://github.com/Asuka109/rspack-linaria-example /202310/ts
  - Example on how to integrate linaria into a project built with Rspack

- https://github.com/nashaofu/workbox-rspack-plugin /202308/ts
  - workbox for rspack plugin
# monorepo

# plugins

- resources
  - https://github.com/rspack-contrib/rspack-plugins
  - https://github.com/sanyuan0704/rspack-community-plugins
# ssr
- https://github.com/upupming/rspack-ssr-examples /MIT/202312/js
  - https://rspack-vanilla-example.vercel.app/
  - https://rspack-react-example.vercel.app/
  - https://rspack-vue-example.vercel.app/
  - Rspack Server-Side Rendering minimal examples, fully-extensible.
  - Basic example using only vanilla JavaScript.
    - Two entry files are constructed for running in the server (entry-server.ts) and client (entry-client.ts).

- https://github.com/Narawit-S/react-on-the-server /js
  - Welcome to the "React on the Server" workshop
# more
