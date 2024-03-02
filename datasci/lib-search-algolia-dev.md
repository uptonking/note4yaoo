---
title: lib-search-algolia-dev
tags: [algolia, search]
created: 2024-03-02T14:52:46.249Z
modified: 2024-03-02T14:53:03.140Z
---

# lib-search-algolia-dev

# guide

# dev

# docs

## [Prefix searching | Algolia](https://www.algolia.com/doc/guides/managing-results/optimize-search-results/override-search-engine-defaults/in-depth/prefix-searching/)

- Prefix matching is central to Algolia’s as-you-type search experience. 
- This is already useful in avoiding insufficient results. 
  - 💡 But you can also use prefix matching to bring back even more results.
- Algolia’s prefix search is configurable, with three available `queryType` modes depending on the use case. Every index can be configured independently.
  - `prefixLast` (default) - where only the last word is a prefix, and the rest are treated as full words
  - `prefixAll` - where all separate text in a query is treated as a prefix
  - `prefixNone` - disables all prefixing. treats none of a search query’s words as prefixes; all words are considered complete and only records containing matches for every query word will be returned.

- Note that the order of the matched words in the result doesn’t need to be the same as the order of the prefixes in the search query. 
# more
