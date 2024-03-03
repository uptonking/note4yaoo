---
title: thread-dev-http-ajax-cookie-session
tags: [ajax, cookie, http, jwt, session]
created: 2021-08-06T08:30:13.653Z
modified: 2021-08-06T08:32:26.142Z
---

# thread-dev-http-ajax-cookie-session

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔 This will forever bother me: await (await fetch(url)).json()
- https://twitter.com/wesleytodd/status/1757555080897646595
  - Nearly zero of my use cases are best with fetch so I hardly ever use it, so I hope someone tells me "there is a better way".

- I prefer something like this: `await fetch(url).then(r => r.json())`

- I prefer `await fetch.then(res => res.json())` but some people view this as VERY CONTROVERSIAL

- Just make `getJSON = res => res.json()` helper.

- because of this, I prefer axios but I hate additional dependencies

- There is a better way. One where you handle errors

- ## 📶 How Programs Communicate Over the Network: Sockets
- https://twitter.com/iximiuz/status/1718230339976389015
  - Browsers opening web pages
  - Services talking to services
  - Your code querying the DB
  - Kubernetes launching its Pods
  - Most of the program communications today happen over the network, and sockets are at the heart of it.
- To understand what sockets represent, let's start with the basics.
- Sockets help abstract this complexity and make interaction over the network look similar to reading and writing data to any other file descriptor.

- 🌰 A beginner-friendly socket programming example
  - Create a server TCP socket
  - Bind it to a network interface
  - Wait for client connections
  - Accept client connection
  - Create client TCP socket
  - Send and receive data
  - Close sockets

- These particular illustrations were done in http://sketch.io. However today I switched to @excalidraw because it allows me to sketch faster. At the price of authenticity, I guess
# discuss
- ## 

- ## 

- ## 

- ## How Data Travels Through the Layers of the Internet
- https://twitter.com/sahnlam/status/1764175138877231570
  - The TCP/IP model provides a more practical framework compared to the theoretical OSI model. 
  - This model more closely matches real-world internet communication by condensing the seven OSI layers into these four fundamental ones.

- The 𝗧𝗖𝗣/𝗜𝗣 𝗠𝗼𝗱𝗲𝗹 contains four key layers:
  - Application - supports end-user processes like HTTP, SMTP
  - Transport - handles host-to-host communication (TCP, UDP)
  - Network - addresses and routes packets (IP protocol)
  - Link - moves the bits over the network's physical wires, cables or wireless channels

- ## RTC 领域，每秒钟需要全球调度上 T 的数据，最好的用户体验，不是全自建或全上云，而是混合云方案（自建+云），理由：
- https://twitter.com/skywind3000/status/1718801244360216701
  - 1）云服务商的 IDC 并不能很好覆盖你的核心用户群，那么你需要多家并存，或者考虑核自建才能提供更好覆盖；
  - 2）风控，出问题随时切换，不会被某家绑架；
  - 3）对他们提要求时更具主动性；

- ## 找业界大佬杨升浩请教 FEC  (Forward Error Correction)  和 WebRTC 相关的问题
- https://twitter.com/_a_wing/status/1718724383483781579
  - 刚刚突然灵光乍现：我们可以把 FEC 用在代理协议上啊。比如我们在 ss 协议里面套一层 FEC 来对抗 GFW 的随机丢包。效果应该会很棒
  - 不过有个问题，要用 UDP 加 FEC 才有意义。墙内的 UDP 环境有点差
- 其实已经widely used了。物理层，FEC面对的更多是错包而非丢包，而无论是UDP还是TCP，遇到最多的都是丢包，因为错包问题早就在之前的各个层面上被吃掉了
  - FEC 也可以处理丢包吧。虽然底层解决了一次，但随着网络节点的增加，中间的路由越来越多。在 UDP 上再来一次 FEC 应该也是有意义的。
- 没什么意义，最后纠错还是靠一层又一层的冗余，那我一开始就扩频不就好了
- 在 ss 外面套一层 kcptun 就行了，前者提供服务，后者提供 tcp 转 kcp+fec 的通道，不用改一行代码
- FEC是对抗弱网环境丢包的常规手段，如果只是对抗GFW，给ss套一层韦老板的kcp目前基本是够了，倒没必要上FEC，kcp的分层设计也方便自己再加一层FEC

- ## 🆚️⚖️ 为什么很少见用 MessagePack 代替 JSON 的 Web 服务，不是更省流量吗？
- https://www.v2ex.com/t/932879

