---
title: web-layout-table-community
tags: [community, css, table]
created: 2023-12-26T10:47:36.499Z
modified: 2023-12-26T10:47:51.891Z
---

# web-layout-table-community

# guide

# discuss-stars
- ## 

- ## 

- ## stick the first row using `<thead>` so you don't lose context, and give it a `margin-bottom` so you don't lose the last row on scroll
- https://x.com/jh3yy/status/1902855264086245830

```CSS
thead {
  position: sticky;
  top: var(--header-height);
  margin-bottom: 1lh;
  /* or whatever row height */
}
```

- that margin bottom trick is slick
  - alternative "hack" is to absolutely position the last row with top: 100%

- What if my rows is not fixed height? 
# discuss
- ## 

- ## When you build modern front-end data grids and tables, what kind of elements or CSS strategies do you use?
- https://twitter.com/KevinVanCott/status/1760317094124540170
  - Semantic `<table>` elements
  - `<div>` with Grid/Flexbox
  - `<table>` with Grid/Flexbox 

- You can use semantic `<table>` elements with virtualization and resizing features. The main thing that has led me to success this way is to use CSS Grid and flexbox on semantic `<table>` elements. Best of both worlds in terms of accessibility and style flexibility

- ## You can use CSS `table-layout: fixed` with text-overflow and column width set to automatically shorten the column content 
- https://twitter.com/davidm_ml/status/1739572523719692702
  - 提供了操作动画效果示例
