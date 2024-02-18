---
title: toc-gis-mapping
tags: [gis, mapping, toc]
created: 2019-12-22T12:22:13.746Z
modified: 2021-01-04T16:21:18.990Z
---

# toc-gis-mapping

# awesome

- open-geo
  - https://www.osgeo.org/projects/
# geomapping
- green-gis /10Star/MIT/202009/ts
  - https://github.com/shengzheng1981/green-gis-js
  - https://green.ispongecity.com/
  - a lite GIS JS API based on Canvas API
  - Only Support Canvas! NO SVG!
- leaflet /BSD/29kStar/202009
  - https://github.com/leaflet/leaflet
  - https://leafletjs.com/
  - library for mobile-friendly interactive maps.
- mapbox-gl-js /BSD/6.3kStar/202009
  - https://github.com/mapbox/mapbox-gl-js
  - https://docs.mapbox.com/mapbox-gl-js/
  - https://docs.mapbox.com/help/troubleshooting/transition-from-mapbox-js-to-mapbox-gl-js/
- deck.gl /MIT/8kStar/202009
  - https://github.com/visgl/deck.gl
  - https://deck.gl/
  - WebGL2 powered geospatial visualization layers
  - 依赖luma.gl
- maptalks.js /3kStar/BSD/202012/js
  - https://github.com/maptalks/maptalks.js
  - A light JavaScript library to create integrated 2D/3D maps.
- protomaps.js /197Star/BSD/202107/ts
  - https://github.com/protomaps/protomaps.js
  - https://protomaps.com/docs/protomaps-js
  - Lightweight vector map rendering, labeling and symbology for the web
  - This project is a complete web map renderer - including quality label layout, pattern fills, and icons - in as simple as possible of an implementation. 
  - It's an alternative to renderers like Mapbox GL JS in a fraction of the size.
  - Render static maps to Canvas elements or interactive maps with Leaflet integration
  - Can read normal Z/X/Y tile URLs or offline, S3-hosted tile archives in PMTiles format
  - [what protomaps.js is, what protomaps.js is not](https://protomaps.com/docs/protomaps-js/)
    - It is not a continuous-zoom system. It displays map tiles at discrete integer zoom levels.
    - It is not a 3D renderer. Protomaps.js is focused on rendering 2D maps from OpenStreetMap data.
    - It is not based on WebGL. It instead uses the web-standard Canvas drawing API.
  - it works with PostGIS vector tiles! Added an example using @pwramsey 's pg_tileserv with Natural Earth data:
  - [Transitioning Protomaps from Open Core to Open Source - Protomaps Blog _20240216](https://protomaps.com/blog/open-core-to-open-source)
    - The core of Protomaps is the PMTiles format and ecosystem, which is an open spec in the public domain
    - The first Protomaps commercial product offering was a one-time basemap download - not an API, not a subscription, just a download with a big Buy Now button
    - The Protomaps Store is closed now, and everything previously proprietary is open source on GitHub.
    - a new Protomaps Commercial Distribution built from the Daylight Map subset of OSM can be a better fit for public-facing deployments by companies.
    - A monthly sponsorship gives you access to new versions.

- openlayers /BSD/7.4kStar/202009
  - https://github.com/openlayers/openlayers
  - https://openlayers.org/
  - feature-packed library for creating interactive maps on the web
- https://github.com/terrestris/react-geo
  - https://terrestris.github.io/react-geo/
  - A set of geo related modules to use in combination with React, Ant Design and OpenLayers.
- harp.gl /Apache2/664Star/202009
  - https://github.com/heremaps/harp.gl
  - https://harp.gl/
  -  open-source 3D map rendering engine written in TypeScript.
- carto /598Star/Apache2/202010/js
  - https://github.com/mapbox/carto
  - https://cartocss.readthedocs.io/
  - CartoCSS (short: Carto) is a language for map design.
  - It is similar in syntax to CSS, but builds upon it with specific abilities to filter map data and by providing things like variables.
  - It targets the Mapnik renderer and is able to generate Mapnik XML and a JSON variant of Mapnik XML. 
  - It can run from the command line or in the browser.
- https://github.com/Esri/calcite-maps
  - A Bootstrap theme for designing, styling and creating modern map apps.

- https://github.com/kothic/kothic-js
  - http://kothic.org/
  - a full-featured JavaScript map rendering engine using HTML5 Canvas. 
  - It was initially developed as a JavaScript port of Kothic rendering engine written in Python
# leaflet
- https://github.com/geoman-io/leaflet-geoman /js
  - https://geoman.io/leaflet-geoman
  - powerful leaflet plugin for drawing and editing geometry layers
# draw-on-map
- https://github.com/JamesLMilner/terra-draw /ts
  - https://terradraw.io/
  - Cross provider map drawing library, supporting Mapbox, MapLibre, Google Maps, OpenLayers and Leaflet out the box
  - Terra Draw centralises map drawing logic and provides a host of out the box drawing modes that work across different JavaScript mapping libraries
# 3d
- cesium /6.2kStar/Apache2/202009/js
  - https://github.com/CesiumGS/cesium
  - https://cesium.com/cesiumjs/
  - JS library for world-class 3D globes and maps

- https://github.com/dvgis/dc-sdk
  - 基于 Cesium 构建二、三维一体 WebGis 开发平台
  -  对 Turf、Heatmap、Mapv、Echarts 等常用可视化库和开源库的功能接入集成

- ViziCities /2.7kStar/BSD/201610/js
  - https://github.com/UDST/vizicities
  - A framework for 3D geospatial visualization in the browser
# collab
- https://github.com/alyssaxuu/mapus
  - Mapus is a tool to explore and annotate collaboratively on a map  
  - Draw, add markers, create lines and areas, find places to go, observe other users, and much more.
# utils
- https://github.com/stamen/toner-carto
  - "Toner" is the name of Stamen's black and white map tiles.
  - CartoCSS port of Toner

- https://github.com/forensic-architecture/timemap /js
  - TimeMap is a standalone frontend application that allows to explore and monitor events in time and space
  - TimeMap uses OpenStreetMap satellite imagery as a backdrop by default, but can also be configured to use mapbox.
  - The recommended way to run a backend for timemap is using datasheet-server.
# tiles
- https://github.com/apache/incubator-baremaps
  - http://baremaps.apache.org/
  - https://demo.baremaps.com/
  - Apache Baremaps is a toolkit and a set of infrastructure components for creating, publishing, and operating online maps.
  - It provides a data pipeline enabling developers to build maps with different data sources with live reload capabilities. 
# map-app
- https://github.com/giswqs/leafmap
  - https://leafmap.org/
  - A Python package for interactive mapping and geospatial analysis with minimal coding in a Jupyter environment

- https://github.com/mapbox/storytelling
  - This template is designed to accelerate building out a "scrollytelling" map story.
    - The output is an HTML and JavaScript file. 
    - These outputs can be hosted on any web-accessible location, with no extra code or infrastructure required. 
    - Note that embedding the output as an iFrame in another page will not work as expected. The scroll-driven interface requires the full page.
  - The template does not rely on any particular CSS framework, fonts, or images. 
    - There are some basic styles in the head of the HTML file that can be changed
