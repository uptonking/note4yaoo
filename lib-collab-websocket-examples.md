---
title: lib-collab-websocket-examples
tags: [collaboration, examples, realtime, websocket]
created: 2023-01-23T19:27:29.544Z
modified: 2023-01-23T19:27:46.948Z
---

# lib-collab-websocket-examples

# guide

- comparison
  - [socket.io vs sockjs vs websocket vs ws | npm trends](https://npmtrends.com/socket.io-vs-sockjs-vs-websocket-vs-ws)
# popular
- https://github.com/phedkvist/crdt-server /ts/单文件
  - A text based CRDT server storing, sending and receiving updates using Express and Websockets
  - 基于ws创建连接，用数组存放changes
  - 初次连接发送所有changes，后续只发送单次change的msg，为中心服务器架构设计

- https://github.com/plantain-00/ws-heartbeat
  - Server-side and client-side heartbeat library for ws and browser-side Websocket.

- https://github.com/valkyrjs/valkyr /ts
  - https://valkyrjs.com/
  - toolkit for creating event sourced applications using javascript/typescript.
  - A collection of TypeScript + JavaScript tools and libraries to build full stack software applications.
  - designed to be framework agnostic and can be used with any framework or no framework at all. We provide initial base support for SolidJS and ReactJS
- https://github.com/cmdo-toolkit/events /ts/legacy
  - A distributed event sourcing solution written in TypeScript.
  - Logical hybrid clock timestamp representing the wall time when the event was created.
  - https://github.com/cmdo-toolkit/react-starter
    - A full stack cmdo boilerplate for react.js, node.js and typescript
    - 全家桶架构: client-db + store + api
  - https://github.com/cmdo-toolkit/db
    - Client side database solution written in TypeScript.
    - 依赖mingo(MongoDB query language for in-memory objects)
  - https://github.com/valkyrjs/valkyr /ts
    - toolkit for creating event sourced applications using javascript/typescript.
# collab

# apps-networking
- https://github.com/paulgreg/semi-persistent-chat
  - a simple semi-persistent PWA chat using web socket. 
  - Messages are kept in memory and purged after X hours on the server (configurable).
# websocket-utils
- https://github.com/tinyhttp/tinyws /ts/单文件
  - a WebSocket middleware for Node.js based on ws, inspired by koa-easy-ws.
  - Easy to use (only req.ws and nothing else)
  - Framework-agnostic (works with tinyhttp, express etc)

- https://github.com/wll8/express-ws /ts
  - Quickly implement websocket API in express.
  - http and ws of the same route can exist at the same time
  - Use directly from app.ws
# realtime
- https://github.com/nodefluent/kafka-streams
  - equivalent to kafka-streams for nodejs
  - this is not a 1:1 port of the official JAVA kafka-streams
  - build on super fast observables using most.js
  - Kafka broker should be version >= 0.11.x

- https://github.com/soketi/soketi
  - fast, and resilient open-source WebSockets server
  - built on top of uWebSockets.js - a C application ported to Node.js
  - soketi implements the Pusher Protocol v7. Therefore, any Pusher-maintained or compatible client can connect to it

- https://github.com/kartikk221/hyper-express /js
  - High performance Node.js webserver with a simple-to-use API powered by uWebsockets.js under the hood
  - Limited Express.js API Compatibility Through Shared Methods/Properties

- https://github.com/centrifugal/centrifugo /202212/go
  - Scalable real-time messaging server in a language-agnostic way
  - [Centrifugo vs RabbitMQ](https://github.com/centrifugal/centrifugo/issues/126)
  - Centrifugo's goal is delivering real-time messages to end users of your application with at most once delivery model (fire and forget in general). 
  - Centrifugo is just a PUB/SUB server designed for client applications, it's not suitable for usage on backend side - for example to coordinate microservices. 
  - Rabbit can be used as queue, PUB/SUB broker etc.

- https://github.com/gotify/server /go
  - A simple server for sending and receiving messages in real-time per WebSocket. (Includes a sleek web-ui)
# WebRTC
- https://github.com/feross/simple-peer /js
  - Simple WebRTC video, voice, and data channels
  - works in node and the browser
  - supports data channel for text, binary data, node.js duplex stream interface
# more
- https://github.com/well-known-components/template-server
  - Template Node.js server using well-known-components library.
  - Extension of "ports and adapters architecture", also known as "hexagonal architecture".
  - With this architecture, code is organized into several layers: logic, controllers, adapters, and components (ports).
  - adapters: The layer that converts external data representations into internal ones, and vice-versa. Acts as buffer to protect the service from changes in the outside world
  - https://github.com/well-known-components/socket-pool

- https://github.com/well-known-components/http-server
  - implements the interface IHttpServerComponent
  - This implementation is based in Koa sources, it provides a small code footprint to create HTTP servers with a powerful async/await programming model.

- https://github.com/openmetaweb/whatwg-http-server
  - An universal way to implement HTTP server listeners, using WHATWG-similar standards. 
  - Translates your endpoint to many HTTP server implementations, like Node.js, Express.js, Azure Functions and more.
