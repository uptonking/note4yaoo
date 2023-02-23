---
title: lib-editor-wangeditor-dev
tags: [slate-editor, wangeditor]
created: 2023-02-22T19:48:08.263Z
modified: 2023-02-22T19:49:14.823Z
---

# lib-editor-wangeditor-dev

# guide

- features
  - L1级编辑器，以slate作为模型层数据结构
  - model与view分离，模块化的架构
  - 使用扩展插件和模块的机制，保证扩展性
  - 内置丰富模块，无需大量二次开发
  - view层没有与具体框架绑定
  - 中文友好

- cons
# codebase

- dev-to
  - link异常
  - image异常

## not-yet

- 状态与视图
  - view > state >view

## overview

- init-default-config
  - 注册了toolbar、hoverbar相关的各种配置
# dev

# docs

- 编辑器主要功能
  - 内容处理 - 获取内容，设置内容，展示内容
  - 编辑器API - 控制编辑器内容和选区
  - 编辑器配置 - 兼听各个生命周期，自定义粘贴
  - 工具栏配置 - 插入新菜单，屏蔽某个菜单等
  - 菜单配置 - 配置颜色、字体、字号、链接校验、上传图片、上传视频等
  - 扩展新功能 - 扩展菜单、元素、插件等

- 自定义扩展新功能
- core 是核心 API ，editor 负责汇总集成。所有的具体功能，都分布在各个 module 中来实现。
- 注册新菜单
- 劫持编辑器事件和操作（插件）
  - 如支持 markdown 语法，以及 ctrl + enter 回车等
- 定义新元素
  - 如果你想让编辑器渲染一个新元素，如 附件 数学公式 链接卡片 等，你就需要根据本节内容来定义。

- 默认可支持中文和英文，默认为中文。

- 可以通过 CSS vars 定义自己的主题

- 架构设计

- editor模块引入 core ，引入各个 module ，然后根据用户配置，最终生成一个编辑器。
  - 配置组装与初始化

- core严格来说应该叫做“view core”。它基于 slate.js 内核，完成编辑器的 UI 部分。
- editor - 定义 slate 用于 DOM UI 的一些 API
- text-area - 输入区域 DOM 渲染，DOM 事件，选区同步，
- formats - 输入区域不同数据的渲染规则，如怎样渲染加粗、颜色、图片、list 等。可扩展注册。
- menus - 菜单，包括 toolbar、悬浮菜单、tooltip、右键菜单、DropPanel、Modal 等。可扩展注册。
- core 本身没有任何实际功能。需要通过 module 来扩展 formats、menus、plugins 等，来定义具体的功能。

- core 没有任何基础功能，所有功能都是 module 来扩展实现。
- menu
- formats
  - renderElement
  - addTextStyle
- plugin（即 slate plugin）
