---
title: job-projects-yaoo
tags: [job, projects, yaoo]
created: '2021-09-21T19:45:54.152Z'
modified: '2021-09-21T19:47:30.211Z'
---

# job-projects-yaoo

# configurable-dashboard 仪表板

- goals
  - 简单易定制的仪表板/管理界面
- tasks
  - 布局
  - 路由配置
  - 登录状态、鉴权状态
- actions
  - bootstrap v4
  - react-router
  - rbac
- results
  - 实现了管理界面
  - 实现了全局数据流
  - 实现了路由鉴权
- 进一步的工作
  - 可复用的组件
  - 依赖升级
# materials-repo 资料库
- goals
  - 为离线优化的文档资料系统
- tasks
  - 网盘文件操作
  - 页面小程序创建
  - 文档浏览导航
  - 文档编辑
- actions
  - 基于仪表板模版实现了类似网盘的文件操作与管理系统
  - 基于动态加载实现了markdown文档转换成小程序
  - 基于prosemirror和rich-markdown-editor实现了文档在线浏览，支持滚动高亮当前编辑目录标题
- results
  - 网盘基本功能已实现
  - 任意文件夹可以资料小程序网站的形式打开
  - 文档浏览体验很方便，类似excel里面切换多张工作表
- 进一步的工作
  - 直接在前端请求网盘中sqlite单文件数据库中保存的数据，因为observable笔记本在推、geojson -> geopackage
  - markdown文档的解析目前很简陋，需要定制的front-matter，针对中文优化空格、字体等
  - 文档编辑需要提高性能
# prospect-garden-design
- goals
  - 可灵活复用的样式和组件
- tasks
  - css, 组件库
- actions
  - 基于style-dictionary实现了design tokens，定义了一系列的json对象，可输出各种格式
- results
  - 基于第三方css实现的设计系统不够标准、规范
- 进一步的工作
  - 不使用虽然的样式值，统一迁移到基于bootstrap的样式值和交互模式
# prosemirror-editor

# didact: react-like library
- goals
- tasks
- actions
- results
