---
title: lib-notb-observablehq-dev
tags: [d3, notebook, observablehq]
created: 2021-05-06T09:42:52.668Z
modified: 2024-06-30T03:20:27.751Z
---

# lib-notb-observablehq-dev

# guide

- onb-cons
  - auto-ref是优点，也是缺点，kibana最新版在鼓励by-value而不是by-reference，折中方案是snapshot+auto-update-option
  - view + collapsible d3js + collapse data/dataseeds，类似html/css/js的面板
  - 文字和代码的切换交互过于偏向代码，更合适的方式是类似组件库的ui示例文档，上面是示例效果，下面的源码可折叠

- dev-xp
  - npm打包分发的方式，不如docker/ollama-run方便，但jspm在线源的设计就很方便了
# notebook-usecase
- [官方数据分析：国家统计局 统计数据，开放性高，但分析不深、体系不全](http://www.stats.gov.cn/tjsj/)
  - 商业性质的报告质量较高，但大多存在版权问题
  - [在哪里能找到各行业的分析研究报告？](https://www.zhihu.com/question/19766160)
  - [各大行业报告的数据都是从哪里找的？](https://www.zhihu.com/question/67387122)
  - [国内外有什么好的数据平台？](https://www.zhihu.com/question/34498225/answer/2087076914)
  - [你看过最优秀的研报是什么？ 数据+方法逻辑+观点](https://www.zhihu.com/question/33537844/answers/updated)
- 开放数据/报告
  - 开放数据集
  - github上公开分析案例，如js-framework-benchmark
  - [Our World in Data](https://ourworldindata.org/) is free and accessible for everyone.
- 主题分析
  - 新冠肺炎分析报告 coronavirus/covid-19
  - 北大毕业生就业质量年度报告
  - 数据结构与算法、leetcode数据
- 行业案例
  - tableau public
  - kaggle
- 找数据分析案例费时费力，可以尝试经典数据集/开放数据集的已有分析
  - 范围太广难以集中精力，可以重点关注**推荐系统、广告点击、销量预测**
  - MovieLens
  - Last.fm
  - OpenStreetMap对poi类别的推荐
- 找数据分析案例费时费力，可以试试经典教材、专著
  - 精益数据分析/8.2/技术与商业结合; 
  - 商务与经济统计/9.2/统计学入门; 
  - 高效商业分析： Excel建模与决策/9.1/excel; 
  - 用数据讲故事/8.4/故事性; 
- more-viz
  - [10 Of The Best Data Visualization Examples From History & Today](https://www.tableau.com/learn/articles/best-beautiful-data-visualization-examples)
# faq-not-yet
- 如何不显示cell name，同时又能通过cell name引用这个cell
# faq

# ref
- [How to: Embed a Notebook in a React App](https://observablehq.com/@observablehq/how-to-embed-a-notebook-in-a-react-app)

- [HQ](https://askubuntu.com/questions/627516) means Headquarters.
  - It's the name given to the website, not the software project per se(本身，自身，本质上).
