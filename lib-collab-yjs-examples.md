---
title: lib-collab-yjs-examples
tags: [collaboration, examples, toc, yjs]
created: 2022-09-21T15:47:19.673Z
modified: 2022-09-21T15:47:41.340Z
---

# lib-collab-yjs-examples

# guide

# yjs-utils

# yjs-apps
- yboard /301Star/MIT/202206/js/vue
  - https://github.com/felipeleivav/yboard
  - https://yboard.lol/
  - Yboard is a multiplayer desktop-like workspace based on Yjs
  - Yboard is a frontend-only project. Only requisite is a [websocket server](https://github.com/yjs/y-websocket).
  - Yboard directly connects to websocket server
  - There is no authentication mechanisms nor additional backend logic implemented
  - All the rooms are publicly accessible (only protected by a random unique id, thanks nanoid)
  - Since a room is basically a shared document, any user could eventually rewrite the whole document by writing their own client application
# yjs-examples
- https://github.com/ToolJet/yjs-crdt-game
  - [Building a realtime multiplayer game using React & Yjs + y-webrtc](https://blog.tooljet.com/multiplayer-tic-tac-toe-using-react-crdt-yjs/)
# yjs-more
