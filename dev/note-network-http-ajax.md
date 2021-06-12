---
title: note-network-http-ajax
tags: [ajax, http, network]
created: '2020-08-07T04:37:22.307Z'
modified: '2020-12-21T06:03:02.191Z'
---

# note-network-http-ajax

# guide

- xhr优点
  - 支持广泛，兼容性强
- xhr缺点
  - 代码冗长，xhr对象操作较混乱
  - callback hell
  - 需要手动解决CSRF攻击
- fetch优点
  - 代码简洁，promise较少callback
- fetch缺点
  - 返回值类型是promise，被promise的缺点限制
    - 不能取消，只能消费一次，操作符只有then和catch
  - 有极少xhr功能未实现，如进度通知
- observable优点
  - 操作符丰富
- observable缺点
  - 需要引入第三方实现库，增加项目复杂度和体积
# xhr/ajax
- 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案。
- 本身是针对MVC的编程, 不符合现在前端MVVM的浪潮。
- JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理
  - （采取个性化打包的方案又不能享受CDN服务）。
# fetch/promise
- Fetch是基于promise设计的，Fetch的代码结构比起ajax简单多了
- fetch不是ajax的进一步封装，而是原生js，没有使用XMLHttpRequest对象
- 符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里
- 更好更方便的写法
- 更加底层，提供的API丰富（request, response）
- 脱离了XHR，是ES规范里新的实现方式
- fetch只对网络请求报错，对400，500都当做成功的请求，需要封装去处理
- fetch默认不会带cookie，需要添加配置项
- fetch不支持abort，不支持超时控制，
  - 使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了资源浪费
- fetch没有办法原生监测请求的进度，而XHR可以

- axios
  - axios 基于promise用于浏览器和node.js的http客户端。
  - 在浏览器中创建 XMLHttpRequest。
  - 在 node.js 创建 http 请求。
  - 支持 Promise API。
  - 提供了一些并发请求的接口（重要，方便了很多的操作）。
  - 支持拦截请求和响应。
  - 转换请求和响应数据。
  - 取消请求。
  - 自动转换 JSON 数据。
  - 客户端支持防止CSRF。
  - 客户端支持防御 XSRF。
# [Web端即时通讯技术盘点：短轮询、Comet、Websocket、SSE](https://zhuanlan.zhihu.com/p/21595082)

## Comet：一种hack技术

- 典型的Ajax通信方式也是http协议的经典使用方式，要想取得数据，必须首先发送请求。在Low Latency要求比较高的web应用中，只能增加服务器请求的频率。
- Comet则不同，客户端与服务器端保持一个长连接，只有客户端需要的数据更新时，服务器才主动将数据推送给客户端。
- Comet的实现主要有两种方式，基于Ajax的长轮询（long-polling）方式和基于Iframe及htmlfile的流（http streaming）方式。
- 在第一种方式中，浏览器在收到数据后会直接调用JS回调函数，但是这种方式该如何响应数据呢？
  - 可以通过在返回数据中嵌入JS脚本的方式，如`<script type="text/javascript">js_func("data from server")</script>`
  - 服务器端将返回的数据作为回调函数的参数，浏览器在收到数据后就会执行这段JS脚本。
  - 但是这种方式有一个明显的不足之处：IE、Mozilla Firefox 下端的进度栏都会显示加载没有完成，而且IE上方的图标会不停的转动，表示加载正在进行。
  - Google 的天才们使用一个称为“htmlfile”的 ActiveX 解决了在 IE 中的加载显示问题，并将这种方法应用到了 gmail+gtalk 产品中。

- ### [有人研究过cometd的Bayeux协议吗？进来一起研究](https://www.iteye.com/topic/142310)
  - 最近在研究comet的相关技术，希望实现一个WebIM。
    - 比较看好DOJO下的Bayeux，抛开DOJO自身存在的问题而言，Bayeux确实是第一个比较全面的实现comet的协议。
    - 特别是对long-polling，callback-polling，iframe这几种comet的实现手段都能支持，
    - 我现在手头只有jetty中自带的一个demo实现了Bayeux，不知道还有没有其他的具体例子？
  - 除了jetty，还有glassfish也可以。好像是只有dojo实现了Bayeux协议。

## Websocket：未来的解决方案1

