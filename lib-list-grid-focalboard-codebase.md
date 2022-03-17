---
title: lib-list-grid-focalboard-codebase
tags: [codebase, focalboard]
created: '2022-03-16T20:47:15.710Z'
modified: '2022-03-16T20:47:26.420Z'
---

# lib-list-grid-focalboard-codebase

# guide

- 多维表格前端实现入口在 src/components/centerPanel.tsx
  - activeView.fields.viewType 支持 board/table/calendar/gallery 4种视图

- 项目国际化方案比较
  - react-intl: focalboard, atlaskit-editor
    - 更多使用 FormattedMessage组件，或intl.formatMessage()方法
    - 翻译可集中定义
  - i1n-next: outline
    - 使用 useTranslation()返回的 t 方法，类似ckeditor
    - 翻译可集中定义
