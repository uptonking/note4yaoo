---
title: pm-office-wiki-datalking
tags: [datalking, pm, wiki]
created: '2021-08-07T19:56:54.345Z'
modified: '2021-08-07T19:58:20.142Z'
---

# pm-office-wiki-datalking

# guide

- 流行模版
  - 飞书知识空间模版
    - 研发部门、产品部们、市场营销、商业化
  - 语雀模版
    - 文档、表格、演示文稿、画板、数据表
  - [Confluence templates](https://www.atlassian.com/software/confluence/templates)
  - [Notion Template Gallery](https://www.notion.so/Notion-Template-Gallery-181e961aeb5c4ee6915307c0dfd5156d)
  - [Microsoft Office Templates](https://templates.office.com/)
  - [明道企业数字化Saas 模版库](ht tps://www2.mingdao.com/library.htm)
  - [腾讯文档 模版](https://docs.qq.com/mall/index)

- usecase
  - 技术文档
    - design: bootstrap、react-spectrum; atlassian
    - editor: prosemirror、tiptap、atlaskit; r-m-e,curvenote
    - list: ag-grid、react-table、luckysheet
    - viz: observable plot、britecharts
    - backend: loopback、dashboard、collab-server、grid-studio
  - 研发管理、分析报告
# 总体设计(暂时5大功能)
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
  - 不主推单篇文章的主题界面，而主推知识库
    - 观点的表达很难用一篇文章表达清楚，文章内容过长体验不好
    - 文件夹方便以后添加新内容和扩展，特别是引入资源文件和处理相对路径
    - observablehq的单片文章方便引用，但显得杂乱
    - 文件夹符合本地文件管理器的操作习惯，方便批量操作

- 存储层
  - files or sqlite

- 协作/同步
# 详细设计
- 适合存储在普通文本文件
  - 文章、速记
  - 代码

- 适合存储在sqlite
  - emails、calendar、tasks、photos

## 知识库/仓库/文件管理器

- core
  - 浏览文档
  - 编辑文档
  - 下载文档
  - 面向数据分析的文档/笔记本/notebook
