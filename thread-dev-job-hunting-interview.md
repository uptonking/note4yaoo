---
title: thread-dev-job-hunting-interview
tags: [interview, job-hunting, thread]
created: 2023-04-25T17:57:04.669Z
modified: 2024-01-07T15:00:50.079Z
---

# thread-dev-job-hunting-interview

# guide

# discuss-stars
- ## 

- ## 

- ## 今年的冬天确实冷。感觉很多互联网公司都只招架构师级别的了_202312
- https://twitter.com/YuTengjing/status/1739176978899755047
  - （怀疑也是为了骗方案或者营造招人的假象），都收紧裤腰带过日子，想去混个大头兵都感觉没啥面试机会
- 虽然只是参加了两场面试，但是感觉社招的时候业务匹配度和项目经历太重要了，反倒还没问什么八股。但是小厂出身+业务比较偏感觉项目就很难出彩啊，难顶。虽然我感觉进去也是🔧，但是他们确实是要求有造过🚀的经验。

- 📝 貌似我了解过的大厂的前端招聘有个业务都缺人：在线文档
- 为什么都要做自己的在线文档呢
  - 搞在线文档的一般都是先搞了自己的 IM，可能是不想泄露数据? 更方便和自己的  IM 打通?

- 最近在知乎经常看到类似 node 凉了的帖子，但是之前面 wxg 的时候好像视频直播带货那边 node 服务端用的挺多的。国内太多博客喜欢搞标题党了，deno 出来的时候说 node 💊，bun 出来的时候说 node 💊，tauri 出来的时候说 electron  💊，oxlint 正式发布的时候说 ESLint 💊
# discuss-boss/hr
- ## 

- ## 

- ## 
# discuss-algorithm
- ## 

- ## 

- ## If you want to become good at solving recursion problems, learn these 6 templates:
- https://twitter.com/Franc0Fernand0/status/1743912605909918083
- 1. Iteration
- 2. Subproblems
- 3. Selection 
- 4. Ordering
- 5. Divide & Conquer
- 6. Depth First Search

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 面经不写了，写个thread写点我遇到的不会的题目吧
- https://twitter.com/wulianwen1/status/1726793525956862125

- 同时发起1w个请求，http1.0/1.1/2.0分别需要建立多少个tcp连接（抖音电商二面）
  - http1.0 应该是1w个，因为连接会立即断开
  - http1.1 应该是浏览器支持的并发数量，因为是长连接
  - http2.0 应该是1个，多路复用支持在一个连接上并发多个请求

- React和Vue更新视图的区别？为什么React上粗粒度更新，Vue是细粒度更新？
  - 简单来说, React是比较渲染树新旧DOM的差异, 并且可能会重新渲染整个组件树，而Vue是精确的更新受影响的部份。

- chatgpt等平台为什么使用SSE的方式进行流式打字？
  - [ChatGPT对话为什么不用Websocket而使用EventSource？ - 掘金](https://juejin.cn/post/7246955055109210149)
  - 在ChatGPT官网我们可以看到，对话的方式仅仅只有一个post请求，而没有使用IM中使用的websocket链接。
  - 与普通的post请求不一样的是，返回信息Response没有了，取而代之的是EventStream。
  - EventSource 接口是 web 内容与服务器发送事件 一个 EventSource 实例会对HTTP服务器开启一个持久化的连接，以 text/event-stream 格式发送事件
  - EventSource只支持从服务器到客户端的单向通信，客户端无法向服务器发送数据。

- react为什么要推出fiber架构?  
  - react15只能同步地更新 相当于while(true) 很卡 
  - fiber是一种协程的实现，可以中断让出js线程

- ## 站酷上看到的UI作品集，大部分都只能用“人云亦云”来形容，
- https://twitter.com/cosmoslee007/status/1650542502943031296
  - 这么多年了，明知道设计前期根本没有“用户画像”、“体验地图”这回事，有的就是PM对老板需求的传话，但大家还是一如既往的堆砌这种没有意义、互相欺骗的页面。行业内好像也都对此心照不宣…
- 最近在面试也有同样的感受，大多数时候面试者也说不出从这些方法论里面得到了什么设计决策，而是再给我介绍这些理论，十分不耐烦。