---
title: lib-collab-websocket-community-webrtc
tags: [collaboration, community, webrtc, websocket]
created: 2022-10-11T08:56:11.457Z
modified: 2023-12-12T08:45:31.670Z
---

# lib-collab-websocket-community-webrtc

# guide
- feathers框架为实时类应用而设计，代码量很少
# discuss-stars
- ## 

- ## [WebSockets or auto-refresh data? : r/django](https://www.reddit.com/r/django/comments/1qv04fv/websockets_or_autorefresh_data/)
- Using something like HTMX makes this trivial. I have been using polling with htmx, but I’m looking to use SSE next.
- Htmx polling is super simple and requires less moving parts than web socket setup will.

- Do you really need real-time? Sounds like you could probably poll for status like once every 10 or 15 minutes?

- I’m going to get hate but web sockets are a real pain. I know some businesses I’ve been to also block the protocol on their network.
  - For near realtime dashboards, I’ve used htmx polling set to a few seconds. I have yet to try it with Django 6 template partials. Probably because it was super simple and I didn’t know any better.
  - SSE is on my list to explore. It seems a bit simpler than websockets still.

- Using websockets with django require a lot of setup (for example, I use uvicorn, its gunicorn worker and django-channels) and programming that is rather different than the usual model, view, template stuff. Additionally, you need to be familiar with the issues that can arise with async stuff and use of threads in case something goes wrong. Not ideal for a one man team. 
  - I don't think it is worth in this case. Imho you should just create a view for the parts of the page you want to update and poll it in a very basic javascript with a small interval like 10 seconds and possibly less often.

- Websockets using channels isn’t hard. You will have to use asgi with something like uvicorn when deploying. For the front end we use a simple wrapper around reconnecting web socket with some callbacks. Just keep it very simple and it should work well.

- ## just intercepting a direct Undici request and handling it on the socket level in Node.js. Is this... socket-level interception, at last? _202508
- https://x.com/kettanaito/status/1952733757037007059
  - Doesn't patch Undici; 
  - Doesn't re-configure Undici; 
  - Doesn't patch "node:http"
  - Works on the "node:net" level.
- 👀 There's a price though. The interceptor now has to be imported before the client code. Previously, it was less sensitive to import order. "node:net" is way down low and as such gets subjected to import order issues.
  - Which means that if we are to pursue this, you'd have to set up MSW as a part of your test environment. Some request clients, like XHR in JSDOM, come from environment and would have to be imported after the interceptor for the things to work.
  - For "node:http"-based requests, all that you have to do is place the interceptor import before the client import. That's usually enough.
- the biggest change here is that interceptors themselves will be able to switch to being protocol-first! Things like HttpRequestInterceptor vs ClientRequestInterceptor. This is huge.
- Undici has really great tooling for mocking on its own, too! They've got MockAgent and mockDispatcher, IIRC, and they handle Undici-initiated requests really well. 
- ## The repeating 2 and 3 messages in Chrome DevTools are Socket. IO heartbeat packets used to keep the connection alive. 
- 2: A ping packet sent by the server to check if the client is alive.
  - 3: A pong packet sent by the client in response to a ping.
- By default, the server sends a ping every 25 seconds (pingInterval).
  - The client must respond with a pong within 5 seconds (pingTimeout).
- Server as the "Source of Truth" for Connection Health
  - Centralized Timing Control: The server can tune pingInterval and pingTimeout globally based on its own load and infrastructure needs. Client-driven pings would require synchronization across diverse clients, complicating scaling.
  - Burst Avoidance: If all clients sent pings independently, the server could face traffic spikes. Server-side scheduling spreads out pings evenly.
- Why Not Client-Initiated Pings?
  - Unpredictable Client Behavior: Clients might use varying intervals, go to sleep (mobile apps), or disconnect abruptly without notifying the server.
  - State Synchronization Overhead: The server would need to track each client’s last ping time, increasing complexity and memory usage.
  - Risk of False Positives: A client might fail to send a ping due to temporary CPU load or throttling, but the connection itself could still be alive.
- Efficient Resource Usage & Rate Control
  - Think of the server as “polling” each client at a fixed cadence it chooses (e.g. every 25 s). It can throttle that down in low‑traffic scenarios or speed it up when clients seem flaky.
  - If the client were free to ping first, misbehaving or buggy clients could hammer the server, driving CPU/network usage up and potentially leading to DDOS‑like scenarios. Server‑initiated pings let the server gate the heartbeat frequency.
- The core reason boils down to efficient and reliable detection of client-side disconnections from the server's perspective, prioritizing server resource management.
  - Server-initiated pings guarantee that traffic flows at regular, predictable intervals configured by the server.
  - It allows the server to rapidly detect and clean up resources for unexpectedly disconnected clients using a dedicated timeout mechanism (pingTimeout). 
- ## [websocket - Is there a limit (practical or otherwise) to the number of web sockets a page opens? - Stack Overflow](https://stackoverflow.com/questions/26003756/is-there-a-limit-practical-or-otherwise-to-the-number-of-web-sockets-a-page-op)
- It seems that the maximum number of possible open Websockets is defined by the browser implementation, and it is being difficult to find numbers.
  - In the Chromium source code (Google Chrome for Linux), I can see a max of 30 per host, 256 overall.
  - In the Firefox configuration, (go to about:config and search for network.websocket) I can see a max of 6 persistent connections per host and 200 overall, but apparently the persistent conection limit does not affect WebSocket connections, so only the 200 limit applies.
