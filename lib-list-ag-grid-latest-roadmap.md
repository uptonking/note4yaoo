---
title: lib-list-ag-grid-latest-roadmap
tags: [ag-grid, lib, roadmap]
created: '2020-08-05T09:30:42.434Z'
modified: '2021-05-13T02:43:35.993Z'
---

# lib-list-ag-grid-latest-roadmap

# guide

- [The ag-Grid pipeline](https://www.ag-grid.com/ag-grid-pipeline/)

- What's Next for React UI
  - In AG Grid v26.2 has a production ready version of React UI. 
    - It is turned on by setting the grid property reactUi=true.
  - In AG Grid v27 we plan to make this the default with a fallback property to keep the old rendering. 
    - The fallback property will be for emergency only and will be released as deprecated.
  - In AG Grid v28 we plan to remove the old way of React rendering.
# latest
- 24.0.0
  - [Aggregation] Custom Aggregation methods to have more information in parameters 
    - Pass nodes, and source to know where the aggregation is for 
    - (ie to Do aggregations based on other aggregations)
  - Cleanup Legacy Properties (> 1 year old)
  - Filter: Allow set filter to be combined with other filters
# discuss
- ## I never liked the property 𝒊𝒎𝒎𝒖𝒕𝒂𝒃𝒍𝒆𝑫𝒂𝒕𝒂=𝒕𝒓𝒖𝒆" or the callback "𝒈𝒆𝒕𝑹𝒐𝒘𝑵𝒐𝒅𝒆𝑰𝒅()" in AG Grid.
- https://twitter.com/niallcrosby/status/1494325782109249545
  - Instead I've implemented "𝒈𝒆𝒕𝑹𝒐𝒘𝑲𝒆𝒚()" which does both.
  - So I deprecated them both for the next release!

- ## We've spent the last 6 months porting AG Grid to React, so it's not longer using a wrapper for AG Grid, but AG Grid 100% React. 
- https://twitter.com/ag_grid/status/1426087043831062528
  - Our release next week is going to showcase it. 
- There is no change to Angular, Vue or VanillaJS.
  - The same business logic grid API is used by all, and will continue to be used.
  - The new ReactUI is a replacement for the current React Wrapper.
