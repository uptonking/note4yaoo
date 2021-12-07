---
title: editoe-features-pivot-table
tags: [editoe, features, pivot-table]
created: '2021-12-07T05:10:28.280Z'
modified: '2021-12-07T05:12:27.586Z'
---

# editoe-features-pivot-table

# guide

- 问题讨论
  - 目前实现的看板场景太具体
    - 字段名都是提前定义好的，应该在当前项目改，还是开新项目
    - 可以在当前项目实现将看板转换成列表，花费很多时间，但通用性不强
  - 多维表格在公司产品中的使用场景或定位
    - 作为workspace的一部分；独立的产品； 都需要自定义字段
  - 字段是预定义的，还是动态创建的
# 多维表格产品的实现思路
- 不支持直接在单元格编辑数据，要在弹窗中编辑一行的数据
# 多维表格产品的设计
- 目标功能
  - 多种视图切换
    - 看板、表格
  - 常用操作：排序、过滤、分组
  - 多人协作
  - 自定义字段
  - 一行数据可以打开成一个单独的文档/页面
  - 可嵌入形式的实现，如插入到文档
  - 提供api

- 非目标功能
  - 不做excel的复杂公式、函数
  - 不做excel
  - 表单提交

- 待定功能
  - 日历、日程视图
  - 看板卡片封面
  - 基本统计功能：sum, avg, median, min, max, range
  - table app store，如在单元格中放图表、树状图、网状图，集成日历、审批等工作流
# 竞品参考

## 飞书多维表格

- features
  - 规范化：结构化数据字段
  - 一键切换5种视图
    - 表格、看板、甘特图、画册平铺视图、表单
    - 用画册视图直观查看含有图片、视频或其他文件附件的记录。
    - 画册视图中展示的缩略图即为添加到附件字段列的图片或文件
  - 分组、排序、筛选过滤
  - 实时协作
  - 视图自动更新

- 使用场景
  - 项目、资料、门店、客户、招聘

- [快速玩转飞书多维表格](https://www.feishu.cn/hc/zh-CN/articles/360049067678)
- 多维表格是一款以表格为基础的新一代效率应用，融合了在线协作、信息管理和可视化能力
- 多维表格的每一行被称为「记录」，每一列被称为「字段」。
  - 每列字段的数据格式是固定的，保证你输入的数据规范有序。
  - 多维表格提供丰富的字段类型，满足你在表格中插入多样信息的需求。
  - 每列的数据类型可以为：多行文本、单选、多选、人员、日期、附件、数字、复选框、公式、单向关联、双向关联等。
- 视图代表信息的展现形式。
  - 在飞书多维表格中，你可使用5种视图整理同一份数据。
  - 每新建一个视图，就等于为该份数据新增了一个展现、汇总形式。
  - 编辑任一视图中的数据信息，都将实时改变该数据源的其他视图。

## notion database

- features
  - Every item is its own editable page; customizable database pages
  - Customizable properties
  - Multiple views you can toggle between

- There are three things that distinguish Notion databases from spreadsheets and databases you can build with other software:
  1. Every item is its own editable page:
     - Every item you enter into your database can be opened as its own Notion page, where you can layer in any information you want.

  2. Customizable properties:
     - Add properties to contextualize, label and augment any database item with more information, like dates, people, text, links, etc.

  3. Multiple views you can toggle between: 
     - Your data isn't stuck in a table. 
     - View the exact same database as a **board, list, calendar, gallery, and timeline** — whatever makes the information most useful. 

## airtable

- features
  - Views
  - custom interfaces
  - Automations: integrate your tools, run custom code, and more

## vika 维表格

- features
  - 视图切换
  - 丰富的字段类型
  - 协作

## [nocodb](https://docs.nocodb.com/)

- features
  - Rich Spreadsheet Interface
  - App Store for workflow automations
  - Programmatic API access via REST/JWT
