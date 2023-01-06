---
title: spec-gis-shapefile-arcgis-geodatabase
tags: [arcgis, geodatabase, gis, shapefile, spec]
created: 2021-09-30T07:49:11.214Z
modified: 2021-09-30T08:07:04.860Z
---

# spec-gis-shapefile-arcgis-geodatabase

# guide

# blogs

## [Switch from Shapefile](http://switchfromshapefile.org/)

- ESRI Shapefile is a file format for storing geospatial vector data. 
  - It has been around since the early 1990s and is still the most commonly used vector data exchange format.

### The good side

- Here are some reasons why Shapefile is so heavily used:
- Shapefile is by far the most widely supported format in existing software packages.
- While the format is proprietary, the specification is open.
- For many use cases, it is good enough.
  - Its index file (*.shx) contains the offset and length of each feature in the main file (*.shp) which enables good reading performance.
  - It is relatively efficient in terms of file size. The resulting file, even un-zipped, is relatively small compared to some other (mostly text-based) formats.

### Shapefile is a bad format

- Here are several reasons why the Shapefile is a bad format and you should avoid its usage:
- No coordinate reference system definition.
  - By default there is no definition of the coordinate reference system used. 
  - You can do it using e.g. `.prj`, but first: this is not standard part of the specification and second, there are still some issues
- It's a multifile format.
  - Shapefile format uses at least 3 files (`*.shp, *.dbf, *.shx`). Users cannot share just one file; you must send them all.
  - thanks to modular, extensible architecture it can have 12+ sidecar files, 3 of which are mandatory.
  - In addition, other geospatial software packages routinely add their own extensions to try to overcome Shapefile limitations. Custom additions are not supported by other tools and limit interoperability.
- Attribute names are limited to 10 characters.
  - Longer names are usually automatically shortened. 
- Only 255 attributes. 
  - The DBF file does not allow you to store more then 255 attribute fields.
- Limited data types. 
  - Data types are limited to float, integer, date and text with a maximum 254 characters.
  - there is no support for big integers
  - There is no support for more advanced data fields such as blobs, images or arrays.
- Unknown character set. 
  - There is no way to specify the character set used in the database.
  - Many applications are using the old Windows-* or ISO-* data encodings, while nowadays we are tending to use UTF-8 more. 
  - Still there is no way to specify this in file header.
  - The support for Unicode characters is also very limited.
- It's limited to 2GB of file size. 
  - Although some tools are able to surpass this limit, they can never exceed 4GB of data.
  - The size of both `.shp and .dbf` component files cannot exceed 2 GB. 
  - GDAL Shapefile driver overcomes this limit, but the Shapefile format explicitly uses 32bit offsets and so cannot go over 8GB (it actually uses 32bit offsets to 16bit words), but the OGR shapefile implementation has a limitation of 4GB.
- No topology in the data. 
  - There is no way to describe topological relations in the format.
  - Shapefile is simple-feature format. There is no way to store more complex geometry relationships.
- No mixed geometry
  - Single geometry type per file. 
  - There is no way to save mixed geometry features.
  - Each file can be only one of the supported geometry formats (Point, Line, Polygon and others). Mixed geometry features are not possible.
- More complicated data structures are impossible to save. It's a "flat table" format.
  - The data structure is limited to flat tables with no hierarchies, relations or tree structure.
- Very limited 3D support
  - Shapefile can't store material definitions nor textures (images with texture coordinates). 
  - 3D models are stored as a triangle or polygon soup, with no watertight models or parametric geometries being supported.
  - There is no way to store 3D data with textures or appearances such as material definitions. 
  - There is also no way to store solids or parametric objects.
- Projection Definition Inconsistencies. 
  - By default, Shapefile contains no information about coordinate reference system at all. 
  - But some software packages do accept `*.prj` files, which may contain CRS description.
  - It uses Esri WKT definitions, which are often incompatible with standard definitions in EPSG or other sources regarding aspects such as axis order or unit definitions. 
  - Furthermore, they often miss parameters required for reprojection ("Missing Bursa Wolf Parameters", anyone?)
- Multi part features has to be defined per-feature
  - Line and polygon geometry type, single or multipart, cannot be reliably determined at the layer level, it must be determined at the individual feature level.
  - This leads to inconsistency during automatic data processing, you can not relay on input geometry type and test each feature, whether it is single geometry or multiple geometries.
- There is no NULL value
  - There is no way to mark no data in a field of the attribute table. 
  - You cannot distinguish zero and no data for numerical fields.

### Alternatives

- To be honest, no alternative format has overthrown the Shapefile hegemony yet. 
  - Some formats nearly took over (KML, GML, GeoJSON), but their usage was limited to relatively narrow use cases only.
  - Although there are more then 80 vector data formats([gdal vector drivers](https://gdal.org/drivers/vector/index.html)) in use out there, only a few can be considered as candidates for Shapefile replacement. 

- geopackage features
  - SQLite as backend
  - File based, single file
  - **Vectors, rasters**
  - Official extensions
  - Supported in many software packages

- flatgeobuf features
  - Binary encoding based on FlatBuffers
  - File based, single file
  - Vectors
  - Can be efficiently serialized and **streamed** (read/write)
- We recommend FlatGeobuf as a Shapefile replacement for scenarios where performance is critical and system to system integrations. 
  - Because of the **streaming capabilities**, it is also suitable as an alternative WFS output format and is available as an official extension to GeoServer.

- geojson features
  - JSON format: **human-readable**, text-based format
  - File based
  - Can handle complex data
  - File size grows fast
  - IETF Standard

- spatialite features
  - File based
  - SQL database
  - OGC Simple Features
- SpatialLite lacks the support for extensions or raster data present in GeoPackage. 
  - While these are not necessarily must-have features, they may be useful. 
  - Like GeoPackage, it is unsuitable for streaming.
- Since **SpatiaLite offers no clear advantages over GeoPackage** at this time, it should only be considered as a Shapefile replacement in niche scenarios.

- arcgis geodatabase features
  - proprietary, closed format
  - native data structure for ArcGIS
  - file-based (or database based)
  - complex data models
