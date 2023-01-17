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
  - rendering(~~web~~) is the future, but not the present.
  - 参考各种解决方案的优点，积累方案、算法、库、框架、应用
  - 深入一个项目: src-code, issues, pr, forks, extensions/alternative

- 技术方向js: 富文本编辑器，多维表格，协作
- 技术扩展js/py: 页面拖拽编辑器LowCode，Excel，图表
- 技术可选1: 画板，图形编辑器, pdf
- 技术可选2: olap，bi，数据工程，数据库

- 产品落地: 表格类笔记创作，运营数据仪表板，for jupyter/notebooks
  - share table/data pieces/snippets
- 团队版/企业版
  - 表单收集与统计，投票收集与统计，如features

## techstacks: rich-editor/builder

- design system
  - themeable; unstyled/headless; a11y/keyboard-ux
- text editor
  - modular/extensible; collaborative; easy-pivotable
  - block-editor with slash-menu/backlinks
  - pdf
- data table/grid
  - pivotable; collaborative; formulas
  - stream-updates/server-side-infinite-row-model
  - scripting/themeable/canvas/viztable/apache-arrow
  - ~~excel-like~~/~~headless~~

## solutions: inter(re)active knowledge-base/wiki

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
# editor
- tips
  - live edit
  - 随意搭建ui的需求过于灵活，而基于controls的在线配置编辑更实用; 有限定制组件+专题场景

- prosemirror
  - atlassian editor
  - rich-markdown-editor; outline
  - milkdown

- react-markdown-editor-lite
  - 基于textarea和React的markdown编辑器，实现简单且清晰，非所见即所得

- more-editor
  - google-docs-like-editor
  - monaco-editor
    - code editor that powers desktop vscode
    - not supported in mobile browsers. not for IE.
# list-grid-table
- tips

- leading
  - 微软 office/word/excel
  - 腾讯 文档
  - 字节 飞书

- react-table /tannerlinsley

- ag-grid /ag-grid

- luckysheet /bytedance

- more-list-grid
  - x-spreadsheet
  - tabulator 
  - frappe-datatable /frappe
# wishlist
- charting-viz
  - leading
    - d3
    - antvis
    - echarts
  - more-charting
    - vega

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
