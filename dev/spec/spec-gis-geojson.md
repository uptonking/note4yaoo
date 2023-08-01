---
title: spec-gis-geojson
tags: [format, gis]
created: 2019-12-24T12:58:14.641Z
modified: 2021-09-30T07:43:15.350Z
---

# spec-gis-geojson

# guide

- geojson features
  - JSON format: **human-readable**, text-based format
  - File based
  - Can handle complex data
  - File size grows fast
  - IETF Standard

- json-ext-gis
  - geojson
  - topojson
  - tilejson
# geojson-spec

# guide

- 列表插件设计
  - 列表类
  - 图表类
  - 地图类
  - 搜索类
# tilejson
- https://github.com/mapbox/tilejson-spec
  - JSON format for describing map tilesets.
# shp

# mvt

# Overture Maps
- resources
  - [Overture Maps: From Data to Map. Including Parquet, GeoParquet, DuckDB and QGIS](https://bertt.wordpress.com/2023/07/31/overture-maps/)

- overture vs osm
  - Overture is a data-centric map project, not a community of individual map editors. 
  - Therefore, Overture is intended to be complementary to OSM. 
  - 👉🏻 **We combine OSM with other sources to produce new open map data sets**. 
  - Overture data will be available for use by the OpenStreetMap community under compatible open data licenses. 
  - Overture members are encouraged to contribute to OSM directly.

- https://github.com/OvertureMaps/schema
  - https://docs.overturemaps.org/
  - Overture Data Schema currently focuses on buildings, places, transportation, and admin data layers. 
  - The Overture Data Schema is documented in JSON Schema, using GeoJSON as a mental model. The final format for Overture deliveries is still to be defined.
  - Feature Geometries follow the OGC Simple Feature Access specifications.
  - Measurements use SI units (e.g. meters for building heights) and local units for regulations and restrictions (e.g. speed limits in mph in the US and km/h in Germany).

## map-data

- Overture data is licensed under the Community Database License Agreement – Permissive v2 (CDLA)

- https://github.com/OvertureMaps/data
  - Overture Maps data is available in cloud-native `Parquet` format.
  - The id column contains temporary IDs that are not yet part of the Global Entity Reference System (GERS).
  - The bbox column is a struct with the following attributes: minX, maxX, minY, maxY
  - The geometry column is encoded as WKB.
# dev

- 
