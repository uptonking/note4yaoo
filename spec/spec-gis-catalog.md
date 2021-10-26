---
title: spec-gis-catalog
tags: [catalog, gis, spec]
created: '2019-12-12T09:07:57.883Z'
modified: '2021-09-30T07:45:22.343Z'
---

# spec-gis-catalog

> specifications about geospatial dev

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
# discuss

## [Modern Geospatial Data formats for serving over HTTP](https://twitter.com/sabman/status/1443294413933928468)

- vector
  - https://flatgeobuf.org/
  - https://github.com/flatgeobuf/flatgeobuf
  - performant binary encoding for geographic data based on flatbuffers that can hold a collection of Simple Features including circular interpolations as defined by SQL-MM Part 3.
  - Inspired by geobuf and flatbush. 
  - Deliberately does not support random writes for simplicity and to be able to cluster the data on a packed Hilbert R-Tree enabling fast bounding box spatial filtering.

- raster
  - https://geotiffjs.github.io/
  - https://github.com/geotiffjs/geotiff.js
  - a small library to parse TIFF files for visualization or analysis. 
  - It is written in pure JavaScript, and is usable in both the browser and node.js applications.

- tiles
  - https://github.com/protomaps/PMTiles
  - Cloud-optimized, single-file archive format for pyramids of map tiles

- point cloud
  - https://copc.io/
  - A COPC file is a LAZ 1.4 file that stores point data organized in a clustered octree(八叉树). 
  - It does this by providing some VLRs and using the variable chunking strategy of LAZ 1.4.
  - Data organization of COPC is modeled after the EPT data format, but COPC clusters the storage of the octree as variably-chunked LAZ data in a single file.
