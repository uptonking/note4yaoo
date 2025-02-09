---
title: lib-ide-vscode-codebase
tags: [codebase, editor, ide, vscode]
created: 2023-01-21T19:19:24.492Z
modified: 2024-08-24T16:15:42.906Z
---

# lib-ide-vscode-codebase

# guide

- [Source Code Organization · microsoft/vscode Wiki](https://github.com/microsoft/vscode/wiki/Source-Code-Organization)
# overview

```JS
// start dev
npm install
// npm run watch
// docs:　https://github.com/microsoft/vscode/wiki/How-to-Contribute
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
  - url包含文件路径，?folder=/Users/user11/repos/，切换文件时url不会变
  - 编辑文件会持久化道磁盘
  - 刷新页面时仓库会恢复，打开文件名也会恢复

- 
- 
- 
- 
- 
- 
- 

# vscode

# coder-server

# more
