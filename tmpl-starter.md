---
title: tmpl-starter
tags: [template]
created: '2020-11-24T10:42:09.474Z'
modified: '2020-11-24T10:42:33.622Z'
---

# tmpl-starter

- 快速开始开发项目的模板

## popular

- [Create React App](https://github.com/facebook/create-react-app)
  - Create React apps with no build configuration by running one command 
- [electron-webpack](https://github.com/electron-userland/electron-webpack)
  - The primary aim of electron-webpack is to eliminate all preliminary setup with one simple install so you can get back to developing your application.
  - HMR for both renderer and main processes

## frontend-starter

- monorepo
  - 基于workspace、lerna、nx
  - 优点
    - 统一管理版本、构建流程
    - 统一devDependencies，减少开发工具的体积
  - 缺点
    - 各子项目的issues会杂糅在论坛

- dependencies
  - 对于大多数重复的devDependencies，提升到顶层
  - npm 7过渡阶段，使用npm install --legacy-peer-deps避免冲突
  - 对于依赖冲突的版本
    - 采用类似yarn的Selective dependency resolutions指定具体版本，npm对应的非官方实现是pm-force-resolutions(不支持npm7)
    - [npm equivalent of yarn resolutions?](https://stackoverflow.com/questions/52416312/npm-equivalent-of-yarn-resolutions) (提供了自定义脚本)

- build
  - tsc: 适合单独库
  - babel
    - babel-cli适合单独库，支持watch目录
    - 不适合后面扩展到ts,css
    - 共享的babel配置文件建议放在顶层
  - webpack/webpack-dev-server
    - 适合复杂应用，支持各种文件格式，易于实现基于module federation的微服务
    - 共享的webpack配置文件建议放在顶层，可在子项目中直接通过require相对路径读取
  - rollup
  - 不需单独编译的库可不编译

- test
  - jest
  - ts-jest

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
