---
title: toc-viz-d3
tags: [d3, toc, viz]
created: 2020-07-13T03:01:35.250Z
modified: 2020-10-22T10:23:02.892Z
---

# toc-viz-d3

# echarts
- https://github.com/ggntju/chart-helper
  - Open Source Cross-Platform Desktop Client for Apache ECharts
  - Chart Helper uses JSON as data exchanging format. 
  - 依赖echarts、react、semantic-ui、electron
- https://github.com/violetiu/yuanliu
  - 跨平台的原型设计工具，目前以设计桌面原型为主。
  - 支持echarts库，实现丰富的图表，也可以手动绘制。
  - 原型可导出为html演示版、vue版、react版和数据库备份
  - 内置git、sftp工具，团队协同、实时发布轻松搞定
# d3-chart
- https://github.com/c3js/c3
  - /8.9kStar/MIT/202008
  - A D3-based reusable chart library
- https://github.com/novus/nvd3
  - /7.1kStar/Apache2/201806
  - http://nvd3.org/
  - A reusable charting library written in d3 v3
  - NVD3 is recommended to go with d3.js version 3.5.3 and later, but NOT d3 4.x yet
- https://github.com/proteus-h2020/proteic
  - /39Star/Apache2/201808
  - a general purpose data visualization library built for both static and streaming data.

- narrative-chart /42Star/BSD/202208/js
  - https://github.com/narchart/narrative-chart
  - visualization library specialized for authoring charts that facilitate data storytelling with a high-level action-oriented declarative grammar.
# d3-fwk
- deepscatter /186Star/MIT/202301/ts
  - https://github.com/nomic-ai/deepscatter
  - This is an evolving library for displaying more points than are ordinarily possible over the web.
  - 依赖apache-arrow, d3-zoom, regl, rbush-3d
  - All data is sent in the Apache Arrow `feather` format, in a custom quadtree(四叉树) format that makes it possible to only load data as needed on zoom
    - This is a 2d library. No fake 3d.
    - The central zoom state is handled by d3-zoom.
  - Most rendering is done in custom layers using WebGL, with a buffer management strategy handled by `regl`. 
  - Almost all grammar-of-graphics transforms such are handled on the GPU, which allows for interpolated transitions with calculations done in parallel.
# d3-app
- https://github.com/paulhoughton/mortgage
  - /202Star/MIT/201902
  - Mortgage overpayment calculator using React and D3
  - 可以修改部分预设值，然后图表立即更新
  - http://paulhoughton.github.io/mortgage/
- https://github.com/g1eb/calendar-heatmap
  - /160Star/MIT/201808
  - This d3.js heatmap representing time series data is used to visualize tracked time over the past year, showing details for each of the days on demand.
  - https://github.com/DKirwan/calendar-heatmap
# d3-geo
- https://github.com/d3/d3-geo
  - /637Star/BSD/202009
  - Geographic projections, spherical shapes and spherical trigonometry.
- https://github.com/yaph/d3-geomap
  - A library for creating geographical maps based on D3.js
# d3-pieces
- https://github.com/uwdata/d3-tutorials
  - D3 Tutorials for CSE512 Data Visualization Course at University of Washington

- https://github.com/Swizec/d3blackbox
  - A simple React wrapper for any D3 code you want
- https://github.com/zhangzn3/D3-Es6.git
  - D3 力导向图 增删改动态更新数据 点击生成节点 拖拽生成连线
- https://github.com/d3/d3-hexbin
  - Group two-dimensional points into hexagonal bins
  - 六边形网格
- https://github.com/ufoe/d3js-geojson
  - 包含世界地图、世界主要国家及中国详细省、市、县数据。
- https://github.com/d3-node/d3-node
  - https://bradoyler.com/projects/d3-node/
  - Server-side D3 for static chart/map generation
- https://github.com/alexandersimoes/d3plus
  - extends D3.js to enable fast and beautiful visualizations
- https://github.com/gregjopa/d3-server-side-demo
  - uses D3.js to render visualizations on the server-side with Node.js.
- https://github.com/Caged/d3-tip
  - d3 tooltips
- https://github.com/joelburget/d4
  - d4 is an experiment in using React to produce data-driven documents (ala d3)
- https://github.com/sujinleeme/data-visualization-experiments
  - https://sujinleeme.github.io/data-visualization-experiments
  - making interactive visualization applications and integrating D3.js in React. 
  - Additionally, I used recharts library to make bar and line graph.
- https://github.com/e2d3/e2d3
  - JS library for using D3.js on Excel 2013 or Excel Online
