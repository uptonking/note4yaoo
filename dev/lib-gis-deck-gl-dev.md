---
title: lib-gis-deck-gl-dev
tags: [deck.gl, gis, lib]
created: 2021-06-22T11:15:36.202Z
modified: 2021-06-22T11:23:05.135Z
---

# lib-gis-deck-gl-dev

# guide

- features
  - Performant rendering and updating of large data sets
  - Interactive event handling such as picking, highlighting and filtering
  - Cartographic projections and integration with major basemap providers
  - A catalog of proven, well-tested layers
  - Deck.gl is designed to be highly customizable.
    - All layers come with flexible APIs to allow programmatic control of each aspect of the rendering. 
    - All core classes such are easily extendable by the users to address custom use cases.
# docs

## overview

- deck.gl /8.8kStar/MIT/202106/js
  - https://github.com/visgl/deck.gl
  - https://deck.gl/docs
  - https://vis.gl/
  - WebGL2 powered geospatial visualization layers
  - deck.gl is designed to simplify high-performance, WebGL-based visualization of large data sets. 
  - deck.gl maps data (usually an array of JSON objects) into a stack of visual layers - e.g. icons, polygons, texts; and look at them with views: e.g. map, first-person, orthographic.

- The deck.gl core library and layers have no dependencies on React or Mapbox GL and can be used by any JavaScript application.
- While not directly based on React, deck.gl is designed from ground up to work with React based applications. 
  - deck.gl layers fit naturally into React's component render flow and flux/redux based applications. 
  - deck.gl layers will be performantly rerendered whenever you rerender your normal JSX or React components.

- While deck.gl works independently without any map component, when visualizing geospatial datasets, a base map can offer the invaluable context for understanding the overlay layers.
  - deck.gl has been designed to work in tandem with popular JavaScript base map providers, especially Mapbox. 

## integrations

### @deck.gl/mapbox

- Use deck.gl layers as custom Mapbox layers, enabling seamless interleaving of Mapbox and deck.gl layers.
- Advantages
  - Mapbox and deck.gl layers can be freely "interleaved", enabling a number of layer mixing effects, such as drawing behind map labels, z-occlusion between deck.gl 3D objects and Mapbox buildings, etc.
  - Mapbox and deck.gl will share a single canvas and WebGL context, saving system resources.
- Limitations
  - deck.gl's multi-view system cannot be used.
  - Unless used with react-map-gl, WebGL2 based deck.gl features, such as attribute transitions and GPU accelerated aggregation layers cannot be used.
  - Mapbox 2.0's terrain feature is currently not supported.

### @deck.gl/arcgis

- Use deck.gl layers with the ArcGIS API for JavaScript.
- Supported deck.gl features:
  - Layers
  - Effects
  - Attribute transitions
  - Auto-highlighting
  - onHover and onClick callbacks
- Not supported features:
  - Multiple views
  - Controller
  - React integration

### @deck.gl/google-maps

- Use deck.gl layers as a custom Google Maps overlay.
- Supported deck.gl features:
  - Layers
  - Effects
  - Auto-highlighting
  - Attribute transitions
  - onHover and onClick callbacks
  - Tooltip
- Not supported features:
  - Tilting
  - Views
  - Controller
  - React integration
  - Gesture event callbacks (e.g. onDrag*)
