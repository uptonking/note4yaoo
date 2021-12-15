---
title: editoe-features-kanban
tags: [editoe, features, kanban, pm]
created: '2021-11-29T08:24:19.539Z'
modified: '2021-11-29T08:25:19.337Z'
---

# editoe-features-kanban

# guide
- features
  - ~~切换 列表视图、看板视图~~
  - 从看板创建文档
  - 看板日程
  - emoji
  - actionsLog，查看操作记录

- 看板主要参考
  - trello、飞书、worktile、tower
  - [trello card api](https://developer.atlassian.com/cloud/trello/rest/api-group-cards/)
  - [trello object definitions](https://developer.atlassian.com/cloud/trello/guides/rest-api/object-definitions/)

- 参考notion database的设计，将文档看板做成通用多维表格的一个可复用模板
# 看板的设计与实现
- 看板的结构
  - Board -> CardListGroup -> Card

## 导出功能

- [Making sense of Trello's JSON export](https://help.trello.com/article/924-making-sense-of-trellos-json-export)
  - 在看板工具条的最右侧 show menu菜单 -> More -> Print and export
  - https://trello.com/b/qoBz7TLE/hello-trello
  - 导出的json文件 https://trello.com/b/qoBz7TLE.json

## ux设计

- worktile
  - #eef3fc
  - #e8edf7

- 一个面板的布局
  - trello
    - 顶栏，左边标题单击重命名，右边更多图标显示菜单列表
    - 卡片列表
    - 底栏，左边添加卡片，右边从模板创建卡片
  - tower
    - 顶栏，左边面板中卡片数量、面板名称，右边添加新卡片图标、更多图标
    - 卡片列表
    - 底部是添加新任务卡片的按钮
  - worktile
    - 顶栏，面板名称，任务进度(已完成、进行中、未开始)
    - 进度条
    - 卡片列表
    - 底部是添加新任务卡片的按钮
  - 飞书看板
    - 顶栏，左边看板名称、任务数量，右边更多菜单
    - 卡片列表
    - 底部是添加新任务卡片的按钮

- 任务卡片布局设计
  - trello
    - 卡片最顶部可显示封面
    - 卡片顶部可以有彩色标签条
    - 卡片默认只显示标题，卡片描述内容只显示指示图标
    - 卡片底部可以显示完成/过期日期、描述图标、任务进度、附件数量
  - tower
    - 顶部是标签
    - 主体是标题
    - 事件日期
  - worktile
    - 标题
    - 任务状态
    - 截止时间
    - 左侧优先级竖条
  - 飞书看板
    - 标题
    - 标签
    - 备注

- hover卡片的交互
  - trello
    - 显示原地编辑的图标，原地编辑的弹窗效果有蒙版层类似dialog
  - tower
    - 左边优先级竖条、左下截止日期，右上操作菜单、右下选择负责人
  - worktile
    - 卡片阴影
  - 飞书看板
    - 卡片显示蓝色边框

- click卡片的交互
  - trello
    - 弹出卡片详情弹窗
  - tower
    - 弹出卡片详情弹窗
  - worktile
    - 弹出卡片详情弹窗
  - 飞书看板
    - 弹出卡片详情弹窗

- 卡片详情弹窗布局设计
  - trello
    - 顶栏，显示标题、所属列表
    - 标签
    - 描述
    - 操作记录：如评论
    - 右边可选择添加自定义字段到卡片
      - 成员、标签、清单、日期、附件、拉伸
      - 自动化按钮
      - 操作：复制、分享、移动
  - tower
    - 顶栏，是否完成任务复选框
    - 是否完成任务复选框、标题
    - 负责人、截止时间、优先级
    - 标签
    - 所属看板
    - 描述
    - 附件
    - 子任务
    - 操作记录
    - 评论
    - 通知设置
  - worktile
    - 顶栏，子任务数量，操作菜单
    - 标题栏
    - 任务状态、负责人、开始时间、截止时间
    - tab： 任务信息、子任务、附件
    - 评论
  - 飞书看板
    - 顶栏，左边任务名，右边上一个任务、下一个任务、
    - 标签
    - 备注
    - 隐藏字段
    - 状态
    - 评论

- 面板内是否该出现滚动条？
  - 整页占满屏幕，单个面板内卡片过多时，一直会显示滚动条
    - tower
    - trello 宅屏幕显示水平滚动条
  - 整页占满屏幕，单个面板内卡片过多时，鼠标进入面板列才会会出现滚动条
    - worktile
    - 飞书看板
# 竞品参考

## [tower看板](https://tower.im/help/articles/295)

- tower-pros
  - 粘贴多段文本到一个新的任务卡片时，会自动创建多个卡片

- tower-cons
  - 任务卡片不支持复制粘贴
  - 任务卡片上的文字不支持单击编辑
  - 不支持显示子任务数量和完成进度

- 看板features
  - 结构：面板(流程阶段) + 卡片(任务)
  - 任务卡片支持 优先级、封面、自定义字段
  - 不同面板本身就可以分组任务，一个面板内的任务支持二次分组，如按优先级、负责人
  - 自定义显示字段，批量改变卡片显示信息的详细程度
  - 任务筛选过滤
  - 看板整体统计页
  - 任务封面

- 列表features
  - 类似excel，支持列排序、修改列宽、列内容过滤
  - 丰富的字段类型：文本、数字、单选、多选、超链接
  - 自定义字段类型
  - 多维度组合筛选过滤
  - 将过滤结果保存为新视图
  - shift批量操作，批量管理任务
  - 导入excel中的数据为列表视图
  - cons
    - 不支持显示内层子任务

- 看板与列表的对应关系
  - 每一个看板都是一个任务清单
  - 面板归档、删除

- ref
  - [tower视频教程](https://space.bilibili.com/511589939/video)
  - 任务三要素：描述、负责人、完成时间
