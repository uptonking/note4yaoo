---
title: editoe-prd-pivot-table
tags: [editoe, features, pivot-table]
created: 2021-12-07T05:10:28.280Z
modified: 2022-07-21T04:11:08.550Z
---

# editoe-prd-pivot-table

# guide

- features
  - required-features
    - modular with rich features
    - extensible and customizable
      - headless / inversion of control
    - typescript by default -> strongly typed
    - zero dependencies
  - 多种视图切换
    - 可能的亮点：支持在同一文档中显示多次，这多个视图会同时更新
    - 比如先在前面显示高优先级的任务，然后在下面显示所有任务列表
    - 修改一处数据源，所有视图同时更新
  - 常用操作：过滤、排序、分组
  - 自定义字段名称、类型、显示隐藏
  - row as page
  - diff CompareTable
  - collapsible cell, not only row
  - database-first的体验，但体验不到可以的database，如文件夹切换列表、平铺视图
  - 批注视图，方便展示presentation，对标miro
  - 可能的亮点
    - optional pivot-table from ul/li
      - 解决需要通过斜杠菜单唤起创建菜单的问题
    - resizable/zoomable
      - 表格可作为整体缩放大小
    - 表格视图分身，可以复制视图和配置
      - 分身的表格会和原表格数据联动，但直接复制的表格不会
      - 分身的表格数据联动但配置不联动，如分身表格可以有单独的组字段
    - diff视图
    - 可离线使用
      - 表格数据可单独导出，但不可导出分组视图，只能导出数据表
    - 交互元素丰富，如图片、折叠展开
    - 分组聚合分析：上卷下钻
    - configurable table，提供快速配置面板
    - 文档内的表格支持分页，方便快速定位
  - 表格小亮点
    - 全局和每个字段的过滤、排序、分组
    - 字段类型转换
    - 图片支持
    - 支持分页
    - 支持 pin rows/columns
    - 支持合并单元格
  - 待定
    - server side 表格，开发适合服务端取数和更新的数据模型

- 多维表格主要参考
  - 飞书多维表格
  - notion database
  - github issues看板
  - clickup
  - 其他
    - tower、worktile
    - [github看板示例](https://github.com/orgs/toeverything/projects/1/views/4?layout=table)
    - [在飞书多维表格使用智能导入](https://helpdesk.feishu.cn/hc/zh-CN/articles/360049067854)
    - [飞书多维表格接入指南](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/bitable/notification)
      - 目前开放多维表格在App、数据表、视图、字段以及记录 5 种内容的 API 

- why react-table
  - powerful
  - headless
  - popular: github issues

- 参考notion database的设计，将文档看板做成通用多维表格的一个可复用模板

- https://notionpages.com/
# 多维表格产品的设计和实现
- notion使用体验
  - 当databse是full page的时候，难以删除，复制粘贴

## 问题讨论

- 🤔 全局菜单
  - 排序
  - 过滤
  - 分组
  - 新建视图
  - redo
  - undo
  - 全部配置，如默认每页元素数量

- 🤔 每列菜单
  - 要不要显示本列的类型图标
  - 排序
  - 过滤
  - 分组
  - 列相关操作：隐藏、插入、修改样式

## 问题已解决

- 🤔 直接在单元格编辑数据，还是在弹窗中编辑一行的数据
  - 🔈 提供2种编辑方式
  - 看板类产品大多在弹窗中编辑
  - 但对短文本直接在单元格中编辑更符合用户需求
  - notion在所有行的第一个文本列的末尾，hover时会显示悬浮按钮，点击时可打开本行内容详情弹窗并编辑
  - 飞书多维表格会在每行开头显示 拖动、复选框、详情3个按钮，点击详情会打开弹窗

- 🤔 单击单元格的行为
  - 🔈 单击时只选择而不编辑
  - github单击会选择单元格，再单击单元格就可直接在看板中修改issue标题、修改值
  - notion单击时，可直接编辑文本单元格和标签单元格
    - notion单击时，首先触发的是正在编辑的单元格失焦
  - 飞书多维表格单击会选中单元格
    - 对文本类型单元格，先单击选中，然后双击单元格才可修改内容，长文本会展开
    - 对下拉菜单类型的单元格，也是先选中，再单击修改单元格内容
  - worktile单击可修改单元格，或弹出当前行的卡片
  - tower单击可修改单元格

- 🤔 分组样式的设计
  - 🔈 偏向多个明显的子表格
  - 偏向单个表格

- 🤔 表格样式实现的问题
  - 🔈 暂时只用css
  - 表格的样式不太适合jss实现样式
    - 直接用css，在_app.js的文件中import
    - 用jss

- 🤔 目前实现的看板场景太具体
  - 🔈 先实现具体的，再考虑通用的；如github看板的场景就很具体
  - 字段名称和类型都是提前定义好的，应该在当前项目改，还是开新项目
  - 可以在当前项目实现将看板转换成列表，花费很多时间，但通用性不强
- 🤔 字段是预定义的，还是动态创建的
  - 🔈 先实现预定义的，后期再改为可配置，动态创建

- 🤔 表格的样式？视觉上单表格？视觉上多表格？
  - 🔈 视觉上多表格其实是通过分组实现的，取消分组字段后就是普通表格

- 🤔 多维表格在公司产品中的使用场景或定位
  - 🔈 根据初版代码的实现效果决定是深入还是废弃
  - 作为workspace的一部分？独立的产品？全局的产品？ 都需要自定义字段

## 多维表格开发计划

- 多维表格开发计划
  - 普通文本字段
  - 全局排序
  - 全局过滤
  - 全局分组
  - 创建新视图
  - 自定义字段
  - 所有字段全部自定义
  - 多维表格插入文档
  - 多维表格的协作
# 多维表格产品的设计
- 目标功能
  - 多种视图切换
    - 看板、表格
  - 常用操作：排序、过滤、分组
  - 自定义字段
  - 多人协作
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

- notion-cons
  - full page的多为表格无法删除，无法恢复到空白页
  - inline的database经常出现水平滚动条，然后删除不掉，从其他视图切回表格仍然显示水平滚动条

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
