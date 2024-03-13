---
title: lib-excel-undb-dev
tags: [excel, undb]
created: 2023-05-17T07:35:48.070Z
modified: 2023-05-17T07:36:07.757Z
---

# lib-excel-undb-dev

# guide

- pros
  - 支持多种类型的字段
  - 支持高级字段，如 reference/lookup field
  - 每一行作为弹窗打开，不支持行内编辑

- cons
  - 不支持undo/redo
  - 只支持sqlite，不支持pg/mysql
  - 每个url只能显示一个table
  - 用户每新建一张表，就会在数据库中创建一张物理表

- features
  - private-first / self-hostable
  - multiple built-in field types
  - multiple views, including grid, kanban, tree, calendar and more

- kanban-examples
  - https://github.com/orgs/sequelize/projects/1
  - https://github.com/orgs/chakra-ui/projects/3
  - [How Notion uses Notion – Notion Template Gallery](https://www.notion.so/templates/categories/how-notion-uses-notion)

- 桌面版
  - 不支持刷新页面恢复状态
# dev-to
- 数据库重构
  - 用户的每张表并不需要对应数据库中物理表，可使用triple store

- 将trpc迁移到rtk-query

- 表格视图
  - 去掉ui依赖
  - 重构为可复用组件
  - absolute position
  - 透视表、database多视图、编辑器内的database
  - editable-react-table、undb/focalboard、noseditor
# dev-later
- 去掉table概念，将field作为最底层基础block
  - 将table只视为field的一种具体组合，field还可以组合为kanban/tree

- cleanup
  - disable attachment(-field)
  - 去掉react-hook-form devtool
  - [x] 去掉loadable-component

- 支持event sourcing架构

- 统一enum的const和类型定义的命名和位置
# dev-maybe
- column-virtualizer

- board-insights
- across-board
# codebase
- undb底层数据库设计包括 table/field/view/attachment
  - 每个table保存了 views_order
  - 每个view保存了 fields_order

- 前端一张表，对应数据库中的一张表

- 前后端模块
  - 共用的模块 core/cqrs/i18n
  - 前端的模块 store-redux, trpc-def
  - 后端的模块 db-sqlite, trpc-def

- 状态管理
  - 服务端缓存使用rtk-query，如table/field数据
  - 前端非持久化状态使用jotai，如弹窗开关、initialValue、lastOpened
# faq-not-yet
- ❓ 在表的中间位置插入row/column时顺序如何决定
  - 插入column时，更新view表的fields_order字段
  - 插入row时，更新
# faq
- 只使用了getCoreRowModel，那么sort/group是如何实现的
  - 每次调整顺序都会从数据库重新全量取数
# design
- 看板整体布局的结构
  - 可以总体为一行，每列包含顶部列标题、当前列内容卡片
    - 案例: github-project-board, wekan,undb,dnd-kit,react-beautiful-dnd
  - 可以总体为两行，第1行展示每列标题，第2行展示每列内容卡片
    - 案例: focalboard
# dev

# docs

- Undb tables function like spreadsheets in that you can sort, filter, aggregate your data and modify many other table features. 
  - In contrast to standard spreadsheets, Undb lets you see tables in several ways as a grid of rows and columns, Tree diagram, form, calendar, or kanban boards.

- A table consists of rows and fields (columns).
  - In a table, a field is a collection of values of the same data type. 
  - Each field is a data structure that holds a defined data type.

- Basic table field types are the different data types that can be stored in a table, such as text, numbers, and dates, and are used to classify and manage data effectively.

- The system field are used to record system information, including the creation and modification times, the creator and modifier’s names, etc. 

- Reference Field
  - 1-1: 比如商品-二维码
  - 1-N: hasMany，比如店铺-商品二维码
  - N-N: 比如商品-类别标签
- Relationships between table records can be established by using `LinkToAnotherRecord` column type.

- Lookup Field
  - Lookup fields are read-only fields. 
  - When creating a lookup field you can choose a ‘Link to table’ field in the same table and a field in the related table.
  - Start by creating a link to table field before using a lookup field.
- The Count field is used to count the number of matching entries in the referenced table for the unique key (foreign key) referenced by the current row. 
# more

# discuss

- ## 

- ## 

- ## 

- ## From a quick look at the code, it appears you only support sqlite right now. Do you plan to support postgres? _202310
- https://discord.com/channels/1095348405749952604/1120844973366067341/1160968073868750889
- I agree with your point that supporting all databases would require a lot of effort with little benefit. 
  - nocode database data often cannot be easily converted to real db data, so our inclination is to support a single database. 
  - The reason for choosing SQLite is its simplicity in terms of getting started and deployment, and its natural support for offline usage. For some simple applications and private deployment scenarios, SQLite is sufficient. 
  - Currently, our plan is to explore distributed database solutions compatible with SQLite, such as rqlite. Another option is to provide limited support for both SQLite and MySQL (PostgreSQL) databases.
