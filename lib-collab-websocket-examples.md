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
