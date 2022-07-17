---
title: lib-list-ag-grid-docs-perf-optimization
tags: [ag-grid, docs, optimization]
created: 2020-08-25T14:01:07.182Z
modified: 2021-05-13T02:42:56.405Z
---

# lib-list-ag-grid-docs-perf-optimization

# performance

- use dom virtualization

1. Setting Expectations

2. Check Cell Renderers
  - ag-Grid can be slowed down by your custom cell renderers. 
  - To test this, remove all cell renderers from your grid and compare the speed again. 
  - If the grid does improve it's speed by removing cell renderers, try to introduce the cell renderers one by one to find out which ones are adding the most overhead.

3. Create Fast Cell Renderers
  - Do NOT use a framework (eg Angular or React) for the cell renderers. 
  - The grid rendering is highly customized and plain JavaScript cell renderers will work faster than framework equivalents. 
  - It is still fine to use the framework version of ag-Grid (eg for setting ag-Grid properties etc) however because there are so many cells getting created and destroyed, the additional layer the frameworks add do not help performance and should be provided if you are having performance concerns
  - Not everyone needs blazing fast cell renderers (eg maybe you have users on fast machines with fast browsers, or maybe your grids have few columns) in which case framework cell renderers may work fine. 
  - The suggestion of not using frameworks for cells is only applicable when you are looking to squeeze for performance gains.
  - We suggest not using frameworks for cell renderers for because of the large number of cells getting created and destroyed. 
  - Most of the time a cell will not have complex features in it, so using plain JavaScript should not be a problem. 
  - For all other components (filters, editors etc), using the frameworks won't make much noticeable difference as these components are not created and destroyed as often as cell renderers.

4. Turn Off Animations

5. Configure Row Buffer
  - The `rowBuffer` property sets the number of rows the grid renders outside of the viewable area. 
  - The default is 10. 
  - For example, if your grid is showing 50 rows (as that's all the fits on your screen without scrolling), then the grid will actually render 70 in total (10 extra above and 10 extra below). 
  - Then when you scroll the grid will already have 10 rows ready waiting to show so the user will not see a redraw (not all browsers show the redraw, only the slower ones).
  - Setting a low row buffer will make initial draws of the grid faster (eg when data is first loaded, or after filtering, grouping etc). 
  - Setting a high row buffer will reduce the redraw visible vertically scrolling.

6. Use Chrome
7. Understand Batch Update Transactions for fast changing data
  - For fast changing data, consider using Batch Update Transactions which allows the grid to take very large amounts of updates without bringing the browser to a crawl. 
  - This is also demonstrated in the blog Streaming Updates in JavaScript Datagrids that shows hundreds of thousands of updates per second.

8. Understand Hacks
  - Read the article 8 Performance Hacks for JavaScript so you know what the grid is doing, that way you will be able to reason with it.

# Row Pagination

- Pagination does not reduce the feature set of the grid, as long as the underlying row model supports it. 
- In other words, if you are paging over the Client-Side Row Model, all features of the Client-Side Row Model (grouping, filtering etc) are still available. 
- Likewise for the other row models, if the row model supports it, it's available through pagination and that row model.
