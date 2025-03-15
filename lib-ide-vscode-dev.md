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
    - 可提取出丰富的工具库
  - 支持运行在多种环境，如 web-memory, web-node-server, electron
  - 实现了很多git操作的ui和展示的ui，可作为git客户端
  - 提供了很多原理深度解析的技术博客
  - 提供了处理 cross-platform/browser 的参考方案

- cons
  - insecure/non-sandboxed by design, 但微软设计就是如此，支持在本地或远程执行代码
  - vscode插件市场归微软所有，第三方不可用
  - ui的可定制性差

- features
  - ?

- who is using #vscode 💠
  - known: cursorai, codeium-windsurf
  - more: redhat-java

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
  - wiki: prosemirror/tiptap
  - hocuspocus/typefox collab for file-tree/tabs
  - version-history for wiki/editor with ai commits messages
  - file/data-provider, 还可参考社区提供的另一种思路editor+mock-vscode-api
  - ui-skin as extension

- vscode提供了electron和web模式，未提供纯前端模式
  - vscode mobile

- ide-ai
  - editor-control MCP, 让ai操作编辑器的协议，可参考browser-use

- extension

- integrations
  - notion database

- 文件操作基于文件实现，如何基于数据库实现
  - 参考markdown-database的实现和数据同步
- 删除文件的回收站(基于git的回收站)

- markdown diff
  - preview diff

- 构建工具迁移到respack/vite

- ecosystem-bridged-to-zed
  - lsp

## ci/cd

- update-version/changelog这样的pr应该被自动化，人工只需要review，不需要敲繁琐的命令
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