- ## [Custom event naming convention · Issue #1571 · socketio/socket.io](https://github.com/socketio/socket.io/issues/1571)
- I have seen examples with 1) lower case and underscore and 2) camelcase, Altso, should I use present tense or past?
- ## [Sharing websocket across browser tabs? - Stack Overflow](https://stackoverflow.com/questions/9554896/sharing-websocket-across-browser-tabs)
- 
- 
- [How does websockets deal with for two tabs of the same browser - Stack Overflow](https://stackoverflow.com/questions/23300615/how-does-websockets-deal-with-for-two-tabs-of-the-same-browser)
- There's a separate websocket for each tab.
  - You don't need to create a separate cookie per tab because the websocket itself already serves as the unique id for each tab.
- [proper way to share a single WebSocket connection across multiple tabs - Stack Overflow](https://stackoverflow.com/questions/72081821/best-proper-way-to-share-a-single-websocket-connection-across-multiple-tabs)
- Unfortunately is not a straightforward task. But because many browsers are limiting the number of connections to the same origin it is an issue I faced a few times.
- Assuming you are forced to share the connection and other options are not feasible, these are the possibilities:
  - SharedWorker (33.17% support). Allows you to share the connection as you already discovered.
  - BroadcastChannel (91.23% support). Allows you to communicate between tabs.
  - SessionStorage (97.25%). Allows you to communicate between tabs. This is a bit of a hack see but worked well for me.
- 
- 
- 
- ## 🧭 Blink: Intent to Ship: WebSocketStream. Someone should do a benchmark comparing message throughput versus WebSocket.
- https://twitter.com/jarredsumner/status/1755136727415681407
  - If this becomes adopted by other browsers, it is inevitable that Bun and Node will end up supporting it eventually
- isn't it already addressed by webtransport?
- I’m a benchmark guy for Redis Enterpise, write benchmarks for CPUs, Fpgas, ASICS, Embedded platforms. Opposite of fake geek bench . Specify what exactly you would like to benchmark in a real life use case.
- ## [websocket一般会用在什么实际的场合？](https://www.zhihu.com/question/269060103/answer/2399818045)
1. 即时通信、社交订阅
2. 多玩家游戏
3. 编程
4. 收集点击流数据
5. 股票基金报价
6. 体育实况更新
7. 多媒体聊天
8. 基于位置的应用
9. 在线教育
- 弹幕
- 适合需要频繁传输数据以及服务端主推数据等场合
  - 需要从服务器高频率更新数据的应用场景，如游戏、社交通讯、实时投票、拍卖、地图定位导航等
  - 协作应用，如白板应用、多人文档、会议等
  - 需要通知的应用，如邮件、实时推送、远程控制、聊天等。
- ## [手写Socks5通信 - HadYang](https://hadyang.github.io/2019/03/socks-proxy/)
- Socks 协议本身是基于 TCP 的协议，位于应用层与传输层之间的会话层，将应用层的数据透明的传输到 TCP 层
- Socks5 协议在进行代理通信时，首先需要进行连接、认证等步骤。
- ## [WebSocket 相比普通的 TCP 长连接有什么优势？ - 知乎](https://www.zhihu.com/question/303724564)
- WebSocket 是应用层协议，tcp 是传输层协议。
  - websocket 本身是基于 tcp 实现的。
  - tcp 本身无所谓长短连接，理想状态下只要不 close，tcp 连接就一直存在（注意是理想）。
  - 所谓的长连接本身是一条虚拟链路。
- TCP：是客户端与服务端，如何建立握手及连接的一种协议方式，
  - 一般使用Socket的服务，就是基于TCP协议连接好后，你要自己定义客户端与服务端如何传输数据，主要考虑的是如何确认服务端是完整的收到了客户请求的报文。 
  - websocket其实也是为了解决可以完整接收报文而衍生出来的。
- WebSocket： 是根据TCP建立了连接后，如何定义数据的传输的方式，如传输的数据的长度，用几个字节表示，内容对应的字节，在哪个位置表示，
  - 目前websocket已经被很多语言支持，一般建议用WebSocket的方式写成服务，实现长连接的通讯。
- WebSocket 既是一种技术，更是一个 Socket 的应用层协议，它规定了两端之间数据传输的编码和解码方案
  - 浏览器那个 WebSocket 对象，就是一个 WebSocket 协议的实现，使用者只需要调用它的 API 就可以使用 WebSocket 协议进行通讯。WebSocket 不止可以在浏览器上使用，在服务器或者其他类型的客户端也同样可以使用，只要有实现的软件包即可。
- ## [为什么当今Web应用不都采用WebSocket形式进行数据交互？](https://www.zhihu.com/question/417163973)
  - 为什么不能统一一下前后端的交互，让绝大部分通信都使用websocket？
- 分析思路
  - 占用服务器cpu、内存

    - 长连接有维护的开销，短连接会很快释放

  - 消耗带宽资源，如传输额外数据
  - 场景通用性，对移动端的支持
  - 水平扩展性
- 致命缺陷就是无法负载均衡，维持连接占用资源
  - 负载均衡可以做，维持连接占用资源才是大头
  - 可以负载均衡，客户端向负载均衡服务器发起新建连接请求，负载均衡服务器根据负载均衡把应用服务器websocket地址发给客户端，客户端再发起具体的连接请求
- 客户端轮询也会占用服务器资源
- websocket出来以后，按说解决了数据交互的问题，如果每个接口都做成websocket模式，岂不是不存在数据不刷新，都是实时显示的了，
  - 为什么http还没有被淘汰呢，原因就在于，既然他连接了不会断开，必然是后端那边用了某种方法来实现，而这个方法肯定是需要占用服务器的，websocket基于tcp实现
  - 如果使用人员一多，同时建立多个websocket链接，若是一个数据改变，可能会向很多用户发送一次数据，这个数据量是庞大的，同样浪费带宽流量而且耗费服务器
  - 长连接有维护的开销，短链接HTTP请求请求完就断开了，即使有keep-alive也是请求完很快会释放。而长连接面对海量用户的时候，开销比短链接会大很多，除非你是WEBIM服务。
- 在中国长连接迫于某些隐秘的政策，使用起来非常的费劲和尴尬，即使使用云服务商的CDN桥接都狠不理想，可能要加一些非常特殊的运营商级别白名单才可以，这其实才是主要原因。
- https://www.zhihu.com/question/417163973/answer/2951435706
- 说说webSocket缺点吧
- 实现成本高：WebSocket需要在服务器端和客户端都进行相应的编程，需要一定的学习成本和编程成本。对于一些小型的Web应用或者只需要偶尔进行实时通信的应用，使用WebSocket可能不划算。
- 兼容性问题：虽然现在大多数现代浏览器都支持WebSocket，但是一些老旧的浏览器不支持WebSocket。如果应用需要兼容老旧浏览器，那么使用WebSocket可能会存在兼容性问题。
- 防火墙限制：有些网络环境下，防火墙可能会限制WebSocket的连接，这样就无法使用WebSocket进行数据交互。此时，可以考虑使用HTTP长轮询、服务器发送事件（Server-Sent Events）等其他技术进行数据交互。
- 数据量小：如果Web应用只需要进行小量的数据交互，那么使用WebSocket可能会过于复杂。在这种情况下，使用简单的Ajax技术也可以满足需求。
- 安全问题：由于WebSocket允许在客户端和服务器之间建立长久的连接，如果不妥善处理安全问题，可能会导致一些安全隐患。为了避免这种问题，需要在应用中加入相应的安全措施，增加了开发的难度。
- https://www.zhihu.com/question/27745845/answer/2302967079
- websocket在技术上，不够通用；多种客户端访问技术，譬如移动端，自己开发的sdk；用http协议，会很通用而简单；
- 并发，http是短连接，而websocket会保持长连接，当交互并不频繁的时候，连接是被大量浪费的，因此服务器的连接容量会大大多于http；
- 负载，http协议，可以很容易的进行web请求转发来扩容，在搭建lbs接入层的时候，很简单和稳定；而websocket协议，虽然nginx也可以转发，但是毕竟是新技术，稳定性未知；
- 简单：在问题诊断的时候，可以直接面向http协议进行切片从而监视原始数据，工具也很多；而websocket，需要更多面向tcp协议的工具，复杂度和难度会增加不少；
- 之前我们也用 WebSocket 做对话和推送，后来全改用 SSE (Server-Send Events, Event-Stream, EventSource)。
  - 即便以前用 WebSocket 做对话，发送消息也改成了 POST。
  - 一来兼容性更好，一个接口多端都能用；
  - 二来发图片、文件处理起来更顺手，就是普通的 HTTP 上传嘛。
  - 既然如此，WebSocket 全双功就显得没多少意义了。POST 负责发，SSE 负责收，一样的全双工互不干扰。
- SSE 也有个缺点，终端断连在服务端不能及时发现。WebSocket 测试断连立马能触发服务端的 onclose，而 SSE 断连后，输出并不会立即产生异常（java servlet 环境），要等一段时间才行，这个时间貌似跟超时设置相关。主动调接口通知中断虽然能适用特定应用场景，即便关窗口也能在对应事件里调，但起码如果能及时知道断连也好清理掉这个没用的连接。如果您知道什么好的、简单的办法，请评论给我，万分感谢。
  - 微信小程序还没封装 EventSource，虽然支持 HTTP 流式数据，但得自行处理数据和重连。翻微信开发者论坛发现这个问题至少被提 3 年了。不知道将来他们会不会封装一个
- 服务端为什么知道客户端断了，不都是靠心跳吗？
  - 可以靠链接
- 我反而不是很能理解你为什么要在断连时中止任务，你把任务和事件流分开处理就不怕断连了，创建任务以后单独创建一个带缓存的消息队列，任务往队列里写，SSE从队列里读，SSE本身有通过last id自动重连的机制的
- sse是单接收，无法发送数据，要实现心跳只能不断post另外一个接口，还不好处理状态，用心跳就有点扯了。
  - 那我觉得为了这个需求从无状态变成有状态似乎不合算
- sse客户端断连确实不会通知服务端，需要服务端定时发送空包检测连接状态（抛异常就是断了）, 以上是基于Java springboot框架的测试结果
  - 而且如果设置了连接时间，即使客户端sse连接正常，如果连接时间超过配置，则会自动断连；如何连接时间设置的永久（-1），客户端断连之后，服务器还会继续维持sse连接，需要定时任务检查连接状态，及时移除已断开的资源，否则连接池会越积越多
- 没啥特殊的库，我服务端用的nodejs，sse在服务定位器注册全局唯一实例，客户端用的python的aiohttp_sse_client，他的实现逻辑也不复杂你可以看看他的代码，核心思路也是迭代器判断流，session管理生命周期，网络异常统一循环重连。
  - 目前好像除了python有个别人封装好的sse连接库，其他的语言都没有，阿里云也是采用多级判断做的连接管理
- 为什么放弃websocket呢？
  - ws 要额外配置 Ningx 的 Upgrade，这还好。另外，需要额外的协议支持包，比如 jetty 里要用到 javax.websocket-api, websocket-servlet, javax-websocket-server-impl 及相关依赖等，我有代码洁癖
- 还有个问题是 websocket 不好过 CDN。
- 500并发的话，用上websocket，可能就只剩下30并发了
- WebSocket在浏览器端的广泛实现似乎只是一个时间问题，值得注意的是服务器端没有标准的API，各个实现都有自己的一套API，并且JCP也没有类似的提案，所以使用WebSocket开发服务器端有一定的风险，可能会被锁定在某个平台上或者被迫降级。
- websocket与http不同的之处在于，http发的请求是同步的(tcp协议会等待响应)，浏览器发起请求会同步等待服务器返回，而socket是发送完了就结束了，不管服务器又没返回，而且先发地数据不一定先收到，不按顺序返回， 难点就在于发送数据在ws.send函数里，而接收数据在ws.onmessage里，数据不能互通
- 很多公司内部http proxy不配置代理websocket，对于toB业务是个很大的障碍
- ws有很多缺点，传数据不是标准的，因为不是标准的，中间件看不到你做了什么，waf无法正常检测，cc 入侵防不胜防
- 数据处理太随意，无法准确负载均衡，可能a机器累死了b机器在围观
- 状态恢复需要更多的确认措施，否则存在安全风险
# discuss-sse
- ## 

- ## 

- ## 

- ## [How to implement EventSource and SSE in your Frontend and Backend - DEV Community](https://dev.to/lagoni/how-to-implement-eventsource-and-sse-in-your-frontend-and-backend-18co)
- When you send data back to the client, it is important to tell the client what to expect from the response. We do this by separating our response by newlines in our stream of data. 
- Single newline \n: Used to separate different fields within a single event. For example, event type (event:), data (data:), id (id:), and retry (retry:) can be separated by single newlines within an event.
- Double newline \n\n: Used to indicate the end of a single server-sent event. After the server sends a double newline, the client knows that the current event has been fully received and can start processing it. The server can start sending a new event at this point.
- An example of utilizing this could be the payment status given earlier:
  - It will wait until the data stream has been sent since we added the double newline in the response.

```JS
res.write('event: PaymentStatus \n')
res.write('data: JSON.stringify({error: null, data: '
  PaymentCaptured '}) \n\n')
```

- [Understanding Server-Sent Events (SSE) with Node.js ](https://itsfuad.medium.com/understanding-server-sent-events-sse-with-node-js-3e881c533081)
  - The server responds with a `text/event-stream` content type, and data is sent in the following format:
  - Data: Each message can contain multiple data fields, with each field separated by a newline (`\n`). The event must end with two newlines (`\n\n`).

- ## [The line break problem when using Server Sent Events (SSE) _202406](https://medium.com/@thiagosalvatore/the-line-break-problem-when-using-server-sent-events-sse-1159632d09a0)
- imagine our backend needs to stream the literal `\n` . The event would look like this: `"event: eventName\ndata: \n\n\n"` .
  - The question arises: how will the SSE library parse this?
  - According to the documented logic, we would receive the following events: `{"event": "eventName", "data": ""} {"data": ""}` .
  - Here’s why this happens: `\n` serves as an end-of-line identifier, so the parser treats everything up to the first `\n` as one block (event) and the subsequent `\n` as another block with empty data. When the frontend parses this, it essentially ignores the second event and appends an empty string to the existing text. Consequently, the line break is ignored, potentially disrupting the entire markdown rendering.
- After evaluating various approaches, we found the best solution was to serialize the data as a JSON object rather than as a raw string.
  - This method offers more flexibility in the types of data we can return and prevents issues like the one we encountered.

- ## ⚖️ [Newlines in SSE data · Issue · bigskysoftware/htmx _202402](https://github.com/bigskysoftware/htmx/issues/2292)
- [HTML Standard](https://html.spec.whatwg.org/multipage/server-sent-events.html#parsing-an-event-stream)

- Have a look at html.spec.whatwg.org/multipage/server-sent-events.html. Two newlines are treated as end of event. One newline as end of line. That's the protocol. SSE has no other encoding.

- SSE spec lets you do what you want with `<pre>`. Just append `data:`  to each line

- you could also base64 encode, or in my case, replace `\n` with `<br>`. Not sure what the "right" way is tho.

- ## 🧩 [Server-Sent Events (SSE) Are Underrated | Hacker News _202412](https://news.ycombinator.com/item?id=42511318)
- A while ago I created Mercure: an open pub-sub protocol built on top of SSE that is a replacement for WebSockets-based solutions such as Pusher. Mercure is now used by hundreds of apps in production.
  - At the core of Mercure is the hub. It is a standalone component that maintains persistent SSE (HTTP) connections to the clients, and it exposes a very simple HTTP API that server apps and clients can use to publish. POSTed updates are broadcasted to all connected clients using SSE. This makes SSE usable even with technologies not able to maintain persistent connections such as PHP and many serverless providers.
  - Mercure also adds nice features to SSE such as a JWT-based authorization mechanism, the ability to subscribe to several topics using a single connection, events history, automatic state reconciliation in case of network issue…

- I used a similar solution called Centrifugo for a while. It allows you to choose which transport to use (ws, sse, others)
  - 👷 I'm the author of Centrifugo. Let me share a bit more about Centrifugo transport choices. 
  - It’s not just about supporting multiple transports — developers can also choose between bidirectional and unidirectional communication models, depending on their needs.
  - For scenarios where stable subscriptions are required without sending data from the client to the server, Centrifugo seamlessly supports unidirectional transports like SSE, HTTP-streaming, unidirectional gRPC streams, and even unidirectional WebSockets (this may sound kinda funny for many I guess). This means integration is possible without relying on client-side SDKs.
  - However, Centrifugo truly shines in its bidirectional communication capabilities. Its primary transport is WebSocket – with JSON or Protobuf protocols, with SSE/HTTP-streaming fallbacks that are also bidirectional — an approach reminiscent of SockJS, but with more efficient implementation and no mandatory sticky sessions. Sticky sessions is an optimization in Centrifugo, not a requirement. 
  - It's worth noting that SSE only supports JSON format, since binary is not possible with it. This is where HTTP-streaming in conjuction with ReadableStream browser API can make much more sense!
  - I believe Centrifugo gives developers the flexibility to choose the transport and communication style that best fits their application's needs. And it scales good out of the box to many nodes – with the help of Redis or Nats brokers. Of course this all comes with limitations every abstraction brings.

- SSE/Mercure (as WebSockets) is much battery-efficient than polling (push vs poll, less bandwidth used).
  - on controlled environnements, SSE can use a « push proxy » to wake up the device only when necessary

- 🐛 It doesn’t mention the big drawback of SSE as spelled out in the MDN docs: “Warning: When not used over HTTP/2, SSE suffers from a limitation to the maximum number of open connections, which can be especially painful when opening multiple tabs, as the limit is per browser and is set to a very low number (6).”
  - One of my company's APIs uses SSE, and it's been a big support headache for us, because many people are being corporate firewalls that don't do HTTP/2 or HTTP/3, and people often open many tabs at the same time. It's unfortunately not possible to detect client-side whether the limit has been reached.
  - Another drawback of SSE is lack of authorization header support. There are a few polyfills (like this one) that simulate SSE over fetch/XHR, but it would be nice to not need to add the bloat.
- 💡 I hate to suggest a solution before testing it myself so apologies in advance but I have a hunch that `BroadcastChannel` API can help you detect browser tab opens on client side. New tabs won't connect to event source and instead listen for localStorage updates that the first loaded tab makes.
  - The problem in this case is how to handle the first tab closing and re-assign which tab then becomes the new "first" tab that connects to the event source but it may be a LOE to solve.
- Rather than Broadcast Channel, you can use the Web Locks API 
  - This handles the leader election pretty seamlessly because all tabs try to become the leader and only one actually can.
  - This library (https://github.com/pubkey/broadcast-channel) from the fantastic RxDB javascript DB library uses WebLocks with a fallback to `BroadcastChannel`. But, WebLocks are supported on 96% of browsers, so probably safe to just use it exclusively now
- This sounds like a good use case for using a service worker. All tabs talk to the service worker and the worker is the single instance that talks to the backend and can use only one connection. Maybe there are some trade offs for using SSE in web workers, I'm not sure.
  - `BroadcastChannel` is a better solution for a couple of reasons. Service Workers are better at intercepting network requests and returning items from a cache, there’s some amount of additional effort to do work outside of that. 
  - The other thing is they’re a little more difficult to set up. A broadcast channel can be handled in a couple lines of code, easily debuggable as they run on the main thread, and they’re more suited to the purpose.
- agreed. Workers was one of my first thoughts but I think BroadcastChannel delivers with much lower LOE
- I disagree. You can just `postMessage` to communicate with the service worker and therefore I imagine the code using broadcast channel to be actually quite similar. About debugging, service workers are easily debuggable, though not on the main thread as you already mentioned.

- caniuse Shared Web Workers 45%
  - caniuse BroadcastChannel 96%
  - the issue with SharedWorkers is that Android Chromium doesn't support it yet

- Supposedly websockets (the protocol) support authorization headers, but often there are no APIs for that in websocket libraries, so people just abuse the subprotocols header in the handshake.
  - I don't think the problem is libraries. Browsers don't support this.

- websockets are great until you have to load balance them. And then you learn why they aren’t so great.

- browser connection limitaions: Does anyone know why it is so low?
  - Historical reasons. The HTTP/1.1 spec actually recommends limited to 2 connections per domain. That said, I'm not sure why it's still so low. I would guess mostly to avoid unintended side effects of changing it.

- Because you're supposed to use a single connection with HTTP Pipelining for all your ressources
  - When index.html loads 4 CSS and 5 JS : 10 ressources in HTTP 1.0 needed 10 connections, with 10 TLS negociations (unless one ressource loaded fast and you could reuse it's released connection)
  - With HTTP1.1 Pipelining you open only one connection, including a single TLS nego, and ask 10 ressources.
  - Why not only 1 per domain so ? IIRC it's because the 1st ressource index.html may take a lot of Time to complete and well race conditions suggest you use another one that the 'main thread' more or less. So basically 2 are sufficient.

- There is little reason to not use HTTP/2 these days unless you are not doing TLS.
  - Corporate proxy servers often downgrade connections to HTTP 1.1 because inertia and lazy vendors.

- nginx can't reverse proxy http/2 or higher, so you end up with very weird functionality, essentially you can't use nginx with SSE.

- For my use cases, the main limitations of SSE are:
  - 1. Text-only, so if you want to do binary you need to do something like base64
  - 2. Browser connection limits for HTTP/1.1, ie you can only have ~6 connections per domain
- Connection limits aren't a problem as long as you use HTTP/2+.
  - Even so, I don't think I would reach for SSE these days. For less latency-sensitive and data-use sensitive applications, I would just use long polling.
- For things that are more performance-sensitive, I would probably use fetch with `ReadableStream` body responses. On the server side I would prefix each message with a 32bit integer (or maybe a variable length int of some sort) that gives the size of the message. This is far more flexible (by allowing binary data), and has less overhead compared to SSE, which requires 7 bytes (`"data:" + "\n\n"`) of overhead for each message.
- `ReadableStream` appears to be SSE without any defined standards for chunk separation. In practice, how is it any different from using SSE? It appears to use the same concept.
  - Presumably,  `ReadableStream` does not auto-reconnect.

- One thing I dislike regards to SSE, which is not its fault but probably a side effect of the perceived simplicity: lots of developers do not actually use proper implementations and instead just parse the data chunks with regex, or something of the sorts! This is bad because SSE, for example, supports comments (`": text"`) in streams, which most of those hand-rolled implementations don't support.
  - For example, my friend used an LLM proxy that sends keepalive/queue data as SSE comments (just for debugging mainly), but it didn't work for Gemini, because someone at Google decided to parse SSE with a regex. if the regex doesn't match the complete line, the library will just throw an error

- https://data-star.dev is a hypermedia-oriented front end library built entirely around the idea of streaming hypermedia responses via SSE.
  - It was developed using Go & NATS as backend technologies, but works with any SSE implementation.

- The part where it says: > SSE works seamlessly with existing HTTP infrastructure.
  - I'd be careful with that assumption. I have tried using SSE through some 3rd party load balancer at my work and it doesn't work that well. Because SSE is long-lived and doesn't normally close immediately, this load balancer will keep collecting and collecting bytes from the server and not forward it until server closes the connection, effectively making SSEs useless.
  - I had to use WebSockets instead to get around this limitation with the load balancer.
- I had a similar issue at one point but if I remember correctly I just had to have my webserver send the header section without closing the connection. Usually things would just get streamed through but for some reason until the full header was sent the proxy didn't forward and didn't acknowledge the connection.
  - Not entirely. If a load balancer is set to buffer say 4kb of data all the time, your SSE is stuck until you close the connection.
  - I think there is a HTTP/2 flush instruction, but no load balancer is obligated to handle it and your SSE library might not be flushing anyway.

- OpenAI's own documentation makes note of how difficult it is to work with SSE and to just use their library instead. My team wrote our own parser for these streaming events from an OpenAI compatible LLM server. The streaming format is awful. The double newline block separator also shows up in a bunch of our text, making parsing a nightmare. The "data:" signifier is slightly better, but when working with scientific software, it still occurs too often. Instead we've had to rely on the totally-not-reliable fact that the server returns each as a separate packet and the receiving end can be set up to return each packet in the stream.
  - The suggestions I've found online for how to deal with the newline issue are to fold together consecutive newlines, but this loses formatting of some documents and otherwise means there is no way to transmit data verbatim. That might be fine for HTML or other text formats where newlines are pretty much optional, but it sucks for other data types.
  - I'm happy to have something like SSE but the protocol needs more time to cook.
- SSE has been part of the WHATWG standard for almost 20 years. Every protocol requires some sort of data encoding. 
  - For SSE you need to either restrict yourself to payloads that can never conflict with the message structure (e.g. an enumeration of short strings to indicate different sorts of events), or you need to encode the data.
  - It sounds like you are trying to send raw, unencoded data and are surprised that it sometimes conflicts with the message structure. Well of course it does! You can’t blame the protocol for that.
- Every other protocol I've used has a standard way to encode arbitrary data, but especially text data, usually using some kind of escape sequence. SSE does not. Just because it has been around for a long time does not mean it is well thought out or complete.

- > SSE works seamlessly with existing HTTP infrastructure
  - This is false. SSE is not supported on many proxies, and isn't even supported on some common local proxy tooling.

- SSE is not underrated. In fact it's being used by Open AI for streaming completions. It's just not always needed unlike the very obvious use cases for normal REST APIs and Websockets.

- I’ve never understood the use of SSE over ndjson.
  - Manually streaming a XHR and parsing the messages is significantly more work, and you lose the built-in browser API. But if you use a fetch ReadableStream with TLV messages I'm sold.

- Does anyone have a good trick for figuring out when the client side connection is closed? I just kill the connection on the server every N minutes and force the client to reconnect, but it's not exactly graceful.
  - The socket closes. Most languages bubble this back up to you with a connection closed exception. In python async world, it would be a cancelled error.

- I'm curious as to how everyone deals with HTTP/2 requirements between the backend servers and the load balancer? By default, HTTP/2 requires TLS which means either no SSL termination at the load balancer or a SSL cert generated per server with a different one for the front end load balancer. This all seems very inefficient.
  - You don't need http2 on the actual backend. All limitations for SSE/http1 are browser level. Just downgrade to http1 from the LB to backend, even without SSL. As long as LB to browser is http2 you should be fine.

- http streaming is even more underrated.

- ### [Server-sent events, WebSockets, and HTTP | Hacker News _202202](https://news.ycombinator.com/item?id=30403438)
- I've used the Broadcast channel API in conjunction with SSE to have only one tab handle the SSE connection, and broadcast incoming SSEs to the other tabs which also reduces the number of connections to the server to one.
  - On the server it's also a PITA because not all instances/pods have the subscribers list. The way I've found to solve this is with clustering the instances with Hazelcast or Redis or a MQ.
- Also, when using an nginx reverse proxy, including `X-Accel-Buffering: no` in the HTTP header of the server response may be required to keep events from being buffered.

- These are all potential issues with plain sse, but are pretty easily solved in a few lines of code.
  - Granted the benefits of sse: no additional port to open, no dependencies - just slip your logic into your routing at /events. Of course this may not be important for some. Websockets are a good choice as well. I tend to id clients on ip address not connections however, depends on the specific app.

- The best way to do pub/sub on the web with a standard protocol is MQTT
  - Strong disagree. MQTT has no place in a world with WebSockets. MQTT knowledge is so esoteric in comparison. Maybe it's the Haskell of transport protocols: really friggin smart, but not if you're trying to be useful to society at large.
- MQTT is neither "esoteric" or "not useful to society at large" nor is WebSockets vs MQTT even a useful contrast, since WebSockets to a large degree addresses a different level of the stack (and indeed "MQTT over WebSockets" is a common way of deploying it).

- Can Web Push Notifications not also be considered as an alternative?
  - Technically it would fit nicely. Unfortunately, it requires the user to explicitly give permissions to show notifications to the website, even if you don't show any notifications. This is a blocker for its usage in many cases.

- ## [http - Stop server-sent events by server - Stack Overflow](https://stackoverflow.com/questions/36669100/stop-server-sent-events-by-server)
- The server-sent events is yet another streaming technique which is one of ways of Comet. To stop streaming data, just close the connection in server. 

- According to html5doctor.com/server-sent-events/#properties) "if the connection drops, the EventSource fires an `error` event and automatically tries to `reconnect`. The server can also control the timeout before the client tries to reconnect."

- ## [How do I close a Server-Send Events connection in Flask? - Stack Overflow](https://stackoverflow.com/questions/11597367/how-do-i-close-a-server-send-events-connection-in-flask)
- It seems the author of Flask does not have a plan to support that yet. For "Server-Sent Events", it is better to use an event-driven architecture like NodeJS.

- It is important to note you need to close the connection on the client as well, otherwise it will try and reopen the connection after a `retry` timeout.
  - my preferred solution was to close the connection from the server by yielding an expected data message.
  - flask: `yield "data: finished\n\n"`

- ## [How to close a "Server-Sent Events"-connection on the server? - Stack Overflow](https://stackoverflow.com/questions/6534572/how-to-close-a-server-sent-events-connection-on-the-server)
- By default, if the connection between the client and server closes, the connection is restarted. 
  - The connection is terminated with the `.close()` method: `evtSource.close()` ; 

- According to the specification:
  - Clients will reconnect if the connection is closed; it is possible to tell a client to stop reconnecting using HTTP response code `204` No Content.

- your client has to close the connection. That leaves two options. The first, is to simply assume any error from the server should close the EventSource.
  - We are assuming that a network error is a graceful shutdown, this may not be the case. There may also be some scenarios where we do want the reconnect behavior.
  - So instead, why don't we just ask the client to gracefully shutdown itself! We have a way to send messages to the client from the server, so all we need to do is send a message from the server that says "shut me down".

```JS
const sse = new EventSource('/events')
sse.onmessage = m => console.log(m.data)
sse.onerror = () => sse.close()
```

- Caution: If you use a package to manage server-sent events in node.js, making a direct call to `response.end()` may cause the package to send additional data after `response.end()`, and this will crash the server with a "WRITE after close" error.
  - Instead of directly calling `response.end()`, my workaround was to call `response.emit('close')`, which allowed the package to handle the close.

- [Node. JS Server Sent Events: Route continues to run after res.end() resulting in ERR_STREAM_WRITE_AFTER_END error - Stack Overflow](https://stackoverflow.com/questions/59797523/node-js-server-sent-events-route-continues-to-run-after-res-end-resulting-in/59798626?noredirect=1#comment105739184_59798626)
  - This seems like the right way to do it. It's a good use of an `eventEmitter` because your routes are not coupled to the actual data source at all, just listening for an event and you can change the data source implementation at any time without having to change the routes at all.

- ## [Comparison of data before and after using Streamable HTTP | by Higress_ai | Medium _202504](https://medium.com/@higress_ai/comparison-of-data-before-and-after-using-streamable-http-b094db8b414e)
- Recently, the MCP repository’s PR #206 introduced a brand new Streamable HTTP transport layer to replace the original HTTP+SSE transport layer. 
- The two protocols are simply compared as follows:
  - HTTP+SSE: The client sends requests via HTTP POST, and the server pushes responses through a separate SSE (Server-Sent Events) endpoint, requiring the maintenance of two separate connections.
  - Streamable HTTP: It uses a single HTTP endpoint to handle requests and responses uniformly, allowing the server to choose between returning standard HTTP responses or enabling SSE streaming as needed.
- Streamable HTTP offers better stability compared to HTTP + SSE, performing better under high concurrency scenarios.
  - In terms of performance, Streamable HTTP has clear advantages over HTTP + SSE, with shorter and more stable response times.
  - The client implementation of Streamable HTTP is simpler than HTTP + SSE, requiring less code and lower maintenance costs.
- Problems with HTTP + SSE
  - The server must maintain long connections, which can lead to significant resource consumption under high concurrency.
  - Server messages can only be transmitted via SSE, which creates unnecessary complexity and overhead.
  - Infrastructure compatibility: Many existing network infrastructures may not correctly handle long-term SSE connections. Enterprise firewalls may forcefully terminate timed-out connections, making the service unreliable.
- Improvements in Streamable HTTP
  - Streamable HTTP removes the dedicated /sse endpoint for establishing connections, integrating all communication into a single endpoint
  - The server can flexibly choose to return standard HTTP responses or stream them via SSE based on the type and content of the request
  - Powerful Session Management: Supports the Last-Event-ID mechanism to ensure that messages not received after a disconnection can be recovered.
- ## 🆚 [SSE vs. Streamable HTTP - which will be the standard for remote servers? : r/mcp _202505](https://www.reddit.com/r/mcp/comments/1kdyse2/sse_vs_streamable_http_which_will_be_the_standard/)
- SSE is effectively legacy now and is basically unworkable for truly distributed MCP anyway. The new world (when the SDKs catch up) will be Streamable HTTP. Of course, how many of the 8000 odd servers that already exist will be updated is debatable.
- Sse is not the problem. The Problem is the stateful connection mcp mandates.
  - The new approach still uses `text/event-stream` , but stateless.
- Exactly. SSE was never the problem. People are complaining about SSE servers being stateful.
  - SSE (i.e. stateful) servers are not going anywhere. There is space for streamable servers, but I don't see them as comparable or functionally equivalent to SSE servers.
- Why did MCP go SSE and then http streaming instead of just starting with something like websockets
  - "We ultimately decided not to pursue WS right now because:
  - Wanting to use MCP in an "RPC-like" way (e.g., a stateless MCP server that just exposes basic tools) would incur a lot of unnecessary operational and network overhead if a WebSocket is required for each call.
  - From a browser, there is no way to attach headers (like Authorization), and unlike SSE, third-party libraries cannot reimplement WebSocket from scratch in the browser.
  - Only GET requests can be transparently upgraded to WebSocket (other HTTP methods are not supported for upgrading), meaning that some kind of two-step upgrade process would be required on a POST endpoint, introducing complexity and latency."
- ## 🌰 did you know that there is another technologie, simpler, native and that use HTTP you can use to do real-time?
- https://twitter.com/soubiran_/status/1773634287918608804
- SSE is great. A lot of apps just don't need bi-directional communication that WS provide.
  - However, currently browsers limits a website to have a maximum of 6 SSE streams. So if someone opens a 7th tab, the SSE connection will fail.
- Do technologies like Firebase auth use SSE to observe auth changes on the client? Any idea?
  - 🌰 i recommend @supabase realtime event subscription instead, easier to implement, especially when deploying on Serverless platform (where SSE is crippled).
- what is the server load for SSEs? If the HTTP connection stays always open, that means that the server needs to more resources?
  - Yes and that's exactly the same for WebSocket. Once the client disconnect, the connection ends.
- ## 有在实际项目中用过 SSE(Server Sent Events) 的吗。有啥坑没
- https://twitter.com/_a_wing/status/1739901379953787028
- iOS 不支持
  - 和你的想法一样，但最后iOS还是用了web sockets
- 原生 event source 没法用，比如 不能带 headers 、浏览器上只支持 GET，找个第三方的就行
- 手机上浏览器切后台秒断
- 早知道，还是轮询
- 其实你用 fetch+ReadableStream 持续拉一路 http 也是一样的效果。 2015年底用到现在了，现在连Safari和FireFox都有
  - ReadableStream 毕竟是新出来的东西。
- SSE 断线了的可以自动重连，可以接着接着之前段的地方续传。当然 fetch + ReadableStream 也可以自己实现这一套机制就是了。
- 前端调包，相比 ws 少写一点代码，，后端如果要做分布式，路由会比较麻烦，
  - 和 ws 一样后端都带状态，需要有 user session 和 node 路由机制，用 redis channel 去实现比较简单。
- 没啥坑，如果是前面有个nginx，需要注意下有设置一个header，具体记不清了。不然前端收不到。
- 唯一一坑，如果发现似乎被 buffer/cache 住了一批值，检查一路上的所有反代（包括 cloudflare，如果用了的话）的配置
- 有一个坑， ，有网关的情况下记得看看网关配置是否开启了对 SSE 的支持，不然又得排查半天
- uber 有一篇介绍他们在后台使用sse的博客，还有具体的代码，可以参考一下
- ## 技术啊，还是要看天时。SSE很早就出来了，基本没人用。
- https://twitter.com/NalaGinrut/status/1673676930036514816
  - 2015年那会儿我说在框架里实现一下，结果一帮年轻人都说现在是websocket的年头，于是就实现了websocket，而把SSE放到了todo里。
  - 这么多年过去了SSE又借着chatgpt steam死灰复燃了
- 是啊，现在能成为 ChatGPT/LLM 等的基础技术或软件都会再起飞
- 还是有不少公司业务在用 SSE 的，电商 feeds, sku 多的场景都挺适合的

# discuss-ssh/tunnel
- ## 
- ## 
- ## 
- ## [What os difference websocket vs ssh-tunnel? - Stack Overflow](https://stackoverflow.com/questions/55685980/what-os-difference-websocket-vs-ssh-tunnel)
- WebSocket is a protocol designed for 2-way real-time communication between browsers and servers to replace hacky solutions like long polling and XHR streaming.
- SSH is a protocol designed for operating network services securely over an insecure network. 
  - Usually it's used for remote logins, file transfers, however it can be used for any protocol, however a few modifications need to be made.
- The difference between them is, well, WebSocket is designed to be used for the browser and has support there. 
  - However, SSH is a more general protocol and can be used for more however it is not supported by browsers directly, but through proxies which bridge WebSocket to SSH.
- ## [what is more secure -- Data transfer using socket programming OR SSH/SCP/FTP - Stack Overflow](https://stackoverflow.com/questions/2642808/what-is-more-secure-data-transfer-using-socket-programming-or-ssh-scp-ftp)
- Just using sockets doesn't give you any security at all. The right choice depends on the application, the systems you're using
- SSH/SFTP/SCP all makes use of sockets under socket programming. Unless you have a better algorithm (for security) than what SSH provides, use a SSH module for Perl.
- Out of the box sockets aren't secure. The data is transmitted in raw form from point A to point B. 
  - Adding SSL adds security. Many protocols support SSL. In particular several flavors of FTP and HTTP support SSL.
- If I were to start from scratch on such a system I would use FTPS.
- SSH is a remote shell protocol and itself it is not used for file transfer (like FTP). 
- SCP file transfer protocol was part of SSH1 but as SSH1 is outdated and flawed, SCP is not recommended for use. 
  - In SSH2 (used in all modern systems) SFTP (SSH File Transfer Protocol) is used.
- FTP (RFC 959) by itself doesn't provide any security. There exist extensions that let you run FTP over SSL/TLS (either implicitly, over pre-encrypted channel, or explicitly, via TLS as a part of FTP protocol). FTP over SSL is called FTPS (don't mix it with SFTP).
- FTPS (FTP over SSL/TLS) - it's equivalent of HTTPS which in simple terms means it's encrypted version of the ordinary FTP protocol. 
  - I think it's great for downloading over the Internet from remote and possibly public machines. It offers superior authentication mechanism in the form of X.509 certificates. 
  - There is some trouble with firewalls because it uses, as FTP does, two connections. 
  - If your goal is to prevent anyone from seeing what you're downloading this is IMHO perfect solution. I tend to use this protocol to access machines that I don't control.
- SFTP (SSH FTP) - it's good protocol, maybe bit superior to the FTPS, but in my opinion it's better suited for controlled environment. 
  - I will use this protocol when I want to download a file from my account on one machine to another. Or when I want to upload new script to a server. 
  - It's for me remote equivalent of me going to the machine with flash drive and logging on the machine.
- VPN - if those machines are fixed so to speak - you are always connecting to the same machines - I would consider using VPN to deliver the security. 
  - The transmissions are protected from outsiders, the server behaves like it's in the same network and I can use any protocol I want.

# discuss-devops-websocket
- ## 

- ## 

- ## 

- ## 

- ## Your WebSocket server handles 50K concurrent connections. When you deploy new code, all connections drop and reconnect simultaneously, causing a thundering herd.
- https://x.com/0xlelouch_/status/2031280038780256327
  - How do you deploy without disrupting connections?

- Use graceful, zero-downtime deployments.
  • Connection draining - stop accepting new sockets, keep existing ones alive
  • Rolling updates - replace instances gradually, not all at once
  • Sticky sessions so clients stay on same node
  • Reconnect jitter/backoff to avoid thundering herd
  • Optionally state externalization (Redis) for session continuity
  - I’m exploring this deeply while building an internal chat service still weighing trade-offs of draining vs fast rollouts vs infra complexity.

- Rolling deployment with connection draining. New pods start accepting new connections while old pods finish existing ones with a grace period. Add exponential backoff with jitter on the client reconnect to prevent the thundering herd. Without jitter you just moved the stampede.

- Graceful draining is the way. Stop accepting new connections on the old nodes, signal the clients to reconnect with a random jitter (to avoid the spike), and let the new fleet take over gradually
# discuss
- ## 

- ## 

- ## 

- ## TIL (and painful reminder): You need to close WebSocket connections with a code for a Node process/thread to properly exit.
- https://x.com/schickling/status/1869081922846220583
- MDN claims it to be automatically set to 1000?
- Every TinyBase documentation snippet doubles up as a unit test. This is why they all include cleanup!
- nodejs - not even once.
- ## I’m increasingly thinking that every client-server connection should be default realtime using websockets, unless you have a very good reason for not doing that.
- https://x.com/jamonholmgren/status/1852568079223681525
  - And most server-server connections too.
  - and SSE is a great way to scale up if you really mainly need one-way realtime (which is common).
- Avoid web protocols entirely. Especially within a backend where you have full control over what’s being used. Real-time is good but Websockets are not that. Build on top of UDP.
  - Why not? Zoom and Slack both offer WebSocket APIs, and you can get events streamed in that way.
- the request / response model is simple, effective and not only scales very well but has decades of infrastructure built explicitly to support it. unless you’re explicitly building a realtime web app (chat, multiplayer) it’s overkill & you will likely get it wrong
- Keeping connections alive with WebSockets can drive up CPU usage and hit connection limits fast, often needing a lot of tweaking at the kernel level to manage. I’d stick to using WebSockets mainly for event-driven apps where real-time updates are key.
  - That’s why Elixir/Phoenix is amazing. Millions on a single server, and easy horizontal scaling
- That mentality is a good way to make your app buggy or completely unusable during network issues.
- don’t think most apps need it. Optimistic updating client-side keeps state snappy on front end and in sync with server. It’s a nice middle ground 
- The websocket overhead is greater than a tcp+tls handshake (on a healthy network) If using http3 you can have 0-RTT for itempodent reqs which basically makes connecting again free (+ UDP benefits on unhealthy networks if some packets get lost)
- This makes caching (of all sorts: BF, CDNs, basic HTTP caching) more difficult, SEO more difficult, debugging more annoying, scaling is horrific (when are connections terminated? How many can a server handle?)
- Request/response over http3 is more than adequate.  Why on earth do you need more than that for simple data hydration?
- Websockets have tons of issues, esp around public internet connections that might block them.
- ## 🤔 how are you doing websockets? assume you have multiple application servers running and broadcasts need to work to clients across all
- https://x.com/thdxr/status/1851038633014198392
- DB backed events, polling works in most cases.. you can make a simple observable event type abstraction. it depends. I’ve never done anything too resource intensive.
- I wrote https://npmjs.com/package/mqemitter before @nodejs had promises, and I never had to reach for something else. Use the Redis/Valkey pubsub adapter.
  - Works well up to several hundred thousands messages per second (depends on the size of message).
- In the past I reached for ZMQ. I keep hearing good things about NATs from GoLang devs.  A lot of times it's Redis TBH. (Or any of the MQ services)
- Use go, Nats or Centrifuge
- we use just a simple socketio like ws wrapper on our api instance, all behind a load balancer on AWS
  - use a few different ways of throwing info from one side of our stack to another, but mainly designed around http://NATS.io, basically a pub-sub model, each user gets an ephemeral channel
  - we ingest data from webhooks often from multiple third party services, so getting it from say, instance A, over to instance B where a client is connected (and even multiple instances) works nicely via this method
- ## 作为 RTC 的从业者说一下 OpenAI 在发布realtime api 的时候为啥会拉上 livekit 以及 agora：
- https://x.com/leeoxiang/status/1841737253024137687
  1、RTC 的接入成本远比http 要高很多倍，简单的场景按照要按照周算，复杂的场景要按照月算。
  2、RealtimeAI  30 多个信令，涉及到长连接的重连，复杂状态处理，技术不好的开发者已经很难 hold 住了。
  3、除了协议之外，音频的前后处理（降噪、人声分割等等）以及各种硬件设备的适配也需要非常专业的团队来处理。
  - 这其中大量的接入工作openai 本身是支持不了的，也不是 openai 擅长的。
- rtc是非常成熟的通信解决方案了，4年前就很成熟了，疫情期间rtc借着视频会议又火了一波，openai没必要自己建设rtc网络，这方面其它rtc供应商早做好了。
- ## Web trivia: Chrome has its own IPC protocol called Mojo that's also used in part by Firefox and is similar in design to how MessageChannels work in JS user land, which are implemented on top of it.
- https://x.com/qwtel/status/1813126057073254690
- ## [Where to hold my socket in my redux store? - Stack Overflow](https://stackoverflow.com/questions/65940957/where-to-hold-my-socket-in-my-redux-store)
- Websockets should typically go in a Redux middleware, where they have access to dispatch and getState
- ## [Socket.io-client on recieving event running useEffect two times - Stack Overflow](https://stackoverflow.com/questions/75250544/socket-io-client-on-recieving-event-running-useeffect-two-times)
- the problem is that you are removing the wrong listener--you have to pass the exact same function that you want to remove (because you can have two listeners on an event). 
- ## 🫧 [address horizontal scalability in documentation · Issue · ueberdosis/hocuspocus _202304](https://github.com/ueberdosis/hocuspocus/issues/575)
- It's not clear to me the guarantees hocuspocus tries to achieve around horizontal scaling. #178 and #279 both talk about horizontal scaling, but I'm hoping for something explicit in the code that yes, hocuspocus supports multiple instances behind a load balancer, if all features (eg stateless messaging) are expected to work, etc. I think the answer is yes, but I'd love more explicit confirmation somewhere!
- [Redis Scaling  · ueberdosis/hocuspocus](https://github.com/ueberdosis/hocuspocus/issues/178)
- ## [Web Sockets are not efficient and hard to scale, change my view. : r/reactjs _202312](https://www.reddit.com/r/reactjs/comments/18ogc0o/web_sockets_are_not_efficient_and_hard_to_scale/)
- Socket.io internally uses ws library as one of their transport options. socket.io provides a lot of options like retries, polling, disconnection detection, multiplexing, retry options etc etc lot of configurations which you may need in real applications sooner or later . You can also check by providing ws as first option as socket.io transports . Better check socket.io performance tuning guide.
- I saw it mentioned in another comment, but definitely look into Server-Sent Events (SSE) using something like Event Source.
- We use websocket for chats and notifications and we can dynamically scale up and down because backend is containerized and we are storing the socket session’s on redis
  - Socket.io has documentation on how to scale the app you can follow that. Or just store the socket session when client join the app thats it
- Web sockets just use TCP. It's pretty lightweight, you can have a metric shit-ton of active TCP connections with no issues.
- ## [The WebSocket Handbook | Hacker News _202201](https://news.ycombinator.com/item?id=29893242)
- We use WebSockets in two regards: handling live page updates via Phoenix Live View for users (eg: real time chat messages, viewer count, etc) and as a transport medium for our real time API. The former is very easy to handle because for the most part users are navigating around pages which can terminate the ws connection and creates a new one (though most of the times not). The advantages Live View provides us is not having to write duplicated logic in the client & server, and instead just push data to users and their browser automatically reflects the changes.
- ## [Proper way of using React hooks + WebSockets - Stack Overflow](https://stackoverflow.com/questions/60152922/proper-way-of-using-react-hooks-websockets)
- As you are only setting the web socket once, I think a better approach is to use a ref instead of a state
- What is the right way to handle authentication over web sockets?
  - As with REST APIs, you'd want to be able to authenticate to a websocket-based API using either basic auth, or a bearer token-based auth scheme. Unfortunately, the browser websocket API doesn't allow you to specify arbitrary headers in the websocket request, so it's typical instead to have credentials supplied via a query param (such as "accessToken" for a bearer token) in the wss request.
- It's the same thing as HTTP. Websocket starts off as an HTTP request with cookies, headers etc. Use those just like HTTP to authenticate, and your Websocket server should pass the user data to the websocket object
- Best solution might be to generate a short-lived one-time-use ticket and pass it in the querystring.
- HTTP servers have already solved traffic management, load balancing, scaling up and down, zero downtime deployments, A/B tests and experimentation and lots more to such a degree that we don't have to even think about them anymore. All of these problems come to the forefront again when you have to scale websocket connections beyond a single server.
  - There's a (relatively) easy trick for this: Redis pubsub. When a message comes into an instance, you push it to Redis and have all of your other instances subscribed to it. Messages sync in real-time and the experience is transparent.
- To be a bit clearer, you don't want to push websocket messages per se; eg auth negotiation or info requests. You do want to pubsub out conditioned messages that are generated by any given instance for the purpose of broadcast; eg "userX connected" or "userX said Y".
- If you want something simpler for real-time communication you can use comet-stream. It goes through all firewalls and scales better than most single threaded websocket servers: https://github.com/tinspin/rupy/wiki/Comet-Stream
- 
- 
- ## [Ask HN: WebSocket data architecture strategies: idempodent vs. incremental data? | Hacker News _202104](https://news.ycombinator.com/item?id=26963959)
- I think you could find some inspiration in cryptocurrency exchanges. Most of them expose public websockets for prices, order books, trades, etc. They're high volume with lots of subscribers.
- If I understand the question: you don’t have to choose between idempotence and efficient incremental updates if you can give your application data a revision number. Send your incremental update(delta) with a reference to the app data’s last revision. Increment the revision number after applying each delta and reject any delta that doesn’t reference the current version on the server, they’ll only be applied at most once, so they’re idempotent. There are fancier versions of this scheme that can be devised based on the business rules for your application.
- ## [Ask HN: How do you scale WebSocket? | Hacker News _202206](https://news.ycombinator.com/item?id=31925145)
- Socket.io has a great article on how you can setup your architecture to scale Web Socket servers: https://socket.io/docs/v4/using-multiple-nodes/
- it sounds like the immediate question is how do you route an external event (webhook) to the right websocket.
  - You need to include information that comes back in the event that identifies the websocket, either directly (server id + an id the server would understand) or indirectly (something that you can look up in a table/hash to get direct information).
- 
- 
- ## 💥 [Millions of active WebSockets with Node.js | Hacker News _202302](https://news.ycombinator.com/item?id=34876935)
- > The theoretical limit is 65k connections per IP address but the actual limit is often more like 20k, so we use multiple addresses to connect 20k to each (50 * 20k = 1 mil).
  - The 65k limit is because of the port limit. WebSocket is using the “trick” of opening a port without answering before the server have any news to give, this way the messages are more push-like.
- We did this with Node.js and uWebSockets and it scaled easily to a few million web sockets on ~10 machines so I can confirm the stack works in practice
- ## [Show HN: DriftDB – an open source WebSocket backend for real-time apps | Hacker News _202302](https://news.ycombinator.com/item?id=34639728)
- have you come across NATS? https://nats.io. The server natively supports WebSockets. There are many clients including Deno, Node, WebSockets, Rust, Go, C, Python, etc. In addition to stateless messaging, it supports durable streams, and optimized API layers on top like key-value, and object storage. The server also natively supports MQTT 3.1.1.
  - Nats is not something I see as a competitor for external clients (browsers, mobile apps), primarily because it doesn't handle reconnections / message delivery / quality-of-service / at-least-once or exactly-once delivery (except for MQTT).
  - Therefore, I don't see what it adds here. It seems designed for service communication, not client-server. They also don't list browsers as a use case https://docs.nats.io/nats-concepts/overview#use-cases. (though it is of course possible, it's just not ideal IMHO.)
- Even with NATS jetstream, NATS has a focus on service communication.
- what's the relationship between driftdb and plane? Can they be used together? Does one depend on another?
  - The idea for DriftDB came from seeing people try to use Plane for things that it wasn’t intended for (e.g. simple WebSocket backends). DriftDB doesn’t depend on Plane if it’s hosted on Cloudflare. For deploying on your own infrastructure, Plane could be useful, but there are a few pieces missing to do the integration.
- 🔀 This is really cool! But how are conflicts handled?
  - As far as the server itself is concerned, it’s just a broadcast channel with replay and compaction capabilities, so it’s not directly concerned with conflict resolution. You could use it as a broadcast channel for CRDTs if you wanted to.
  - The useSharedState react hook is more opinionated, it uses last-write-wins semantics in the case of a conflict. The useSharedReducer hook’s behavior on conflict is up to the reducer provided.
- ## [Woe be unto you for using a WebSocket | Hacker News _202112](https://news.ycombinator.com/item?id=29651447)
- I think this conflates a very specific paradigm for using WebSockets (state synchronization with a stateful "server") with WebSockets as a technology.
  - WebSockets are just, well, sockets, with a goofy HTTP "upgrade" handshake and some framing on top of them. You could implement the exact same request/response model as in an HTTP based service over a WebSocket if you wanted to.
  - Stateful services are a tradeoff whether you use a WebSocket or not.
- Websockets work great for message passing but it struggles with data structures more complicated than what JSON can represent. Jsynchronous syncs any javascript object or array with arbitrarily deep nesting and full support for circular data structures.
- I am the author of Centrifugo server (https://github.com/centrifugal/centrifugo) - where the main protocol is WebSocket. Agree with many points in post – and if there is a chance to build sth without replacing stateless HTTP to persistent WebSocket (or EventSource, HTTP-streaming, raw TCP etc) – then definitely better to go without persistent connections.
- 💡 My advice:
  • Make push updates optional. If no push connection can be established, fall back to polling. You can start by implementing polling only and add push later.
  • Use websockets only for server-to-client communication. Messages from the client are sent via regular HTTP requests.
  • Keep no meaningful state on the server. That includes TCP connection state. You should be able to kill all your ec2 instances and re-spawn them without interrupting service.
  • Use request/response for all logic on the server. All your code should be able to run in an AWS lambda.
  • Use a channel/subscription paradigm so client can connect to streams they're interested in
  • Instead of rolling your own websocket server, use a hosted service like pusher.com or ably.com. They do all the heavy lifting for you (like keeping thousands of TCP connections open) and provide a request/response style interface for your server to send messages to connected clients
- I work at MSFT and on the fluid framework.
  - We use websockets and solve a lot of the state management problem called out here by keeping very little state on the server itself. The primary thing on server is a monotonically increasing integer we use to stamp messages, this gives us total order broadcast which we then build upon
  - The main server logic is in the Alfred and Deli lambdas. Alfred sits on the socket and dumps message into Kafka. Deli sits on the Kafka queue, stamps messages, the puts them on another queue for Alfred’s to broadcast
- come to phoenix/elixir land. Channels are amazing and the new views system allows you to seamlessly sync state to a frontend using websockets with almost no javascript
- Worth looking at Elixir Phoenix Channels if you’re wanting to use sockets. Handle a lot of the messy stuff for you.
- The answer is simple: Abstraction, or the lack thereof. Building real-time web applications are difficult. But the difficulty is accidental complexity that could be abstracted away. However, most of the tech stacks are not there yet - mainly because the request-response model is good enough for most of the sites, so the industry wouldn't push it forward wholeheartedly. Maybe the situation would start to change after WASM take off, or maybe not.
  - The best bet is to work on platforms that already have great WebSocket support. PHP might not be a great choice. Node.js is okayish but not great. Blazor sounds interesting but I'm not sure about the performance. Elixir/Phoenix is probably the best bet for now. It has nice, abstracted APIs, it's performant, and it can form clusters either by itself or with Redis.
  - It's very hard to scale WebSocket because of its stateful nature, so please look for platforms already solved this problem.
- You can turn websockets into a flawless request/response with async/await included on like 20 lines of JavaScript. I do it all the time. Generate an ID, make a request, store the promise resolve/reject in a map (js object). Your onmessage handler looks up the promise based on the ID and resolves the promise.
- The biggest challenge when migrating from HTTP to any kind of stream is the loss of callback on response, because there is no request/response. There is only push. That means your messaging and message handling becomes far more complex to compensate.
- ## 🏹 [Deepstream 5.0: Resurrected using MIT license | Hacker News _201910](https://news.ycombinator.com/item?id=21371658)
- Generally deepstream is an alternative to using firebase, socket.io, featherJS and meteor. However rather than putting the logic within the server you instead run them as microservices and allow deepstream to handle load-balancing for you.
- The two main things deepstream offers are: 
  - Events: pubsub mechanism
  - Records: Records is events with persistence. They are more heavy weight objects that persist their content in a cache + db and across all connected devices without the user/developer having to actually do anything. The also support offline support if you want to be able to get/set data while offline.
- It's a real-time pub/sub messaging system (competitive to NATS), with built in messaging patterns like request/response.
  - Also supports persistence of data records (JSON docs) and syncing changes to those docs (competitive to Firebase, etc), backed by Redis.
  - Works with different protocols (websocket, MQTT, HTTP) and has client libraries for popular languages.
- The biggest pain point I've experienced with these pubsub services is how to negotiate client connections so that all the subscribers to a topic are directly connected to the same machine. 
  - In other words, clients' messages do not have to ever be relayed at the networking level. 
  - This means providing some reconnecting or connection-info data for the client, and it's why I think most of these frameworks fail to improve on home cooked solutions: you have to touch the message to help squeeze out efficiency.
  - A non-IP based routing mechanism requires some kind of header/parsing/deserialization of the message being passed. In application level code this is quite slow, you have to query some kind of map synchronized about cluster nodes. This is especially shitty if message addresses are ephemeral, especially per RPC call (which is the default behaviour in most cluster-based RPC frameworks), because then your near cache of the cluster map is never populated. Alternatively you can just broadcast to everyone (skip the cluster map) but then why cluster?
  - It would be great if we just had IPv6 adoption though. Then you could just uh, route. The DNS based routing in stuff like Kubernetes is close but not for external Internet facing clients. The whole point is to avoid a bastion host.
- I totally agree. Having a single point of entry gives us some small benefits like a single connection/simplified deployments but it isn't efficient to have a provider connected on one node in a cluster and have to forward data to subscribers on another just because of how they were distributed by a load-balancer. Theres actually an action in the handshake protocol which allows a node in a cluster to redirect a connection to a different/more optimal node. It was used for multi-tenancy clusters previously. In theory you can run multiple isolated clusters (or individual nodes) and have multiple connections from the client, routed based on which subscription lives where. It's a pattern I have been talking about with a couple of users but it hasn't been required by anyone yet. It isn't as efficient as doing it on a network layer but it at least reduced intercluster traffic dramatically.
- I used to be really concerned about this, but one day I sat down and did the math and realized that the worst case scenario is that I'd have no more than two times as many messages, which means this isn't a scalability issue: if a topic has N subscribers, at bare minimum you are going to have N+1 messages to send a given event (one to receive it into the cluster, and N to dispatch it to the subscribers); if everyone is connected to some random machine, then you need to take the incoming event and send it to the right internal machine that is storing that topic (which is one extra message) and then that machine will need to indirectly send the message to the connecting computers of the subscribers (which is one extra message per subscriber), so you end up with 2N+2 messages. The alternative, where users cluster themselves based on topic with their entry connections, is that these individual end users have to maintain a ton of separate connections for inbound messages for each of the topics they are interested in, which is often going to work out to be much worse for everyone involved.
- 
- 
- 
- 
- 
- 
- ## After working with WebSockets for a while I'm wondering why devs don't use them more.
- https://x.com/jamonholmgren/status/1798803384541302814
- Great technology but I always opt for SSE + a good API kind of achieves everything you need, easier to maintain and feels cleaner
- Market data providers like @AlpacaHQ use websockets, there’s no other way 
  - http://HawkAlpha.com uses websockets to stream and place trades in real time
- Elixir/Phoenix/LiveView is the on true way.
- Compensating for data loss on disconnect / reconnect
- typical cookie based Authentication isn't as straightforward with web sockets because cookies only get sent once on initial connect
- Scaling tends to be much harder with web  sockets due to no caching and more resources
- To me the big two things are:
  - 1) Event-driven architecture is unfamiliar to most and generally harder to reason about 
  - 2) scaling/deployment requires extra work
- ## 🆚️ Server-sent events, WebSocket, and Webhooks. How do they differ?
- https://twitter.com/Franc0Fernand0/status/1777675213729136987
- WebSocket 
  - They provide a bidirectional communication channel over a single TCP connection.
  - The client and server can both send messages through the channel in real-time.
  - To use WebSocket, the client must include specific fields in the HTTP header to tell the server to switch to the WebSocket protocol.
  - Once the server replies, a WebSocket connection is set up.
- Server-sent events 
  - A bidirectional channel is overkill in scenarios where the data flow is unidirectional.
  - SSE addresses this problem and allows the server to push messages to a client over HTTP.
  - The client sends a GET request to the server, specifying it’s waiting for an event stream.
  - This will start an open connection that the server can use to send messages to the client.
- WebHooks 
  - While SSE is usually used to get updates to the front end, Webhooks generally get updates to the back end.
  - They work like a callback informing the client of new updates. The server set up a clear API endpoint to receive updates from outside.
- ## 🌰 ChatGPT网页版从SSE改成Websocket了 _20240202
- https://twitter.com/wong2_x/status/1753351893211037994
- https://twitter.com/wong2_x/status/1759403801394794789
  - 更新：又全部改回SSE了 _20240219
- 1. 对终端用户来说使用感觉基本没有变化。
  - 2. 但从技术角度看, ChatGPT改用Websocket技术与服务器端通信可以提升通信效率, 降低延迟, 且支持性更好。
- http://pplx.ai 也改成了 Websocket.
- 说明生成和计算速度更快了，也扩容了。
- 感觉没什么必要，除非交互形式不再需要问一句答一句，而是支持连续提问或者多人群聊
- 从生命周期来看 Websocket 管理起来更麻烦一些, 但的确建立连接次数会降，也算一个优化吧。工程上提升复杂度，性能上拿到收益。
- 想问下怎么判断的
  - 浏览器看下Network
- 是两种都在用 我今天还是wss
- AB Test测试后回滚？
  - 应该是的
- 对于这种只需要response流式返回的场景，sse就足够了而且架构足够简单，服务端不需要做什么特殊设置（设置一些content-type）就可以了，相反websocket在chatgpt这种场景下有点杀鸡用牛刀了。
- 是的，ws有状态，维护起来还是麻烦
- Gradio 4.0 也从ws改成了SSE
- ws的后端把上下行拧在了一个连接上，增加复杂度，不易解耦。
  - 对于前端来说sse还是ws其实无所谓。
- 对这样的场景来说，websocket 太复杂了。
- ## 🆚️ You can use two ways to let web apps talk to each other: polling and webhooks.
- https://twitter.com/Franc0Fernand0/status/1748620224767701040
- In API Polling, your app continuously requests updates to the email-sending server to know if the mail has been sent. 
- this method is simple and easy to use, it does have  some drawbacks:
  - It requires a lot of resources
  - It doesn't give real-time updates
  - The 3rd party service service talks to your app directly, which makes it less secure.
- Webhooks, on the other hand, work like a callback or a direct phone call informing your app of new updates. 
- This push-based approach has many advantages:
  - Ensure real-time data updates
  - Reduce the number of API calls and resources you use
  - Guarantee better scalability and system decoupling
- there are also some things to think about when setting up Webhooks.
  - First, it is necessary to set up a clear API endpoint to send updates from outside services.
  - Second, it is important to set up security measures for webhook requests and failure handling measures for when the webhook doesn't get an answer
- Over the years, I've seen webhooks become dominant while integrating with 3rd party APIs.
- One failure-handling measure in webhook is using a message broker like RabbitMQ to ensure that updates are delivered again until your server acknowledges them.
- How do you deal with webhook failure?
  - You can implement a retry policy for failed delivery but limit the number of retries to prevent endless attempts. 
  - As a fallback strategy, you can consider an alternative communication channel.
- How do we implement robust failure handling in both Webhook and Polling scenarios?
  - Retry strategies are at the base of failure handling in both cases. With polling, you can consider adaptive polling to adjust the frequency based on the system load.
- ## 🆚️ Polling vs Webhooks
- https://twitter.com/ProgressiveCod2/status/1734474112670822904
  - In polling, a client repeatedly requests data from a server at predefined intervals.
  - Webhooks are like having a built-in notification system. Data is pushed to you as soon as it’s available.
- The choice depends on how realtime the client needs data. Webhooks have drawbacks too
  - server needs to keep inventory of clients
  - server should be resilient to network partitions 
- Notification backed by scalable APIs could be another approach.
- ## [在多媒体通信中，信令服务器和流媒体服务器各充当什么角色？各自的主要功能是什么？ - 知乎](https://www.zhihu.com/question/281716536)
- 信令是协调通信的过程。为了使WebRTC应用程序能够建立一个“通话”，其客户需要交换以下信息：
  - 会话控制消息用于打开或关闭通信
  - 错误消息
  - 媒体元数据，如编解码器和编解码器设置，带宽和媒体类型
  - 密钥数据，用于建立安全的连接
  - 网络数据，如外界缩减的主机IP地址和端口
- 这个信令过程需要一个方式使客户来回地进行消息传递。
- 没有信令服务器，各个WebRTC之间是没办法通信的。传递媒体数据有两个信息，必须经过信令服务器进行交换。
- 我们要实现p2p直接的通信，需要交换几个信息：媒体信息，网络信息，具体业务。
- 媒体信息
  - 通过SDP来表示，如编解码器是什么？是否支持音频视频？编码方式是什么？等
  - 这些信息是通过SDP协议描述出来，通过信令服务器中转的
- 网络信息
  - 两个WebRTC客户端会尽可能选择P2P进行连接，那么进行连接前是如何发现对方的？就是通过信令服务器。
  - 首先将你所有网络相关信息传到信令服务器，服务器帮你交换到对端，对端拿到你的信息后，
  - 若在同一局域网内，直接通过P2P传输；若不在，首先进行P2P穿越，看是否能打通，打通则传输，打不通则中转等。
- 具体业务
  - 还有一点也需要信令服务器进行传输，比如加入房间，离开房间，禁言等功能
- ## [[译] WebSockets 与长轮询的较量 - 知乎](https://zhuanlan.zhihu.com/p/69950157)
- 长轮询-pros
  - 几乎得到了设备的普遍支持
  - 可以使用 XMLHttpRequest 或通过 JSONP 利用简单的 HTML 脚本标签。
- 长轮询-cons
  - 大量占据服务器资源。
  - 可靠的消息排序 可能是长轮询的一个问题，因为来自同一个客户端的多个 HTTP 请求可能同时运行
  - 根据服务端实现的不同，一个客户端对消息的确认接收也可能导致另一个客户端根本不会收到预期的消息
- websocket-pros
  - 保持一个唯一的连接打开，同时消除长轮询的延迟问题
  - 无需发送头部数据。反过来说，这又减少了数据发送到服务器时需要付出的高昂的数据负载代价。
- websocket-cons
  - 当连接终止时，WebSockets 无法自动恢复连接 —— 这是需要你自己实现的部分，也是导致存在许多 客户端库 的原因。
  - 早于 2011 年的浏览器无法支持 WebSocket 连接
- ## [Web通信中使用长轮询（long polling）Hold住连接的时间应该设置为多久好呢？ - 知乎](https://www.zhihu.com/question/31593363)
- long poll要断掉是因为考虑到链路中间的组件（比如Proxy）可能会强行断开造成问题，不如主动断开重连。
  - 各种组件配置的超时通常可能是60秒或30秒。所以过去一般保守设置为30秒。
  - 百度贴吧设为60秒也许是考察过链路的情况，也可能就是随手一设。具体要找开发人员问了。
- ## 🆚️ [WebRTC和WebSocket有什么关系和区别？](https://www.zhihu.com/question/424264607)
- 这两种技术本质上半毛钱关系都没有，除了它们都可以在web中用之外。
  - socket 和 rtc 有多大区别，这两种技术就有多大区别。
- websocket就是借助于http建立一个tcp的连接，然后在这个tcp连接中传输websocket这种特定协议对应格式的二进制分帧数据。
  - 简单点说，websocket 就是封装了 tcp 来给 web 的 JavaScript 用。
- webrtc则主要是给rtc封装了个web端的js接口。
  - 底层webrtc的库需要完成全部 rtc 相关的逻辑，包括 p2p连接，音视频的，采集，处理，编码，解码，传输，拥塞控制等等等一大堆东西。
  - 另外，传输层协议，webrtc主要在用udp，而不是websocket的 tcp。
- 但说它们一点关系也没有，其实也不一定。
  - 有些 webrtc 的部署方案中，会把 websocket 用作信令协议的传输通道。

### [WebRTC(Web Real-Time Communication)实时通信技术介绍](https://www.zhihu.com/question/424264607/answer/2394172608)

- https://github.com/caiya/webrtc-p2p
  - 在两个浏览器中进行实时视频通话
- https://github.com/caiya/webrtc-p2p-datachannel
  - p2p视频聊天，加入datachannel进行简单的消息发送
- https://github.com/hughfenghen/rtc-live-show
  - 基于WEB RTC + rrweb实现的页面“直播”demo
- WebRTC目的是无插件实现web端的实时通信的能力。
- WebRTC提供了视频会议的核心技术，包括音视频的采集、编解码、网络传输、展示等功能，并且还支持跨平台，包括linux、windows、mac、android等。
- 👉🏻 建立WebRTC连接需要如下几个步骤：
- 获取本地媒体（getUserMedia()，MediaStream API）
- 在浏览器和对等端（其它浏览器或终端）之间建立对等连接（RTCPeerConnection API）
- 将媒体和数据通道关联至该连接
- 交换会话描述（RTCSessionDescription）
- 在WebRTC中，信令起着举足轻重的作用。但实现没有标准化，比如http、websocket、xmpp等。
- 信令就是协调通讯的过程，一旦信令服务建立好了，两个客户端之间建立了连接，理论上它们就可以进行点对点通讯了。
  - 协商媒体功能和设置
  - 标识和验证会话参与者的身份（交换SDP对象中的信息：媒体类型、编解码器、带宽等元数据）
  - 控制媒体会话、指示进度、更改会话、终止会话
  - 双占用分解
- WebRTC要求在两个对等端建立双向的信令通道，通常有三种方式来传输WebRTC信令：http、websocket、数据通道
- WebRTC提供了浏览器端的P2P通信，但并不意味着WebRTC不需要服务器。
- 撇开应用服务器不说，至少以下两种服务器是必须的：
  - 浏览器之间建立通信前交换各种元数据（信令）的服务器（信令服务）
  - 穿越NAT和防火墙的服务器（stun、turn、rsip等）
- 元数据是通过信令服务器中转发给另一个客户端，但是对于流媒体数据，一旦会话建立，首先尝试使用点对点连接。
  - 简单一点说就是：每个客户端都有一个唯一的地址，他能用来和其他客户端进行通讯和数据交换。
- WebRTC使用RTCPeerConnection建立连接传送流数据，在建立RTCPeerConnection实例之后，想要建立点对点的信道，需要做两件事：
  - 确定本机上的媒体流的特性，比如分辨率、编解码能力啥的（SDP描述符）
  - 连接两端的主机的网络地址（ICE Candidate）
- WebRTC定义了两组主要的功能，分别是：媒体捕获（getUserMedia()）、媒体传输。
  - 对等连接和提议/应答协商的概念是媒体传输的核心。
- RTCPeerConnection接口是WebRTC的主要API，用来在P2P端建立媒体连接及数据连接路径。
- RTCDataChannel，数据通道是浏览器之间建立的非媒体的交互连接。
  - 即不传递媒体消息，绕过服务器直接传递数据。
  - 相比WebSocket、http消息，数据通道支持流量大、延迟低。
- 单个对等连接中的多个数据通道底层共享一个流，所以只需一次offer、answer即可建立首个数据通道。之后再建立数据通道无需再次进行offer、answer交换。
- ## [到底什么是WebRTC服务器，以及它是如何联接通话的](https://webrtc.org.cn/webrtc-server/)
- WebRTC并不是真正意味着你不需要服务器来协商和联接通话。它只意味着，在多数情况中，你可以直接地在浏览器之间进行通信。
- 要想让任何WebRTC服务正常的工作，你需要如下2个后端服务器
- 信令服务器
  - 对于浏览器的对话来说，最重要的就是某种中介器—一个了解通话双方端点的服务器。
  - 这就是信令服务器，负责协商会话，而且可能是最接近WebRTC服务器的东西了。
  - 通常，这个服务器也会穿过会话发送相关数据。
  - 信令服务器可以实施像SIP或XMPP的标准化协议，或者私有协议。
  - 有时，信令内容也会作为Web服务器的一部分来操作网页。其他情况中，信令服务器就专门用来处理信令了。
- TURN和STUN服务器
  - 当通话两端端点都检测到了对方的时候，他们会尝试着在其之间建立直接联接—有时候会有用，但也有不起作用的时候。
  - 当没有用的时候，是因为在通信通道上的网络地址转换或者防火墙机制，要么掩盖了浏览器的地址，将其从私人IP地址转换到公共地址，要么它们认为这个会话是不安全的，以至于它们会阻拦流入的数据流并且不允许通话的进行
  - 为了克服这些问题，WebRTC使用了STUN和TURN，它们是要求服务器构件来协助协商媒体传输的协议，而且有时将所有的媒体都中继给TURN服务器。
- 媒体服务器
  - 甚至在协商信令以及联通媒体之后，我们可能还想要在服务端处理媒体。
  - 这种功能是需要有的，因为这样用户就可以实施一个有着大量参与者的会话，并且记录存档会话或会话到其他类型的网络协议的网关。
  - 在这些情况中，我们就会用到后端的媒体服务器。
