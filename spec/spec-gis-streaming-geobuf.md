---
title: spec-gis-streaming-geobuf
tags: [geobuf, gis, spec, streaming]
created: '2021-09-30T08:15:38.824Z'
modified: '2021-09-30T08:17:00.070Z'
---

# spec-gis-streaming-geobuf

# guide

- flatgeobuf features
  - Binary encoding based on FlatBuffers
  - File based, single file
  - Vectors
  - Can be efficiently serialized and **streamed** (read/write)
- We recommend FlatGeobuf as a Shapefile replacement for scenarios where performance is critical and system to system integrations. 
  - Because of the **streaming capabilities**, it is also suitable as an alternative WFS output format and is available as an official extension to GeoServer.
# docs
