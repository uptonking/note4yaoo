---
title: thread-gis-examples-mapping-carto
tags: [carto, examples, gis, mapping, thread]
created: 2021-03-26T11:29:28.403Z
modified: 2021-08-16T06:45:26.099Z
---

# thread-gis-examples-mapping-carto

# pieces

- ## 

- ## 

- ## 五一准备去哪
- https://twitter.com/sun0225SUN/status/1778210771874578773
  - 小红书地图

- ## Farewell, orange highways. 
- https://twitter.com/dbabbs/status/1729550577841877169
  - Gray and blue now rule the cartography scene, as 6 of the top digital map providers all use a shade of gray or blue to represent highways.
  - Just like UI design, cartography design trends seem to converge every few years.
- Introduction of gray/blue highways in each map:
  Google - 2023
  Mapbox - 2023
  HERE WeGo - 2021
  Apple - 2021
  Meta / FB - 2022
  Uber - 2018
- The remaining holdouts that have yet to converge: Waze, Bing/Azure, and Amazon AWS

- our reasoning: orange/yellow highways pulled visual attention from full color place iconography we were adding and clashed with our new global landcover layer. our map is also heavily focused on pedestrian + social use cases.

- To show you some different perspectives: Map providers in China 
  - P1 百度地图(Baidu Map) P2 天地图(Tianditu) P3 Gaode(Amap) P4 Tencent(QQ), P5 Sogou, P6 Google (As control group)

- ## 有没有友友知道这种图怎么做. 浅灰白背景上建筑立体凸起
- https://twitter.com/Jackywine/status/1660121948381229063
- Probably Rayshader or ArcGIS
  - 见过用QGis做的
- 在unity 里可以新建一个很大的地图，然后导入转为黑白的地形高资料图，然后对照卫星图用笔刷工具绘制绿色草地等贴图。其他地方绘制白色、蓝色贴图即可。最后把主光源设置好，添加一个看板标签即可。
- dem做个阴影再叠加底图就差不多了，一模一样的需要仔细微调。
- 游戏里称为，灰度图
- 现在可以试试看midjourney啥的。

- ## Voronoi World Map 100% made with #Javascript & #d3js.
- https://twitter.com/neocartocnrs/status/1383025241434247169
  - https://observablehq.com/@neocartocnrs/world-grids
  - 由小多边形拼接成的世界地图，可在三角形、正方形、六边形、voronoi多边形几种实现中切换
  - 泰森多边形又叫冯洛诺伊图（Voronoi diagram）

- ## Powering China’s coal to clean transition with actionable analytics
- https://turning-the-supertanker-cn.transitionzero.org/
  - /storystelling-map

- ## A US map using a hexagon shape to represent the states. 
- https://twitter.com/Highcharts/status/1382106532477861893
  - /amazing
  - 全是六边形构成的地图，提供了三种主题
  - https://www.highcharts.com/demo/maps/honeycomb-usa
  - https://codepen.io/uptonking/pen/bGgMBGr

- ## [Let's Sketch a Map](https://observablehq.com/@neocartocnrs/lets-sketch-a-map)
- 可控制边框粗细、详略程度

- ## https://observablehq.com/@neocartocnrs/world-elevation-line-map
