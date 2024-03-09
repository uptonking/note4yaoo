---
title: lib-collab-websocket
tags: [collaboration, realtime, websocket]
created: 2022-10-11T08:54:41.610Z
modified: 2022-10-11T09:02:26.869Z
---

# lib-collab-websocket

# guide

- feathers框架为实时类应用而设计
# blogs
- [Pushpin | Generic Realtime Intermediary Protocol](https://pushpin.org/docs/protocols/grip/)
  - GRIP makes it possible for a web service to delegate realtime push behavior to a proxy component

## [都2022年了，实时更新数据你还只会用短轮询? - 掘金](https://juejin.cn/post/7139684620777291807)

- 分析思路
  - 连接创建和销毁次数
  - 传输数据的实时粒度

- 日常工作中，我们往往会遇到客户端需要实时获取服务端最新数据的场景，例如聊天系统(WeChat/Telegram)，股票行情查看软件(同花顺/富途)，feed推送系统(Twitter/微博)等等
  - 技术方案是有很多的，本文将会给大家介绍四种常见的实时获取服务端数据的方案，它们分别是：短轮询(polling)，长轮询(long polling)，长连接(WebSocket)以及服务器事件推送(Sever-Sent Events, aka SSE)

### 轮询

- 简单来说轮询就是客户端不停地调用服务端接口以获得最新的数据
  - 客户端在发起请求后服务端会立即响应，不过因为这时服务端的数据没有更新所以返回了一个空的结果给客户端。
  - 客户端在等待了一段时间后(可能是几秒)，再次请求服务端的数据

- 优点就是实现简单

- 缺点
- 无用的请求多: 因为客户端不知道服务端什么时候有数据更新，所以它只能不停地询问服务端，如果服务端的数据更新并不频繁的话，这些请求大多都是无用的。无用的请求会导致服务端的带宽占用增加，消耗服务端资源，同时如果客户端是一些移动设备的话，耗电速度也会很快。
- 数据实时性差: 由于不想消耗太多客户端或者服务端的资源，我们通常在实现轮询时不会拿到上一个请求的结果后立即发送第二个请求，这就导致了即使服务端的数据更新了，我们客户端还是需要一段时间才能拿到最新的数据，这对于一些数据实时性要求高的应用例如IM系统是致命的。

### 长轮询

- 客户端发起请求后，服务端发现当前没有新的数据，这个时候服务端没有立即返回请求，而是将请求挂起，在等待一段时间后(一般为30s或者是60s)，发现还是没有数据更新的话，就返回一个空结果给客户端。
  - 客户端在收到服务端的回复后，立即再次向服务端发送新的请求。
  - 每来一个新的连接我们都会将它挂起来(保存在set里面)，然后当有新的事件产生时再将所有该客户端没有获取过的事件返回给它

- 优点
  - 服务端在没有数据更新的情况下没有给客户端返回数据，所以避免了客户端大量的重复请求
  - 客户端在收到服务端的返回后，马上发送下一个请求，这就保证了更好的数据实时性

- 缺点
- 服务端资源大量消耗: 服务端会一直hold住客户端的请求，这部分请求会占用服务器的资源。对于某些语言来说，每一个HTTP连接都是一个独立的线程，过多的HTTP连接会消耗掉服务端的内存资源。
- 难以处理数据更新频繁的情况: 如果数据更新频繁，会有大量的连接创建和重建过程，这部分消耗是很大的。
  - 虽然HTTP的keep-alive字段可以解决一部分问题，不过每次拿到数据后客户端都需要重新subscribe，因此相对于WebSocket和SSE它多了一个发送新请求的阶段，对实时性和性能还是有影响的。

### WebSocket

- 客户端和服务器之间建立一个持久的长连接，这个连接是双工的，客户端和服务端都可以实时地给对方发送消息
  - 首先客户端会给服务端发送一个HTTP请求，这个请求的Header会告诉服务端它想基于WebSocket协议通信，如果服务端支持升级协议的话，会给客户端发送一个Switching Protocal的响应，它们之间后面都是基于WebSocket协议来通信了。
  - 客户端连接服务端的时候，服务端会记住客户端的时间戳，当新事件产生的时候会给客户端推送所有的新事件。

- 优点
- 客户端和服务端建立连接的次数少：理想情况下客户端只需要发送一个HTTP升级协议就可以升级到WebSocket连接，后面所有的消息都是通过这个通道进行通信，无需再次建立连接。
- 消息实时性高：由于客户端和服务端的连接是一直建立的，所以当数据更新的时候可以马上推送给客户端。
- 双工通信：服务端和客户端都可以随时给对方发送消息，这对于本文的其它三种方案都是很难做到的。
- 适用于服务端数据频繁更新的场景：和长轮询不同，服务端可以随时给客户端推送新的信息，而客户端在拿到信息后不需要重新建立连接或者发送请求，因此WebSocket适合于数据频繁更新的场景。

- 缺点
- 扩容麻烦：基于WebSocket的服务是有状态的。这就意味着在扩容的时候很麻烦，系统设计也会较复杂。
- 代理限制：某些代理层软件(如Nginx)默认配置的长连接时间是有限制的，可能只有几十秒，这个时候客户端需要自动重连。要想突破这个限制你就需要将从客户端到服务端之间所有的代理层的配置都改掉，在现实中这可能是不可行的。

- WebSocket的应用场景是一些实时性要求很高的而且需要双工通信的系统例如IM软件等。

### Server-Sent Events

- 是一个基于HTTP协议的服务端向客户端推送数据的技术
  - 客户端向服务端发起一个持久化的HTTP连接，服务端接收到请求后，会挂起客户端的请求，有新消息时，再通过这个连接将数据推送给客户端。
  - 每次客户端给服务端发送请求后，服务端先给客户端返回所有的现存事件然后将该请求挂起，在新的事件生成时再给客户端返回所有的新事件
- 打开Chrome的网络调试工具，会发现HTTP请求变成了EventStream类型，而且服务端给客户端所有的事件推送都在这个连接上，而无需建立新的连接。

- 优点
- 连接数少： 客户端和服务端只有一个持久的HTTP连接，因此性能也是很好的。
- 数据实时性高: 它比长轮询更加实时，因为服务端和客户端的连接是持久的，所以有新消息的话可以直接推送到客户端。

- 缺点
- 单向通信: SSE长连接是单向的，不允许客户端给服务端推送数据。
- 代理层限制: 和WebSocket一样会遇到代理层配置的问题，配置错误的话，客户端需要不断和服务端进行重连。

- SSE技术适合一些只需要服务端单向推送事件给客户端的场景，例如股票行情推送软件。

## [论一个低配版Web实时通信库是如何实现的（ EventSource篇) - 知乎](https://zhuanlan.zhihu.com/p/77635294)

- simple-socket是我写的一个"低配版"的Web实时通信工具（相对于Socket.io），在参考了相关源码和资料的基础上，实现了前后端实时互通的基本功能，
  - 选用了WebSocket ->server-sent-event -> AJAX轮询这三种方式做降级兼容，
  - 分为simple-socket-client和simple-socket-server两套代码。
  - https://github.com/penghuwan/simple-socket

## [JS实时通信三把斧系列之三: eventsource - 知乎](https://zhuanlan.zhihu.com/p/90626342)

- 前两篇文章分析了websocket和http://socket.io
- eventsource其实是单向通信，而websocket是双向通信
  - SSE的简单模型是：一个客户端去从服务器端订阅一条“流”，之后服务端可以发送消息给客户端直到服务端或者客户端关闭该“流”，所以eventsource也叫作"server-sent-event"

- [EventSource - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)
  - EventSource interface is web content's interface to server-sent events.
  - An EventSource instance opens a persistent connection to an HTTP server, which sends events in `text/event-stream` format. 
  - The connection remains open until closed by calling `EventSource.close()`.
# more
