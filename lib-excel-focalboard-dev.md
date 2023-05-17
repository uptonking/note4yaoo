---
title: lib-excel-focalboard-dev
tags: [focalboard, notion-database, pivot-table]
created: 2022-03-16T20:44:07.289Z
modified: 2022-08-21T09:56:53.708Z
---

# lib-excel-focalboard-dev

# guide

- pros
  - notion-like database
  - 支持多种类型的字段
  - 数据模型专注于任务管理，以看板、卡片作为基础数据模型
  - 支持权限控制
  - 每一行可作为页面打开

- cons
  - 每个url只能显示一个database

- features
  - notion-like database
  - open source self-hosted project management tool
  - offline support with win/mac/linux client
  - Group, filter, and sort tasks
  - File sharing
  - Customizable templates
  - Archiving & back-up snapshots
  - User permissions
  - Multi-team views
  - more
    - some database features have mobile support
# design
- focalboard底层数据库设计包括 blocks/boards
  - block表拥有 boardId 属性与业务关联，还有type/fields
  - board表不直接与block相关，通过props和cardProps描述内容
# focalboard-rewrite
- goals
  - relicense => better-coding/pattern
  - local-first
  - more notion-like database views => list/gantt/timeline
  - flexible views
    - tabs/multi-tiles
    - dynamic-ref vs detached-copy
    - 通过detached-copy部分解决数据安全问题
  - tested headless react database view components
    - kanban
    - table
    - gallery/card
    - gantt
# focalboard-examples
