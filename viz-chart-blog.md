---
title: viz-chart-blog
tags: [blog, charting, viz]
created: '2020-08-08T11:30:42.489Z'
modified: '2021-01-19T12:47:29.048Z'
---

# viz-chart-blog

# [GitLab: Why we chose ECharts for data visualizations instead of d3.js_201909](https://about.gitlab.com/blog/2019/09/30/why-we-chose-echarts/)

- As GitLab continues to grow in depth and breadth across the DevOps lifecycle, the use of charts and data visualizations has increased in frequency and complexity. 
- As the number of different libraries increased along with our charting requirements, we decided it was time to start **unifying our charting libraries** to help us move quickly.
- At first, we wanted to unify our charts using D3.js but this was difficult because D3.js isn't a charting library.
  - D3.js is a JavaScript library for manipulating documents based on data.
  - D3.js is powerful but it has a big learning curve.
  - Our team did not have the time to develop the expertise without impacting our product development velocity.
- ECharts
  - Robust yet flexible chart types
    - enough flexibility for us to create our own custom charts
  - Performance
  - Growing ecosystem
# ref
- [How to compare data using charts](https://www.highcharts.com/blog/post/how-to-compare-data-using-charts/)
- [how to feed live data to a chart with Highcharts API](https://www.highcharts.com/docs/working-with-data/live-data)
