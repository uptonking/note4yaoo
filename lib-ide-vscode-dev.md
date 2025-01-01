---
title: lib-ide-vscode-dev
tags: [editor, ide, vscode]
created: 2023-01-21T18:53:37.366Z
modified: 2024-08-24T16:15:11.456Z
---

# lib-ide-vscode-dev

# guide

- pros
  - 完善的编辑器和ide功能，包括 editor/workbench/files/search/ext/cmd-palette
  - 支持运行在多种环境，如 web-memory, web-node-server, electron
  - theia is licensed under EPL, not as friendly as vscode/MIT

- cons
  - vscode插件市场归微软所有，第三方不可用

- features
  - ?

- who is using #vscode 💠
  - known: cursorai, codeium-windsurf

- who is using #theia
  - eclipse-che
  - ide: Arduino Pro IDE
  - more: Google Cloud Shell

- tips
  - gitpod早期参与研发了theia，但2020年vscode开源remote和web后，gitpod将ide替换到了vscode

- resources
  - ide类的参考实现包括: vscode, jupyter(codemirror), jetbrains
  - 参考设计 capabilities
# draft
- vscode提供了electron和web模式，未提供纯前端模式

- 删除文件的回收站

- ide-ai
  - editor-control MCP, 让ai操作编辑器的协议

- 文件操作基于文件实现，如何基于数据库实现
  - 参考markdown-database的实现和数据同步
# dev

# docs

- 

# more
