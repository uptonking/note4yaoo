---
title: tmpl-starter-monorepo
tags: [engineering, starter]
created: 2020-11-24T10:42:09.474Z
modified: 2020-12-08T13:53:36.730Z
---

# tmpl-starter-monorepo

- 快速开始开发项目的模板

# popular

- [Create React App](https://github.com/facebook/create-react-app)
  - Create React apps with no build configuration by running one command 
- [electron-webpack](https://github.com/electron-userland/electron-webpack)
  - The primary aim of electron-webpack is to eliminate all preliminary setup with one simple install so you can get back to developing your application.
  - HMR for both renderer and main processes

# frontend-starter

- monorepo
  - 基于workspace、lerna、nx
  - 优点
    - 统一管理版本、构建流程
    - 统一devDependencies，减少开发工具的体积
  - 缺点
    - 各子项目的issues会杂糅在论坛

- todo
  - npm workspaces暂不支持使用`.`添加顶层包作为workspace
    - 临时方案：直接在顶层加代码，或在packages/*子目录再复制一份源码
  - jest测试中import三方包时优先根据main，可自定义defaultResolver and packageFilter设置优先使用module
    - jest-module-field-resolver使用module后react导入出现问题
    - 不能轻易改

- dependencies
  - 对于大多数重复的devDependencies，提升到顶层
  - npm 7过渡阶段，使用npm install --legacy-peer-deps避免冲突
  - 对于依赖冲突的版本
    - npm shrinkwrap
    - 采用类似yarn的Selective dependency resolutions指定具体版本，npm对应的非官方实现是pm-force-resolutions(不支持npm7)
    - [npm equivalent of yarn resolutions?](https://stackoverflow.com/questions/52416312/npm-equivalent-of-yarn-resolutions) (提供了自定义脚本)

- build
  - 编译tips
    - 不需单独编译的库可不编译
  - node
    - 使用ts-node时，main字段必须是.ts文件
  - tsc
    - 适合单独库
    - `tsc -p tsconfig.json --traceResolution`打印日志
  - babel
    - 不适合后面扩展到ts,css
    - 共享的babel配置文件建议放在顶层
    - babel-cli适合单独库，支持watch目录
    - babel-node is a CLI that works exactly the same as the Node.js CLI, with the added benefit of compiling with Babel presets and plugins before running it.
      - Due to technical limitations, ES6-style module-loading is not fully supported in a babel-node REPL.
    - 所有简单包的编译命令可相似甚至相同，`babel --root-mode upward src -d lib`
      - lerna-yarn-workspaces-monorepo-js
      - monorepo-babel-ts-lerna-starter
      - `BABEL_ENV=build babel src --root-mode upward --out-dir dist --source-maps --extensions .ts,.tsx --delete-dir-on-start --no-comments`
  - webpack/webpack-dev-server
    - 适合复杂应用，支持各种文件格式，易于实现基于module federation的微服务
    - 共享的webpack配置文件建议放在顶层，可在子项目中直接通过require相对路径读取
  - rollup
  - 编译参考
    - 还可以利用现有脚本如react-scripts-ts编译，但不直观

- test
  - jest
    - 测试monorepo时，import子目录包的main默认指向dist，不方便

- hot-reload
  - 不是简单的watch增量编译，而是修改后自动编译且应用状态数据保持

- lint
  - eslint: tslint已废弃
  - stylelint

- framework
  - vanillajs
  - react
  - vue
  - components

- css
  - css
  - scss
  - styled-components
  - css-in-js

- more-tools-required
  - prettier

---

- storybook
  - 展示单个组件的不同状态
  - 缺点
    - 最终展示的文档灵活性不够高
    - breaking changes太多

- more-tools-optional
  - vscode
  - github: issue-template, pr, code-conduct
