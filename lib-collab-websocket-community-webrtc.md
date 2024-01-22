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

- ## [websocket一般会用在什么实际的场合？](https://www.zhihu.com/question/269060103/answer/2399818045)
1. websocket即时通信、社交订阅
2. websocket多玩家游戏
3. websocket协同编辑/编程
4. websocket收集点击流数据
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

- WebSocket在浏览器端的广泛实现似乎只是一个时间问题，值得注意的是服务器端没有标准的API，各个实现都有自己的一套API，并且JCP也没有类似的提案，所以使用WebSocket开发服务器端有一定的风险，可能会被锁定在某个平台上或者被迫降级。

- websocket与http不同的之处在于，http发的请求是同步的(tcp协议会等待响应)，浏览器发起请求会同步等待服务器返回，而socket是发送完了就结束了，不管服务器又没返回，而且先发地数据不一定先收到，不按顺序返回， 难点就在于发送数据在ws.send函数里，而接收数据在ws.onmessage里，数据不能互通

- 很多公司内部http proxy不配置代理websocket，对于toB业务是个很大的障碍

- ws有很多缺点，传数据不是标准的，因为不是标准的，中间件看不到你做了什么，waf无法正常检测，cc 入侵防不胜防
- 数据处理太随意，无法准确负载均衡，可能a机器累死了b机器在围观
- 状态恢复需要更多的确认措施，否则存在安全风险
# discuss-sse
- ## 

- ## 

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

# discuss
- ## 

- ## 

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
