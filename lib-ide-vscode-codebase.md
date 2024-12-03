---
title: lib-ide-vscode-codebase
tags: [codebase, editor, ide, vscode]
created: 2023-01-21T19:19:24.492Z
modified: 2024-08-24T16:15:42.906Z
---

# lib-ide-vscode-codebase

# guide

# overview

```JS
// start dev
npm install
// npm run watch
```

- ./scripts/code.sh
  - Running on Electron with extensions run in NodeJS
- ./scripts/code-web.sh
  - Extensions and UI run in the browser
  - 切换文件时url不变， url不包含文件路径
  - 编辑文件会持久化到磁盘
  - 刷新页面时打开的仓库会丢失，需要重新打开
  - 数据保存在indexeddb
- ./scripts/code-server.sh --launch
  - UI in the browser, extensions run in code server (NodeJS)
  - url包含文件路径，?folder=/Users/user11/repos/，切换文件时url也不会变
  - 编辑文件会持久化道磁盘
  - 刷新页面时仓库会恢复，打开文件名也会恢复

- 
- 
- 
- 
- 
- 
- 

# blogs-vscode-src-reading
- blogs
  - [vscode 源码解析 - 进程间调用 · hullis/blog](https://github.com/hullis/blog/issues/41)
  - [vscode 源码解析 - 事件模块 · hullis/blog](https://github.com/hullis/blog/issues/40)
  - [vscode 源码解析 - vscode loader · hullis/blog](https://github.com/hullis/blog/issues/43)
  - [vscode 源码解析 - 依赖注入 · hullis/blog](https://github.com/hullis/blog/issues/25)

- https://github.com/fzxa/VSCode-sourcecode-analysis
  - 微软VSCode IDE源码分析
  - 1.37.1版本
  - 依赖版本 Nodejs x64 version >= 10.16.0, < 11.0.0, python 2.7(3.0不能正常执行)
# vscode

# coder-server

# more
