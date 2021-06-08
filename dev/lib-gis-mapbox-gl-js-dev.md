---
title: lib-gis-mapbox-gl-js-dev
tags: [gis, lib, mapbox-gl-js]
created: '2020-12-23T10:50:16.346Z'
modified: '2021-01-04T16:27:30.895Z'
---

# lib-gis-mapbox-gl-js-dev

# guide

- todo
  - glue between mapbox-gl and deck.gl
# mapbox-gl-js v2s

# discuss

- ## What other alternatives exist?
- https://news.ycombinator.com/item?id=25349195
- Openlayers has web GL support but not for vector tiles and I would like to have fast vector tiles
- It's unfair to call Leaflet dead
  - What someone can see as less development activity is simply a sign of a mature product that doesn't need many new features and changes to remain useful — focusing on the core basic mapping needs has always been its goal, and it continues to adhere to it.
- I wrote a really good incremental tile based renderer for leaflet that could easily be adapted for vector tiles.
- +1 for CesiumJS, they have been doing 3D since ages
  - but no vector tiles support
  - It has had 3D tiles for a long time. Not Mapbox 2D vector tiles though.
- Note that deck.gl was originally developed inside Uber, but was donated to the Urban Computing Foundation (part of the Linux Foundation) and is now under open governance.
