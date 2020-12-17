---
title: page-web-ajax
tags: [ajax, web]
created: '2020-08-07T04:37:22.307Z'
modified: '2020-12-16T09:31:18.867Z'
---

# page-web-ajax

## [Web端即时通讯技术盘点：短轮询、Comet、Websocket、SSE](https://zhuanlan.zhihu.com/p/21595082)

### Comet：一种hack技术

- 典型的Ajax通信方式也是http协议的经典使用方式，要想取得数据，必须首先发送请求。在Low Latency要求比较高的web应用中，只能增加服务器请求的频率。
- Comet则不同，客户端与服务器端保持一个长连接，只有客户端需要的数据更新时，服务器才主动将数据推送给客户端。
- Comet的实现主要有两种方式，基于Ajax的长轮询（long-polling）方式和基于Iframe及htmlfile的流（http streaming）方式。
- 在第一种方式中，浏览器在收到数据后会直接调用JS回调函数，但是这种方式该如何响应数据呢？
  - 可以通过在返回数据中嵌入JS脚本的方式，如`<script type="text/javascript">js_func("data from server")</script>`
  - 服务器端将返回的数据作为回调函数的参数，浏览器在收到数据后就会执行这段JS脚本。
  - 但是这种方式有一个明显的不足之处：IE、Mozilla Firefox 下端的进度栏都会显示加载没有完成，而且IE上方的图标会不停的转动，表示加载正在进行。
  - Google 的天才们使用一个称为“htmlfile”的 ActiveX 解决了在 IE 中的加载显示问题，并将这种方法应用到了 gmail+gtalk 产品中。

- #### [有人研究过cometd的Bayeux协议吗？进来一起研究](https://www.iteye.com/topic/142310)
  - 最近在研究comet的相关技术，希望实现一个WebIM。
    - 比较看好DOJO下的Bayeux，抛开DOJO自身存在的问题而言，Bayeux确实是第一个比较全面的实现comet的协议。
    - 特别是对long-polling，callback-polling，iframe这几种comet的实现手段都能支持，
    - 我现在手头只有jetty中自带的一个demo实现了Bayeux，不知道还有没有其他的具体例子？
  - 除了jetty，还有glassfish也可以。好像是只有dojo实现了Bayeux协议。

### Websocket：未来的解决方案1

- 如果说Ajax的出现是互联网发展的必然，那么Comet技术的出现则更多透露出一种无奈，仅仅作为一种hack技术，因为没有更好的解决方案。
- Comet解决的问题应该由谁来解决才是合理的呢？浏览器，html标准，还是http标准？
- 本质上讲，这涉及到数据传输方式，http协议应首当其冲，是时候改变一下这个懒惰的协议的请求/响应模式了。 
- W3C给出了答案，在新一代html标准html5中提供了一种浏览器和服务器间进行全双工通讯的网络技术Websocket。
- Websocket是一个全新的、独立的协议，基于TCP协议，与http协议兼容、却不会融入http协议，仅仅作为html5的一部分。
- 于是乎脚本又被赋予了另一种能力：发起websocket请求。
- 这种方式我们应该很熟悉，因为Ajax就是这么做的，所不同的是，Ajax发起的是http请求而已。

### SSE：未来的解决方案2

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
