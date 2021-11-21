---
title: lib-list-react-table-faq-repeat
tags: [faq, react-table, repeat]
created: '2021-11-21T18:27:10.862Z'
modified: '2021-11-21T18:27:22.494Z'
---

# lib-list-react-table-faq-repeat

# guide

# faq-repeat

## 选用哪种布局 

- useAbsoluteLayout
  - adds support for headers and cells to be rendered as absolutely positioned divs (or other non-table elements) with explicit `width`. 
  - this becomes useful if and when you need to virtualize rows and cells for performance.

- useBlockLayout
  - adds support for headers and cells to be rendered as `inline-block` divs (or other non-table elements) with explicit `width`.
  - this becomes useful if and when you need to virtualize rows and cells for performance.

- useFlexLayout
  - adds support for headers and cells to be rendered as `inline-block` divs (or other non-table elements) with width being used as the `flex-basis` and `flex-grow`. 
  - This becomes useful when implementing both virtualized and resizable tables that must also be able to stretch to fill all available space.
