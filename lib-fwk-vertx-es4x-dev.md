---
title: lib-fwk-vertx-es4x-dev
tags: [docs, es4x, java, vertx]
created: '2020-01-10T12:55:33.206Z'
modified: '2020-12-08T13:28:50.105Z'
---

# lib-fwk-vertx-es4x-dev

# guide

# discuss

- ## [Vert.x 与 Node.js 有哪些区别？](https://www.zhihu.com/question/22021343/answers/updated)
- vert.x实在是太好用了，根本不需要rxjava，promise这些，自带扁平化callback hell的工具

- ## [Vert.x未来会取代tomcat和现在流行的spring全家桶吗？](https://www.zhihu.com/question/302482388/answers/updated)
- vert.x说简单点就是一个evenloop模型的实现，用来取代传统的同步多线程编程模式。
  - 拿它作为基础库，实现事件驱动，提高应用的并发能力还是很好用的
- Spring是传统Servlet WEB framework的杰出代表，事件驱动方面也有 spring flux
  - 在纯异步编程这块，我个人还是倾向于使用vert.x 简单小巧。

- ## [vert.x相比spring全家桶系列, 除了性能外, 还有什么优势?](https://www.zhihu.com/question/277219881/answers/updated)
- 这两个名词不太适合直接比较，Spring Boot 显然是很成熟的业务框架。
  - Vert.x可以当成一个封装了 IO 设施与常用协议(File/HTTP/TCP/UDP/Buffer)的 lib
  - 工程上面想做到类似 Spring Boot 的程度，需要组装一些脚手架设施，推荐Quarkus
