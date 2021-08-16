---
title: spec-gis
tags: [gis, spec]
created: '2019-12-12T09:07:57.883Z'
modified: '2021-01-04T17:06:14.968Z'
---

# spec-gis

- specifications about geospatial dev

# guide

- features
  - mdx based map-doc, 简单读写无需借助专业软件

# popular-formats-about-mapping

- Mapbox Vector Tile specification
  - https://github.com/mapbox/vector-tile-spec
  - 文件后缀为 `.mvt`
  - implementations 
    - https://github.com/mapbox/awesome-vector-tiles
    - https://github.com/wdtinc/mapbox-vector-tile-java
      - protoc generated model for Mapbox Vector Tiles v2.1.
      - Provides MVT encoding through use of the jts library

# ogc

# more-gis-format

- CityJSON
  - https://www.cityjson.org/
  - CityJSON is a JSON-based encoding for a well-documented subset of the OGC CityGML data model (version 2.0.0). 
  - Now published as an OGC community standard!
  - https://github.com/cityjson/cityjson-threejs-loader
