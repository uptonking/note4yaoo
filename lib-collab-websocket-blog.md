---
title: lib-collab-websocket-blog
tags: [blog, websocket]
created: 2024-07-07T11:43:36.323Z
modified: 2024-07-07T11:43:43.228Z
---

# lib-collab-websocket-blog

# guide

# blogs-socket-ha/scalable

## [How to scale WebSocket – horizontal scaling with WebSocket _202307](https://tsh.io/blog/how-to-scale-websocket/)

- The horizontal scalability approach allows us to scale almost infinitely. Nowadays it’s even possible to have dynamic scaling – instances are being added and removed depending on a current load
  - On the other hand, it requires a little bit more configuration, since you need at least one additional piece – load balancer, something responsible for request distribution to a specific instance – and for some systems we need to introduce additional services, for example messaging. 

- Horizontal scaling with WebSocket Issue #1: State
- the load balancer redirects traffic to the available server if a given server goes down. Each time a new WebSocket server shows up, the load balancer is there to begin even traffic distribution.
- HAProxy is an example of a load balancer. All we need is to provide a simple configuration.
  - The frontend will be public (this is the address used for communication with our backends).
  - By default, HAProxy is using a round-robin strategy – each request is forwarded to the next backend on the list and then we iterate from the start.
- Most REST APIs are stateless. It means that nothing related to a single user making a request is saved on an instance itself. The thing is, it is not the same case with WebSockets.
- Each socket connection is bound to a specific instance, so we need to make sure that all the requests from specific users are forwarded to a particular backend.
- The solution: sticky sessions(sticky connection)
  - Thankfully, we are using HAProxy, so the only thing that needs to be done is some configuration tweaks
- First of all, we’ve changed the balancing strategy. Instead of using round-robin, we decided to go with leastconn
  - The second change is to sign every request from a single user with a cookie. It will contain the name of the backend to be used.
  - After that, the only thing that is left is to tell which backend should be used for a given cookie value.

- Horizontal scaling with WebSocket Issue #2: Broadcasting
- The WebSocket Server knows only about clients connected to this specific instance. This means we’re sending a message from the same server only to a set of connected clients, not all of them
- The solution: Pub/Sub
- The easiest option is to introduce communication between different instances. For example, all of them could be subscribed to a specific channel and handle upcoming messages.
- This is what we call publish-subscriber or pub/sub. There are many ready-to-go solutions, like Redis, Kafka, or Nats.
- instead of sending messages to the WebSocket client right now, we’re publishing them on a channel and then handle them separately
  - By doing this, we’re sure that the message is published to every instance and then sent to users.

## [Horizontal scaling WebSockets on Kubernetes and Node.js _202102](https://www.shebanglabs.io/horizontal-scaling-websocket-on-kubernetes-and-nodejs/)

# blogs-perf-ws ⚡️

## [How Discord Reduced Websocket Traffic by 40% _202409](https://discord.com/blog/how-discord-reduced-websocket-traffic-by-40-percent)

- When your client connects to Discord, it receives real-time updates about what’s happening through a service that we call the “gateway.” 
  - Since late 2017, the client’s gateway connection has been compressed using zlib, making messages anywhere from 2 to 10 times smaller.
  - Since then, zstandard (originally released in 2015) has gained enough traction to become a viable replacement for zlib. Zstandard offers higher compression ratios and shorter compression times and supports dictionaries
  - We attempted to use zstandard in the past, but, at the time, the benefits weren’t worth the costs. Our testing in 2019 was desktop-only and used too much RAM. 
  - The graph below further illustrates that zstandard performed worse than zlib
  - It turns out that one of the key differences between our zlib and zstandard implementations was that zlib was using streaming compression, while zstandard wasn’t. 
  - Our gateway service is written in elixir, and while zstandard supports streaming compression, the various zstandard bindings for elixir/erlang we looked at didn’t.
  - We ultimately settled on using ezstd as it had dictionary support (more on that later). While it didn’t support streaming at the time, in the spirit of open source we forked ezstd to add support for streaming, which we later contributed back upstream.
- While the original plan was to only consider zstandard for mobile users, the bandwidth improvements were significant enough for us to ship to desktop users as well
- We employ passive sessions to avoid sending most messages that a server generates to clients that may not even open the server. For example, a Discord server could be very active sending thousands of messages per minute, but if a user isn’t actually reading those messages, it doesn’t make sense to send them and waste their bandwidth. 

- Through the combined effects of Passive Sessions v2 and zstandard, we were able to reduce the gateway bandwidth used by our clients by almost 40%. 
  - While the passive sessions optimization was an unintended side-effect of the zstandard experimentation, it shows that with the right instrumentation and by looking at graphs with a critical eye, big savings can be achieved with a reasonable amount of effort.
# blogs
- [Pushpin | Generic Realtime Intermediary Protocol](https://pushpin.org/docs/protocols/grip/)
  - GRIP makes it possible for a web service to delegate realtime push behavior to a proxy component

- [Scaling WebSocket in Go and beyond | Centrifugo _202011](https://centrifugal.dev/blog/2020/11/12/scaling-websocket)

## [My tips for using Socket.io _201803](https://www.ux-republic.com/en/my-tips-for-using-socket-io/)

- The first step before you start anything is to develop a standard for naming your socket events. 
  - For my part, I use the format domain:action
  - This format allows initially to avoid duplicates and especially to have a better readability on the role of the event. 
  - Splitting events into Domaine also makes it possible to logically divide its functions into several files corresponding to their respective domains.

- handlers are neither more nor less than files where we will implement the logic of events. 
  - The goal is to separate your code by respecting the same logic as for the naming (i.e., by creating a file by Domaine). 

- Validate your events: Joi to the rescue

- create helpers in another file
  - we are not going to rewrite our whole piece of code each time we are going to create an event.
  - we are going to create a helper which will allow us to create an event and validate the payload of the event with a Joi schema
  - `bindEvent` allows you to create the event on the socket, to check the payload (if a schema has been passed to it), to return an error if it is not valid, and finally to call the callback by adding the socket current in it.

## 🪧 [都2022年了，实时更新数据你还只会用短轮询? - 掘金](https://juejin.cn/post/7139684620777291807)

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
