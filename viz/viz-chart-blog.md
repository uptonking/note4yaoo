---
title: viz-chart-blog
tags: [blog, charting, viz]
created: '2020-08-08T11:30:42.489Z'
modified: '2021-01-19T12:47:29.048Z'
---

# viz-chart-blog

# guide
- search 
  - echarts site:preset.io/blog
# [20 ideas for better data visualization](https://uxdesign.cc/20-ideas-for-better-data-visualization-73f7e3c2782d)
01. Choose the right chart type
02. Use correct plotting directions based on the positive and negative values
03. Always start a bar chart at 0 baseline
04. Use adaptive y-axis scale for line charts
05. Consider your time series when using a line chart
06. Do not use “smoothed” line charts
07. Avoid confusing dual-axis
08. Limit the number of slices displayed in a pie chart
09. Label directly on the chart
10. Don’t label on top of slices
11. Order pie slices for faster scanning
12. Avoid randomness
13. Thin donut charts are impossible to read
14. Let data speak for itself
15. Pick a color palette that matches the nature of your data
16. Design for accessibility
17. Focus on legibility
18. Use a horizontal bar chart instead of rotating labels
19. Choose your charting library
20. Go beyond static reports
# [Why Apache ECharts is the Future of Apache Superset™_202104](https://preset.io/blog/2021-4-1-why-echarts/)
- Superset community consider ECharts as the replacement for NVD3 for its primary charting library.
  - When Superset was started back in 2015, the D3 library was the clear choice for building data visualizations, and NVD3 offered a nice set of reusable charts built on top of D3 that allowed hooks and callbacks that integrated nicely with D3 primitives. 
  - Over the past few years, the library has not been maintained actively and we've had to fork the project recently to ensure we could fix some bugs
- When deciding what charting library to bet on next, the following factors were considered by the Superset community:
  - large library of visualization types, rooted in a consistent visual design and API
  - an active and growing community
  - strong governance model where anyone can contribute and influence the direction
  - high performance, ideally supporting canvas rendering
  - powerful declarative API for customizing and theming charts
  - internationalization support
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
