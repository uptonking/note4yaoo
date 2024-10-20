---
title: lib-saas-overleaf-codebase
tags: [codebase, overleaf]
created: 2024-10-19T09:28:09.211Z
modified: 2024-10-19T09:28:20.354Z
---

# lib-saas-overleaf-codebase

# guide

- codeEditor(文本)和visualEditor(WYSIWYG)都基于codemirror.v6实现
  - services/web/frontend/stories/source-editor/source-editor.stories.tsx
  - 两个编辑器支持同步滚动和随光标自动滚动到对应位置

- DocumentDiffViewer的实现参数只有2个，doc代表最新文本内容，highlights包含add/del的范围
  - services/web/frontend/stories/history/document-diff-viewer.stories.tsx
  - 默认渲染视图是add范围显示为蓝背景，del范围显示黄色中划线
  - 每个变更块支持显示tooltip
  - [ ] 每个变更快未实现accept/reject

- pdf的预览基于pdfjs实现

- storybook开源的示例
  - diff-viewer
  - fileTree, outline/toc
  - pdf preview
  - chat
# architecture

# codebase

## codeEditor

- 使用了官方扩展、fork过官方扩展、实现了很多自定义扩展，总共100+扩展
  - services/web/frontend/js/features/source-editor/extensions/index.ts
  - codemirrorDevTools, trackChanges, bracketSelection, mathjax, thirdPartyExtensions

- source-editor支持codemirror6/ace(deprecated)
  - https://github.com/overleaf/ace /202108/js/inactive/Ajax.org Cloud9 Editor

## visualEditor

## collab

- 基于sharejs.v0.5魔改实现，未使用官方collab插件
  - https://github.com/overleaf/overleaf/tree/main/services/document-updater/app/js/sharejs /202205/MIT/js

## scaling

- 🫧 [Horizontal Scaling: Starting with version 3.5.6 Server Pro supports horizontal scaling _202305](https://github.com/overleaf/overleaf/wiki/Horizontal-Scaling)
  - A deployment of Server Pro with horizontal scaling involves a set of external components, such as a Load Balancer and an S3-compatible backend
  - 💰 [We do a customer-taylored capacity planning as part of our Enterprise Solution, Overleaf Server Pro _202009](https://github.com/overleaf/overleaf/issues/784)
# more
