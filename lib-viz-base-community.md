---
title: lib-viz-base-community
tags: [community, viz]
created: 2021-06-30T10:55:27.273Z
modified: 2021-06-30T10:55:44.959Z
---

# lib-viz-base-community

# guide

- 可视化技术选型要考虑生态扩展和示例代码
  - github-search-js: echarts vs g2 = 4475 vs 1525

- https://www.data-to-viz.com/
  - From data to Viz | Find the graphic you need
  - 提供了6类数据的推荐图表：numeric、categoric、num-&-cat、maps、network、time-series
  - 样式非常友好
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 使用antv/G2生态半年有感_202112
- https://juejin.cn/post/7043068238539784206
- g2plot就是g2版本的echarts. 他降低了开发者的使用门槛
  - g2plot使用了g2, g2使用了component. 实际上, component还依赖了其他的antv的库
- 在一些第三方库的使用过程当中, 社区活跃度是非常重要的. 
  - 在G2的使用过程中, 根据我自己的观察和自己的体验, 官方回复效率比较慢. 大量issue处于无人问津的状态.
- G2生态算是比较不错的图表库的, 文档质量谈不上特别好, 凑合看吧, 基本上能解决业务问题
  - 源码的技术架构还挺有意思的, 值得去研究. 不过代码质量我个人感觉一般, TS的类型校验使用的比较一般. 一大堆函数没有返回值、参数没有类型等

- ## echarts 数据可视化
- https://wuchengran.com/2020/02/27/charts/
- 优秀的 UI system 有很多共通的地方：
  - 底层操作是命令式（dom 操作、canvas、webGL）;
  - 封装时大多会遵循的原则: MV**、 单向数据流、自定义事件 eventEmitter

