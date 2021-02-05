---
title: toc-gis-mapping-carto
tags: [carto, gis, mapping]
created: '2020-11-13T07:58:23.358Z'
modified: '2021-01-04T16:21:29.894Z'
---

# toc-gis-mapping-carto

# popular-mapbox-carto-esri

# [mapbox repos](https://github.com/search?o=desc&q=user%3Amapbox&s=stars&type=Repositories)

- https://github.com/maplibre/maplibre-gl-js
  - /558Star/BSD/202012/js
  - a community led fork derived from mapbox-gl-js
  - The primary goal is consistency and backwards-compatability with previous releases and continued bug-fixes and maintenance going forward.
  - 最后的v1版本号为v1.13.0(20201119)
  - https://github.com/cgcs2000/mapbox-gl-js
    - a fork of mapbox/mapbox-gl-js, adding support for CGCS2000.
  - https://github.com/socrata/mapbox-gl-js
    - Support for clustering points like supercluster by SOQL(Salesforce)

- https://github.com/mapbox/mapbox-gl-js
  - https://github.com/mapbox/mapbox-gl-js/tree/v1.13.0
  - /7.1kStar/BSD/202012/js
  - customizable maps in the browser, powered by vector tiles and WebGL
  - It takes map styles that conform to the Mapbox Style Specification, applies them to vector tiles that conform to the Mapbox Vector Tile Specification, and renders them using WebGL.
  - Mapbox gl-js version 2.0 or higher (“Mapbox Web SDK”) must be used according to the Mapbox Terms of Service.
  - [v2.0.0(20201209) changes merged with updated TOS and license](https://github.com/mapbox/mapbox-gl-js/issues/10162)
    - v2: reducing map load time by 30%, 3D terrain rendering, new satellite imagery, a low level camera API, and a new sky layer type
    - All new features and improvements will only be available in v2.
    - Mapbox GL JS v2+ are governed by the Mapbox Terms of Service (this is a change from the old v1 3-clause BSD license).
- https://github.com/mapbox/mapbox-gl-native
  - customizable maps in native Android, iOS, macOS, Node.js, and Qt applications
  - A C++ library that powers customizable vector maps in native applications on multiple platforms 
  - by taking stylesheets that conform to the Mapbox Style Specification, applying them to vector tiles that conform to the Mapbox Vector Tile Specification, and rendering them using OpenGL or Metal.
  - Mapbox GL JS is the WebGL-based counterpart to Mapbox GL Native that is designed for use on the Web.
- https://github.com/mapbox/mapbox.js
  - A Mapbox plugin for Leaflet, a JS library for traditional raster maps.
  - For the state-of-the-art Mapbox vector maps library, see Mapbox GL JS
- https://github.com/mapbox/carto
  - CartoCSS (short: Carto) is a language for map design. 
  - It is similar in syntax to CSS, but builds upon it with specific abilities to filter map data and by providing things like variables. 
  - It targets the Mapnik renderer and is able to generate Mapnik XML and a JSON variant of Mapnik XML.
  - It can run from the command line or in the browser.
- https://github.com/mapbox/vector-tile-spec
  - A specification for encoding tiled vector data.
  - https://github.com/mapbox/awesome-vector-tiles
    - awesome implementations of the Mapbox Vector Tile specification
- https://github.com/mapbox/geojson-vt
  - Slice GeoJSON into vector tiles on the fly in the browser
  - primarily designed to enable rendering and interacting with large geospatial datasets on the browser side (without a server).
  - Created to power GeoJSON in Mapbox GL JS, but can be useful in other visualization platforms like Leaflet, OpenLayers and d3, as well as Node.js server applications.
  - Resulting tiles conform to the JSON equivalent of the vector tile specification
  - https://github.com/mapbox/geojson-vt-cpp
    - Port to C++ of JS GeoJSON-VT for slicing GeoJSON into vector tiles on the fly
- https://github.com/mapbox/tippecanoe
  - Builds vector tilesets from large (or small) collections of GeoJSON, Geobuf, or CSV features, like these.
  - The goal of Tippecanoe is to enable making a scale-independent view of your data
- https://github.com/mapbox/rasterio
  - Rasterio reads and writes geospatial raster datasets with gdal
- https://github.com/mapbox/robosat
  - Semantic segmentation on aerial and satellite imagery.
  - Extracts features such as: buildings, parking lots, roads, water, clouds
  - Robosat is neither maintained not actively developed any longer by Mapbox.
  - RoboSat is an end-to-end pipeline written in Python 3 for feature extraction from aerial and satellite imagery. 
- https://github.com/mapbox/geojson.io
  - A fast, simple editor for map data.
- https://github.com/mapbox/supercluster
  - fast geospatial point clustering library for browsers and Node.
- https://github.com/mapbox/geobuf
  - A compact binary encoding for geographic data.
  - Geobuf provides nearly lossless compression of GeoJSON data into protocol buffers.
- https://github.com/mapbox/pbf
  - A low-level protocol buffers implementation in JavaScript.
  - A low-level, fast, ultra-lightweight (3KB gzipped) JavaScript library for decoding and encoding protocol buffers
  - Works both in Node and the browser.
- https://github.com/mapbox/osm-bright
  - A Carto template for OpenStreetMap data

- more
  - https://github.com/mapbox/node-sqlite3
    - Asynchronous, non-blocking SQLite3(C语言) bindings for Node.js
  - https://github.com/mapbox/pixelmatch
    - fastest JavaScript pixel-level image comparison library,originally created to compare screenshots in tests.
    - Features: accurate anti-aliased pixels detection and perceptual color difference metrics.
    - Inspired by Resemble.js and Blink-diff, however pixelmatch is around 150 lines of code, has no dependencies, and works on raw typed arrays of image data, 

# [carto repos](https://github.com/search?o=desc&q=user%3Acartodb&s=stars&type=Repositories)

- https://github.com/CartoDB/cartodb
  - /2.5kStar/BSD/202012/js/ruby
  - CARTO Engine, our embeddable platform for web and mobile apps
  - CARTO Builder, a drag and drop analysis tool.
  - With CARTO, you can upload your geospatial data (Shapefiles, GeoJSON, etc) using a web form and then make it public or private.
    - After it is uploaded, you can visualize it in a dataset or on a map, search it using SQL, and apply map styles using CartoCSS. 
    - You can even access it using the CARTO APIs, or export it to a file.

- https://github.com/CartoDB/carto.js
  - CARTO.js is a JavaScript library to create custom location intelligence applications that leverage the power of CARTO. 
  - It is the library that powers Builder and it is part of the Engine ecosystem.

- https://github.com/CartoDB/cartoframes
  - A Python package for integrating CARTO maps, analysis, and data services into data science workflows.
  - Python data analysis workflows often rely on the de facto standards pandas and Jupyter notebooks.
  - CARTOframes give the ability to communicate reproducible analysis while providing the ability to gain from CARTO's services like hosted, dynamic or static maps and Data Observatory augmentation.

- https://github.com/CartoDB/torque
  - Render big, timeseries data in the client. 
  - Uses CartoDB to generate a datacube format. 

- https://github.com/CartoDB/Windshaft
  - A Node.js map tile library for PostGIS and torque.js, with CartoCSS styling

# [esri repos](https://github.com/search?o=desc&q=user%3Aesri&s=stars&type=Repositories)

- https://github.com/Esri/esri-leaflet
  - Leaflet plugins for working with a handful of the most popular ArcGIS Service types. 
  - This includes Esri basemaps and feature services, as well as tiled map, dynamic map and image services.
  - The goal of this project is not to replace the ArcGIS API for JavaScript 
    - but rather to provide small components for only some aspects of the ArcGIS platform for developers who prefer leaflet
- https://github.com/Esri/arcgis-python-api
  - a Python library for working with maps and geospatial data, powered by web GIS.
- https://github.com/Esri/terraformer
  - A geographic toolkit for dealing with geometry, geography, formats, and building geo databases
  - Terraformer Core - Contains methods and objects for working with GeoJSON.
  - WKT Parser - Parse Well Known Text into GeoJSON and vice versa.
  - ArcGIS Geometry Parser - Parse the ArcGIS Geometry Format into GeoJSON and vice versa.
  - GeoStore - A framework for persisting and querying GeoJSON features with pluggable indexes and persistent stores.
- https://github.com/Esri/wind-js
  - demo animation of wind on a Canvas layer
  - this project uses nothing but an HTML5 Canvas element and pure Javascript.
  - https://github.com/cambecc/earth
- https://github.com/Esri/bootstrap-map-js
  - JS/CSS extension for building awesome mapping apps with Bootstrap3 and ArcGIS.
- https://github.com/Esri/calcite-maps
  - The framework is designed to work with the ArcGIS JS 3.x, 4.x and Esri-Leaflet API. with Bootstrap3
- https://github.com/Esri/cedar
  - JavaScript Charts for ArcGIS
  - powered by data from ArcGIS maps, scenes, and services
  - include smart default visualization choices
  - Cedar uses amCharts library as it's charting engine. 
  - Cedar also uses @esri/arcgis-rest-feature-layer and @esri/arcgis-rest-request to query feature data. 
- https://github.com/Esri/storymap-tour
  - By downloading the template and putting it on your own web server or website, you can make unlimited customizations and changes to the template

# more
