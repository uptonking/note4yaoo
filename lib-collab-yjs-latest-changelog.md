---
title: lib-collab-yjs-latest-changelog
tags: [changelog, yjs]
created: 2024-04-06T16:54:16.943Z
modified: 2024-04-06T16:54:27.145Z
---

# lib-collab-yjs-latest-changelog

# guide

# roadmap

# changelog

## v14

- v14.0.0-1_2023-06-28
  - remove toDom methods

- [v14.0.0-0_2022-08-19](https://github.com/yjs/yjs/releases/tag/v14.0.0-0)
  - This PR enables single-range moves in `Y.Array`s. 
  - The data structure is forwards compatible. That means that v14 can read v13 updates, but v13 can't read v14 updates (if content has ever been moved).
  - The feature is stable. I plan to do a couple of breaking API changes before I make a final v14 release.
  - Remove apis that use the DOM (e.g. toDOM)
  - extend move info field by three bits for future usage
  - remove old move-ranges if collapsed 

## v13

- v13.6.0_2023-04-23
  - Implement function that obfuscates a ydoc and scrambles its content 
# y-websocket
- [v2.0.0_2024-03-20](https://github.com/yjs/y-websocket/releases/tag/v2.0.0)
  - make this a proper esm module
  - Add y-redis backend
# more
