---
title: lib-excel-tanstack-table-codebase
tags: [codebase, lib, tanstack-table]
created: 2020-08-21T09:01:31.263Z
modified: 2022-08-21T10:19:58.756Z
---

# lib-excel-tanstack-table-codebase

# guide

- tanstack-query
- tanstack-virtual
# not-yet
- e.persist()
  - getToggleSortingHandler
# codebase
- table和virtual都用到了react forceRender模式

- createTable 的初始化流程
  - 计算插件options，~~合并feature options~~
  - 添加插件initialState到全局initialState
  - 合并coreInstance到table
  - 逐个执行插件的createTable方法，并更新table

- 一个feature的设计
  - 添加到table options
  - 在table、column、header暴露api
# virtual
- 固定高度的原理
  - 在目标区域上下方显示invisible元素高度和

- 动态计算内容元素高度的原理
  - 利用callback ref在首次渲染时计算元素高度
  - 首次渲染时注册scroll事件，让滚动时执行
