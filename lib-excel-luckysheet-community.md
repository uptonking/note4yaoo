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


- I will keep saying this every single time some one gets this wrong (which is at least 49 times out of 50): 👉🏻 the only way to handle scrolling properly on the web is for your `scroll` events to fall onto a real scrollable area, and to observe the effect it has (e.g. apply the scroll position to what you’re rendering with). 
  - This can be tricky to achieve well when you have dynamic content that the mouse needs to be able to interact with within that area, but it is possible to do well, with careful application of `position: sticky` and/or `position: fixed`.
  - As it stands, scrolling is nigh(几乎) unusable on my Surface Book: vertical scrolling goes at a million times the speed it should, and horizontal scrolling goes a million times as fast as it should in the wrong direction.
  - Don’t do scrolljacking. It’s bad, every single time. With the tools the web gives you it’s not possible to get it completely right that way.
- Absolutely. In the development process of our product DataGridXL we've also experimented a lot with "scrollwheel" events and such, for months really. It's just not possible to get it to feel natural. You might be able to get it working nicely on one specific OS+browser combo, but that's about it. 👉🏻 Always listen to the native "scroll" event
- You know your stuff, I can tell! In a pre-release version, we had hidden the native scrollbar and put our own scrollbar graphic on it that would animate using CSS transform according to native scroll offsets vs. DGXL viewport dimensions. The scrollbar size (width/height) and position made more sense, but at the end we couldn't get it to feel quite right.We're quite happy with the native scrollbar. It's fine on mobile too.
- The way I solved this in my own (not finished) web-based spreadsheet app is to have a scrollable div positioned over the canvas and to size the transparent div contents to the width/height of the sheet. Then I register scroll event handlers and redraw the canvas appropriately when the scroll changes. I think this is how Google sheets works, although it's a bit difficult to tell for sure.
- It seems difficult for a canvas-based spreadsheet to do native scrolling. The DOM is drawn in advance and there is no cost to scroll. But canvas is different, every frame of scrolling means calculation. In this case, the use of native scrolling will cause jamming and poor experience.









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
