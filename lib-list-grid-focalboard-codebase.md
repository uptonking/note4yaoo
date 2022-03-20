---
title: lib-list-grid-focalboard-codebase
tags: [codebase, focalboard]
created: '2022-03-16T20:47:15.710Z'
modified: '2022-03-16T20:47:26.420Z'
---

# lib-list-grid-focalboard-codebase

# guide

# faq
- 删除或编辑卡片的操作，状态是如何变化、更新的？
  - 全局的数据操作通过调用全局的mutator方法
# 多维表格相关
- activeView.fields.viewType 支持 board/table/calendar/gallery 4种视图

- 多维表格前端实现入口在 src/components/centerPanel.tsx
  - TopBar page header
  - title block
    - left: ViewTitle
    - right: ShareBoardButton
  - ViewHeader
    - view dropdown with Editable view name
    - ViewHeaderPropertiesMenu
    - ViewHeaderGroupByMenu
      - ViewHeaderDisplayByMenu GroupName
    - FilterComponent
    - ViewHeaderSortMenu
    - ViewHeaderSearch
    - ViewHeaderActionsMenu more actions
    - NewCardButton add new row
  - view Kanban
  - view Table
  - view CalendarFullView
  - view Gallery

## Kanban

- Kanban jsx vdom
  - 顶层是 scrolling div
  - board header
    - visible KanbanColumnHeader
    - hidden message
    - add group button
  - board body
    - visible KanbanColumn
    - hidden KanbanHiddenColumnItem

- KanbanColumn
  - 一个简单的容器div

- KanbanCard
  - 状态管理
    - 会从 useAppSelector 中获取全局数据
    - 全局的数据操作通过调用全局的mutator方法
  - 操作菜单工具条
    - 删除、重复、复制链接
  - card icon + title
  - visiblePropertyTemplates => PropertyValueElement
  - CardBadges
  - OpenCardTourStep / CopyLinkTourStep

## Table

- table-cons
  - 不支持删除行
# codebase
- 项目国际化方案比较
  - react-intl: focalboard, atlaskit-editor
    - 更多使用 FormattedMessage组件，或intl.formatMessage()方法
    - 翻译可集中定义
  - i18n-next: outline
    - 使用 useTranslation()返回的 t 方法，类似ckeditor
    - 翻译可集中定义