- 如果说Ajax的出现是互联网发展的必然，那么Comet技术的出现则更多透露出一种无奈，仅仅作为一种hack技术，因为没有更好的解决方案。
- Comet解决的问题应该由谁来解决才是合理的呢？浏览器，html标准，还是http标准？
- 本质上讲，这涉及到数据传输方式，http协议应首当其冲，是时候改变一下这个懒惰的协议的请求/响应模式了。 
- W3C给出了答案，在新一代html标准html5中提供了一种浏览器和服务器间进行全双工通讯的网络技术Websocket。
- Websocket是一个全新的、独立的协议，基于TCP协议，与http协议兼容、却不会融入http协议，仅仅作为html5的一部分。
- 于是乎脚本又被赋予了另一种能力：发起websocket请求。
- 这种方式我们应该很熟悉，因为Ajax就是这么做的，所不同的是，Ajax发起的是http请求而已。

## SSE：未来的解决方案2

- SSE（Server-Sent Event，服务端推送事件）是一种允许服务端向客户端推送新数据的HTML5技术。
- 与由客户端每隔几秒从服务端轮询拉取新数据相比，这是一种更优的解决方案。
- 与WebSocket相比，它也能从服务端向客户端推送数据。那如何决定你是用SSE还是WebSocket呢？
- 概括来说，WebSocket能做的，SSE也能做，反之亦然，但在完成某些任务方面，它们各有千秋。
- 个人认为SSE最大的优势就是便利：不需要添加任何新组件，用任何你习惯的后端语言和框架就能继续使用。
  - 你不用为新建虚拟机、弄一个新的IP或新的端口号而劳神，就像在现有网站中新增一个页面那样简单。我喜欢把这称为既存基础设施优势。
- SSE的第二个优势是服务端的简洁。
  - 相对而言，WebSocket则很复杂，不借助辅助类库基本搞不定（我试过，令人痛苦）。
- 因为SSE能在现有的HTTP/HTTPS协议上运作，所以它能直接运行于现有的代理服务器和认证技术。
  - 而对WebSocket而言，代理服务器需要做一些开发（或其他工作）才能支持
- SSE还有一个优势：它是一种文本协议，脚本调试非常容易。
- WebSocket相较SSE的一个潜在优势：
  - WebSocket是二进制协议，而SSE是文本协议（通常使用UTF-8编码）。
  - 当然，我们可以通过SSE连接传输二进制数据
  - 但用SSE传输二进制数据时数据会变大，如果需要从服务端到客户端传输大量的二进制数据，最好还是用WebSocket。
- WebSocket相较SSE最大的优势在于它是双向交流的，这意味向服务端发送数据就像从服务端接收数据一样简单。
  - 用SSE时，一般通过一个独立的Ajax请求从客户端向服务端传送数据。
  - 相对于WebSocket，这样使用Ajax会增加开销，但也就多一点点而已。
- 当你在享用SSE的既存基础设施优势，并在客户端和服务端脚本之间设了一个网络服务器，区别就显现出来了。
  - 一个SSE连接不仅使用一个套接字，还会占用一个Apache线程或进程，如果用PHP，它会为这个连接专门创建一个PHP新实例。
  - Apache和PHP会使用大量的内存，这会限制服务器所能支持的并行连接数。
  - 所以，要做到用SSE在数据传输性能上和WebSocket完全一样，需要写一个自己的后端服务器

