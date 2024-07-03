---
title: watarble-dev
tags: [dev, watarble]
created: 2022-11-24T11:39:02.440Z
modified: 2022-11-24T11:39:26.000Z
---

# watarble-dev

> have data and insights at your fingertips

# guide

# goals
- powerful editing
- dom-based view, simple and enough
- crdt

- 兼容主流数据格式, 如docx/xlsx
# dev-to

# dev-later
- devtools like ckeditor/lexical-editor

- ~~将ClientId改为actorId~~，client更通用
# dev-maybe

# usecase

- 文件列表及搜索，很适合切换为多维表格的交互
# codebase
- 数据库第一次构建索引会很慢
  - 思路1: 持久化索引来快速还原，参考BST的序列化和反序列化
  - 思路2: 对特定类型的字段，提前构建索引，如多选字段、日期字段
