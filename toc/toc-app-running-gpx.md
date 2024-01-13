---
title: toc-app-running-gpx
tags: [app, gpx, running, toc]
created: 2022-02-23T18:57:58.521Z
modified: 2022-02-23T18:59:51.587Z
---

# toc-app-running-gpx

# guide
- 导出nike run club的数据
  - [n+exporter](https://nexporter.bullrox.net/)
  - 支持导出gpx和tcx，部分数据只有tcx而没有gpx格式
  - 支持直接将数据上传到 strava和runkeeper

- nike问题数据记录，由tcx转换得到的pgx经纬度全为0，需要寻找新的有效的转换工具
  - 20170114.gpx
  - 20170110.gpx
  - 20170107.gpx
  - 20161004-0.3km.gpx
  - 20160902-3km.gpx
  - 20160904.gpx
  - 20160822.gpx
# popular
- https://github.com/erik/derive
  - https://erik.github.io/derive/
  - Generate a heatmap from GPS tracks.
  - No data is ever uploaded, everything is done client side. 

- https://github.com/gpxstudio/gpxstudio.github.io
  - https://gpx.studio/
  - The online GPX file editor

- https://github.com/yihong0618/running_page
  - https://running-page.vercel.app/
  - Make your own running home page
  - GitHub Actions manages automatic synchronization of runs and generation of new pages.
  - Gatsby-generated static pages, fast
  - Support for Vercel (recommended) and GitHub Pages automated deployment
  - Mapbox for map display
  - Supports most sports apps such as nike strava...
  - If you don't want to make the data public, you can choose strava's fuzzy processing, or private repositories.

- https://github.com/janmonschke/gpx-editor /202111/ts
  - A simple GPX viewer and editor


# utils for gpx/fit
- https://github.com/sports-alliance/sports-lib
  - Sports Lib tries to achieve a common domain model and lib for sport activity formats such as GPX, TCX, FIT and other popular formats.
  - Currently the support is limited to the main formats: GPX, TCX, FIT and JSON*
  - 提供了转换示例
    - Example converting a FIT file to GPX

- https://github.com/mapbox/togeojson
  - converts KML & GPX to GeoJSON, in a browser or with Node.js.
  - Dependency-free

- https://github.com/Luuka/GPXParser.js
  - parse .gpx file and get or compute various data

- https://github.com/stefanocudini/gpx-simplify-optimizer
  - Online Simplifier and Optimizer for GPX / GeoJSON / KML tracks.

- https://github.com/mpetazzoni/leaflet-gpx
  - allows for the analysis and parsing of a GPX track in order to display it as a Leaflet map layer

- https://github.com/tumic0/GPXSee
  - https://www.gpxsee.org/
  - GPS log file viewer and analyzer with support for GPX, TCX, KML, FIT, IGC, NMEA, SLF, SML, LOC, GPI, GeoJSON and OziExplorer files.
# running
- https://github.com/flopp/GpxTrackPoster
  - Create a visually appealing poster from your GPX tracks

- https://github.com/jedie/django-for-runners
  - Store your GPX tracks of your running (or other sports activity) in django.
# more-repos
