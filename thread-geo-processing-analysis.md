---
title: thread-geo-processing-analysis
tags: [analysis, geoprocessing, thread]
created: '2021-03-26T11:28:39.211Z'
modified: '2021-03-26T11:29:22.438Z'
---

# thread-geo-processing-analysis

# pieces

- ## 

- ## I think I should write a blog post where I explain what's wrong with every single spatial file format.
- https://twitter.com/stevage1/status/1376721603405307908
- Bet you can’t find any fault with .shp files or any of the 42 mandatory files that go with it.
  - they're only good when exported from manifold with auxiliary xml
- @shapefiIe is RUBBISH! GeoJSON is RUBBISH! @GeoPackage1 is RUBBISH! MapInfo TAB is RUBBISH! GeoBuf is RUBBISH! GML is RUBBISH! KML is RUBBISH! PostGIS geometry is RUBBISH! PostGIS geography is RUBBISH! CSVs with lat/lon are RUBBISH! TopoJSON is RUBBISH!
  - we can automate this with gdalinfo --formats