- Vert.x相对于Spring系的优势，整体还是不小的。
  - 性能、低内存占用、冷启动速度(如果连接的中间件不多或者启动时候没有很重的初始化任务，可以轻松压到 2s 以内，
  - 在容器平台里 rolling upgrade/scale up 时候简直不要太开心

- ## [国内有用 Vert.x 作为开发框架的公司么？](https://www.zhihu.com/question/33038931/answers/updated)
- 总体感觉很棒，异步模型性能杠杠的，直接支持分布式开发
  - 缺点就是异步回调hell

# Vert.x

- vert.x vs spring+tomcat
  - Vert.x是面向IO的，而Spring是面向Web的。或许Vert.x Web无法撼动Spring的地位，但是其他领域呢？比如mqtt和其他非http领域，Vert.x仍然是JVM最具竞争力的IO框架
  - Spring可以跟Vert.x结合使用，比如可以在一个Spring3的旧项目中，引入Vert.x集群，用Vert.x的集群下EventBus替换其他RPC解决方案。
    - 使得在不同Tomcat实例下的Web项目可以互相通信。
    - 同样在这个项目里，面向浏览器的Websocket消息推送，用Vert.x来做非常方便
  - spring的生态基础摆在那里，最主要的spring也在不断进步，也支持异步功能

- vert.x简介
  - vert.x说简单点就是一个evenloop模型的实现，用来取代传统的同步多线程编程模式。拿它作为基础库，实现事件驱动，提高应用的并发能力还是很好用的
  - Spring是传统Servlet WEB framework的代表，事件驱动方面也有 spring flux
  - vert.x-web有潜力取代spring-mvc和spring-webflux，可以用springboot+vert.x-web来构建应用，毕竟vert.x并没有自带一套依赖注入系统，并且对于ide的支持和加载配置方面也不如spring那么人性化
  - servlet的容器也有基于nio的undertow
  - 现在很多框架开发都会选择netty作为web server。例如vertx。就算是自己实现。也是基于nio去实现的。很少再去拿着servlet那些套进去。毕竟nio相对于传统的io是很省资源的。
  - spring也在进化过程中，比如webflux也是基于netty。
  - 因为java本身的问题，所以现在用vertx写稍微麻烦点的东西代码还是非常不美观的。java本身还在开发一个loom的项目，发布后可能会改善
  - tomcat也只是请求连接用的nio，但是他的worker还是用的线程池的吧？这样整体来说也并没有达到nio是吧？是的，最主要的是你的db啊之类的还是同步的，是nio但是也是阻塞的，并不像vertx之类的从头到尾都是异步
  - 为什么vert.x没有提供傻瓜化的框架呢？
    - 因为数据库会先于应用服务器触发吞吐瓶颈，一个传统系统，比如是tomcat和mysql的组合，当并发量上去之后，mysql会先于tomcat之前顶不住
    - 所以第一步一般是引入nosql以增加吞吐，比如cassandra，同时会弱化mysql等的rdbms的属性，以提速增加吞吐，比如用pg替换掉mysql，用jsonb类型替换掉传统的table表
    - 然后才是把tomcat等换成vert.x，等到你用vert.x的时候，vert.x面对的是一个json等的数据结构，以及nosql的数据库
    - 所以vert.x优先解决跟nosql以及json等半结构或者无结构数据格式的交互问题，提供能够跟json，文件系统的api，而不是去适应传统的rdbms，那个是落后产能
    - 如果你还在用rdbms，意味着数据持久化本身成为瓶颈，用不用vert.x都改变不了这个瓶颈的存在，比如tomcat吞吐是2000，但是rdbms是1000，你换成vert.x，把appserver的吞吐提高到40*2000=80000，但是rdbms怎样都只能吞吐1000，你的系统最终的吞吐也还是只有1000，vert.x跑得再快又怎样？
    - 所以用vert.x是跟整个系统发展趋势相符的，光换vert.x可能并不能整体提升系统性能，还需要其他部分整体配合才行

- 使用vert.x的知名公司或项目(大多不活跃)
  - https://github.com/Knotx/knotx
- 背景
  - java在1.4有了nio，netty真正需要用到的api就是nio，所以在2002年，java就已经具备有了用callback大幅优化io的基础工具
  - java在1.7有了nio 2，future来包装callback，更为重要的是1.8之后的lambda，没有lambda之前，你要想写一个callback，你需要匿名内部类
  - 以前之所以没有出现高并发的方案，一方面需求也没有达到，java主要还是应用于银行等传统企业领域，但互联网领域的技术多数时候觉得java尤其是j2ee有些heavy
  - 互联网领域更多的技术革新出现在其他语言的领域，当然java自身也在吸收这些东西，并逐步改善。
    - callback在java还没有lambda之前，js里面实现lambda就比java简单点，function声明下就好，所以有了node.js，然后eventloop模式开始在server side推广，所以有了vert.x，vert.x形成之初，初衷就是想做一个jvm上的node.js，所以原名叫做node.x
    - scala那边也有akka等类似erlang的actor model的实现，他们能够将其吸收进来，所以vert.x的实现一开始也借鉴了akka，actor在vert.x里面就是handler，不是verticle，然后结合eventloop和handler/actor发展出了自己的一套verticle based并发体系
    - vert.x很早就提出了要兼容bio的api，所以提出了worker verticle/thread pool，这个以后慢慢发展，可以应用fiber，也就是goroutine
    - vert.x还提出了polyglot的概念，就能使用其他语言的特性
    - nosql解决了rdbms的吞吐太小的问题，现在分布式技术的nosql正在替换rdbms，对于db的改造没有完成之前，netty，vert.x这种技术还谈不上大规模的推广，不过现在pg，mysql也都有了自己的异步api，尤其是pg，上升势头跟mongo不相上下

# Vert.x docs

- Vert.x is a toolkit for building reactive applications on the JVM
- https://vertx.io/docs/
- https://github.com/vert-x3/wiki/wiki
- Module-Core
  - https://vertx.io/docs/vertx-core/java/
  - Vert.x core contains fairly low level functionality including support for HTTP, TCP, file system access, and various other features. 
  - Vert.x core provides functionality for things like:
    - Writing TCP clients and servers
    - Writing HTTP clients and servers including support for WebSockets
    - The Event bus
    - Datagram Sockets
    - File system access
    - DNS client
    - ...
- Module-Web
  - https://vertx.io/docs/vertx-web/java/
  - Vert.x-Web is a tool-kit for writing sophisticated modern web applications and HTTP microservices.
  - It takes inspiration from projects such as Express in the Node.j.
  - Some of the key features of Vert.x-Web include:
    - Routing (based on method, path, etc) and Sub routers
    - Regular expression pattern matching for paths
    - Extraction of parameters from paths
    - Request body handling
    - Cookie parsing and handling
    - Multipart forms and Multipart file uploads
    - Session support - both local (for sticky sessions) and clustered (for non sticky)   
    - CORS (Cross Origin Resource Sharing) support
    - Basic Authentication
    - Redirect/JWT based authentication
    - User/role/permission authorisation
    - Template support for server-side-render,including freeMarker...
    - Response time handler
    - Static file serving, including caching and directory listing.
    - ...
- Module-Web Client
  - Vert.x Web Client is an easy to use advanced HTTP client.
- Module-Data access: Reactive PostgreSQL/MySQL client + MongoDB/Redis/...
  - Vert.x provides a few different asynchronous clients for accessing various data stores from your application.
  - you could also use clients direct from the vendor if you prefer 

# ES4X 

# ES4X docs

- A Modern JavaScript runtime for Vert.x
- https://reactiverse.io/es4x/
- https://github.com/reactiverse/es4x
- features
  - Minimal setup with npm-centered project structure  
  - Use Vert.x components in js, and develop with js or TypeScript
  - ES4X runs on top of GraalVM offering a great performance for JavaScript applications on par or better than Java.
  - ES4X requires GraalVM or Java >= 8.
- ES4X is small runtime for EcmaScript >=5 applications that runs on graaljs with the help of vert.x. 
  - JavaScript is the runtime language but it does not use nodejs
- ES4X makes use of GraalVM which is a polyglot runtime on the JVM. 
  - This means it is possible to use any JVM language as well as JavaScript in applications
- Vert.x is used by ES4X in order to provide an optimized event loop and high performance IO library
- ES4X is the fastest on all tests when compared to JavaScript frameworks
