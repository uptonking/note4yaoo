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
# examples
- https://github.com/paulgreg/semi-persistent-chat
  - a simple semi-persistent PWA chat using web socket. 
  - Messages are kept in memory and purged after X hours on the server (configurable).

- https://github.com/aws-samples/aws-iot-chat-example /apache2/202310/js
  - This is a React application demonstrating how to use the AWS IoT platform via MQTT over the WebSocket protocol to build a live chat application. 

- https://github.com/maxnachlinger/redux-websocket-example /202008/js/inactive
  - Preact/Redux + Websocket Example: For Fun
  - Show idle users with idle times ("idle for N minutes" etc)

## sse-eg

- eg
  - 单文件示例 [Understanding Server-Sent Events (SSE) with Node.js _202409](https://itsfuad.medium.com/understanding-server-sent-events-sse-with-node-js-3e881c533081)
  - [How to Use Server-sent Events in Node.js _202402](https://www.sitepoint.com/server-sent-events-node-js/)
  - [Server-Sent Events vs Streamable HTTP: Complete Developer Guide _202507](https://zivukushingai.medium.com/server-sent-events-vs-streamable-http-complete-developer-guide-ff55bb0d76d4)
  - [Implement HTTP Streaming with Node.js and Fetch API _202204](https://www.loginradius.com/blog/engineering/guest-post/http-streaming-with-nodejs-and-fetch-api)

- https://github.com/rcarubbi/nodejs-server-sent-events-example /201803/js/inactive
  - An simple example showing how to user server sent events with node.js

- https://github.com/tom-takeru/sse-demo /202411/go/ts/gin/inactive
  - a project that demonstrates a simple setup for a React frontend and a Go backend using Server-Sent Events (SSE).
  - [The simplest demo on SSE(Server-Send Events) - DEV Community _202411](https://dev.to/tom-takeru/the-simplest-demo-on-sseserver-send-events-1mib)
# websocket-react/vue/fwk
- https://github.com/robtaussig/react-use-websocket /MIT/202402/ts
  - https://robtaussig.com/socket
  - React Hook for WebSocket communication
  - designed to provide robust WebSocket integrations to your React Components. Experimental support for SocketIO
  - Handles reconnect logic
  - No more waiting for the WebSocket to open before messages can be sent. Pre-connection messages are queued up and sent on connection
  - Seamlessly works with server-sent-events and the EventSource API
  - [Send/Emit to socketIO with useSocketIO ](https://github.com/robtaussig/react-use-websocket/issues/173)
    - sendMessage(`42["chat_type",${JSON.stringify(payload)}]`);
    - [Cannot JSON.parse received data when using socket.io ](https://github.com/robtaussig/react-use-websocket/issues/8)
  - [Blocks UI thread ](https://github.com/robtaussig/react-use-websocket/issues/234)
    - When someone sends a lot of events to the socket (~ 5-10 per second), it locks the main thread completely, until messages stop. Consider using webworkers.
    - the library is just calling setState whenever a message is received, which is necessary in order for your components to react to changes. I don’t think WebWorkers can help here as the the heavy lifting will still be performed on the main thread.
    - If I had to come up with a solution that still leverages this library, then my first thought would be to use the filter option and always return false. This will prevent the hook from updating your components directly.
    - Websockets are non-blocking. If they weren't, you could never use them without a webworker, because it would block the only thread.
  - [useEffect throttling? ](https://github.com/robtaussig/react-use-websocket/issues/200)
    - I run into a situation when useEffect invocation was skipped during a higher number of incoming events
    - Added a buffer for incoming events with useRef to avoid re render on each event
  - [Possible to send Authorization header? ](https://github.com/robtaussig/react-use-websocket/issues/69)
    - My understanding is the JS implementation of WebSockets does not support additional headers -- see here for a discussion. That said, the library gives you access to the optional protocols param through options.protocols

- https://github.com/itaylor/redux-socket.io /MIT/201810/js
  - An opinionated connector between socket.io and redux.
  - Socket.io client->server messages should be sent by dispatching actions to redux's store, where the action is the payload.
  - Socket.io server->client messages should be dispatched as actions when received.
  - [Handling authentication · itaylor/redux-socket.io](https://github.com/itaylor/redux-socket.io/issues/13)
  - https://github.com/PlatziDev/socket.io-redux /201704/js
    - Redux middleware to emit action via socket.io

- https://github.com/mfrachet/server-push-hooks /MIT/202102/ts/inactive
  - React hooks for Socket.io, SSE, WebSockets and more to come
# websocket-utils
- https://github.com/tinyhttp/tinyws /ts/单文件
  - a WebSocket middleware for Node.js based on ws, inspired by koa-easy-ws.
  - Easy to use (only req.ws and nothing else)
  - Framework-agnostic (works with tinyhttp, express etc)

- https://github.com/wll8/express-ws /ts
  - Quickly implement websocket API in express.
  - http and ws of the same route can exist at the same time
  - Use directly from app.ws

- https://github.com/k8w/tsrpc /MIT/202304/ts
  - https://tsrpc.cn/
  - 专为 TypeScript 设计的 RPC 框架
  - 支持在 JSON 中传输更多数据类型，例如 ArrayBuffer、Date、ObjectId
  - 同时支持 HTTP/WebSocket

- https://github.com/Actionhero/Actionhero /apache2/202406/ts
  - https://www.actionherojs.com/
  - a realtime multi-transport nodejs API Server with integrated cluster capabilities and delayed tasks
  - The reusable, scalable, and quick node.js API server for stateless and stateful applications
  - The goal of actionhero is to create an easy-to-use toolkit for making reusable & scalable APIs for HTTP, WebSockets

- https://github.com/diy/intercom.js /201802/js
  - UNMAINTAINED: A client-side cross-window message broadcast library built on top of the HTML5 localStorage API.

- https://github.com/Rolands-Laucis/Socio /MIT/202312/ts
  - A WebSocket based realtime duplex Front-End and Back-End syncing API paradigm framework
  - This lets you write SQL in your frontend code, that automagically refreshes on all clients when a resource is changed on any (optionally) connected DB. 
  - Additionally, create any generic JS variables on your server to be realtime synced across all clients using "Server Props".
  - Agnostic of framework, build tool, server lib and SQL database.

- https://github.com/replit/river /MIT/202409/ts
  - ✨⚖️ [River protocol v2.0](https://github.com/replit/river/blob/main/PROTOCOL.md)
  - River provides a framework for long-lived streaming Remote Procedure Calls (RPCs) in modern web applications, featuring advanced error handling and customizable retry policies to ensure seamless communication between clients and servers.
  - The primary goal of the River protocol is to simplify the development of long-lived client-server systems by abstracting the complexities of network programming, like connection management, message serialization/deserialization, and error handling.
  - River provides a framework similar to tRPC and gRPC but with additional features:
    - JSON Schema Support + run-time schema validation
    - full-duplex streaming
    - snappy DX (no code generation)
    - transparent reconnect support for long-lived sessions
    - over any transport (WebSockets and Unix Domain Socket out of the box)
  - The River protocol enables communication between clients and servers via remote procedure calls (RPCs). 
    - A 'client' can initiate remote procedure calls to the server
    - A 'server' can execute remote procedure calls and return the result to the requesting client
    - River handles disconnections and reconnections in a transparent manner wherever possible when explicitly requested. To do this, it uses a combination of a send buffer, heartbeats, acknowledgements, and sequence numbers. This metadata is tracked within the Session object.
    - Though this is very TCP inspired, River has the benefit of assuming the underlying transport is an ordered byte stream which simplifies the protocol significantly.
# realtime
- https://github.com/nodefluent/kafka-streams
  - equivalent to kafka-streams for nodejs
  - this is not a 1:1 port of the official JAVA kafka-streams
  - build on super fast observables using most.js
  - Kafka broker should be version >= 0.11.x

- https://github.com/soketi/soketi /4.4kStar/AGPL3/202402/ts
  - https://soketi.app/
  - Next-gen, Pusher-compatible, open-source WebSockets server
  - built on top of uWebSockets.js - a C application ported to Node.js
  - ⚖️ soketi implements the Pusher Protocol v7. Therefore, any Pusher-maintained or compatible client can connect to it
  - Soketi is capable to hold thousands of active connections with high traffic on less than 1 GB and 1 CPU in the cloud

- https://github.com/fanout/js-serve-grip /MIT/202309/ts
  - GRIP library for Node.js, provided as connect-compatible middleware.
  - [Pushpin | Generic Realtime Intermediary Protocol](https://pushpin.org/docs/protocols/grip/)
    - GRIP is a protocol that enables a web service to delegate realtime push behavior to a proxy component, using HTTP and headers.

- https://github.com/kartikk221/hyper-express /MIT/202402/js
  - High performance Node.js webserver with a simple-to-use API powered by uWebsockets.js under the hood
  - Limited Express.js API Compatibility Through Shared Methods/Properties
  - HyperExpress is mostly compatible with Express but not 100% therefore you may encounter some middlewares not working out of the box

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
# cluster
- https://github.com/SocketCluster/socketcluster /MIT/202403/js
  - https://socketcluster.io/
  - Highly scalable realtime pub/sub and RPC framework
  - Highly scalable pub/sub and RPC SDK optimized for async/await
  - [SCC: horizontally scalable cluster](https://github.com/SocketCluster/socketcluster/blob/master/scc-guide.md)
    - SCC is designed to scale linearly and is optimized for running on Kubernetes but it can be setup without using an orchestrator
    - scc-state service is made up of a single instance - Its job is to dispatch the state of the cluster to all interested services to allow them to reshard themselves. 
    - Note that SCC can continue to operate without any disruption of service while the scc-state instance is down/unavailable
  - Pub/sub channels are lightweight and efficient. Channels are automatically cleaned up when they are no longer used
  - The socketcluster CLI tool exposes kubectl (Kubernetes) shortcut commands to make it easy to deploy your app to any Kubernetes cluster
  - Guarantee message order. Streams behave like processing queues by default.
  - SocketCluster supports JWT authentication by default
  - Monitor message backpressure
  - Throttle and transform data using middleware streams
  - https://github.com/SocketCluster/socketcluster-client
  - https://github.com/SocketCluster/socketcluster-server
    - Minimal server module for SocketCluster
    - This is a stand-alone server module for SocketCluster. 
    - SocketCluster's protocol is backwards compatible with the SocketCluster protocol.
  - 🆚 Benefits of async Iterable over EventEmitter
    - More readable: Code is written sequentially from top to bottom. It avoids event handler callback hell.
    - More succinct: Event streams can be easily chained, filtered and combined using a declarative syntax (e.g. using async generators).
    - More manageable: No need to remember to unbind listeners with removeListener(...); just break out of the for-await-of loop to stop consuming
    - Less error-prone: Each event/RPC/message can be processed sequentially in the same order that they were sent without missing any data

- https://github.com/colyseus/colyseus /5.6kStar/MIT/202406/ts
  - https://colyseus.io/
  - an Authoritative Multiplayer Framework for Node.js, with clients available for the Web, Unity3d, Defold, Haxe, and Cocos
  - The project focuses on providing synchronizable data structures for realtime and turn-based games, matchmaking, and ease of usage both on the server-side and client-side.
  - WebSocket-based communication
  - Automatic state synchronization from server-to-client (delta compressed)

- https://github.com/jamsocket/plane /MIT/202406/rust
  - https://plane.dev/
  - A distributed system for running WebSocket services at scale.
  - 💡 heavily inspired by Figma’s mulitplayer infrastructure, which dynamically spawns a process for each active document.
  - You can think of Plane as a distributed hashmap, but instead of storing data, it stores running processes.
  - When you ask Plane for the process associated with a key (via an HTTP API), it either returns a URL to an existing process, or starts a new process and returns a URL to that.
  - Plane will keep the process running for as long as there is an open connection (usually a WebSocket connection) to it. Once all connections to a process have been closed for some time threshold, Plane will shut down the process.
  - Plane guarantees that only one process will be running for each key at any given time, allowing that process to act as an authoritative source of document state for as long as it is running.
  - [Plane vs. Jamsocket – Plane](https://plane.dev/plane-vs-jamsocket)
    - Jamsocket is a managed platform for session backends, built on Plane. Jamsocket is a proprietary commercial product, while Plane is MIT-licensed open source.
    - Jamsocket’s goal is to be to Plane akin to what GitHub is to Git
  - https://github.com/jamsocket/stateroom /MIT/202405/rust
    - lightweight framework for building WebSocket-based application backends
    - a minimalist framework for building lightweight, single-threaded services that send and receive messages through WebSockets.
    - Stateroom has a modular architecture. 
    - stateroom-server provides an Axum-based WebSocket server that runs a Stateroom service.

## scaling-websocket

- [kubernetes-ingress websockets with nodejs](https://gist.github.com/jsdevtom/7045c03c021ce46b08cb3f41db0d76da)

- https://github.com/sw360cab/websockets-scaling /MIT/202211/js/inactive
  - A tutorial to scale Websockets both via Docker Swarm and Kubernetes
  - Purpose of this is achieving a scalable environment when WebSocket are involved. The pattern to reproduce is a Multi-Server to Multi-client communication via websocket.
  - The result should be a client connected to a specific server host and keeping its connection bound to it (`sticky` connection). Whereas the server hosts will broadcast messages in turn and all the connected clients should receive them. The latter will be achieved leveraging the pub/sub paradigm of Redis.
  - The application is made of server and client part. Both are based `socket.io` library.

- https://github.com/cnych/k8s-socketio-cluster-demo /201711/js
  - 在kubernetes下部署多节点socket.io服务，查看原文：kubernetes 下实现socket.io 的集群模式

- https://github.com/va1da5/xtermjs-for-k8s-pods /202010/js
  - PoC for communicating with Kubernetes websocket for executing shell commands in pods
  - This is a proof-of-concept (PoC) attempt to communicate directly with Kubernetes/OpenShift Websocket, proxy the requests and expose it using xterm.js terminal emulator.

- https://github.com/manavendrasen/scalable-chat-app /202402/go
  - Scaling Go web socket chat app using Redis + Docker + K8s
  - This Proof of Concept (POC) project demonstrates the scaling capabilities of a WebSocket server implemented in Golang, utilizing the Gorilla WebSocket library. 
  - The project includes containerization with Docker and deployment on Kubernetes with features like load balancing, preventing direct client communication, and integrating Redis Pub/Sub for efficient message broadcasting.
  - Kubernetes cluster set up (Minikube for local development)
  - Goroutines are used to handle concurrent connections efficiently.
  - The WebSocket server is deployed on Minikube with three replicas and a LoadBalancer service, showcasing horizontal scaling and load balancing. Clients are isolated from direct communication.
  - Redis Pub/Sub is integrated to enable broadcasting messages on a specific channel. This feature enhances real-time communication across WebSocket server instances. Without redis all the pods were independent and Clients connected to different pods could not connect to each other. Redis acts as a store for chats.

- https://github.com/piyushgarg-dev/Scaleable-WebSockets /202312/ts
  - [Build Scaleable Realtime Chat App with NextJS and NodeJS Tutorial - YouTube](https://www.youtube.com/watch?v=CQQc8QyIGl0)
  - In this video, we will build a scaleable socket real-time application using Redis on Aiven cloud. We'll see how to use Redis PubSub architecture to scale our web sockets.

- https://github.com/hnasr/javascript_playground/tree/master/ws-live-chat-system /202007/js
  - [Scaling Websockets with Redis, HAProxy and Node JS - High-availability Group Chat Application - YouTube](https://www.youtube.com/watch?v=gzIcGhJC8hA)
  - In this video I want to demonstrate how to scale websockets connection to multiple servers using a load balancer such as HAProxy.

- https://github.com/ramank775/chat-server /MIT/202311/js
  - A chat server based on the microservice architecture to ensure high availability, high throughput, horizontal scalability
  - Prerequisites Apache Kafka / Nats Mongodb Nginx Firebase project Redisl
  - 使用了firebase的auth/notify
  - [Vartalap: Open Source Personal Messaging App | One9x _202106](https://blog.one9x.org/vartalap/2021/04/04/vartalap-personal-messaging-app.html)

- https://github.com/Codename-404/socket.io-express.js-horizontal-scaling /202408/js/单文件/inactive
  - [Horizontal Scaling Socket. IO Applications Using Express.js and Redis, a Step-by-Step Guide _202409](https://medium.com/@nayeemurrahman/horizontal-scaling-socket-io-applications-using-express-js-and-redis-a-step-by-step-guide-ba3b1bb2f8e5)
  - https://github.com/Codename-404/socket.io-react-front
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
