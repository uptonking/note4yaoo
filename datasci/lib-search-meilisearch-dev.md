---
title: lib-search-meilisearch-dev
tags: [meilisearch, search]
created: 2024-03-02T14:57:49.282Z
modified: 2024-03-02T14:58:08.147Z
---

# lib-search-meilisearch-dev

# guide

# dev

# docs

## [Prefix search — Meilisearch documentation](https://www.meilisearch.com/docs/learn/advanced/prefix)

- In Meilisearch, you can perform a search with only a single letter as your query. This is because we follow the philosophy of prefix search.
  - Prefix search is when document sorting starts by comparing the search query against the beginning of each word in your dataset.
  - All documents with words that match the query term are added to the bucket sort, before the ranking rules are applied sequentially.
  - In other words, prefix search means that it's not necessary to type a word in its entirety to find documents containing that word—you can just type the first one or two letters.
- Prefix search is only performed on the last word in a search query—prior words must be typed out fully to get accurate results.
- Searching by prefix (rather than using complete words) has a significant impact on search time. 
  - The shorter the query term, the more possible matches in the dataset.
# more
