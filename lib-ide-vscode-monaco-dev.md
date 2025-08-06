---
title: lib-ide-vscode-monaco-dev
tags: [code-editor, monaco-editor, vscode]
created: 2021-05-06T09:44:17.064Z
modified: 2024-08-24T16:16:15.959Z
---

# lib-ide-vscode-monaco-dev

# guide

- pros
  - diff的计算较准确，支持可视化move操作
  - 语法高亮支持超多语言，比codemirror多得多，一些小众语言也能找到高亮插件
  - 对LSP的支持较好，能找到很多第三方LSP Server

- cons
  - 不支持移动端

- features
  - monaco-editor未使用contenteditable，而使用隐藏的textarea接收输入

- who is using #monaco-editor
  - theia
  - ide: codesandbox, stackblitz, gitpod, molecule, opensumi, vscodium
  - gitlab
  - more: PlayCanvas
# dev

# more
