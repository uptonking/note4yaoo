---
title: thread-blog-pm-products
tags: [blog, pm, products, thread]
created: 2021-06-29T07:04:44.912Z
modified: 2021-06-29T07:05:13.621Z
---

# thread-blog-pm-products

# office-doc

# bi-data-tooling
## [New in Kibana: How we made it easier to manage visualizations and build dashboards_202106](https://www.elastic.co/blog/new-in-kibana-how-we-made-it-easier-manage-visualizations-and-build-dashboards?utm_content=&utm_medium=social&utm_source=twitter)
  - My hope for this post is that it helps inform the mental models of our curious power users while they attempt to learn these new dashboard creation flows.
  - By-ref vs By-value
  - A dashboard is populated with panels. 
  - Each panel has what’s known as an embeddable. 
  - Embeddables are responsible for displaying your visualization, whether it’s a chart, map, or tag cloud. 
  - In 7.11 and earlier, all visualization panels that you added to a dashboard were **by-reference** embeddables. 
  - Kibana stores by-reference embeddables as saved objects, which contain a saved object ID that is used to render the visualization in the panel.
  - Kibana stores by-reference embeddables as saved objects, which contain a saved object ID that is used to render the visualization in the panel.
  - In 7.12, you can now also add **by-value** embeddables to your dashboards.
  - By-value embeddables are NOT saved in the Visualize Library. 
  - Instead, everything that the dashboard needs to render the visualization is packaged in the by-value embeddable that is stored in the dashboard data structure. 
  - Visualizations contained within by-value embeddables only exist within the dashboard. 
  - If you compare the JSON of a dashboard with only by-value embeddables to a dashboard with only by-reference embeddables, you’d see that the dashboard with by-value embeddables contains much more information than the by-reference embeddable dashboard. 
  - In 7.12, the new flow is streamlined so you can spin up dashboards as quickly as possible. 
  - The new visualization is a by-value embeddable and only exists within your dashboard. 
  - This means you can freely edit or delete the visualization without affecting other dashboards or visualizations. 
  - This is the dashboard-first flow: if you create a visualization directly from a dashboard, you are returned directly to the dashboard with your new visualization when you select Save and return. 
# more-products
