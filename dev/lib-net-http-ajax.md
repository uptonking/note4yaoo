---
title: lib-net-http-ajax
tags: [ajax, http, network]
created: 2020-08-07T04:37:22.307Z
modified: 2023-02-06T09:14:40.114Z
---

# lib-net-http-ajax

# guide

- react程序中，通过事件处理器如onClick触发网络请求的实现应该放在事件处理器，还是放在useEffect?
  - ajax放在事件处理器如onClick，更易理解
    - react准备移除[setState on unmounted Comp](https://github.com/facebook/react/pull/22114)的warning，提到了事件处理器的side effect可能引发重复请求的问题
  - ajax放在useEffect
    - ❌️ 首次render不应该自动执行useEffect，因为ajax应该由点击事件触发
    - ❌️ 其他state/props/deps的变化不应该自动执行useEffect，因为ajax应该由点击事件触发
    - ✅️ 更符合react中执行side effects的设计
    - ✅️ 用户连续点击按钮触发事件时，因为state未变，不会重复触发

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

- [Inside React Query_202212](https://tkdodo.eu/blog/inside-react-query)

- [Arrow Flight RPC — Apache Arrow](https://arrow.apache.org/docs/format/Flight.html)
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
# http-range
- https://github.com/uphold/koa-pagination
  - koa-pagination is a middleware to handle Range Pagination Headers using Range & Content-Range entity-headers.

- https://github.com/academia-de-codigo/parse-content-range-header
  - Parses an HTTP Content-Range header and returns response range information.
  - allows for missing range unit for compatibility with headers generated by hapi-pagination

- more-range
  - https://github.com/expressjs/express-paginate
  - https://github.com/UlisesGascon/express-simple-pagination
  - https://github.com/purposeindustries/express-range
  - [Paginated list in Typescript (from Content-Range header)](https://gist.github.com/merlosy/1c333cf3e149ba182a7c0676a802bad8)
  - [NodeJS - Simple Pagination for Express and Sequelize](https://gist.github.com/arkanister/d2bcd2016e410e6843826e5fa7500c33)

- [Why most API paginations do not rely on HTTP Range header? - Stack Overflow](https://stackoverflow.com/questions/21765555/why-most-api-paginations-do-not-rely-on-http-range-header)
  - Most of the times you don't want to show all of your items by default. With `?p=2` style pages it's ok to reserve root `/` for first page. With "Range" header it would be strange behavior. HTTP became overbloated long time ago so I wouldn't recommend to accept every its headers as Truth.
  - Here the answers 
    - 👉🏻 考虑兼容性
    - First, custom units are proposed in this draft
    - Second, there is a subtle difference, the first statement has been made for parsing purpose, While the second statement has been made for producing HTTP request.
    - I conform to the HTTP spec when I'm sending [a custom range unit] and they conform to HTTP when they ignore it
    - WebDAV uses HTTP extensions correctly, IMO, but rarely works over the Internet for exactly this reason

- https://github.com/interagent/http-api-design
  - This guide describes a set of HTTP+JSON API design practices, originally extracted from work on the Heroku Platform API.
  - [Further explanation of the Range header for pagination](https://github.com/interagent/http-api-design)

- https://github.com/OpenAPITools/openapi-generator
  - allows generation of API client libraries (SDK generation), server stubs, documentation and configuration automatically given an OpenAPI Spec (v2, v3)
  - [support range header for pagination](https://github.com/OpenAPITools/openapi-generator/issues/5753)
    - Currently we are using, limit / offset query params but our api design docs call for using the header.
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

## [PUT vs PATCH & PUT vs POST - DEV Community](https://dev.to/mehmehmehlol/put-vs-patch-put-vs-post-56i9)

- PUT vs POST
  - The most obvious difference is that PUT can both create and modify a resource while POST can only create a resource.
  - The PUT method is idempotent. Meaning if you (re)try to send a request multiple times, this is equivalent to a single request modification.
  - Whereas, the POST method is NOT idempotent. If you retry to send a request multiple times, you will end up having multiple resources with multiple different URIs on the server.
  - Generally, PUT method is used for UPDATE operations while the POST method is used for the CREATE operations.

- PUT vs PATCH
  - PUT and PATCH can both be used for updating resources. However, the biggest difference between these two is that one can update and replace the resource while the other one can update partially.
  - In other words, when making a PUT request, the enclosed entity is viewed as the modified version of the resource, and the client is requesting to replace with the new info; when making a PATCH request, it modifies only some part of the resource.
  - PUT is idempotent, while PATCH is not idempotent. If a request is reattempted to be made, it will result a failed request (Method Not Allowed). If a PATCH request is made to a non-existent URI, it would simply fail without creating a new resource like PUT.

## Why I still use XHR instead of the Fetch API

- [Why I still use XHR instead of the Fetch API_2018](https://gomakethings.com/why-i-still-use-xhr-instead-of-the-fetch-api/)

- UPDATE: I’ve completely changed my mind on this. I’m now all-in on fetch()

## How to use the Fetch API with vanilla JS

- [How to use the Fetch API with vanilla JS](https://gomakethings.com/how-to-use-the-fetch-api-with-vanilla-js/)

## ⚖️ [The Bayeux Protocol Specification 1.0](https://docs.cometd.org/current/reference/index.html#_bayeux)

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
# more
- [AsyncAPI 2.0: Enabling the Event-Driven World_202105](https://tech.ebayinc.com/engineering/asyncapi-2-0-enabling-the-event-driven-world/)
  - Learn about how eBay is standardizing on and publishing AsyncAPI Specification 2.0-based contracts for event notifications.
# discuss-http2
- ## 

- ## My favorite HTTP/2 feature is Connection Coalescing.
- https://twitter.com/iamakulov/status/1731629685094920349
  - In HTTP2, normally, a browser opens a new connection for every new domain it sees. (So if your site loads via www. but serves images from img., that’d be 2 connections.)
  - Making domains use the same IP address and HTTPS certificate is an *implicit* way to enable connection coalescing; the control is on the browser’s side, and it’s not always great. (Plus sharing IPs is tricky.) But (TIL!) there’s also an *explicit* way.

# discuss-stream
- ## 

- ## 

- ## 🌰 Implementing basic HTML streaming with node
- https://x.com/asidorenko_/status/1857475654364655751
- PHP days all over again

# discuss-polling
- ## 

- ## 

- ## 

- ## 最近把一个 polling based 的任务调度系统改造成 push based，观察到 scheduling delay 从分钟级别降到到了毫秒级别
- https://x.com/_foreverbell/status/1819003908083400923
- 被拒绝了吗？答：polling based也够用了
- 要是我就直接把 poll 间隔改短点 
  - 底层存 event 的 storage 压力会很大
- 底层 event sourcer 系统 bookkeeping message 的成本会上去，不过比起轮询对系统造成的压力来说，这个代价基本上算是 net win 

# discuss-cors
- ## 

- ## cors-anywhere​ can bypass CORS errors
- https://x.com/aidenybai/status/1886446801089081733
  - it tricks the browser by adding `Access-Control-Allow-Origin: *` headers to the response
  - yes it's a reverse proxy
- btw if you are deciding to fork and host it - there are a list of providers that don't allow this (notably vercel!)
  - I always wondered why vercel is not offering a .vercel.dev domain for localhost like ngrok

- This is cool for personal projects, but for a production-level app, depending on a third-party service to proxy data may not be completely reliable

- I always wonder why all the folks here love to rely on third party tools … You can just add the required headers urself

- Just a reminder that websockets do really well in real time communication where the architecture requires persistent, stateful connection and low latency.  This would be a good use case for this.

- ## [Why does my JavaScript code receive a "No 'Access-Control-Allow-Origin' header is present on the requested resource" error, while Postman does not? - Stack Overflow](https://stackoverflow.com/questions/20035101/why-does-my-javascript-code-receive-a-no-access-control-allow-origin-header-i)
- Regular web pages can use the XMLHttpRequest object to send and receive data from remote servers, but they're limited by the same origin policy. Extensions aren't so limited. An extension can talk to remote servers outside of its origin, as long as it first requests cross-origin permissions.

- The CORS standard is a client-side standard, implemented in the browser. So it is the browser which prevent the call from completing and generates the error message - not the server.
  - Postman does not implement the CORS restrictions, which is why you don't see the same error when making the same call from Postman.
  - Why doesn't Postman implement CORS? CORS defines the restrictions relative to the origin (URL domain) of the page which initiates the request. But in Postman the requests doesn't originate from a page with an URL so CORS does not apply.

- A client (most Browsers and Development Tools) has a choice to enforce the Same-Origin Policy.
  - Most browsers enforce the policy of Same-Origin Policy to prevent issues related to CSRF (Cross-Site Request Forgery) attack.
  - Postman as a development tool chooses not to enforce SOP while some browsers enforce, this is why you can send requests via Postman that you cannot send with XMLHttpRequest via JS using the browser.

- CORS is a client side measure implemented in the browser and therefore not something which can prevent DDOS attacks from bot farms.

- 🐛 通过fetch请求文件地址响应404和cors问题，可能是文件存储的磁盘未挂载到kong/nginx配置的路径位置
# discuss-stars
- ## 

- ## 

- ## TIL: In browser, `fetch()` will hide any custom HTTP response header unless you have the `Access-Control-Expose-Headers` header in your response.
- https://x.com/ocavue/status/1910344852803563845

# discuss
- ## 

- ## 

- ## 

- ## node-fetch-server Write servers for Node.js using the web fetch API primitives, like Request and Response
- https://x.com/mjackson/status/1831746987517264056
  - The main API is a createRequestListener() function you can use to create a http. RequestListener that seamlessly integrates with http.createServer() and https.createServer().
  - You can use this to power your Remix app *today* if you aren’t using any special features of Express
  - This is how the web evolves. The people who wrote the spec weren't thinking about server applications for it, but it happened. And now that it has (and we're not going back) it'll improve and adapt.
- I have been saying this for years, this needs to be added to nodejs itself. Looks promising really nice job !
  - There's an effort in the Node.js committee to redesign the http module. I believe that will include the way servers are created. Fingers crossed!
- Very nice. If you still need advanced APIs (express like) use hono instead. Still all web APIs are there.
  - I wish that were true, but they have a bunch of bespoke APIs as well like: request.headers is not a Headers object, but a function you use to get headers (like request.headers('content-type') for example).

- ## [国内 dns 解析国外域名竟然这么慢 - V2EX _202409](https://v2ex.com/t/1069396)
  - 本来用的 AdGuardHome 白名单模式分流国内外域名，腾讯系域名用的 dnspod ，国内其他域名用的 alidns ，其他域名用的 quad9 、cloudflare 、opendns 等国外 dns ，今天突然改成黑名单模式，少数域名用国外 dns ，剩下的腾讯系继续用 dnspod ，其他的都用 alidns 。
  - 结果发现打开很多国外网站特别慢，一看查询日志，原来 alidns 解析很多国外域名都是 1000ms+，这不慢才怪了，看来还是白名单模式更适合，虽然会存在部分错杀（部分国内域名由于用了默认的国外 dns 解析到了非最优的国内 ip 上）。
  - 以前是真没想到国内 dns 解析国外域名比直接从国外 dns 解析还慢的，访问多外 dns 多出那几十上百 ms 跟国内 dns 解析慢的上千 ms 比起来真不算啥

- 别折腾了, 国内直接走运营商的拉到了，国外走 8888 和 1111 ，完事
  - 关键问题是你如何能确定完整的国内域名名单？如果能有全名单，那我除国内域名外的其他域名走国外 dns 就简单了。而且运营商 dns 有个挺致命的问题，HTTPS 解析，也就是 type 65 要么没结果，要么就是错的，这算是我国内用 alidns 最大的原因吧，当然成都电信 alidns 的速度本来也就跟电信 dns 差不多，5ms 左右吧

- 你不用 AdGuardHome 这种软件估计对自己一天的 dns 解析数量没太大概念，我也是用了之后才大吃一惊，我一个人在家的时候一天的解析量就有 5w 左右吧，这还是没开屏蔽的情况下，如果开了屏蔽会窜到将近 10W （有些 app 在得不到相应的情况下会重复请求）。虽然这其中绝大多数是重复的，但其中不重复的也有几百上千个域名吧，很多 app 和网站一打开就会请求两位数域名的。

- alidns 和 dnspod 开始限速了你居然不知道，现在只支持个人使用，家里设备一多请求速上来不卡才怪嘞。
  - 我当然知道要开始限速了，不过不是还没开始吗，而且我除了用公共的外，还都用了个人账户的，并不是这个原因，应该是国外域名在 alidns 和 dnspod 服务器上没缓存，导致访问缓慢

- ## It seems that `fetch` , and by extension all browsers, only support "half duplex" streaming. 
- https://twitter.com/BenLesh/status/1761092192242729125
  - Meaning you can stream the request to the server, but you can't simultaneously stream the response back.
- I think the web is ready for a new API. Observables support this time
  - There's already the WebTransport API, which is http/3. But that's not supported everywhere yet. In particular, I don't think Node supports it yet (but I'm unsure).

- Presumably a WebSocket would work here?
  - Yup. But then I’m hand-rolling multiplexing logic on both ends or using some bloated library.

- It's indeed implied by HTTP protocol which is half-duplex. Websockets allow to upgrade the connection to fullduplex.

- ## 🆚️ Is there any reason to use axios in environments where fetch is available? Other than familiarity.
- https://twitter.com/mattpocockuk/status/1758552616500445329

- [You may not need Axios - Dan Levy's Programming Blog](https://danlevy.net/you-may-not-need-axios/)

- I think Axios can abort a request?
  - Fetch can too, using AbortSignal
- Axios DOES NOT use fetch. (last I checked)
  - In browsers, it uses `XMLHttpRequest` .
  - In Node, it uses the builtin modules `http` & `https` .
- Here's the feature comparison table.  Fetch can do virtually anything Axios can.

- Mostly no, but there are a few use cases like nice defaults, interceptors, retrys, caching. Most of this could be built with a lightweight abstraction on top of fetch, but there are reasons people haven’t moved off. 

- The interface is nice. `const { data, headers, status } = await axios.get<User>('/user')`. This takes a lot more effort with fetch. Still, I think I would use a simple fetch wrapper for new projects.
- But do you really call axios/fetch directly? In my case it’s always inside a service that check status for auth stuff anyway
  - Not all APIs need authentication. Also you can authenticate using Axios interceptors, or cookies.
- the generic is the problem here, interface is actually decent to destructure. fetch wrapper is cheaper and doesn’t use xmlhttprequest

- ky ( @sindresorhus ) and ofetch ( @unjsio ) are both excellent modern fetch wrappers

- axios has cool extras like interceptors, JSON parsing, and better error handling.

- Interceptors. It allows me to automatically assign auth tokens on each request and. Also if you have a global loader in the application you can automatically toggle that on each request

- There are some advantages, I've made good use of axios's interceptor system for tagging on auth and stuff like that

- we use axios between our services internally because you can add interceptors to make axios aware of cache headers. It means that internal HTTP endpoints can be set up with the same type of cache headers as external ones, and you don't have to think about two different types of endpoint response caching depending on where the request came from

- Fetch doesn’t throw on 400/500 so you have to write your own wrapper or rewrite it every place you use fetch. 
  - Axios has a lot of other nice-to-haves too, like base href and interceptors. 
  - I went all fetch then went back to axios

- When using fetch, we end up creating a wrapper around it to do basic things, like: 
  - Parsing the body
  - Throwing errors
  - Insert interceptors
  - Set global default headers config
- interceptors
- instances with common configuration
  - base URL
  - Auth header
  - serialization of search params from JSON
  - serialization of URL params - which is not built-in, but doable using instance configuration
- automatic parse to and from JSON
- Default Headers / Cookies
- Upload Percentage
- Not 32 awaits to get a response
- Throws error on error status codes

- Any project I use fetch in, I end up writing a wrapper that handles errors, converts body to json, simplifies setting headers. Axios does this out of the box. So it is in some ways the better option.

- Axios automatically treats non-2xx responses as errors, which is a nice convenience. But writing a fetch wrapper to do that is trivial.

- 💡 I love fetch and have switched over to it but there are some caveats worth knowing:
  - It doesn't support HTTP/1.1 chunked transfer encoding (ajax does). So if you want to upload a stream of data that you don't know the size of then you're forced to use HTTP/2 and set the duplex: 'half'. Support for all of that is mixed.
  - There are no progress events. Imagine uploading a large file and wanting to show percent uploaded indicator or progress bar. Can't be done right now afaict.
  - In Node.js (undici), ReadableStream and fetch are way slower than built-in http client. However, these will catch up in time.
  - A lot of folks, myself included, can cope with these restrictions though.

- Consider axios only if your project benefits from features like global error handling or progress tracking, which are more straightforward with axios.

- If you build isomorphic web apps, use an LTS version of Node, and don’t use experimental APIs, then you can’t use fetch. It became stable in Node 21.

- ## What made HTTP/1.1 so popular? It was launched in 1997. 
- https://twitter.com/ProgressiveCod2/status/1736330988807152063
  - Persistent Connections. The connection isn't closed immediately after the server sends the response to the client. The client can send additional requests over the same TCP connection.
  - Pipelining. Pipelining allows multiple requests to be sent to the server without waiting for the corresponding response.
  - But there are limits to the number of concurrent TCP connections.

- the 3-way handshake is indeed a foundational aspect of TCP.
  - With HTTP/3, they are going away from TCP to QUIC.

- ## HTTP verbs: I agree there should be only GET and POST.
- https://twitter.com/diegohaz/status/1717196146232246280
  - The issue is that we already have a well-established convention around HTTP verbs, which simplifies the process of building and consuming REST APIs.
  - What if we POST everything? /things/create, /create-thing, /things/id/delete? Or perhaps /delete-thing with the ID included in the body? At this point, it seems too arbitrary.

- ## Here's a wrapper around `fetch()` that validates the response body against a zod schema.
- https://twitter.com/gimenete/status/1688297547243077632
  - I use it when I need to use a 3rd party API and using their SDK would be overkill, or there's no SDK or the SDK is Node-only and I'm on Cloudflare workers.
  - [A wrapper around the fetch function that validates the response body against a Zod schema](https://gist.github.com/gimenete/dd1886288ee3d3baaeae573ca226048f)

- ## [浏览器允许的并发请求资源数是什么意思？ - 知乎](https://www.zhihu.com/question/20474326)
- 首先，是基于端口数量和线程切换开销的考虑，浏览器不可能无限量的并发请求，因此衍生出来了并发限制和HTTP/1.1的Keep alive。
  - 而随着技术的发展，负载均衡和各类NoSQL的大量应用，基本已经足以应对C10K的问题。 
  - 但却并不是每个网站都懂得利用domain hash也就是多域名来加速访问。
  - 因此，新的浏览器加大了并发数的限制，但却仍控制在8以内。

- 补充一小点就是浏览器即使放弃保护自己，将所有请求一起发给服务器，也很可能会引发服务器的并发阈值控制而被BAN，而另外一个控制在8以内的原因也是keep alive技术的存在使得浏览器复用现有连接和服务器通信比创建新连接的性能要更好一些。

- 浏览器的并发请求数目限制是针对同一域名的。
  - 同一时间针对同一域名下的请求有一定数量限制。
  - 超过限制数目的请求会被阻塞，这就是为什么会有zhimg.com, http://twimg.com 之类域名的原因。

- 半开连接指的是 TCP 连接的一种状态，当客户端向服务器端发出一个 TCP 连接请求，在客户端还没收到服务器端的回应并发回一个确认的数据包时，这个 TCP 连接就是一个半开连接。
  - 若服务器到超时以后仍无响应，那么这个 TCP 连接就等于白费了，所以操作系统会本能的保护自己，限制 TCP 半开连接的总个数，以免有限的内核态内存空间被维护 TCP 连接所需的内存所浪费。

- 由于 TCP 协议的限制，PC 端只有65536个端口可用以向外部发出连接，而操作系统对半开连接数也有限制以保护操作系统的 TCP\IP 协议栈资源不被迅速耗尽，因此浏览器不好发出太多的 TCP 连接，而是采取用完了之后再重复利用 TCP 连接或者干脆重新建立 TCP 连接的方法。
- 如果采用阻塞的套接字模型来建立连接，同时发出多个连接会导致浏览器不得不多开几个线程，而线程有时候算不得是轻量级资源，毕竟做一次上下文切换开销不小。
- 这是浏览器作为一个有良知的客户端在保护服务器。就像以太网的冲突检测机制，客户端在使用公共资源的时候必须要自行决定一个等待期。当超过2个客户端要使用公共资源时，强势的那个邪恶的客户端可能会导致弱势的客户端完全无法访问公共资源。从前迅雷被喷就是因为它不是一个有良知的客户端，它作为 HTTP 协议客户端没有考虑到服务器的压力，作为 BT 客户端没有考虑到自己回馈上传量的义务。

- ## 争议: We will very likely be removing the onSuccess / onError / onSettled callbacks from `useQuery` in v5. 
- https://twitter.com/TkDodo/status/1647347026135330816
  - I tried very hard to come up with a good use-case, but imo there is none.
- I use them to span toast of a success or error event, find them super useful
  - This would show the toast multiple times if you call the same hook in multiple components, so it's likely not what you want. The global callbacks on the QueryCache are better suited for toast notifications
- I put logging and trigger snackbars alerts in onError. Guess it can be in a useEffect, but doesn't seem as clean.
  - should probably both be in the global queryCache callback so that you a) only have to set it up once and b) it doesn't trigger multiple times.
  - in mobile apps there are lot of cases where we need to handle every error differently. having it setup once will not be suitable for this case.
  - depends on what handling it differently means. I've had a good experience with the global callbacks + the meta field

- ## [OData adoption rate? : dotnet](https://www.reddit.com/r/dotnet/comments/11eoa6d/odata_adoption_rate/)

- ## 换个角度想想，#GraphQL 好像是双赢。
- https://twitter.com/lovedebug/status/1646680811402584066
- 我觉得还挺好维护的，习惯了就好了。
  - 习惯了 REST ，觉得 GraphQL 约束太多，还要提前定义类型和数据结构。
  - 习惯了GraphQL，觉得 REST 太随意，不看文档连参数和返回值是什么都不知道。
  - 只要思维转变了，手上的活只是肌肉记忆而已。
- 其实 REST 的几个提案也解决了查参数和返回值的问题，比如 odata, HAL 等，可惜开源的后端实现不好找

- ## Which library should I use for fetching data in React?
- https://twitter.com/shashwatnauti/status/1622901075648061440
  - Tha lack of "automatic garbage collection" in SWR is an important issue for me.
- Depending on if you're planning to do some advanced cache management, mutations.
  - My rule of thumb: simply fetching - SWR. It's gotten better at mutations but not quite.
  - If your use-case is beyond "get the data, show it's status, display the data", you might want to look into RQ

- ## Fetch data from an api in useEffect or in event handler directly in react
- https://stackoverflow.com/questions/62277013/
- It depend on your usecase
- fetching data in useEffect is useful in following scenarios
  - Fetching data during some lifecycles like initial render
  - Fetching data when some prop changes
  - fetching data in an interval but setting up a subscription or setInterval
- Fetching data in handler is useful
  - Based on a user interaction such as search button click, search input change
- I would say you should go with the hooks implementation. 
  - It's recommended in the React docs for performing side effects
  - Data fetching, setting up a subscription, and manually changing the DOM in React components are all examples of side effects. 

- ## How to send request on click React Hooks way?
- https://stackoverflow.com/questions/55647287
- why would you prefer using useCallback instead of useEffect? 
  - Well, because it's a callback and not a side-effect
  - well, depends on how you treat it. if you use reactive/declarative way, it can be sideEffect. if you use imperative way, it can be a callback. both work. 
  - I wouldn't recommend using useEffect. To do that, it would become an effect triggered by a state-change, which would also cause an unnecessary re-render. Callbacks are inherently side-effects when they are triggered by a user-action
- You don't need an effect to send a request on button click, instead what you need is just a handler method which you can optimise using `useCallback` method
  - Tracking request using variable with `useEffect` is not a correct pattern because you may set state to call api using `useEffect` , but an additional render due to some other change will **cause the request to go in a loop**
- In functional programming, any async function should be considered as a side effect.
  - When dealing with side effects you need to separate the logic of starting the side effect and the logic of the result of that side effect (similar to redux saga).
  - Basically, the button responsibility is only triggering the side effect, and the side effect responsibility is to update the dom.
  - It's always better to separate the logic of your side effect from the logic that triggers the effect (the useEffect)

- ## React Hooks API call - does it have to be inside useEffect?
- https://stackoverflow.com/questions/61348598
  - I wanted to ask if every single API call we make has to be inside the useEffect hook?
  - my data fetching actually takes place in a function run on a button click and not in the useEffect itself. It seems to be working.
- Yes, apis calls that happen on an action like button click will not be part of `useEffect` call. It will be part of your event handler function.
  - When you call useEffect, you’re telling React to run your “effect” function after flushing changes to the DOM
  - Note: You should always write async logic inside useEffect if it is not invoked by an event handler function.
- Yes, you can make api requests in an event handler such as onClick.

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
