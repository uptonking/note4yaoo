---
title: lib-olap-blog
tags: [blog, olap]
created: 2022-12-05T19:09:50.507Z
modified: 2022-12-05T19:09:59.634Z
---

# lib-olap-blog

# guide

# blogs

## [A Tale of Three Real-Time OLAP Databases: Apache Pinot, Apache Druid, and ClickHouse__202304](https://startree.ai/blog/a-tale-of-three-real-time-olap-databases)

## [Comparison of the Open Source OLAP Systems for Big Data: ClickHouse, Druid, and Pinot | by Roman Leventov__201802](https://leventov.medium.com/comparison-of-the-open-source-olap-systems-for-big-data-clickhouse-druid-and-pinot-8e042a5ed1c7)
# mdx-query-language

## [Comparing tabular model DAX with multi-dimensional MDX](https://www.wiseowl.co.uk/blog/s1450/dax-versus-mdx.htm)

- Suppose that we want to show the total value of transactions in a pivot table (that is, we want to sum Price * Quantity)

```shell
#  typical DAX expression, giving total price * quantity.
Total value:=sumx('Transaction', [Price]*[Quantity])

# A measure in MDX to create the expression for summing.

create member currentcube.measures.[Amount] as [Measures].[Price] * [Measures].[Quantity]

```

# more-blog

- [Vectorization in OLAP Databases — tech ramblings](https://aneesh.mataroa.blog/blog/vectorization-in-olap-databases/)
