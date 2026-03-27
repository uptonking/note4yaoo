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
  - 支持运行在多种环境，如 electron, web-memory, web-node-server, 
    - 提供了处理 cross-platform/browser 的参考架构
    - vscode对于本地c/s架构的参考价值高，web架构需要scale的价值不高
  - 💥 支持打开超大文件，而普通web-editor在编辑器卡死(如打开超大文件)时，容易造成整个页面不可用
  - 实现了很多git操作的ui和展示的ui，可作为git客户端
  - diff的计算较准确，支持可视化move操作
  - 对LSP的支持较好，能找到很多第三方LSP Server
  - 提供了很多原理深度解析的技术博客

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

- [VS Code: Open Source AI Editor _202505](https://code.visualstudio.com/blogs/2025/05/19/openSourceAIEditor)
  - [Open-source AI functionality provided by the Copilot Chat extension _202505](https://github.com/microsoft/vscode/issues/249031)
    - is agent mode also part of the open source plan?
    - yes, everything but ghost text completions
    - [Copilot Chat web support _202504](https://github.com/microsoft/vscode/issues/245860)
  - [Open Source AI Editor: Second Milestone _202511](https://code.visualstudio.com/blogs/2025/11/04/openSourceAIEditorSecondMilestone)
    - inline suggestions are now open source.
    - For the past few years, GitHub Copilot in VS Code has been split across two extensions: the GitHub Copilot extension (for ghost text suggestions) and the GitHub Copilot Chat extension (for chat and next edit suggestions). 
    - We are working towards providing all Copilot functionality in a single VS Code extension: Copilot Chat.
    - To achieve this, we are now testing disabling the Copilot extension and serving all inline suggestions from Copilot Chat. 
    - We have ported the vast majority of features into the chat extension
    - we now use inline suggestions to refer to all AI-generated code suggestions that appear as you type (including ghost text and next edit suggestions).
    - The next phase of our OSS journey is to refactor some AI features and components from the Copilot Chat extension into VS Code core. 

- pm-ai-vscode
  - 任何插件都可以使用其他插件的ai功能来修改文件和操作，可以互补，也可以转移成本
# draft
- toys
  - wiki: prosemirror/tiptap
  - hocuspocus/typefox collab for file-tree/tabs
  - version-history for wiki/editor with ai commits messages
  - github-like search for vscode

- roadmap-ai
  - acp
- roadmap
  - file/data-provider, 还可参考社区提供的另一种思路editor+mock-vscode-api
  - ripgrep for database
  - ext: comfyui
  - ui-skin as extension
  - 缺少一个好用且功能丰富的 pdf-viewer

- vscode提供了electron和web模式，未提供纯前端模式
  - vscode mobile

- vscode-ext-pattern
  - command-palette
  - editor
  - context-menu for editor/fileTree/toolbar
  - terminal

- ide-ai
  - editor-control MCP, 让ai操作编辑器的协议，可参考browser-use
  - mcp for drawio

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

- fileTree
  - 读文件的api/mcp 可以与 github公开的mcp-server 保持一致

## extensions-to

- vscode-knowledge-base
  - obsidian-like

- markdown-viewer
  - open in browser button
  - toc: auto highlight the title according to scroll position, by codemirror

- tables
  - obsidian-bases

- gitLens pro
  - gitLens for data/docs, **without vscode** 

- github repo的insights统计可实现为vscode扩展，如contributor/LOC-by-lang
  - 🔍 可在 git graph 的基础上实现，提供表格快速filter/group/合并author
  - 可参考 pingcap/ossinsight, chrome-history-trends

- file-tree
  - 类似github的目录视图，方便查看修改日期和commit-message

## ci/cd

- update-version/changelog这样的pr应该被自动化，人工只需要review，不需要敲繁琐的命令
# dev-xp
- themes
  - Github Light Default能将python的from-import渲染为不同颜色，Github Light不能
  - Github Light Default在import部分多褐色，Github Light多紫色

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
