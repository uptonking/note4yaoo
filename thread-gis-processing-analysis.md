---
title: thread-gis-processing-analysis
tags: [analysis, geoprocessing, gis, thread]
created: '2021-03-26T11:28:39.211Z'
modified: '2021-05-25T08:41:18.938Z'
---

# thread-gis-processing-analysis

# pieces

- ## 

- ## 

- ## 

- ## Has anyone laid out concrete reasons for building shiny apps instead of using out-of-the-box enterprise software like Tableau?
- https://twitter.com/mdsumner/status/1304710241293012993
- Well arc topology doesn't exist in the SF standard, and geojson can't do this. 
  - TopoJSON was a web-era reconstruction of old Arc/Info vectors "arc-node" topology.
  - It's very much aligned to how it's used by D3, it's a mesh format kinda

- ## Difference between COG and GeoTIFF basically (but not only) is, that COG uses internal index.
- https://twitter.com/gdaltips/status/1405615640799551488
- To speedup work (e.g. in @QGIS ) with raster data, use gdaladdo script to create overviews. 
  - GeoTIFF will store overviews internally.
- And sometimes it is very useful thing to add `TILED=YES` option to geotiff creation command.
- Are overviews similar to pyramid layers?
  - You mean in QGIS? it uses the same tool, so yes.

- ## Thinking that GDAL, GEOS and QGIS all have C++ geometry classes (you know Point, LineString, etc.) implementing the same standard(s). Probably too late to fix history.
- https://twitter.com/EvenRouault/status/1383190934200942602
- IMO the problem is that geos doesn’t have support for curved geometries or m values. Otherwise it’d be a natural fit for a “common” geometry representation. (Alternatively we could make a new common library for JUST geometry representation storage...)
- IMO the problem is that the simple feature standard has only be thought through for Cartesian coordinates, but the earth is round. Why not go straight for S2 geometry? With "half-open polygons" S2 geometry also solves sfa / DE-9IM's lacking support for polygon coverages.
  - S2 is cool in this respect... Even though there is a point, line, and polygon class, the primary unit is an interface (Shape) with no requirements for how/if coordinates are in memory
  - S2 would be cool if it wasn't just 1D shapes ... polygons are just lines (topologically, the geometry can be spherical ... it can be  whatever as you say, it's unrelated to the topology ...)
- @postgis doing it right. @GRASSGIS is another world.

- ## I think I should write a blog post where I explain what's wrong with every single spatial file format.
- https://twitter.com/stevage1/status/1376721603405307908
- Bet you can’t find any fault with .shp files or any of the 42 mandatory files that go with it.
  - they're only good when exported from manifold with auxiliary xml
- @shapefiIe is RUBBISH! GeoJSON is RUBBISH! @GeoPackage1 is RUBBISH! MapInfo TAB is RUBBISH! GeoBuf is RUBBISH! GML is RUBBISH! KML is RUBBISH! PostGIS geometry is RUBBISH! PostGIS geography is RUBBISH! CSVs with lat/lon are RUBBISH! TopoJSON is RUBBISH!
  - we can automate this with gdalinfo --formats
