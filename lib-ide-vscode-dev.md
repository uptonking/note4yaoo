---
title: lib-ide-vscode-dev
tags: [editor, ide, vscode]
created: 2023-01-21T18:53:37.366Z
modified: 2024-08-24T16:15:11.456Z
---

# lib-ide-vscode-dev

# guide

- pros
  - reliable, 开源十几年，有商业公司和开源社区持续投入
  - MIT, theia is licensed under EPL
  - 完善的编辑器和ide架构，包括 editor/workbench/files/search/ext/cmd-palette
  - 支持运行在ci多种环境，如 web-memory, web-node-server, electron
  - 实现了很多git操作的ui和展示的ui，可作为git客户端

- cons
  - insecure/non-sandboxed by design, 但微软设计就是如此，支持在本地或远程执行代码
  - vscode插件市场归微软所有，第三方不可用
  - ui的定制性差

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
  - [Visual Studio Code for Education](https://vscodeedu.com/)
# draft
- toys
  - version-history for prosemirror/codemirror
  - hocuspocus collab for file-tree/tabs
  - file/data-provider
  - ui-skin

- vscode提供了electron和web模式，未提供纯前端模式

- ide-ai
  - editor-control MCP, 让ai操作编辑器的协议
- extension
- integrations
  - notion database

- 文件操作基于文件实现，如何基于数据库实现
  - 参考markdown-database的实现和数据同步
- 删除文件的回收站

- 构建工具迁移到respack/vite
# dev-xp

## hot-keys

- Navigate back:     Ctrl-Alt--
- Navigate forward:  Ctrl-Shift--

- Move line up and down: Alt+Up/Down
- Copy line up / down: Ctrl+Shift+Alt+Up/Down
- Shrink / expand selection: Shift+Alt+Left/Right

- Whole document format: Ctrl+Shift+I

- Code folding: Ctrl+Shift+[/]

- Open Markdown preview: Ctrl+Shift+V

- Ctrl+Space to trigger the Suggestions widget.

- Go to References: Select a symbol then type Shift+F12
  - Shift+Alt+F12: Find All References view

- 
- 
- 

# more
