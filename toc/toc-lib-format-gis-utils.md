---
title: toc-lib-format-gis-utils
tags: [format, geojson, geopackage, gis, shapefile, toc, utils]
created: 2022-11-06T15:47:28.547Z
modified: 2022-11-06T15:48:09.723Z
---

# toc-lib-format-gis-utils

# guide

# popular

# examples

# parser-generator

# extension-superset
- https://github.com/bmschmidt/trifeather
  - This library defines a binary file format for collections of projected polygon map data bound for geojson.
  - It builds on the Apache Arrow project's feather format; each feature from a feature collection is stored as a single row, and all keys are stored as columns. 
  - Rather than store coordinates, it uses the mapbox earcut library to triangulate polygons, and stores those triangles directly.
  - The combination of this strategy and apache arrow means that the binary data can be pushed straight to a GPU for plotting without any need for Javascript, without an extraordinary size penalty.
# utils
- https://github.com/dimfeld/merge-geo
  - A utility to read CSV data about geographic locations and merge it into a GeoJSON FeatureCollection.
# more
