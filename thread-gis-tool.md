---
title: thread-gis-tool
tags: [gis, thread, tool]
created: '2021-05-25T08:39:27.936Z'
modified: '2021-05-25T08:40:27.880Z'
---

# thread-gis-tool

# guide

# tooling
- GADM maps and data
  - https://gadm.org/index.html
  - GADM provides maps and spatial data for all countries and their sub-divisions. 
  - You can browse our maps or download the data to make your own maps.
# discuss
- ## Anyone know how to use Overpass Turbo to run queries that generate a lot of data, to save as GeoJSON, without attempting to render them in the browser?
- https://twitter.com/stevage1/status/1407454768646156291
- I always use query-overpass to do the job (use the same lib as the one used in the https://overpass-turbo.eu to do the conversion to GeoJSON). You have some options to flatten GeoJSON properties.
  - Make queries to OpenStreetMap's overpass API and output as GeoJSON.
- That generates OSM JSON, not GeoJSON, so then I'd have to go through an extra processing step locally
- https://observablehq.com/@georift/overpass-to-geojson
