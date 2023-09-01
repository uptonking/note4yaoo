---
title: lib-viz-britecharts-dev
tags: [britecharts, charting, lib, viz]
created: 2021-05-27T19:57:55.517Z
modified: 2021-05-27T19:59:02.463Z
---

# lib-viz-britecharts-dev

# guide
- cons
  - 近年来维护不活跃

- pros
  - 基于d3 v5实现，属于较新的一批库，很多旧图表如c3、nvd3都不维护了
  - api的设计与d3很切近，链式调用
  - 内部实现与d3也很贴近，方便定制修改，如果不维护了，切换到d3代码也方便
  - 文档丰富
# issues
- ## [Make charts responsive by default](https://github.com/britecharts/britecharts/issues/110)
  - Right now, in our demos we use a small helper to debounce a listener to the 'resize' event of it's container. 
  - This makes it possible to redraw our chart and make it responsive. 
  - Any developer would need to do the same to get a responsive chart.
  - We could easily move that logic inside our charts, making the debounce delay configurable. Or even the method (debounce or throttle).
- I'm curious is it necessary to redraw chart on each resize? I mean scaling is the awesome feature of vector graphics and you can let the browser do the work for you
  - That's true, SVG scales great, but in the context of D3 visualizations, most of the positioning of the elements is 'absolute' and dependant on the data. That's why we need to re-render with new data or new dimensions.
- AFAIK, when you specify `viewbox` for svg element, all coordinates within it will be relative to a viewbox. Since viewbox height is larger than actual svg height, this rect will be displayed right in the middle. No matter its y coordinate is absolute and equals to the actual svg height.
  - that's a nice trick! However, I don't think it would scale into the size of elements a regular D3 chart has. Off the top of my head, I don't think this could be applicable to the axis.
  - yes, you're right about the axis. Still, you can handle them independently, for example, decrease count of ticks
# roadmap

## [Road to V3](https://github.com/britecharts/britecharts/issues/870)

- https://github.com/britecharts/britecharts/projects/2

- Priorities
  - TypeScript types √
  - Fix Color-related issues √
  - Streamline our bundles and dependencies √
  - Fix and standardize the locales √
  - Fix the security issues derived from our dependencies √
  - Remove all data-key setting accessors to make the data shape fixed √
  - Review our bugs to pick low hanging fruit that involves breaking changes
  - Update Britecharts React API

- not
  - update to d3 v6
# discuss
- ## Britecharts: D3.js based charting library of components_201705
- https://news.ycombinator.com/item?id=14307608
- Slightly off topic, but after discovering Vega, I can't quite imagine using a template based charting library again.
  - The declarative markup is interesting for custom datasets. But without some sort of UI builder it's unusable by clients
  - nvd3 and pretty much all charting libraries are built around the idea of charting templates. 
  - What Vega (and its simplified cousin Vega-lite) provide is a grammar for describing the mapping between the data space and the visual space.
  - What this essentially means is that you are able to build your own visualisations. If you for instance check this sample, and in the JSON editor, inside the "encoding" section you swap x with y, and y with x, then click on the parse button, the chart will be redrawn with the x and y axis flipped.
- Specifically, stacked against C3, Britecharts has a more 'D3-like' API, while C3 is a lot more declarative
  - his means that on C3, we will render charts by passing large configuration objects, while in Britecharts we strive to use a different API, chaining settings like we do on D3.
- When I scroll on iPhone on this example page, the chart keeps redrawing itself.
  - t seems scrolling is triggering a viewport resize, so we will review our viewport resize listener on the demos

- ## [Introducing Britecharts: Eventbrite’s Reusable Charting Library Based on D3_201704](https://www.eventbrite.com/engineering/introducing-britecharts/)
- API-wise, I see them more or less like this:
  - D3 —NVD3——Britecharts———Plottable—OOP———C3— Declarative
