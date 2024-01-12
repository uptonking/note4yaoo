---
title: algs-search-dev
tags: [algorithms, search]
created: 2021-01-02T10:42:32.711Z
modified: 2021-01-02T10:42:48.262Z
---

# algs-search-dev

# guide

# gis
- ## 

- ## 

- ## 🌲 Regarding nearest neighbor search implementation, I see R-trees but not space-filling curves. 
- https://twitter.com/strlen/status/1745550175425397217
  - For GIS databases, Z-order curves can be used instead of R trees. Any reason they aren't used for NNS in vector dbs?
- 🐛 Space-filling curves have poor locality, selectivity, and adaptivity for skewed high-dimensionality data models. 
  - Simple curves (Morton, Hilbert, etc) are too rigid. 
  - Intersections are best directly computed on a succinct(简明的；简洁的) index even if you did use them (GIS usually does it this way). 
- 🌲 R-trees are deeply flawed and scale poorly but are better behaved for sparse high-dimensionality data. 
  - Adaptive sparse-friendly curves are a thing but that asymptotically(渐近的) approaches incomputable/intractable problems in data compression and is poorly studied AFAIK.

# more
