---
title: lib-excel-luckysheet-community
tags: [community, luckysheet]
created: 2021-05-06T09:56:41.040Z
modified: 2022-08-21T09:57:42.969Z
---

# lib-excel-luckysheet-community

# discuss

- ## 

- ## 

- ## [hacker news: Luckysheet, an open-source spreadsheet ](https://news.ycombinator.com/item?id=23994619)
- One reason I prefer Apple Numbers to Excel is that in Numbers you arrange tables on a canvas. 
  - The tables can refer to each other. 
  - I think it makes it easier to work with, for example, an input table and an output table because they are separate entities and not just different ranges on the same grid. 
  - It’s similar to how some websites enable you to configure a dashboard view of multiple tables and charts.
  - I’m wondering if the Numbers approach might work better. 
  - In particular it might be more natural for dynamic arrays because they would not “overlay” a range of cells.
  - They would be their own dynamically resizing table on the canvas.
- The main reason I tend to avoid Google Sheets is that they're slow. Slow to open, slow to update more complex sheets

- ## [Feature request]精简数据结构
- https://github.com/dream-num/Luckysheet/issues/418
- 通常excel导入后数据量会膨胀很多倍，
  - 方案一是pako压缩，
  - 再者，Luckysheet的本身数据也可以做优化，因为有许多配置是重复的，考虑写一个转换引擎作为前置插件，获取到用户操作类的配置，走插件转化为Luckysheet可识别的格式

- 我目前的做法是后端只保存表头跟开始行的数据结构，其余行的数据根据开始行这一行的数据结构，在前端去遍历组装。这样数据量就少很多很多

- ## 10 powerful Google Sheets formulas advanced users should know
- https://twitter.com/benlcollins/status/1511054363363524621
- 1) QUERY
- 2) SPARKLINE
