---
title: lib-excel-tanstack-table-community-faq
tags: [examples, faq, tanstack-table]
created: 2023-05-09T17:15:47.077Z
modified: 2023-05-09T17:16:21.374Z
---

# lib-excel-tanstack-table-community-faq

# guide

# discuss
- ## 

- ## 

- ## 

- 
- 
- 
- 

- ## [[v8] - How do I setup external ColumnFilter components?](https://github.com/TanStack/table/discussions/4361)
  - my goal is to have a dashboard with filters at the top of the page that when set, filter down through all the various charts and tables on the screen.

- This discussion can be closed. Aggregating data like what I was attempting isn't a good approach in the front-end. We moved to backend filtering and sorting.

- [Move filtering outside table(v7)](https://github.com/TanStack/table/discussions/2234)
  - https://codesandbox.io/s/react-table-filter-outside-table-bor4f

- ## [How does TanStack/react-table compare to a spreadsheet?](https://github.com/TanStack/table/discussions/3963)
- @tanstack/react-table is mostly focussed on the headless logic for displaying data in columns, rows, pagination, grouping, expanding, filtering, searching, etc. 
  - You can easily build on editing and all of the other stuff you mentioned, but you have to implement it yourself. 
  - Though react-table will give you a pretty good base for it.

- ## [How to add a custom dropdown filter?](https://github.com/TanStack/table/discussions/4133)
- `meta: { filterComponent: CustomFilter }`
