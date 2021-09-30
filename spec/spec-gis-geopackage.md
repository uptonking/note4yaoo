---
title: spec-gis-geopackage
tags: [geopackage, gis, spec]
created: '2021-09-30T07:46:25.527Z'
modified: '2021-09-30T07:46:40.968Z'
---

# spec-gis-geopackage

# guide
- geopackage features
  - SQLite as backend
  - File based, single file
  - **Vectors, rasters**
  - Official extensions
  - Supported in many software packages
# docs

## [OGC GeoPackage Overview](http://www.geopackage.org/)

> GeoPackage is an open, standards-based, platform-independent, portable, self-describing, compact format for transferring geospatial information. 

- The GeoPackage standard describes a set of conventions for storing the following within an SQLite database
  - vector features
  - tile matrix sets of imagery and raster maps at various scales
  - attributes (non-spatial data)
  - extensions
- GeoPackage is the SQLite container 
  - and the GeoPackage Encoding Standard governs the rules and requirements of content stored in a GeoPackage container.
  - Since a GeoPackage is a database container, it supports direct use. 
  - This means that the data in a GeoPackage can be accessed and updated in a "native" storage format without intermediate format translations. 
  - GeoPackages are particularly useful on mobile devices

- Does GeoPackage replace Shapefile?
  - It could but it doesn’t have to. 
  - If all you need is simple exchange and display then `GeoPackage` may be overkill and something like `GeoJSON` may be more appropriate. 
  - If you are looking for database capabilities like random access and querying then GeoPackage is a platform-independent, vendor-independent choice. 
  - GeoPackage was carefully designed this way to facilitate widespread adoption and use of a single simple file format by both commercial and open-source software applications

- What were the reasons to go with SQLite, when OGC has invested heavily in PostGIS?
  - OGC has not invested in PostGIS, rather PostGIS implements OGC standards.
  - PostGIS is just like any other RDBMS implementation of the Simple Features spec. 
  - The primary use case for designing GeoPackage was mobile device use, and that's why SQLite was chosen as a platform. 

- https://github.com/opengeospatial/geopackage
  - An asciidoc version of the GeoPackage specification for easier collaboration
