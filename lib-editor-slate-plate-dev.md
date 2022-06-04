---
title: lib-editor-slate-plate-dev
tags: [plate, slate, text-editor]
created: '2022-06-03T20:18:16.778Z'
modified: '2022-06-03T20:18:42.086Z'
---

# lib-editor-slate-plate-dev

# guide

- features
  - simple to start with only one component `<Plate>`.
  - zustand store is internally used to support multiple editor states.
  - provide a default design system for quick start 
    - but you can plug-in your own one using a single function.
  - enforce separation of concerns by packaging each feature for build optimization and versioning.
  - All plugins accept extensible options 
    - if you need to fork a plugin, all its functions are exported.
  - TypeScript types
