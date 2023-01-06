---
title: editoe-latest-changelog
tags: [changelog, editoe]
created: 2021-10-23T18:07:10.580Z
modified: 2021-10-23T18:07:42.972Z
---

# editoe-latest-changelog

# guide

# feedback

## [Editoe v0.6 版本规划__202104](https://github.com/toeverything/editoe/issues/215)

- 协作
  - 支持 Team/Organization 管理
  - 支持内容版本控制

- 内容创作
  - 块引用
  - 经典内容模版
  - 视频插入外链

- 专业内容
  - mermaid模版按钮
  - 数学公式 + 图片 + 表格 标号
  - 支持自动补全 + WYSIWYG 的数学公式编辑 (类似于 Mathcha)

- 格式转换
  - 支持导入 .tex
  - 支持导出 .tex

- 交互增强
  - 飞书文档式菜单栏
  - 新功能通知

- 数据监控
  - 易观方舟

## [Editoe v0.5 版本规划__202102](https://github.com/toeverything/editoe/issues/2)

- 协作
  - 支持内容分享
  - 支持同屏协作

- 内容创作
  - 补足尚未支持的markdown语法
  - 可在 Sidebar 中完成文档和文献的完整 创建，移动，删除 使用流，抛弃 文档/文献 大页。
  - 双栏模式
  - 分页
  - 分章
  - 脚注与边注
  - shaded box？

- 专业内容
  - 类似 draw.io 的 GUI 绘图插件

- 格式转换
  - 支持多种常见导入格式：.doc .markdown .tex
  - 支持多种常见导出格式: .doc .pdf .tex .markdown

- 交互增强
  - 用户第一次使用，悬浮气泡教学指引
  - Safari/Firefox 浏览器兼容
# changelog

## v0.6.0__202103

- 页面添加Sidebar组件。
- Markdown导入导出功能。
- 实现Plotly实时更新。
- Timeline添加创建、删除文件夹功能。
- 侧边栏实现触控移动。

- 修复后退失效

## v0.5.0__202102

- 时间轴添加创建文件夹功能。
- 登录页面样式重构。

- 兼容Safari和Firefox浏览器。Safari浏览器忽略Authorization header。
- 右键唤醒toolbar会被遮挡。

## v0.4.0__202102

- 上线数学公式符号面板。
- 上线Plotly绘图工具。
- 添加功能介绍文档。
- Mermaid实时更新编辑。
- 图床验证回调。
- 实现Bitex导入文献。

## v0.3.0__202102

- Editoe中植入Plotly。
- 编辑页面实现双向链接和引用文献。
- Toolbar完善。
- Timeline组件完善。
- 实现多页面数据同步。
- 在线数学环境唤起。

## v0.2.0__202102

- 实现引用唤起列表的嵌套。
- 实现权限效验跳转页面。
- 添加文件导航展开合并按钮。
- 浏览器document title同步。
- 实现微信登录。
- 增加用户行为上报功能。

## v0.1.0__202102

- 完成文献页创建表格的开发。
- codeblock添加语言图标。
- 只引入所需语言highlight.js的包。
- 修复无序列表无法唤起的bug。
- 修复了文档/文件夹、文献/文献夹的一些bug。
- 实现右键菜单插件（粘贴功能暂时没有实现）
- 实现全局标题样式更改插件。
- 更换了新 Logo。
- 增加 Loading 页面。
- 首页的功能介绍组件的开发 + 窄屏适配。
