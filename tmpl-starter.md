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

- build
  - tsc:适合单独库
  - babel
    - babel-cli适合单独库，支持watch目录
    - 不适合后面扩展到ts,css
  - webpack/webpack-dev-server
    - 适合复杂应用，支持各种文件格式
  - rollup
  - 不需单独编译的库可不编译

- test
  - jest
  - ts-jest

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
