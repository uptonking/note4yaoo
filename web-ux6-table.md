---
title: web-ux6-table
tags: [data-grid, list, table, ux]
created: 2023-02-24T11:06:00.253Z
modified: 2023-02-24T11:06:44.191Z
---

# web-ux6-table

# guide

# tables

# more

# discuss
- ## 

- ## 

- ## 

- ##  `<table>` highlighting with CSS `:has()` ; 
- https://x.com/i/bookmarks
  - 示例效果类似excel高亮光标所在的行和列

```CSS
td:has(~ td:hover),
/* previous sibling cells */
table:has(td:nth-of-type(3):hover)

/* column cells */
tr:not(:first-of-type):has(~ tr:hover) td:nth-of-type(3) {
  background: var(--highlighted);
}
```
