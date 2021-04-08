---
title: viz-chart-solutions-products
tags: [charting, products, solutions, viz]
created: '2021-04-08T12:15:44.953Z'
modified: '2021-04-08T12:16:54.274Z'
---

# viz-chart-solutions-products

# solutions

## d3

## vega

- ### [Vega and D3](https://vega.github.io/vega/about/vega-and-d3/)
- Vega is not intended as a “replacement” for D3. 
  - D3 is intentionally a lower-level library.
  - D3 is intended as a supporting layer for higher-level visualization tools. 
  - Vega is one such tool, and Vega uses D3 heavily within its implementation.

- Vega provides a higher-level visualization specification language on top of D3.
  - we intend Vega to be convenient for a wide range of common yet customizable visualizations. 

# discuss

- ## [如何评价蚂蚁金服新一代数据可视化引擎 G2 ？](https://www.zhihu.com/question/46474722/answers/updated)
- 17年的时候很看好这个，在图形语法的复现上，坐标系部分的实现在当时是一个很大的亮点。
  - 当时虽然很多实现不太理想，但是种种迹象给人的感觉是G2未来会是一个完成度很高的图形语法实践
- “图形语法”是一个很美好的梦想，现实是G2在一些语法的灵活性带来优势的的地方却复现的不太好，如algebra表达式，分面。
  - 图形语法理论诞生的比较早了，起初主要是描述静态可视化，而现代可视化中的交互联动、动画等元素在当时都尚未吸引人们太多的关注。
  - 后来，随着交互式可视化，可视化动画技术的成熟与很多优秀案例的涌现，人们希望像图形语法的思想中获得的种种便利一样，能在交互式的可视化、借助动画做可视化叙事上都能获得类似的便利。
  - 由于缺乏既有成熟理论的指导，同时对创新能力的和对新问题研究的方法要求就要高的多，G2在这一块的表现一直相对保守与乏力。
- G2在前沿领域一直处于掉队状态。
  - G2花了很多精力在对于一线业务可视化的支持上，很多需求是各种样式灵活度的需求，事件灵活度的需求
  - 这些需求里有很多是一些和数据理解无关的内容，本身是不应该在可视化中被过多强调的。G2为了这些需求开放了很多配置，但这本身使得有些配置是保留初心，支持响应式的，而有些却不行；有些可以方便的映射到数据字段上，有些却不行。
- G2近两年的关注点在Graphics上，而不是Statistical Graphics。
  - G2的一些新增API实际上是G层面关注的API，一些是和数据与可视化分析无关的，纯粹的图形问题。
  - G2做了很多这样的向一线开发人员的妥协，根据工程师的习惯设计了使用方式，从而使得其在图形语法的灵活特性上也越来越难以实现。
  - 比如GPL里的分面是可以通过坐标系和代数表达式搭配而灵活生成的，但G2的实现却是给各种不同的分面实现一个对应的类，所以其分面很难自由组合
  - G2的代数表达式比较可烂尾了（如position里的表达式就是，理论上是很自由的不局限于*(cross)运算符的）。
  - 不再那么聚焦在数据分析上使得我这种屁事多的老粉越来越少的使用G2，但的确由于更熟悉的API设计和能够对付设计师的灵活圈了大量的新粉。
- 20年G2的交互语法，给人的感觉是G层面的交互行为的抽象，和数据有些剥离。
  - 相比vega-lite，则是专注在数据分析的交互上，这带来的好处是可以对一种分析行为对所有可能的交互进行枚举，从而实现交互逻辑的推荐。
  - G2这里选择了对更多可能需求的支持而牺牲了对数据的聚焦。
  - 类似的，20年IDL的Gemini就是一种动画语法的实践，并在此基础上实现了动画的自动推荐

- G2只是图形语法（The Grammar of Graphics）的“又”一个实现。
  - 这本书向我们介绍了看待统计图形的一种形式化方法，也就是“图形语法”。
- 图形语法的作者，Leland Wilkinson，从上世纪80年代就开始开发统计软件包SYSTAT，然后把它卖给了大名鼎鼎的IBM的SPSS统计学软件，并为SPSS工作了十年之久
  - SPSS中用于描述图表的语言叫做GPL（Graphics Production Language），便是Wilkinson的图形语法最初的实现。
- 现在市面上所流行可视化库，大部分是类似HighCharts、ECharts、Google Charts等这种基于图表分类的可视化库。
  - 另外一个具代表性的是D3可视化库，但D3略偏向底层，学习曲线也略陡峭
  - R语言中著名的ggplot2，是Hadley Wickham针对R语言基于图形语法的一个实现，免费又开源。
  - Vega: A Visualization Grammar，华盛顿大学那边最近几年搞出的一套基于D3的可视化语法，其中一些概念借鉴了图形语法，神似而形不似。
  - Bokeh，是一个基于图形语法的Python可视化库。个人觉得比G2更加成熟。
