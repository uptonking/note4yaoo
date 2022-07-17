---
title: toc-gis-processing
tags: [geoprocessing, gis, toc]
created: 2020-11-13T07:35:23.232Z
modified: 2021-01-04T16:21:40.119Z
---

# toc-gis-processing
- guide
  - postgis, vector tiles
  - map server, node

- ref
  - [@turf/helpers vs @turf/turf vs geolib vs geometric](https://www.npmtrends.com/@turf/helpers-vs-@turf/turf-vs-geolib-vs-geometric)
# js
- turf /MIT/5.5kStar/202007
  - https://github.com/Turfjs/turf
  - http://turfjs.org/
  - a library for spatial analysis. 
  - It includes traditional spatial operations, helper functions for creating GeoJSON data, and data classification and statistics tools.
  - geojson to topojson: @turf/concave使用了
- h3-js /400kStar/Apache2/202012/js
  - https://github.com/uber/h3-js
    - provides a pure-JavaScript version of the H3 Core Library, a hexagon-based geographic grid system.
    - The H3 geospatial indexing system is a multi-precision hexagonal tiling of the sphere indexed with hierarchical linear indexes. 
  - https://github.com/uber/h3
    - /2.5kStar/Apache2/202011/c
  - ref
    - [Comparisons: geohash, h3, s2 & Use cases](https://h3geo.org/docs/usecases)

- loam /96Star/Apache2/202105/js
  - https://github.com/azavea/loam
  - A wrapper for running GDAL in the browser using gdal-js
  - https://github.com/ddohler/gdal-js
    - An Emscripten port of GDAL 2.1
  - [Introducing Loam: A Client-Side GDAL Wrapper for Javascript](https://www.azavea.com/blog/2021/05/03/introducing-loam-a-client-side-gdal-wrapper-for-javascript/)
    - we compiled GDAL into WebAssembly using the Emscripten project.
    - Loam wraps the low-level GDAL interface provided by Emscripten with a Promises-based interface 
    - The actual GDAL code is executed from within a Web Worker in order to prevent blocking the main thread on long-running computations.

- geolib /3.5kStar/MIT/202005/ts
  - https://github.com/manuelbieh/geolib
  - Zero dependency library to provide some basic geo functions
  - This library is currently 2D, meaning that altitude/elevation is not yet supported by any of its functions!
# spatial-index
- https://github.com/mourner/flatbush
  - A really fast static spatial index for 2D points and rectangles in JavaScript.
  - An efficient implementation of the packed Hilbert R-tree algorithm.
# opengis
- geoserver /GPLv2/java
  - https://github.com/geoserver/geoserver
  - http://geoserver.org/
  - https://github.com/geoserver/geoserver/wiki/DRAFT---Do-I-need-a-proprietary-license-FAQ
- h2gis /LGPL3/java
  - https://github.com/orbisgis/h2gis/
  - http://www.h2gis.org/
  - https://github.com/h2database/h2database
- QGIS /GPLv2/cpp
  - https://github.com/qgis/QGIS
- uDig /BSD/java
  - https://github.com/locationtech/udig-platform
  - uDig is an open source (EPL and BSD) desktop application framework, built with Eclipse Rich Client (RCP).
    - [Committee has accepted an RFC making uDig available under a dual BSD and EPL license](http://udig-news.blogspot.com/2012/10/udig-change-to-epl-and-bsd-license.html)
  - uDig 2.0.0 is released on 20180426
- postgis /GPLv2/c
  - https://github.com/postgis/postgis
  - http://postgis.net/
  - https://github.com/postgres/postgres /BSD
- gdal /MIT/cpp/python
  - https://github.com/OSGeo/gdal
  - https://gdal.org/
- jts - java - EPL1.0/BSD
  - https://github.com/locationtech/jts/
  - https://locationtech.github.io/jts/
- spatial4j /Apache2.0
  - https://github.com/locationtech/spatial4j
  - https://projects.eclipse.org/projects/locationtech.spatial4j
- openmap /CustomLic/java
  - https://github.com/OpenMap-java/openmap
  - http://openmap-java.org/
  - We want you to be able to do pretty much anything with it as long as we get credit for our work 
  - and as long as you offer your changes to us so we can possibly add them to the standard version we distribute.
- GRASS GIS /GPLv2/cpp
  - https://github.com/OSGeo/grass
  - https://grass.osgeo.org/
- mapserver /MIT/c
  - https://github.com/mapserver/mapserver
  - https://mapserver.org/
  - MapServer is released under an MIT-style license
  - MapServer is not a full-featured GIS system, nor does it aspire to be.
- mapnik /LGPLv2/cpp
  - https://github.com/mapnik/mapnik
  - https://mapnik.org/
- geowebcache /LGPL/java
  - https://github.com/GeoWebCache/geowebcache
  - https://www.geowebcache.org/
- geotools /LGPLv2/java
  - https://github.com/geotools/geotools
  - https://geotools.org/
- geos /LGPLv2/cpp
  - https://github.com/libgeos/geos 
  - https://trac.osgeo.org/geos
  - port from jts
# more-repos
- https://github.com/DentReality/GeoDBSCAN
  - js implementation and API for the DBSCAN clustering algorithm using a geographic distance function. 
  - This allows developers to create clusters based on the geographic density of the points. 
  - The code is a modernisation and extension of density-clustering.
  - https://github.com/uhho/density-clustering
