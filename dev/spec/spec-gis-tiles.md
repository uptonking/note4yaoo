---
title: spec-gis-tiles
tags: [gis, map-tiles, spec]
created: 2021-09-30T08:29:41.711Z
modified: 2021-09-30T08:30:09.395Z
---

# spec-gis-tiles

# guide

- resources
  - [地图瓦片加载计算原理介绍](https://zhuanlan.zhihu.com/p/546459841)
    - https://github.com/antvis/L7/tree/master/packages/utils/src/tileset-manager

## pmtiles vs mbtiles

- I believe this is protomaps approach: re-encode the mbtiles (sqlite-based ) format in to something that can be requested with a http range request and thus served from a single dumb webserver that doesn't need to understand sqlite or mbtiles parsing
  - This is the approach I took with protomaps/pmtiles, though it's optimized for the very specific use case of going from Z/X/Y integer coordinates to binary blobs, and takes shortcuts to accomplish that (fixed-width keys and root index page)

- SQLite-based nature of MBTiles is really a blocker for wider usage.
  - Great that PMTiles is trying to solve it using a principle similar to COG. 
  - It's a structured static file, so that tiles can be queried with HTTP range requests.
# PMTiles
- https://github.com/protomaps/PMTiles
  - https://protomaps.com/docs/pmtiles/
  - Cloud-optimized, single-file archive format for pyramids of map tiles
  - PMTiles is a single-file archive format for pyramids of tiled data. 
# discuss

## [This is super clever: - basically querying SQLite files from the browser. So I have to ask, how well would this work with mbtiles files on S3?](https://twitter.com/jimmyrocks/status/1388983562775539717)

- I really love the work that @bdon is doing with protomaps. I was trying a similar approach with the ESRI bundle files (vtpk), but his work is next level!

- PMTiles is an interesting approach, but to be clear it isn't using SQLite at all, and has a **custom binary layout**. The interesting question here is whether you can use existing MBTiles _directly_ with range requests, and how performant that would be.
  - I think overall PMTiles is a much better approach. The SQLite approach loads the index into memory & requests it as chunks. It leaves it up to the browser/WASM to reassemble the chunks back into tiles. This would probably lead to more reads from the server.
- PMTiles right now is designed to fulfill any tile read down to z14 in at most 3 fetches (2 directories + 1 tile) from a cold cache - and since map panning is highly localized, further close reads should be cache hits
- The marginal cost of a 1kb fetch vs 100kb fetch is not high (networking overhead) so I think these serverless approaches should optimize for few fetches; unfamiliar if SQLite can be forced to behave this way. What benefits would MBTiles have besides backwards compatibility ?
  - Of course you can serve SQLite from a server to HTTP z/x/y which is useful for renderers and existing services; working on a PMTiles solution for that protomaps/go-pmtiles which without needing SQLite is so dead simple it's a single 2mb static executable
  - I don't think SQLite would be able to optimize the fetches at all. I think the main drawback is the need to load the ~1.34mb WASM library to even perform the lookup. I agree that there isn't much real benefit.
- This is really cool! Really bridges the gap. Would it be possible to do something like this for lambda/api gateway? Keeping it serverless, while still supporting TMS.
  - Yes, though shape of solution become very vendor-specific and other concerns start leaking in (CORS, billing model, etc) - if you are already on lambda/API Gateway let me know and I can look into making it work on that

## [Releasing PMTiles, my new cloud-optimized archive format for "serverless" map applications](https://twitter.com/bdon/status/1377274271190319119?lang=en)

- A single PMTiles file can contain thousands of vector or raster tiles; 
  - served directly from S3 or other storage into your map renderer
- COGs(Cloud Optimized GeoTIFF, DEFLATE mode) are useful for backwards compatibility with GeoTIFF readers; I am seeking the minimum possible binary spec for ZXY data

- A map you can zoom+pan is just a video you can seek into; both are sequences of images, but map parts are arranged in space and not time
  - Seekable video already standardized on the web, time to do the same for the map
- The design isn't limited to geographic information; 
  - museum collections, documents can be displayed progressively at multiple resolutions with one file

---

- Looks like mutation requires rewriting all of the offsets, but entries could be added/modified by appending the new data, albeit leaving dead data? Eager to see the formal spec!
  - Yep, not designed for updates. I'll write a slightly more formal spec, but it's intentionally open-ended in some parts such as: metadata, ordering of entries and tiles

- If I understand what your doing, this is akin to an mbtile implementation that works well will http requests to access a specific tile on S3? If so love this approach! Quick q how big are the files? Say for a global dataset down to z 15? Great work man!
  - Directory overhead isn't a lot; z15 is challenging, a full pyramid is >1billion for that level, but the design affords deduplication since multiple entries can point to the same offset; other downside is HTTP Range broken with compression (see Transfer- vs Content-Encoding)
- How many requests to get an arbitrary leaf tile? 1 for headers + 1 for the tile? Are all of the range offsets contained in the 512k header, and that's why it's limited to L7?
  - One request for the headers+root directory L0-L7, and one more for L7-L14 dir. Beyond L14 I haven't thought about; beyond my current use case. But if your tree is sparse, like for part of a world, directories from multiple leaves can be combined (the reference impl does this)

## [protomaps: A new way to make maps with OpenStreetMap__202104](https://news.ycombinator.com/item?id=26918259)

- Existing formats like MBTiles are based on SQLite. This limits the ability to self-host maps to those confident running a server in production.
  - Originally, MBTiles was designed for mobile offline. 
  - Then, Mapbox started serving directly from the SQLite for web & other clients, creating the Node.js SQLite bindings in the process. 
  - Eventually, they had an `unpacker` for MBTiles uploads that would stick the tiles in CDN. 
  - So, really no more complex than old school static content hosting.
  - > Source: I created MBTiles
- I use the tile unpacker as well! I didn't point this out in the OP(protomaps), but I found the ergonomics of uploading tiles to S3 etc get bad once you're over a couple tens of thousands of tiles, as each upload has some overhead. I've tested PMTiles on S3 successfully with hundreds of millions of tiles. Deduplication is also important to save space on redundant ocean/earth tiles; MBTiles can deduplicate via views, PMTiles deduplicates by reference, but unpacked Z/X/Y tiles on S3 can't.
- When I was playing around with hosting rendered Minecraft slippy maps, I found the upload overhead to S3 to be pretty poor due to the “lots of tiny files” problem. (It renders as hundreds of thousands of rasterized image files for the various zoom levels). You could parallelize it, but it was still poor, and made me want to come up with a way to pack them into fewer files and fetch portions of them at render time so that the upload could be faster. It sounds like that’s what you did for the the PMTiles format?
  - **That's exactly what PMTiles is for**, and there's nothing in it specific to maps or geographic coordinates, **just a Z/X/Y pyramid structure**. I chose to support Leaflet for now because it is very popular; there's other viewers like OpenSeadragon for which a decoder plugin would be possible.
  - Fantastic. The renderer I was using was indeed leaflet based, so this sounds drop-in easy. The only **downside** would be that these maps are often re-rendered periodically and only have a few tiles that actually get updated. In that case, it’s nice to have to update only a handful of files. But I think the benefits would far outweigh the costs. Upload one massive file repeatedly is still gonna be faster I would think. Thanks!
- That was the impetus(动力，刺激) behind MBTiles as well. I was building out an iOS toolkit to render OSM-based maps on iPad, offline, and transferring 1000s of rasters (at the time) even over USB was way too slow and error-prone.
  - Thanks for this! I love SQLite, and think this is an **excellent use case**. (File systems, especially networked ones, don’t handle “lots of tiny files” well). I think using SQLite as the primary, writeable storage mechanism makes sense because I could ship that around easily to rendering nodes and incrementally update it easily. Then, I could export to a static PMTile for upload to S3 for serving purposes.

- You can already host vector tiles within S3 that work with Mapbox and other libraries. Not really sure what problem this is trying to solve.
  - The typical way to build and distribute Mapbox vector tiles has been by packing them into a sqlite database with individual rows for each Z/X/Y quad tree coordinate. This is what tools like `tippecanoe` typically produce.
  - **The problem** with this is it still requires a running server process colocated with that sqlite db in order to service requests for individual tiles, like what you'll receive from a client-side mapping library.
  - This project has a lot of different parts, but one of them is a spec for serving this type of data at low latency without a server by combining a custom packing format with S3 range-get requests to read individual tiles direct from blob storage. So that is certainly interesting for this kind of use-case.
- OP author here; one thing I didn't touch on is the way that most map services license their basemap data explicitly disallows "caching" which would be inclusive of hosting basemaps yourself on your own storage. So for the cases where it makes engineering or product sense to have your maps on S3, it goes against the dominant map business model.
