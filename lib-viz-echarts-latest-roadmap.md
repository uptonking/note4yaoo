---
title: lib-viz-echarts-latest-roadmap
tags: [echarts, roadmap]
created: 2023-02-08T15:05:25.373Z
modified: 2023-02-08T15:05:45.715Z
---

# lib-viz-echarts-latest-roadmap

# guide

# roadmap

# changelog

- [版本记录 - Apache ECharts](https://echarts.apache.org/zh/changelog.html)

## v5_2020-12-03

### [v4 升级 v5 指南](https://echarts.apache.org/handbook/zh/basics/release-note/v5-upgrade-guide/)

- 代码库迁移为 TypeScript
- 支持了状态切换时的过渡动画。这能提供更好的视觉效果，尤其比如当常见的部分图形元素因为被“高亮/淡出”时。

- 在大部分情况下，我们都推荐大家尽可能用这套新的**按需引入**，
  - 它可以最大程度的利用打包工具 tree-shaking 的能力，并且可以有效解决命名空间冲突的问题而且防止了内部结构的暴露
  - `CanvasRenderer`将不再被默认引入，这样可以保证只需要使用 SVG 渲染模式的时候不会把不需要的 Canvas 渲染代码也一起打包进来
- v5移除了内置的 geoJSON（原先在 echarts/map）
- 配置项调整
  - v4 中，visualMap 组件 中生成的视觉样式（如，颜色、图形类型、图形尺寸等）的优先级，比开发者在 itemStyle | lineStyle | areaStyle 中设置的样式的优先级高
  - v5 调整了 rich.?.padding 的格式使其更符合 CSS 的规范

- 不再推荐使用的 API
  - position、scale 和 origin 仍然支持，但已不推荐使用。
  - 除了 Text 元素之外，其他元素中的属性 style.text 都不推荐使用了。取而代之的是新属性 textContent 和 textConfig，他们能带来更丰富的功能。

## v4_2018-01-16

- v4变更为流式结构，并且配合各种细致的优化，对于大数据量的渲染场景，支持了增量加载数据和渐进渲染。支持最高达千万级数据量渲染。
- ZRender SVG 渲染引擎发布，从而支持 Canvas/SVG 双引擎渲染，可进按照场景所需进行切换。
  - 例如，SVG 可适用于移动端、单页多图表等场景，Canvas 适用于大数据量、视觉特效需求等场景。
  - Canvas 渲染引擎仍为默认引擎。
- 新增 dataset 组件，从而能够数据与样式分离，便于单独管理数据，支持数据映射到视觉配置，可以多个系列共享数据，也省去数据分割处理的步骤。
