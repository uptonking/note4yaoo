---
title: lib-collab-websocket
tags: [collaboration, realtime, websocket]
created: 2022-10-11T08:54:41.610Z
modified: 2022-10-11T09:02:26.869Z
---

# lib-collab-websocket

# guide

- who is using #websocket
  - NodeBB
  - feathers框架为实时类应用而设计
  - more: 

- tips
  - usecase: realtime, collaborative, multiplayer
# draft
- 跨标签页共享ws连接，模拟共享的效果
  - 基于 BroadcastChannel
- 多分析，不一定要共享，不同页面展示不同产品也许是特色
  - 共享的不一定要是连接，可以是数据
# docs
- [Introduction | Socket. IO](https://socket.io/docs/v4/)
  - `socket.emit("hello", "world")` will be sent as a single WebSocket frame containing `42["hello","world"]` with:
  - 4 being Engine. IO "message" packet type
  - 2 being Socket. IO "message" packet type
  - `["hello", "world"]` being the `JSON.stringify()`-ed version of the arguments array
  - a few additional bytes for each message, which can be further reduced by the usage of a custom parser

- [Emit cheatsheet | Socket. IO](https://socket.io/docs/v4/emit-cheatsheet/)

- [How to use with React | Socket. IO](https://socket.io/how-to/use-with-react)
  - We strongly advise against registering event listeners in your child components, because it ties the state of the UI with the time of reception of the events: if the component is not mounted, then some messages might be missed.
  - you will need to properly handle the temporary disconnections, in order to provide a great experience to your users.
- [Emit cheatsheet | Socket.io](https://socket.io/docs/v4/emit-cheatsheet/)
# more
