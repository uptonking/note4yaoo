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
  - [明道企业数字化Saas模版](https://www2.mingdao.com/library.htm)

- usecase
  - 技术文档
    - bootstrap、react-spectrum
    - prosemirror、tiptap、atlaskit
    - ag-grid、react-table、luckysheet
    - backend: loopback、dashboard、collab-server、grid-studio
  - 研发管理、分析报告
# 总体设计(暂时6大功能)
- 主页/工作台/最近动态 dashboard
- 知识库/文库集合/仓库/批量操作 wiki lib
- 知识空间/文件夹集合/管理空间 spaces
  - 文章/笔记/随记 pages/articles
  - 素材/资源/图片/附件/数据 attachments
- 收藏/标签 bookmarks
- 分享/协作 sharing
- ~~数据 data~~
- 回收站 trash
# 详细设计

## 知识库/仓库/文件管理器

- core
  - 浏览文档
  - 编辑文档
  - 下载文档
  - 面向数据分析的文档/笔记本/notebook
