---
title: lib-list-grid-focalboard-codebase
tags: [codebase, focalboard]
created: 2022-03-16T20:47:15.710Z
modified: 2022-03-16T20:47:26.420Z
---

# lib-list-grid-focalboard-codebase

# guide

- 最新代码使用的是 go 1.18，server端无法编译通过
  - 从commit历史可以找到升级升级go之前的commit id
    - 8cefcd8e8cea70bd470ad0505d266ada4db91e2a
    - [v20220603](https://github.com/mattermost/focalboard/commits/main?after=e31821501c2d5f53329916b0ebd5165c09e480d8+69&branch=main)
  - 前端webapp开发历史记录
    - https://github.com/mattermost/focalboard/commits/main/webapp/src
# faq
- 删除或编辑卡片的操作，状态是如何变化、更新的？
  - 全局的数据操作通过调用全局的mutator方法
# 多维表格相关
- 视图切换原理
  - activeView.fields.viewType 支持 kanban/table/calendar/gallery 4种视图

- 多维表格各种视图的前端实现入口在 src/components/centerPanel.tsx
  - TopBar 最顶部，不能算作导航条，只有feedback/help
  - PageTitle
    - left: ViewTitle 页面标题
    - right: ShareBoardButton
  - ViewHeader 多维表格的表头组件
    - view dropdown with Editable view name 视图下拉列表
    - ViewHeaderPropertiesMenu 所有字段
    - ViewHeaderGroupByMenu 分组
      - ViewHeaderDisplayByMenu GroupName
    - FilterComponent 过滤
    - ViewHeaderSortMenu 排序
    - ViewHeaderSearch 搜索
    - ViewHeaderActionsMenu more actions
      - export .csv/.archive
    - NewCardButton add new row
      - new template (card)
      - insert card/row from template
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
- 前端整体结构
  - MainApp 传入reduxStore、处理用户初始化、首次连接websocket
  - App 准备ui相关Provider数据，IntlProvider/DndProvider
  - Router 基于路由守备定义了核心ui与路由对应的结构
    - /:boardId?/:viewId?/:cardId?
    - 所有核心路由对应的视图组件统一都是 `<BoardPage />` 组件

- webapp/src/pages/boardPage/boardPage.tsx 
  - 作为Workspace的入口
  - 注册了websocket事件处理函数、undo/redo快捷键

- 项目国际化方案比较
  - react-intl: focalboard, atlaskit-editor
    - 更多使用 FormattedMessage组件，或intl.formatMessage()方法
    - 翻译可集中定义
  - i18n-next: outline
    - 使用 useTranslation()返回的 t 方法，类似ckeditor
    - 翻译可集中定义
