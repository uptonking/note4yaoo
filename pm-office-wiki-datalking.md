---
title: pm-office-wiki-datalking
tags: [datalking, pm, wiki]
created: 2021-08-07T19:56:54.345Z
modified: 2021-08-07T19:58:20.142Z
---

# pm-office-wiki-datalking

# guide

- usecase
  - 技术文档
    - design: bootstrap、react-spectrum; atlassian
    - editor: prosemirror、tiptap、atlaskit; r-m-e,curvenote
    - list: ag-grid、react-table、luckysheet
    - viz: observable-plot、britecharts
    - backend: dashboard-api、collab-server、grid-studio
  - 分析报告

- 技术实现
  - 存储层考虑主流方式，如sqlite、S3、fake-s3这类易兼容的格式
# 功能设计
- 文档格式
  - 以流行的gfm markdown为主
  - 考虑后期不依赖具体的文件格式，使用json/rpc协议

- 类似文档网站、文档阅读器
  - 提供熟悉的文档阅读和编辑体验
  - toc目录、书签视图
  - 文章评论、批注
  - 不同点
    - 文档目录/文件目录支持外部链接
    - 文章目录支持自定义标签、图标
    - 阅读快捷键：j、k、gg

- 类似网盘
  - 提供便捷的文件操作，如移动、拖拽、上传下载
  - 切换多种文件显示模式，如列表、详情、平铺
  - 不同点
    - 专门的文档小程序视图，会显示文档目录而不是a-z排序
    - 网盘文件通常支持按时间、按首字母排序，支持拖拽移动，但不支持拖拽排序；拖拽排序来指定文档目录顺序
    - 就地文件树方便快速导航
    - 支持在限额之内下载文件夹

- 类似github
  - 以repo为核心提供丰富的功能和扩展
  - git pages，支持指定文件夹作为文档浏览小程序的根目录
    - 甚至支持创建多个小程序，支持共用公共资源
  - 支持discussion、issues、pr/suggestion
  - 支持actions自动更新引用文本块或数据
  - 支持sponsor、paid-only-access
  - 支持references by; contributors
# 总体设计(核心5大功能)
- 主页/工作台/最近动态 dashboard
- 知识库/文库集合/仓库/批量操作 wiki lib
- 知识管理/知识空间/文件夹集合/管理空间 spaces
  - 文章/笔记/速记 pages/articles
  - 素材/资源/图片/附件/数据 attachments
- 标签/收藏夹 bookmarks
- 协作/分享 sharing

- ~~数据 data~~
- 回收站 trash

- non-goals
  - 不主推单篇文章的主题界面，而主推知识库、资料库、资源库
    - 观点的表达很难用一篇文章表达清楚，文章内容过长体验不好
    - 文件夹方便以后添加新内容和扩展，特别是引入资源文件和处理相对路径
    - observablehq的单篇文章方便引用，但显得杂乱
    - 文件夹符合本地文件管理器的操作习惯，方便批量操作
- discussion
  - 主推浏览，还是主推编辑？

- 存储层
  - files or sqlite
  - 考虑多种存储方式结合

- 协作/同步
# 详细设计
- 适合存储在普通文本文件
  - 文章、速记
  - 代码

- 适合存储在sqlite
  - emails、calendar、tasks、photos
# keyboard-shortcuts
- edit

- nav
  - cmd/win+k: spotlight command menu 弹出式命令菜单

## 知识库/仓库/文件管理器

- core
  - 浏览文档
  - 编辑文档
  - 下载文档
  - 面向数据分析的文档/笔记本/notebook