1. MessagePack 和 Json 都是自释的，都带有了 key 信息，都是相当于动态结构
2. MessagePack 二进制、省去了 Json 的那些双引号、冒号、逗号、括号之类的，能省一些但毕竟 key 信息还在
3. PB 这种是 c/s 各自都持有了消息体的定义，根据消息定义的字段顺序进行序列化、反序列化时根据消息定义的字段顺序从 buffer 里挨个取出来解析就可以了，不需要把 key 信息也放到序列化后的数据里，而且本身也不需要引号冒号那些，所以节省更多。一些数值类型会做一些压缩，比如 int64 需要 8 字节但当前的值比较小、2 字节就够了，那就省一点。MessagePack 是否也有这个数值压缩我不记得了，好像是也有的
4. 不管用哪种，如果消息结构定义的重复率比较高、序列化后的包体 size 比较大，通常 gzip 之类的压缩算法加一道，就省更多了
- 用 Json 更灵活、自由、方便，版本更新升级做兼容性也容易
- 用 PB 更严格、工程化、规范，版本升级要考虑协议兼容性的更多、要考虑 c/s 是否必须同步停服维护升级之类的
- MessagePack 挺不错，但是不如 Json 那种明文、方便调试之类的，它相比于竞品，优点都是处于中间水平，省流优秀但不是最佳、自释义但不明文，而且出生也晚，所以反倒是用的人最少

- 说到底，还是前端不善于处理二进制流数据。
  - js有能完美处理二进制 api ，但是前端真正会的人群，估计不到 10%。

- HTTP本来就是基于文本的，用 HTTP 的情况下就不考虑这点性能了

- 互联网的主流协议，大多都是底层需要效率和精确控制的用 binary ，上层易于理解和观察的用 text ，有特殊场景需要违背时才做反例。
- 并没有省太多吧，key 还在数据里。要省流的话 protobuf 不是更好。
- 单纯为了省流的话 protobuf 多好，但是现实是原来好多 protobuf 协议的接口现在都换成 json 了
- gzip 一下差不了多少，甚至有可能 json 更小。 而且在浏览器里用 messagepack 还要额外消耗 messagepack 解析库的流量

- 如果你同时支持两种格式，那只能让功能向 json 对齐，msgpack 的额外功能就用不到，结果无非就是省些流量。如果再 gzip 一下，那两者连流量的差距都很小了，这只要在 nginx 配一下就行，对应用来说都是透明的。
  - 如果说性能，正是因为 json 流行，现在各个语言都有一堆高度优化甚至 simd 加速的库，其他格式没这个待遇的。有特殊需求的，这里还有一堆二进制格式可选呢

- ## RateLimit是吧，做了API限流是吧，是在网关层做的吧？
- https://twitter.com/Beijing_Hot/status/1623508364109180928
- rpc 层也能做。。。 限流和熔断一般都是成对出现。。。 比如底层rpc 接口，有些耗性能的接口，在出现高频访问的时候，上游服务发现有报错， 就会熔断（降级）， 等会再去访问
- rpc 做的话，侵入式的吧？
  - 要是想省事， 都不用网关，直接nginx 上跑

- ## After 3 years, I still love that data fetching hooks maximize the concurrency automatically. Which has been something tricky with awaits/Promises.
- https://twitter.com/shuding_/status/1529264553900531712
  - Data dependency is a directed acyclic graph. We used to describe that graph using `Promise.all` s, but in many cases it's still not optimized enough.
  - With Dependent Fetching, we can walk through it as parallelized as possible (no extra code needed).

- ## Thunks are great for "run some code now and dispatch eventually" logic, but they can't _listen_ for other actions.
- https://twitter.com/acemarke/status/1440494692836069392
  - Sagas and observables are widely used for that, but they're heavyweight syntactically and conceptually.
- Would love to have folks try out the "action listener callback middleware" we've got as an upcoming RTK API
  - It lets you add listeners ahead of time (statically), but also dynamically add listeners at runtime. Listeners can call `dispatch` and `getState` , unsubscribe, etc.

```JS
let mw = createActionListenerMiddleware()

mw.addListener(todoAdded, (action, listenerApi) => {
      console.log(`Text was: ${action.payload}, new num todos: ${listenerApi.getState().todos.length})
})
```

- ## JWT shouldn't be the default way of storing session data - because it doesn't allow logging out a user. 
- https://twitter.com/francoisz/status/1394258658641514514
  - Good old session cookies do the job fine, but yes, you'll have to keep track of sessions in a shared server-side storage. 
- You can store server side JWT and have logout
- But if you are going to have a shared server-side storage it's trivial to invalidate a JWT token on logout. And then your non-HTTP services don't need to understand cookies.
