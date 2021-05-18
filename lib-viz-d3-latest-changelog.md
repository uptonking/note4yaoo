---
title: lib-viz-d3-latest-changelog
tags: [changelog, d3, lib, viz]
created: '2021-05-18T18:25:19.917Z'
modified: '2021-05-18T18:25:41.202Z'
---

# lib-viz-d3-latest-changelog

# guide

# changelog

- ref
  - [major changes](https://github.com/d3/d3/blob/master/CHANGES.md)

## v6.0--202008

- D3 now uses native collections (`Map` and `Set`) and accepts iterables. 
  - `d3.group` and `d3.rollup` are powerful new aggregation functions that replace d3.nest 
  - There are lots of new helpers in `d3-array`
- Remove `d3.event`
  - D3 now passes events directly to listeners, replacing the `d3.event` global and bringing D3 inline with vanilla JavaScript and most other frameworks.
- `d3-delaunay` replaces `d3-voronoi`
  - there’s a new `d3-geo-voronoi` for spherical (geographical) data

- Breaking Changes
  - Remove d3.event.
  - Remove d3.mouse/touch/clientPoint
  - Rename d3.histogram to d3.bin.
  - Rename d3.scan to d3.leastIndex.

## v5.0--201803

- D3 now uses Promises instead of asynchronous callbacks to load data.
- D3 now uses the Fetch API instead of XMLHttpRequest
  - `d3-request` module has been replaced by `d3-fetch`
- removes `d3-queue`
  - Use `Promise.all` to run a batch of asynchronous tasks in parallel, 
  - or a helper library such as `p-queue` to control concurrency.
- new `d3-scale-chromatic` replacing d3.schemeCategory20
- `selection.clone` for inserting clones of the selected nodes
- `d3.create` for creating detached elements

## v4.0--201606

- v4 is modular, instead of one library
- every symbol in D3 4.0 now shares a flat namespace rather than the nested one of D3 3.x.
  - `d3.scale.linear` is now `d3.scaleLinear`
- 4.0 uses only ASCII variable names and ASCII string literals (see rollup-plugin-ascii), avoiding encoding problems.
  - 3.x employed Unicode variable names such as λ, φ, τ and π for a concise representation of mathematical operations.
