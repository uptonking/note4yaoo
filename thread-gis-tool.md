---
title: thread-gis-tool
tags: [gis, thread, tool]
created: 2021-05-25T08:39:27.936Z
modified: 2021-05-25T08:40:27.880Z
---

# thread-gis-tool

# guide

# discuss
- ## 

- ## 

- ## 

- ## [A POI Database in One Line | Drew Breunig _202404](https://www.dbreunig.com/2024/04/18/a-poi-database-in-one-line.html)
  - This week, the Overture Maps Foundation released a handy command-line tool for downloading a subset of the Overture dataset.
  - This command downloads a GeoJSON file containing all the Overture buildings in a chunk of Boston. We’re outputting GeoJSON to a local file named boston.geojson.
  - we can pipe to Simon Willison’s geojson-to-sqlite

- ## Two people are claiming to be an expert in your field, one is and one is faking. What question do you ask to find the imposter?
- https://twitter.com/bdon/status/1520306344318095361
  - "run Douglas–Peucker on all the individual parts" is not an acceptable answer
  - [多顶点折线简化算法 Douglas-Peucker算法](https://www.jianshu.com/p/33daae916175)
- To be an expert do I need to just say apply ST_SimplifyGeometry or do I need to know the name of the algorithm applied?
  - How do you simplify a polygon _without using JTS or a derivative_…

- ## Anyone know how to use Overpass Turbo to run queries that generate a lot of data, to save as GeoJSON, without attempting to render them in the browser?
- https://twitter.com/stevage1/status/1407454768646156291
- I always use query-overpass to do the job (use the same lib as the one used in the https://overpass-turbo.eu to do the conversion to GeoJSON). You have some options to flatten GeoJSON properties.
  - Make queries to OpenStreetMap's overpass API and output as GeoJSON.
- That generates OSM JSON, not GeoJSON, so then I'd have to go through an extra processing step locally
- https://observablehq.com/@georift/overpass-to-geojson
