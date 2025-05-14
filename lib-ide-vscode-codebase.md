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
npm run watch
// npm run watch-web
// docs:　https://github.com/microsoft/vscode/wiki/How-to-Contribute
```

- 🚀 ./scripts/code.sh
  - Running on Electron with extensions run in NodeJS
- 🚀 ./scripts/code-web.sh
  - Extensions and UI run in the browser
  - 切换文件时url不变， url不包含文件路径 `http://localhost:8080/`.
  - 编辑文件会持久化到磁盘
  - 刷新页面时打开的文件夹会丢失，需要重新打开文件夹及文件
  - 数据保存在indexeddb
  - hover类型提示只支持浏览器内置的js对象及BOM对象，不支持node_modules下的提示如useState
- 🚀 ./scripts/code-server.sh --launch
  - UI in the browser, extensions run in code server (NodeJS)
  - 切换文件时url不会变, url包含项目根目录路径但不包含文件名，`?folder=/Users/user11/repos/proj11`.
  - 编辑文件会持久化道磁盘
  - 刷新页面时打开的文件夹会恢复，打开的文件名及tabs也会恢复
  - hover类型提示支持node_modules下的提示如useState

- 
- 
- 
- 
- 
- 
- 

# vscode

- 
- 
- 
- 
- 
- 
- 

# extensions
- ⚖️ 很多extensions都使用了markdown-it来处理markdown
  - markdown-language-features: highlight.js
  - markdown-math: markdown-it-katex
  - extension-editing
  - ipynb
  - [The TextMate grammar VS Code uses for Markdown syntax highlighting](https://github.com/microsoft/vscode-markdown-tm-grammar)

- 
- 
- 

# coder-server
- ❓ 待确认原因: 使用`./scripts/code-server.sh`启动vscode时，能在chrome devtools看到2条websocket连接
  - ws://localhost:9888/oss-dev?reconnectionToken=80d0daf1-ce1f-44ac-9861-a90054bdd4f5&reconnection=false&skipWebSocketFrames=false
  - ws://localhost:9888/oss-dev?reconnectionToken=1676ba6a-f452-4fe7-967f-c444eb325b25&reconnection=false&skipWebSocketFrames=false

- VS Code's web/server edition uses two separate WebSocket channels for different purposes:
  - a. Main Connection: Handles core editor functionality (e.g., file operations, UI interactions).
  - b. Extension Host Connection: Manages extensions and their communication with the core editor.
  - If the extension host crashes (a common scenario with third-party extensions), the core editor remains functional.
  - The WebSocket server logic is in `src/vs/server/remoteExtensionHostAgentServer.ts`.
  - The client-side WebSocket management is in `src/vs/platform/remote/browser/browserSocketFactory.ts`.

- 
- 
- 
- 
- 
- 
- 
- 

# more