- ref
  - [为什么网页版微信/QQ，GTalk的IM通讯用的都是comet长连接而不用websocket？](https://www.zhihu.com/question/350007333)
# blog

## Why I still use XHR instead of the Fetch API

- [Why I still use XHR instead of the Fetch API_2018](https://gomakethings.com/why-i-still-use-xhr-instead-of-the-fetch-api/)

- UPDATE: I’ve completely changed my mind on this. I’m now all-in on fetch()

## How to use the Fetch API with vanilla JS

- [How to use the Fetch API with vanilla JS](https://gomakethings.com/how-to-use-the-fetch-api-with-vanilla-js/)

## [The Bayeux Protocol Specification 1.0](https://docs.cometd.org/current/reference/index.html#_bayeux)

- Bayeux is a protocol for transporting asynchronous messages (primarily over web protocols such as HTTP and WebSocket), with low latency between a web server and web clients.
- The primary purpose of Bayeux is to support responsive bidirectional interactions between web clients, for example using using AJAX, and the web server.
- Bayeux is a protocol for transporting asynchronous messages (primarily over HTTP), with low latency between a web server and a web client. 
- The messages are routed via named channels and can be delivered:
  - server to client
  - client to server
  - client to client (via the server)
- By default, publish/subscribe routing semantics are applied to the channels.
- Delivery of asynchronous messages from the server to a web client is often described as server push. 
- The combination of server push techniques with an AJAX web application has been called **Comet**. 
- CometD is a project by the Dojo Foundation to provide multiple implementation of the Bayeux protocol in several programming languages.
- Bayeux seeks to reduce the complexity of developing Comet web applications by allowing implementers to more easily interoperate, 
  - to solve common message distribution and routing problems, 
  - and to provide mechanisms for incremental improvements and extensions.

- [Difference between async servlet long poll and bayeux protocol (Comet)](https://stackoverflow.com/questions/14268606/difference-between-async-servlet-long-poll-and-bayeux-protocol-comet)
  - It is true that "Comet" is the term for these technologies, but the Bayeux protocol is used only by few implementations. 
  - A Comet technique can use any protocol it wants; Bayeux is one of them.
  - there are two main differences between an async servlet solution and a Comet+Bayeux solution.
  - The first difference is that the Comet+Bayeux solution is independent of the protocol that transports Bayeux. 
    - In the CometD project, there are pluggable transports for both clients and servers that can carry Bayeux. 
    - You can carry it using HTTP, with Bayeux being the content of a POST request, 
    - but you can also carry it using WebSocket, with Bayeux being the payload of the WebSocket message. 
    - If you use async servlets, you cannot leverage WebSocket, which is way more efficient than HTTP.
  - The second difference is that async servlets only carry HTTP, and you need more than that to handle remote Comet clients.
    - Quickly you realize that you're building another protocol on top of HTTP.
    - At that point, it's better to reuse an existing protocol like Bayeux, and proven solutions like CometD
# discuss
- ## Performance is a top priority of SWR.
- https://twitter.com/shuding_/status/1324405638986788864
- why and how SWR ensures your app to be always fast and reactive:
  ✅ No extra requests
  ✅ No extra re-renders
  ✅ No extra code imported
- If only the server-side prefetcher were as good as the one in React Query, I would definitely think about switching to SWR
- Nice - Is it doing a fetch request within a useEffect hook under the hood?

- ## TIL: no way to fetch huge (2GB+) files, and XHR on readyState 3 is hopeless too (it keeps incrementing responseText even if consumed).
- https://twitter.com/WebReflection/status/1395733097187090442
- If you’re wondering the use case: CSV files is just one of them, and you gotta be smart about lines split, but it works after all and it’s the best solution we have
- [Streaming requests with the fetch API](https://web.dev/fetch-upload-streaming/)
- Chrome 85 has an experimental implementation of request streams, 
  - meaning you can start making a request before you have the whole body available.
- usecase
  - Warm up the server. 
    - In other words, you could start the request once the user focuses a text input field, and get all of the headers out of the way, then wait until the user presses 'send' before sending the data they entered.
  - Gradually send data generated on the client, such as audio, video, or input data.
  - Recreate web sockets over HTTP.

- ## I've just included Undici as the best way for fetching data on the server-side in my "Real-World Next.js" book. 
- https://twitter.com/MicheleRivaCode/status/1386357676540579844
- https://github.com/nodejs/undici
  - An HTTP/1.1 client, written from scratch for Node.js
  - https://github.com/Ethan-Arrowood/undici-fetch
    - A WHATWG Fetch implementation based on @nodejs/undici
- Next.js automatically polyfills fetch API on the server-side, but in my book I do explore alternatives... and Undici is by far my favorite one
- Yep. Undici is more reliable, it's well designed and tested, and it has better defaults for serverless environments. 
  - We're already using it inside some places of the @vercel core production infrastructure which gives us the confidence to adopt it more broadly.
  - I could even see it providing the `fetch` global in the default Node.js distribution 
# ref
- [AsyncAPI 2.0: Enabling the Event-Driven World_202105](https://tech.ebayinc.com/engineering/asyncapi-2-0-enabling-the-event-driven-world/)
  - Learn about how eBay is standardizing on and publishing AsyncAPI Specification 2.0-based contracts for event notifications.
