---
title: dev-log-repeat-solutions
tags: [dev, repeat, solutions]
favorited: true
created: '2021-01-08T00:10:18.987Z'
modified: '2021-07-20T13:50:23.433Z'
---

# dev-log-repeat-solutions

# guide

- tips
  - rendering(~~web~~) is the future, but not the present.
  - 参考各种解决方案的优点，积累方案、算法、库、框架、应用

- techstacks: rich editor
  - design system
    - themeable/headless/a11y
  - text editor
    - modular/extensible/collab
    - slashable-block
    - pictures and text wrapping
    - pdf
  - data table/grid
    - pivotable/formulas/stream-updates/server-side-infinite-row-model
    - scripting/themeable/canvas/viztable/apache-arrow
    - ~~excel-like~~/~~headless~~

- solutions: live/inter(re)active/reproducible doc
  - dashboard/spaces
    - themeable/configurable/widgets
  - wiki/knowledge-base/markdown-editor
    - offlineable/localizable; ~~local-first~~
    - portable format: markdown-based text format; no vendor lock in
    - collaborative
    - backlink/bidirectional: [[Wikilinks (stub)]],providing more context around backlink reference
    - relations:trilium-relation-map,trilium-link-map,dendron-hierarchical
    - interactive: collapsible, floating
    - scientific writing: latex, bibtex, citation，data
    - templates
    - es search-ui experience, algolia-docsearch/autocomplete
  - live-notebook
    - cell-style/nonlinear
    - reproducible
    - collaborative
    - easy pivot table in document
    - more: easy viz

- integrations/connections
  - wechat小程序、公众号、实时通知
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

- more-editor
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
