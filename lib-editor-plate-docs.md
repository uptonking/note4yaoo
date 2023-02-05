---
title: lib-editor-plate-docs
tags: [docs, plate, slate-editor]
created: 2022-06-03T20:19:28.437Z
modified: 2023-02-05T19:03:12.721Z
---

# lib-editor-plate-docs

# guide

- plate /1.4kStar/MIT/202205/ts
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - A plugin framework for building rich text editors with slate.
  - ✨ Features
    - 编辑器开箱即用、功能丰富、架构比较稳定
      - 光标、选区、快捷键、拖拽
    - 提供了自定义plate插件系统和40+插件，方便自定义，可扩展
      - 还提供了可复用的编辑器相关资源，如slate操作operation
    - 支持多编辑器实例
      - A store is used to handle multiple editor out of the box
    - block支持拖拽改变顺序
    - 支持常用markdown快捷键
    - 支持嵌入各类媒体资源，如youtube、excalidraw
    - built with typescript
    - 分离了 plate-ui、plate-headless
  - 🐛 Drawbacks
    - 编辑器整体的技术选型比较opinionated
    - 状态管理使用jotai和类似redux的zustand
    - 未实现斜杠菜单
    - mention和悬浮工具条功能比较简单
    - table实现过于简单
    - 未实现多栏布局
  - plate的官方示例支持拖拽移动block，示例非常完整
    - Slate is a low-level editor framework that helps you deal with difficult parts when building an editor, such as events handlers, elements, formatting, commands, rendering, serializing, normalizing, etc.
    - `@udecode/plate` is built on top of slate to handle plugins and state management for an optimal development experience. 
    - This repository comes with a lot of plugins as elements, marks, serializers, normalizers, queries, transforms, components and so on.
    - `slate-plugins` repo has been renamed to `plate`.
    - The library formerly known as @udecode/slate-plugins is now available as @udecode/plate
    - [Generic typescript for slate](https://github.com/ianstormtaylor/slate/pull/4177)
      - I unfortunately don't have the time to complete that PR, so I've forked that PR into Plate.

- https://github.com/udecode/editor-protocol
  - Editor Protocol is an open standard for building a rich text editor. 
  - The protocol aims to cover all use-cases as there is no clear definition of what the standard should be.
  - Plate is an example framework that will follow the Editor Protocol.
# docs
