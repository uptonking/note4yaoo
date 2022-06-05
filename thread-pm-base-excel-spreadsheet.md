---
title: thread-pm-base-excel-spreadsheet
tags: [excel, pm, spreadsheet, thread]
created: '2022-04-23T18:47:38.924Z'
modified: '2022-04-23T18:48:32.550Z'
---

# thread-pm-base-excel-spreadsheet

# discuss

- ## 

- ## 

- ## 

- ## 

- ## Really powerful UI for working with relational databases! Nesting tables to represent joins is really clever.
- https://twitter.com/ccorcos/status/1520273524161581057
  - [Ultorg at the 2022 HYTRADBOI Database](https://vimeo.com/695905306)

- ## The biggest reason Excel is the most popular layfolk programming language is that its UX and IDE is miles miles miles better than any other language
- https://twitter.com/hillelogram/status/1525217533518831621
- This is probably true but we should emphasize that the UX is mostly driven by the spreadsheet concept, rather than particular details about Excel.
- It also makes program state extremely visible, something that I think PLs generally don’t think about much. Not saying the idea wasn’t there, eg, with smalltalk, but excel goes way beyond.
- Arguably the UX comes down to just having a visible location for a value, rather than the idea of a constant or variable held in a named location off screen.

- ## Need a versatile function that can make static spreadsheets fun & interactive? It’s gotta be the 🔥 IF function 🔥
- https://twitter.com/GRID_hq/status/1524796293004107776

- ## The QUERY function: the most powerful and versatile spreadsheet function in existence.
- https://twitter.com/benlcollins/status/1521528069105893378

- ## EXCEL 是你最被忽视的设计工具
- https://twitter.com/nishuang/status/1519558823622680581
  - 这些美观、易用的数据可视化图表和控制台面板，都是用 EXCEL 设计的
  - 作者是数据可视化专家，介绍了利用形状、图片、图标、文本和色彩、特殊的图表样式，在 EXCEL 里进行设计。他还顺便卖模板

- ## I feel like so many tools for "building interactive apps in a spreadsheet" end up struggling w/ the same problem: how to fit side effects and async computations into the simple spreadsheet model of reactivity.
- https://twitter.com/geoffreylitt/status/1516904903184060416
  - The spreadsheet model is awesome: data updates, pure formulas re-evaluate, the whole sheet is consistent, nice.
  - But what happens when a cell can "do something" when it updates?
  - You can try to fit it more closely into the existing spreadsheet model, or you can bolt on an events/triggers system... these days I tend to think a separate event system is more straightforward. Jotted some notes on different approaches
- Asynchrony is also tricky. Even if your computation is pure, if it's slow and async then you have two options:
  - a) refreshing the spreadsheet is slow
  - b) you can partially refresh the spreadsheet, now the sheet is no longer guaranteed consistent at any given time
- Feels like many of the challenges in UI and state management frameworks boil down to answering these kinds of questions. 

- @observablehq seems to handle it well!
