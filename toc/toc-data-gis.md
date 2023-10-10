---
title: toc-data-gis
tags: [datasource, gis]
created: 2020-11-13T08:01:05.045Z
modified: 2021-01-04T16:20:47.941Z
---

# toc-data-gis

# guide

- Spatial Data sources Notion Pages
  - https://vlckel.notion.site/vlckel/a360dea317234868a0f7cfb1ef249843
# popular
- https://github.com/amcharts/amcharts4-geodata
  - 大多json，少数js

- https://github.com/giswqs/geospatial-data-catalogs
  - open geospatial datasets available on AWS, Earth Engine, Planetary Computer, NASA CMR, and STAC Index

- [google spreadsheets list of GIS data sources](https://docs.google.com/spreadsheets/d/1utQRlrX3lJniBjWE3rNjLZeTRsbjH-zdjxNmXhhvO9Q/edit#gid=47)
# tiles
- https://github.com/michael-laoyu/MapTileGenerator /inactive
  - 依赖c#
  - 支持TMS、WMTS标准瓦片下载，支持百度地图瓦片、高德地图瓦片、腾讯地图瓦片、天地图、ArcGIS Rest、geoserver等瓦片下载。
  - 默认以png文件方式保存瓦片，也支持以sqlite（mbtiles格式）保存瓦片。
# 3d
- https://github.com/hobu/usgs-lidar
  - https://registry.opendata.aws/usgs-lidar/
  - WS Entwine Point Tiles USGS LiDAR Public Dataset
# more-geo-data
- https://github.com/djaiss/mapsicon
  - /2kStar/MentionLic/201707/python
  - collection of maps for every country in the world, available in 11 sizes or in SVG.

- https://github.com/martgnz/bcn-geodata
  - The official shapefiles of Barcelona, converted to GeoJSON and TopoJSON

- https://www2.gov.bc.ca/gov/content/data/geographic-data-services/lidarbc
  - This LiDAR data includes LAZ point cloud data and various LiDAR-derived products.

- https://github.com/opengeos/open-buildings /python
  - https://opengeos.github.io/open-buildings
  - a set of useful scripts for getting and converting Open Building Datasets using Cloud Native Geospatial formats. 
  - Initially the focus is on Google's Open Buildings dataset and Overture's building dataset.
  - get_buildings command lets you supply a GeoJSON file to a command-line interface and it'll download all buildings in the area supplied, output in common GIS formats (GeoPackage, FlatGeobuf, Shapefile, GeoJSON and GeoParquet).
