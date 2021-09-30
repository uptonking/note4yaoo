---
title: spec-gis-spatialite
tags: [gis, spatialite, spec]
created: '2021-09-30T07:59:26.096Z'
modified: '2021-09-30T07:59:56.263Z'
---

# spec-gis-spatialite

# guide

- spatialite features
  - File based
  - SQL database
  - OGC Simple Features
- SpatialLite lacks the support for extensions or raster data present in GeoPackage. 
  - While these are not necessarily must-have features, they may be useful. 
  - Like GeoPackage, it is unsuitable for streaming.
- Since **SpatiaLite offers no clear advantages over GeoPackage** at this time, it should only be considered as a Shapefile replacement in niche scenarios.

- SQLite is intrinsically simple and lightweight:
  - a single lightweight library implementing the full SQL engine
  - standard SQL implementation: almost complete SQL-92
  - a whole database simply corresponds to a single monolithic file (no size limits)
  - any DB-file can be safely exchanged across different platforms, because the internal architecture is universally portable
