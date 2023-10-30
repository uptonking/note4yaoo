---
title: lib-db-app-community-gis-spatial
tags: [community, database, gis, spatial]
created: 2023-10-27T06:37:16.463Z
modified: 2023-10-27T06:37:55.413Z
---

# lib-db-app-community-gis-spatial

# guide

- [Virtual r-tree mapped to an extendible-hash based file system - Google Patents_201012](https://patents.google.com/patent/US20120158736)
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-spatial-index
- ## 

- ## 

- ## 

- ## [Performance of RTree vs kd-trees - Stack Overflow](https://stackoverflow.com/questions/20605250/performance-of-rtree-vs-kd-trees)
- This depends on various parameters. Most importantly on your capability to implement these algorithms.
  - For tiny data, kd-trees will likely be faster, plus they are much simpler to implement.
  - I've personally found bulk-loaded R*-trees to be faster for large data, probably because they have a better fan-out. 
  - Bulk-loaded R-trees is a more fair comparison, as kd-trees are commonly bulk-loaded (in fact, they don't support incremental operation very well at all).

- ## 🆚️🌲 [What is the difference between a KD-tree and a R-tree? - Stack Overflow](https://stackoverflow.com/questions/4326332/what-is-the-difference-between-a-kd-tree-and-a-r-tree)

- 流行度 r-tree : kd-tree 
  - github仓库/topic 59: 206
  - stackoverflow 263: 460

- KD-trees are only efficient in bulk-loading situations. Once built, modifying or rebalancing a KD-tree is non-trivial. R-trees do not suffer from this.

- They serve similar purpose (region queries on spatial data), and they both are trees
- k-d-trees are a lot easier to implement in memory, which actually is their key benefit
- R-Trees are balanced, k-d-trees are not (unless bulk-loaded). 
  - This is why R-trees are preferred for changing data, as k-d-trees may need to be rebuilt to re-optimize.
- R-Trees are disk-oriented. They actually organize the data in areas that directly map to the on-disk representation. This makes them more useful in real databases and for out-of-memory operation. 
  - k-d-trees are memory oriented and are non-trivial to put into disk pages
- k-d-trees are elegant when bulk-loaded, while R-trees are better for changing data (although they do benefit from bulk loading, when used with static data).
- R-Trees do not cover the whole data space. Empty areas may be uncovered. 
  - k-d-trees always cover the whole space.
- k-d-trees binary split the data space, R-trees partition the data into rectangles. 
  - The binary splits are obviously disjoint; 
  - while the rectangles of an R-tree may overlap (which actually is sometimes good, although one tries to minimize overlap)
- R-trees can store rectangles and polygons, k-d-trees only stores point vectors (as overlap is needed for polygons)
- R-trees come with various optimization strategies, different splits, bulk-loaders, insertion and reinsertion strategies etc.
- k-d-trees use the one-dimensional distance to the separating hyperplane as bound; R-trees use the d-dimensional minimum distance to the bounding hyperrectangle for bounding (they can also use the maximum distance for some counting queries, to filter true positives).
- k-d-trees support squared Euclidean distance and Minkowski norms, while Rtrees have been shown to also support geodetic distance (for finding near points on geodata).

- kd-trees partition the whole of space into regions whereas R-trees only partition the subset of space containing the points of interest.

- ## 🆚️🌲 [Advantages of R-trees in comparison to geohashes - Geographic Information Systems Stack Exchange](https://gis.stackexchange.com/questions/108557/advantages-of-r-trees-in-comparison-to-geohashes)
  - Geohashes are being widely used in products like: Lucene, mongodb, etc and have become one of the most important technology of present day.
  - Have Geohashes replaced the good old R-trees or do R-trees have any advantages as compared to Geohashes?

- Geohash are very simple and effective way of indexing spatial features, particularly point features. 
  - Line and polygon features are little harder to index, but can be done. 
  - Geohash is a static hierarchical fixed size grid, overlayed on top of the earth surface. 
  - Grid cells of the same hierarchical level do not overlap. 
- R-Tree is a dynamic grid which cell location and size change depending on the features they are indexing. 
  - R-Tree indexes features bounding boxes and cells change every time you insert and update data. 
- Geohash is mostly used for indexing point features and cells do not change with every insert and update of data. Geohash cells do not adopt to the features like with R-tree.
- 😄 Some of the advantages of geohash (comparing to r-tree) could be:
  - easy implementation
  - no performance degradation with growing number of features
  - proximity searches (partially true)
- 😩 Some of the disadvantages of geohash (comparing to r-tree) could be:
  - arbitrary precision of grid
  - harder to index (and query) line and polygon features
  - size of the index could be large with some methods of line and polygon indexing
  - by the specifications, it can be only used with longitude/latitude coordinate system, although the same method could be applied to other coordinate systems also
- Those products (databases) that you mentioned use geohash because geohash is mainly used for indexing points and there are lot of applications that need such a feature. 
  - Lines and polygons are not that often used (except for the GIS applications of course), so why bother with it. 
  - Other reason, is of course, ease of implementation. 
  - Geohash converts two-dimensional coordinate to one-dimensional value. This is called dimensional reduction. One-dimensional value is easy to indexed by standard b-tree which is mostly used in those products.
- I have to mention that there are similar algorithms to geohash but most of them are proprietary and require licensing. Geohash is in public domain. This could be also the reason for such a large usage in the recent years.

- why do geohashes give arbitrary precision of grid. 
  - Geohash converts longitude and latitude coordinate into the one-dimensional string. Length of this string is directly tied to the converted precision of the coordinate.
  - Basically, geohash converts point into a polygon area (one geohash grid). The size of this polygon area is dependant of the length of the geohash string and what latitude you are calculating the geohash
# discuss
- ## 

- ## 

- ## 

- ## 🌎🔥 [GeoDesk is a spatial database engine for OpenStreetMap features | Hacker News_202212](https://news.ycombinator.com/item?id=33812983)
- 
- 
- 
