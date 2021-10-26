---
title: lib-list-ag-grid-latest-roadmap
tags: [ag-grid, lib, roadmap]
created: '2020-08-05T09:30:42.434Z'
modified: '2021-05-13T02:43:35.993Z'
---

# lib-list-ag-grid-latest-roadmap

# guide

- [The ag-Grid pipeline](https://www.ag-grid.com/ag-grid-pipeline/)



# latest

- 24.0.0
  - [Aggregation] Custom Aggregation methods to have more information in parameters 
    - Pass nodes, and source to know where the aggregation is for 
    - (ie to Do aggregations based on other aggregations)
  - Cleanup Legacy Properties (> 1 year old)
  - Filter: Allow set filter to be combined with other filters

# discuss

- ## We've spent the last 6 months porting AG Grid to React, so it's not longer using a wrapper for AG Grid, but AG Grid 100% React. 
- https://twitter.com/ag_grid/status/1426087043831062528
  - Our release next week is going to showcase it. 
- There is no change to Angular, Vue or VanillaJS.
  - The same business logic grid API is used by all, and will continue to be used.
  - The new ReactUI is a replacement for the current React Wrapper.
