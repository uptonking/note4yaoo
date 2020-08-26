---
title: docs-ag-grid-performance
tags: [ag-grid, docs, performance]
created: '2020-08-25T14:01:07.182Z'
modified: '2020-08-26T11:08:12.323Z'
---

# docs-ag-grid-performance

## performance

- use dom virtualization
1. Setting Expectations
2. Check Cell Renderers
3. Create Fast Cell Renderers
4. Turn Off Animations
5. Configure Row Buffer
6. Use Chrome
7. Understand
8. Understand

## Row Pagination

- Pagination does not reduce the feature set of the grid, as long as the underlying row model supports it. 
- In other words, if you are paging over the Client-Side Row Model, all features of the Client-Side Row Model (grouping, filtering etc) are still available. 
- Likewise for the other row models, if the row model supports it, it's available through pagination and that row model.
