---
title: pm-office-notion-database
tags: [notion-database, office, pm]
created: 2022-03-17T17:49:48.020Z
modified: 2022-03-17T17:50:05.384Z
---

# pm-office-notion-database

# guide
- features
  - Every item is its own editable page; customizable database pages
  - Customizable properties
  - Multiple views you can toggle between

- notion-cons
  - full page的多为表格无法删除，无法恢复到空白页
  - inline的database经常出现水平滚动条，然后删除不掉，从其他视图切回表格仍然显示水平滚动条

- 国内竞品
  - 飞书多维表格、vika维格表
- 国外竞品
  - airtable、notion-database

- [Airtable VS 多维表格 VS 黑帕云](https://zhuanlan.zhihu.com/p/434307680)
  - [Airtable、飞书多维表格、黑帕云 对比表/只读](https://canglang.feishu.cn/sheets/shtcnGVElCIwuYoVXicwwnzCyQg)
# features
- ✨️ 考虑多维表格中各标签页的数据不相关的场景，此时标签页只作为普通ui组件，作用类似折叠面板，只用来展示部分信息
  - 如何在多维表格标签页中支持数据无关的展示视图，如提供图例、描述说明

- ✨ 安全性
  - 飞书多维表格安全性特别高，一个对比表无法复制下来
# draft
- cell content auto convert to tag

- database as site 类似画册视图去掉边框，偏向页面
  - https://pwapp.net/
  - https://appsco.pe/
# obsidian-dataview
- 查询依据
  - 文件自带的元数据，如createTime
  - 手动添加yaml，如

- 查询语法，类似sql
  - 输出：list、table
# notion-database
- [Working with databases](https://developers.notion.com/docs/working-with-databases)
# notion-like-database
