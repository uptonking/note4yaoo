---
title: lib-olap-blog
tags: [blog, olap]
created: 2022-12-05T19:09:50.507Z
modified: 2022-12-05T19:09:59.634Z
---

# lib-olap-blog

# guide

# mdx

## [Comparing tabular model DAX with multi-dimensional MDX](https://www.wiseowl.co.uk/blog/s1450/dax-versus-mdx.htm)

- Suppose that we want to show the total value of transactions in a pivot table (that is, we want to sum Price * Quantity)

```shell
#  typical DAX expression, giving total price * quantity.
Total value:=sumx('Transaction', [Price]*[Quantity])

# A measure in MDX to create the expression for summing.

create member currentcube.measures.[Amount] as [Measures].[Price] * [Measures].[Quantity]

```

- 
- 
- 
