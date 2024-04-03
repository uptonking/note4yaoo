---
title: lib-saas-nocodb-dev
tags: [cms, lowcode, nocodb, pivot-table]
created: 2023-01-22T18:44:46.312Z
modified: 2023-12-15T16:51:49.971Z
---

# lib-saas-nocodb-dev

# guide

- pros
  - open source with AGPLv3
  - 🛢️ 支持已有数据库，不需要import data
  - ✅ 支持rename table/field
  - ✅ rich-fields: rich-text, Formula, Links, Lookup, Rollup
    - 支持custom field, 基于json
  - rich-views: grid, kanban, gallery, form
  - app store支持在线安装discord/mail
  - ✨ 支持Group: supports three levels of record segregation
  - 支持拖拽自动填充单元格
  - 支持cell级别的comment
  - 支持attachment
  - Audit: We are keeping all the user operation logs under one place
  - 支持undo/redo

- cons
  - 👀 不支持拖拽调整row顺序和拖拽row内容，但支持拖拽调整column顺序
  - 不支持在任意位置插入row, 支持在某一列前后插入列
  - 表格的产品形式对于长文本的编辑和展示不友好

- features
  - 表格默认处于编辑状态
  - Multiple Views Types: Grid (By default), Gallery, Form View and Kanban View
  - View Permissions Types: Collaborative Views & Locked Views
  - Access Control with Roles : Fine-grained Access Control at different levels
  - App Store for Workflow Automations
  - Audit: We are keeping all the user operation logs under one place

- tips
  - 动态关联数据的缺点是难以实现行级别的undo/redo，且架构复杂
# draft

# dev-xp
- 用户在界面上创建表时，数据库层也会添加一张新表, 表名前缀 nc__k4v___/nc_rbby___/nc_r12u__

- 支持rename table/field, db中的表名和字段名也会变化
# 💰 [pricing](https://github.com/orgs/nocodb/projects/13/views/2)
- [What is available in free version ?](https://docs.nocodb.com/faqs/#what-is-available-in-free-version-)

- 🆚️ NocoDB has just one version that is free & open source.
  - In it you will notice advanced features are all available for free
  - ACL; Collaboration; Views; Share; protected; Automations
  - And we would never move these features from free to an enterprise version of NocoDB.
  - There is no limitations to number of projects, records or fields either.

- Do we plan to have an Enterprise Edition?
  - SSO, SLA, Organisation wide reports and analytics, 
  - Advanced Audit or ACL, 
  - Bespoke implementations & integrations, 
  - A hosted solution.

- How do we decide if a feature is Enterprise or not ?
  - Depends on the effort and whether the intended users are enterprises.
# more
