---
title: dev-log-repeat-solutions
tags: [dev, pm, repeat, solutions]
favorited: true
created: 2021-01-08T00:10:18.987Z
modified: 2021-07-20T13:50:23.433Z
---

# dev-log-repeat-solutions

# guide

- tips
  - rendering(~~web~~) may be the future.
  - 涉猎saas解决方案，积累方案、算法、库、框架、业务模版
  - 深入一个项目: src-code, issues, pr, forks, extensions/alternative, most-commented-issues
  - 抽空在线体验，工作专注代码

- 技术方向js: 富文本编辑器，多维表格，协作
- 技术扩展js/py: 支持拖拽的页面编辑器/LowCode，Excel，图表
- 技术可选1: 画板，图形编辑器, pdf
- 技术可选2: olap，bi，数据库，大数据工程
- 技术可选3: vscode，可参考设计 extensions、capabilities

- 🚀 产品落地
  - 表格类内容创作与管理
  - 运营数据仪表板
  - sharing table/data pieces/snippets
  - 个人数据管理，开放api，允许其他app获取
  - tags

- 生态与集成
  - office365，从 word/excel 复制粘贴的表格，如果其中有合并的单元格，也能支持正常展示
  - jupyter-notebook
  - observable-notebook

- enterprise-marketplace
  - browser-extensions
  - figma
  - table-capture/shot
  - ocr

- 团队版/企业版-features
  - 表单/投票收集与统计，如features
  - 编辑器内的时间变化动态表格
  - 类似多个图表facet的多个表格
  - table in table
  - 移动端优化的表格

## techstacks: rich-editor/builder

- design-system
  - themeable; unstyled/headless; a11y/keyboard-ux
- editor/WYSIWYG
  - modular/extensible; collaborative; easy-pivotable
  - 👉🏻 prosemirror, tiptap, textbus, typewriter, slate, lexical; cms
  - block-editor with slash-menu/backlinks
  - pdf
- excel/data-grid
  - pivotable; collaborative; formulas
  - 👉🏻 tanstack-table, ag-grid, luckysheet/univer; nocodb
  - stream-updates/server-side-infinite-row-model
  - scripting/themeable/canvas/viztable/apache-arrow
  - ~~excel-like~~/~~headless~~
- collab
  - 👉🏻 yjs, rga, fluid-framework, hlc

## solutions: inter(re)active knowledge-base/wiki

- ✨ cms(content-mgmt)
  - 👉🏻 payloadcms  (MIT/mongoose+slate)
  - 👉🏻 nocobase(apache2/sequelize+umi)
  - outline    (apache2/sequelize+prosemirror)
  - directus      (AGPL/knex+vue3+tinymce5)
- ✨ airtable-like(data-mgmt)
  - 👉🏻 nocodb     (AGPL/knex+nuxt3)
  - apitable      (AGPL/spring-mybatis+canvas)
  - focalboard    (AGPL/go+react-dnd)
  - undb          (AGPL/nestjs+mikro-orm+dnd-kit/table)
  - locokit        (MIT/knex+vue2)
  - rowy       (apache2/firebase+tinymce5)
  - baserow        (MIT/django+nuxt2)
- ✨ workflow
  - n8n           (AGPL/typeorm+vue2+jsplumb)
  - budibase      (AGPL/knex+svelte)
  - automatisch   (AGPL/knex+graphql+slate)
- ✨ bi
  - 👉🏻 lightdash   (MIT/knex+echarts)
  - superset   (apache2/flask+echarts)

- ✨ admin-dashboard
  - react-admin
  - tremor
- ✨ editor-wiki(web+pc)
  - outline
  - notesnook
  - mdSilo

- features
  - local-first/offlineable/localizable
  - collaborative
  - easy pivot table in document
  - interactive-contents: variable, attachment, viz
  - backlinks/bidirectional: [[Wikilinks (stub)]], providing more context around backlink reference
  - relations: trilium-relation-map, trilium-link-map, dendron-hierarchical
  - scientific writing: latex, bibtex, citation，data
  - rich-ui: collapsible, floating, emoji
  - portable format: text format; no vendor lock in; partially export cuz mobile
  - templates
  - es search-ui experience, algolia-docsearch/autocomplete

- byproduct-apps
  - live/reactive-notebook
    - cell-style/nonlinear; reproducible/computational; math
  - dashboard/spaces
    - themeable/configurable/widgets-blocks

- integrations/connections
  - wechat-miniapp、公众号、实时通知
  - github/gitee
  - 腾讯文档
  - 类似outline集成slack
  - 类似superset支持各种数据源
# ideas
- editor/ide-settings sync/store/sharing
- comments
  - 编辑态评论
  - 阅读态评论
  - 分享态评论

- excel
  - apache-arrow
# editor
- tips
  - live edit
  - 随意搭建ui的需求过于灵活，而基于controls的在线配置编辑更实用; 有限定制组件+专题场景

- leading
  - 微软 office/word/excel
  - 腾讯 文档
  - 字节 飞书

- prosemirror
  - atlassian editor
  - rich-markdown-editor + outline
  - milkdown

- react-markdown-editor-lite
  - 基于textarea和React的markdown编辑器，实现简单且清晰，非所见即所得

- more-editor
  - google-docs-like-editor
  - monaco-editor
    - code editor that powers desktop vscode
    - not supported in mobile browsers. not for IE.
# excel
- tips

- react-table /tannerlinsley

- ag-grid /ag-grid

- luckysheet

- more-list-grid
  - x-spreadsheet
  - tabulator 
  - frappe-datatable /frappe
# wishlist
- charting-viz
  - leading
    - echarts
    - d3
    - vega
  - more-charting
    - antvis

- faves
  - design: adobe-spectrum, tailwind
  - editor: prosemirror, codemirror, gutenberg
  - geomapping:mapbox-gl, leaflet
  - geoviz:deck.gl
  - geoprocessing:turfjs, mapnik
  - geo: gdal, esri，计算工具大部分都基于cpp

- design-system
  - tips
  - material
  - carbon
  - spectrum
  - ui: material-ui, ant design, atlaskit , theme-ui, bootstrap
  - design-tokens: polaris-tokens

- dashboard
  - tips
    - 实际仪表板常与业务紧密相关，建议结合window-layout和drag实现
  - coreui
  - creativetim
  - olap(js intensive)

- layout/window-manager
  - tips
    - 常作为app的基础组件
  - golden-layout: 场景丰富功能全面的window
  - elara: demo示例非常酷，特别是layer，dashboard, shell, pic-viewer
  - ventus: 快速切换到窗口平铺预览
  - rc-dock: 类似ide的拖拽停靠效果
# fundamentals
- format
  - excel/csv/office open xml
  - markdown
  - pdf
  - json

- rendering
  - canvas
  - webgl
  - animation
    - FLIP
