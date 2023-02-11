---
title: lib-collab-fluid-docs
tags: [docs, fluid-framework]
created: 2023-02-11T11:06:54.804Z
modified: 2023-02-11T11:07:05.558Z
---

# lib-collab-fluid-docs

# guide

# docs
- FluidFramework /4.2kStar/MIT/202302/ts
  - https://github.com/microsoft/FluidFramework
  - https://fluidframework.com/
  - Library for building distributed, real-time collaborative web applications
  - cons
    - 依赖中心服务器转发op及定顺序
    - 不支持长时间的offline，但只要保存op就可合并

- examples-官方示例，共用服务器tinylicious(npm run start:debug)
  - textarea示例未渲染协作鼠标
  - prosemirror示例是单页面多实例
  - shared-text是自定义编辑器，光标靠方向键移动，可显示协作用户光标
  - canvas画布示例是单页面多实例
  - canvas-data-object-grid示例支持在新标签页编辑部分画布元素，多页面
  - view-fwk-sampler使用了react/vue/vanillajs 3个示例
  - table-view提供了类似excel的示例，基于自定义table-document作为model
  - tips
    - 安装依赖用pnpm i

## overview

# more
