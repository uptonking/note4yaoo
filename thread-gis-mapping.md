---
title: thread-gis-mapping
tags: [gis, mapping, thread]
created: 2021-03-26T11:27:57.480Z
modified: 2021-05-25T08:41:02.257Z
---

# thread-gis-mapping

# discuss

- ## 

- ## Protomaps is moving from being "open-core", or partly proprietary, to an open source project. 
- https://twitter.com/protomaps/status/1642060504741867520
  - The only closed part has been the basemap planet.pmtiles generation; an open source implementation is WIP here! 

- ## I haven't checked in on the harp.gl WebGL vector tile renderer in a while, but it looks like it's either stopped development or gone closed source
- https://twitter.com/bdon/status/1599698770262118403
  - Without harp/tangram, @maplibre is the only open source WebGL option left?
- https://gitlab.com/IvanSanchez/gleo is promising! I don’t think it has implemented labeling yet, which in my (biased) opinion is >50% of the complexity of these libraries
- At some point I'll make a Gleo plugin for Leaflet, but right now it's a standalone one-person project (I know, website is lacking).
  - Text label collisions are, indeed, a (very) hard problem to solve (and the collision algorithms can only run in CPU, not GPU)
  - Also, Gleo is the only GPL-licensed WebGL map library out there. That **should** please folks worried about libraries going closed-source.

- deck.gl can render manually styled data from MVT. There is no support for Mapbox style spec yet though

- ## Maps in Slack using quick-map
- https://sparkgeo.com/quick-map-landing-page/
  - The quick-map slash command uses Mapbox Static Images and Geocoding APIs to convert an address or pair of coordinates into a simple map.

- ## The new Static Playground -- now, developers can see how Static Images API responses will look based on the position, resolution, padding, overlays, and any style parameters
- https://twitter.com/Mapbox/status/1382449857097515008

- ## Roofs on 3D buildings are now level relative to the earth rather than the terrain. 
- https://twitter.com/Mapbox/status/1382457903513231364
  - Level roofs are now drawn for all fill-extrusion layers drawn on top of terrain. 
  - @Mapbox GLJS v2.2.0 just launched

- ## Voronoi polygons for hover interactivity of points are popular and make sense to dataviz practitioners but maybe we should have been teaching people how to use quadtrees instead? 
- https://twitter.com/Elijah_Meeks/status/1378880759713333252
  - Familiarity with quadtrees is more valuable in the long-term and gives greater dataset flexibility.
  - As far as flexibility, you can do the same radius-constrained lookup, but you can also use quadtree hierarchies for clustering. 
  - As for long-term value, understanding quadtrees and spatial search is better than proficiency with an otherwise seldom-used visualization approach.
- voronoi/quadtree hover overlays look cool, but i don't think there's any number of points where they're actually the best choice
  - low n: just check every point onmousemove instead
  - high n: computing a voronoi locks up the browser
- Any reference for beginners?
  - The quadtree from #d3js is something I'm most familiar with and is well-documented and easy to use. I have never written any tutorials about it and haven't seen any, though.
