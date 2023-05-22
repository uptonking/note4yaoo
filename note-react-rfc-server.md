---
title: note-react-rfc-server
tags: [react, rfc]
created: 2020-12-22T14:08:04.179Z
modified: 2020-12-22T14:08:27.952Z
---

# note-react-rfc-server

# react server components

# guide
- RSC优点
  - 将数据请求频繁的组件和计算仅放在服务端执行，减轻客户端压力
  - 将部分代码放在服务端，可作为一种代码分割方式，可减小传输量加快显示
  - 定制的格式能使refetch时客户端状态不丢失，流式传输能边下载边渲染

- RSC缺点
  - 致命：若组件使用RSC的形式，会与具体后台服务耦合，可复用性变得极低
    - 参考graphql难以推广的原因，因为需要服务端的配合，甚至重写服务端
  - rsc组件请求数据的逻辑部分不能通用到移动端和其他设备，它们仍需实现单独的api
    - 虽然工作量未减少，但能加快react前后端一体化应用的开发
  - 会消耗服务端资源，请求过多时要考虑服务端计算优化
  - 传输的是自定义格式，不是html
  - 其他限制
    - rsc不能使用state和effect

- RSC usecase
  - Suspense组件的另一种形式

- tips
  - 分析具体项目组件的输入输出，估算引入rsc的成本
  - 我认为是玩具，但可推动指定云端组件的标准

- rsc vs ssr/nextjs
  - rsc设计目标是兼容多个框架
  - nextjs的ssr，所有组件的js bundle会发送到客户端
    - rsc只发送你需要的bundle，能加快显示
  - 传统ssr可以提前渲染出html，能加快显示，但若要支持交互，仍要下载所有js构建
    - rsc只发送所需的bundle
  - rsc发送的不是html，定制的格式能使refetch时客户端状态不丢失
  - ssr渲染到html是同步的，渲染时不能取数
    - rsc支持异步取数，渲染时也能取数，流式传输能边下载边渲染
# blogs
- [Understanding React Server Components_202305](https://www.callstack.com/blog/understanding-react-server-components)
# discuss-stars
- ## React should have a `useUniqueId()` hook that is SSR-stable built-in, 
- https://twitter.com/buildsghost/status/1397347873637818370
  - [Add useOpaqueIdentifier Hook](https://github.com/facebook/react/pull/17322)
  - there is not a single React app that doesn't need it once you start implementing accessibility features
# discuss
- ## I want to recap a few points from our talk about the different kinds of components.
- https://twitter.com/dan_abramov/status/1342260256638951425
- Server Components are the new proposed kind of components. 
  - They execute on the server, and on the server only. 
  - They have the `.server.js` extension. 
  - They can access the backend resources directly (e.g. database, filesystem, internal API services). 
  - They cannot use state or effects.
- Client Components are the regular components you’re already familiar with. 
  - They primarily execute on the client (but also during first render to HTML). 
  - They have the `.client.js` extension. 
  - They may use state or effects, but cannot access the backend resources (e.g. databases etc).
- We’ve found that many components only contain some logic to transform data, and don’t actually use either state/effects or backend resources. 
  - This means they could run anywhere — server or client. 
  - We’re calling them Shared Components, 
  - and they stay as regular `.js` files.
  - You can think of a Shared Component as being in a different role depending on what imports it. 
    - If it’s imported from a Server Component, it acts as a Server Component itself. 
    - If it’s imported from a Client Component, then that’s the role that it takes. 
    - You can use it either way.
- There are no limitations on the props of Server Components or props of Client Components per se(本身, itself). 
  - In both cases we’re dealing with regular React top-down data flow, and we can pass anything. 
  - But props passed *from Server to Client* must be serializable. They cross the network.
- There are also no limitations on what can be nested inside of what. 
  - Both types can be interleaved as much as you want. 
  - The limitation is only on *imports*:
  1. Server can import either Server or Client components.
  2. Client can only import other Client components.
  - Server importing Server, and Client importing Client are regular imports that work as you’d expect. Nothing special about them.
  - Server importing Client is the special one. 
    - Under the hood, the bundling integration turns that import into an instruction to load that Client module.
  - Although Client Components can’t import Server ones, they can still be composed together from a *parent* Server one. Because Server can import both types.
- You can read it in detail in the RFC. 
  - All of this will make it into the docs when the feature is stable
- let me also briefly summarize the difference between Server Components and traditional SSR (“server rendering” — might have to refer to it differently in the future to help prevent this confusion).
  - In React, traditional SSR only produces an initial HTML snapshot of the page. 
    - If you use it, it only runs once before the page loads, and then you still have to download all the JS code before your app can respond to interactions.
  - Server Components, by contrast, use a richer format than HTML which can (and should — for the first render!) be translated to HTML, 
    - but can *also* be refetched. 
    - This format lets us avoid destroying client state on refetch, as would happen if you replace HTML in a running app.
  - Also, with traditional React SSR, the rendering to HTML is synchronous. 
    - This means your components cannot load data on the server. 
    - There are various workarounds (such as a “prepass” that tries to render components once before the SSR) but they’re not ideal or idiomatic
  - By contrast, Server Components have built-in support for asynchronous data fetching.
    - This means that you can fetch data inside of them, on the server, and not just at the top level of the tree, but at any depth. 
    - And thanks to streaming, you don’t have to wait for the whole tree.
  - Now, I’m comparing them but really they’re complementary. 
    - Server Components are the mechanism that lets you do data fetching and run some logic without shipping it to the client at all. 
    - Rendering to HTML is still a useful optimization on top for the first render before JS loads!
- discussion
  - It's hot module replacement, but in production.
    - And it's not a dev triggering the reload but a machine, the server.

- ## New video: React Server Components(with Next.js Demo)
- https://twitter.com/leeerob/status/1344741266135912458
  - https://github.com/vercel/next-server-components
  - How is this different from PHP/Rails?
  - How is this different from SSR?
  - Why Hybrid Applications?
  - React Suspense and Concurrent Mode

- ## [如何看待 React Server Components？](https://www.zhihu.com/question/435921124/answers/updated)

- 业务开发中需要权衡三个点：体验（user experience）、可维护性（maintenance）、性能（performance）
  - 这是一个很常见的组件化组合的场景，问题在于每个组件都需要不同的数据，
    - 但是就体验而言我们更希望这些组件的渲染尽量同时，而且如果关注性能的话，我们也会考虑并行的去fetch数据，
    - 于是我们通常会fetch逻辑放到顶层，然后通过 Props 或者 Context 传递下去。
    - 这样会把可维护性变差，每个组件从逻辑上就不那么解耦了，我们于是会考虑每个组件自己处理 fetch 逻辑。
    - 这又会让体验变差，因为浏览器从服务端 fetch 数据是比较贵的 IO
    - 我们之所以需要从服务端 fetch 数据，是因为我们把所有渲染操作放到了客户端，那如果我们把部分渲染逻辑放服务端呢
    - 于是就有了 React Server Components
  - 不是ssr
    - 框架启动了后端服务，通过 /react 异步地输出页面内容，
    - 只是这个页面内容不是HTML，是一个自定义的结构。
    - 之所以不是直接输出HTML猜测是因为需要做些高级的事，比如维持组件状态。
- 最常和Server Components对比的就是传统的PHP/ASP技术和为框架而生的SSR技术
  - 听起来和 SSR 很像，而代码看起来则和 PHP 很像，很多人认为这是一种倒退
  - 用一种“和现有技术类似的”方式来解决某个痛点的做法，正是一种先进而优雅的方式
    - jsx 和 html 很相似，vue template 和 mustache 很相似
- 在PHP/ASP时代，页面都是由服务器来渲染。
  - 服务器接到请求后，查询数据库然后把数据“塞”到页面里面，最后把生成好的 html 发送给客户端。
  - 当用户点击链接后，继续重复上面的步骤。
  - 这样用户体验不好，每个操作几乎都要刷新页面，服务器处理完之后再返回新的页面
- 我们可以概括为：
  - 痛点：用户体验太差（user experience）
  - 原因：页面总是刷新
  - 解决：让页面别刷新
  - 方案：使用 ajax
- Angular/Vue/React这种单页应用(SPA)则主要是客户端渲染。
  - 服务器接到请求后，把 index.html 以及 js/css/img 等发送给浏览器，浏览器负责渲染整个页面。
  - 后续用户操作和前面的 php/jquery 一样，通过 ajax 和后端交互。
  - 但和php相比，第一次访问时只返回了什么内容都没有的index.html空页面，没法做SEO
  - 另一点是页面需要等到js/css和接口都返回之后才能显示出来，首次访问会有白屏。
- 概括
  - 痛点：首次访问白屏
  - 原因：首次访问只返回了 index.html 页面
  - 解决：首次访问时返回渲染完的页面
  - 方案：SSR
- SSR的方式是
  - 首次访问的时候由服务器（通常是Node.js）来渲染页面，
  - 然后把已经渲染好的html发送给浏览器。
  - 后续的用户操作依然通过ajax获取数据，
  - 然后在浏览器端渲染组件和页面。
- 能不能让首屏的体验更好呢？
  - 痛点：SSR首屏还是太慢
  - 原因：服务端渲染是请求的接口太多，导致响应时间太长
  - 解决：分块渲染，把已经渲染好的部分尽早的发送到浏览器
  - 方案：bigPipe
- 根据这种思路重新审视一下 React Server Components 解决了什么问题。
- 例子很简单，页面中的三个组件应该如何请求数据？
  - 顶层组件通过1个接口fetch所有数据，这样请求的时候会变长。
    - 用户体验v 可维护性x 性能x 
  - 顶层组件通过3个接口并行fetch所有数据
    - 用户体验v 可维护性x 性能v 
  - 每个组件自行fetch数据
    - 用户体验x 可维护性v 性能v
- 面对种种痛点，我们也都有自己的方案。
  - 解决思路是让接口响应变快。可通过增加服务器配置来解决，或优化后端代码来解决。
  - 使用graphql按需查询后端数据。
- React团队分析了导致痛点的原因：**组件需要反复从服务器请求数据**
- React团队给出的解决方案是：
  - 把组件放到服务器端，这样客户端和服务器端只需要往返一次。
  - 和graphql的思路很像，但是更加贴近react生态，也更加 frontend style。
- graphql落地的最大障碍就是 “明明是解决的前端痛点，却非要改造后端”。
  - 而把 graphql 做 BFF 来用坑也不少。
- React Server Components则完全是按React的思维来解决这个问题。
  - 甚至可以说是按前端组件化的思维来解决这个问题，这种思想Vue也可以实现。
  - 前端发起请求，服务器端组件可以查询 db，可以访问接口 api
  - 而且和 SSR 不同，服务器响应的不是 html，而是一个序列化的“指令”。
  - 客户端根据此“指令”集来渲染组件和页面。
- 服务器直接返回 html 片段的技术也有了，叫 pjax/turbolinks。
  - 我去年和一个团队交流，说他们在做基于 React 组件的 pjax，后来放弃了
- Server Components的这种思路还有很大的挖掘空间。
  - 比如可以开发 WebSocket Components，通过WebSocket向浏览器主动的实时推送“指令”。
  - 再比如可以开发 Native Components，在 App 内嵌的 H5 页面中向原生代码发请求，原生代码完成业务处理后返回给 H5 序列化的“指令”。
  - 这种序列化的指令还可以被存储，可以被回放，可以被 mock，调试起来应该可以像 redux 一样具有时间旅行功能。
- 跟SSR完全不是一个东西，大概说一下整体流程：
  - Server先启动一个express服务，同时执行webpack编译，把src目录的组件编译成静态资源，
    - 但是稍有不同的是，因为会用到react-server-dom-webpack这个库，所以只会编译属于Client的组件
  - 打开Client（浏览器），输入Server提供的"Server组件"地址，回车
  - Server接收到请求，去拿对应的Server组件，并将该Server组件和所有Client组件，使用react-server-dom-webpack这个库组合在一起序列化一个特殊的格式，并返回给Client
  - Client拿到返回的Response，也是用react-server-dom-webpack这个库，去解析这个特殊的格式，
    - 如果遇到J那就反序列化JSON得到一个真正的组件，如果遇到M那就在运行时执行__webpack_require__来引用静态资源
    - J是Server组件实体，就是在Server执行React.createElement(Server组件)的JSON序列化结果
    - M是Client组件引用路径，仅仅是引用信息
    - J的反序列化直接在内存里执行，没有任何网络请求；
    - M的引用就相当于“webpack动态import”，因此体现为Network里的一个请求；
  - 得到一个完整的组件，包含反序列化的Server组件和动态import进来的Server组件，在Client进行渲染
    - 因为涉及到JSON序列化，Server组件必须足够简单，才能在序列化反序列化的过程中不丢失信息
- 跟SSR的区别是什么？
  - SSR是在Server进行渲染，然后把渲染得到的HTML返回给Client；
    - 而这个Server Component，所有组件，不管Server组件还是Client组件，都是在Client进行渲染。
    - 只不过Server组件会自带一些在Server端获取的数据放在props里，这样就不用在Client再进行请求了。
  - SSR因为每个请求都是一个新的HTML，就相当于两个应用，你的应用都变了，那你原来应用里的状态肯定都丢了；
    - 但是Server Component不管你向Server请求多少次，都是同一个HTML，同一个应用，你的状态不会丢。
- 使用Server Component是完全没法SEO的，因为Server返回的不是HTML。其实官方也提过，我们可以结合起来用：
  - 我们的首页请求Server的/路径，这个路径对应的是SSR渲染
  - Client拿到SSR返回HTML后，后续的组件，请求Server的/component路径，这个路径对应的是Server Component
- 如何评价这个东西？
  - 它必须要有Server支持，幻想着让一个纯CSR应用去接入一个Server组件是不现实的（云组件没那么容易）。
  - 它应该是渐进式的，可以在一个纯CSR应用之上，很快的叠加上Server组件的功能。
  - React越来越像Framework了。
- 跟SSR的区别
  - SSR 输出的是 HTML，Server Components 输出的是 chunks。
  - Server Components 跟过去的SSR相比，你在拉取后不会丢失客户端的状态；
- Server Components 的思路很有意思，把前端往业务层又推进了一步。
  - 如果整个后端做数据仓储提供中台支持的话，那么前端开发者是否可尝试独立支撑业务开发？
  - 我觉得相比 GraphQL 提供了更为统一的解决方案 —— **组件即服务**。
- 快速捋一下这项服务端渲染partial页面更新技术的发展脉络
  - innerHTML
    - DOM 提供了渲染后更新的能力。甚至可以直接替换一部分 html。
    - 这是一切 partial update 的起点。在小程序上做就非常困难。
  - ajax + innerHTML
    - 客户端就只需写非常少量的 html 替换代码，而复用绝大多数的服务端渲染逻辑。
    - 这个做法非常流行于 ruby on rails 这样的服务端渲染的社区。
  - 缺点
    - 需要先用 id 等方式定位到要刷新的区块，然后再去请求刷新。
    - 用户体验不佳：在服务端返回，html 被替换之前是没法看到进展的。如果网络慢了，用户就可能会焦虑。如果立即出 loading，用户也焦虑。
    - 纯客户端的交互没法搞：这种替换 html 的做法适合表单提交这样的场景。但是客户端搞个 tree 组件，accordian 组件就没法这么弄了。
  - 引用“组件”的 html
    - 既然可以动态替换 html，例如 `<div>hello</div>`。那么为什么不能把 `<div>` 换成 `<UserNote>` 这样的自定义组件呢?
    - 这种做法就是 wordpress 等 rich text editor 的做法。可以服务端渲染，也可以是用户编辑的内容。然后到客户端再做二次渲染。
  - 把 html 增强为组件
    - 这个是 HTML Over The Wire 中 stimulus 做的事情。
    - 把客户端已有的 html，通过 css selector 就地重建 dom 元素和 js object 的映射关系。
    - 和 react 先有 js object，再渲染 dom 元素正好反过来。
    - 解决的就是服务端渲染出来的html是死的，缺乏客户端交互能力的问题。
  - React Server Components的解决方案
    - 不需要你手工用id找到DOM元素，然后去刷新。比turbo frame的做法高明
    - 用户体验不佳：
      - 用 comet long polling 技术，让服务端分次推送给客户端内容。
      - 服务端推一点，客户端就立马渲染一点。
      - 和浏览器渲染html一样，这样就缓解了用户焦虑。
      - 还可以让服务端推个 `<suspense>` 过来，让客户端出 loading indicator
    - 纯客户端的交互没法搞
      - 服务端推过来的更新不仅仅引用 `<div>` 这样的原生组件，也可以引用 `<UserNote>` 这样的 react 客户端组件
- 在这条主发展路径上，也绕过两个弯路。特点就是都想要“保持”state。
  - rehydration
    - 就是传统的 SSR 指代的 rehydration
    - Dan 明确指出了这次的 React Server Component 的特点是 Server Component 仅仅运行在服务端。
    - 而 SSR 的“同一个”组件，既要考虑自己运行客户端，又要运行在服务端。这就给组件造成了很大的复杂度。
    - 只有当“同一个”组件需要同时运行时在服务端，又要在客户端复活，才会有复杂的 state rehydration 问题。
    - 如果只是在服务端运行，state 用完了就扔了。
    - 而服务端即便在服务端渲染出了客户端组件，也只是给了客户端组件的 props，这个时候客户端组件仍然未开始执行，自然没有 state 需要从服务端搬迁到客户端去。
  - stateful connection
    - 不是说 server 是 stateful，谁的 server 都是 stateful 的。
    - 而是说是不是有 websocket 连接来保持一个 stateful 的服务端状态。
    - elixir 的 LiveView 就是这样的技术（对比：Hotwire by Basecamp）。Meteor / Blazor 也是这样的技术
    - 这种技术的缺点是连接断开，状态就丢失了，业务只能完全刷新才能恢复正常。
    - 除非服务端做非常复杂的连接保持技术（欢迎打脸，这块确实不确信是不是有黑魔法）。在移动端网络下应用 stateful connection 就要三思了。
- 现在的 RSC 产出物是序列化的 JSON 字符串，需要反序列化后解析出组件，再生成HTML，是一种中间态。
  - 而 SSR 的产出物就是 HTML，不存在中间态，
  - 所以本质上 React Server Component 还是属于 CSR，而非 SSR。
  - 利用这种中间态，可以想象到很多有意思的玩法，云组件是其中一种，
  - 主要还是受限于JSON没办法搞更多的魔法，所以可以用这个技术来优化的场景限制蛮多的，虽然很期待但暂时感觉实战上没有那么好用。
- 看起来比较类似Blazor Server，但也不完全一样，Blazor Server还是让服务器来处理所有状态了。
  - Blazor Server的做法可以写起来很爽，完全没有fetch数据等操作，但是对服务器和网络状态要求比较大，比较适合自己搞一些用户量不太大的东西用。
  - React这个只让服务端渲染部分东西，应该最后是会更加实用的。
- 感觉能替代部分微前端的功能。
  - 颗粒度是到组件级别了，比微前端这种页面级的（或者系统级的）感觉更好点，复用性能大大提高。
  - 我认为，把复用的组件提到服务端反而降低可维护性。
- 感觉就是Suspense和lazyload的云端实现，
  - lazy load 已经是lazy了，那这个component 是从本地引入的还是云端的，就没有什么太大的区别了。
# [rsc faq](https://github.com/reactjs/rfcs/blob/2b3ab544f46f74b9035d7768c143dc2efbacedb6/text/0000-server-components.md#faq)
- not-yet
  - 若将view的数据样式都频繁变化的部分采用rsc形式实现，组件更新时rerender如何实现，性能如何

- Does this replace SSR?
  - No, they’re complementary. 
  - SSR is primarily a technique to quickly display a non-interactive version of client components. 
    - You still need to pay the cost of downloading, parsing, and executing those Client Components after the initial HTML is loaded.
  - You can combine Server Components and SSR, where Server Components render first, with Client Components rendering into HTML for fast non-interactive display while they are hydrated. 
  - When combined in this way you still get fast startup, but you also dramatically reduce the amount of JS that needs to be downloaded on the client.

- Does this replace GraphQL?
  - GraphQL is one approach for building API endpoints that can help apps reduce under/over-fetching and reduce round trips (among other features)
  - Server Components are focused on building user interfaces.
  - developers may find it helpful to use GraphQL client to load data for their Server Components too. 

- Is this just working around the lack of a compiler in JavaScript?
  - No, a static compiler can help with some things 
  - but we found that many real world apps have a lot of dynamic branches such as user-specific options, A/B tests, feature flags, etc. that make static optimizations hit a limit. 

- Are you reinventing PHP/JSP/whatever for the front end?
  - The history of application development is a series of pendulum swings between “thin” and "thick" clients
  - But the reality is that some parts of any app are more "static" - non-interactive, don’t need immediate data-consistency
  - while others are "dynamic" and need interactivity and immediate responsiveness. 
  - Neither pure server rendering or pure client rendering are ideal for all situations. 
  - Server Components — when combined with existing Client Components — allow developers to write each part of their app using the approach that makes the most sense, 
  - while sharing a single language and framework and even sharing code across server and client.

- Is this in production at Facebook?
  - We are running an experiment with a small number of users on a single page, 
  - with encouraging results (already ~30% product code size reduction). 
  - We expect more savings in an app designed with Server Components for the start.

- Is this specific to Nextjs?
  - No. We are partnering with Next.js to build out an initial integration. 
  - However, Server Components are designed from the beginning to be used with any framework or integrated into custom application setups. 
  - Given the scope of Server Components — including router, bundler, and server/client coordination aspects
  - we felt that a high-quality initial integration would allow us to demonstrate the setup to other developers.

- Why don’t you just use HTML instead of a custom protocol?
  - We do want to use streaming HTML for the initial render, 
  - but the custom protocol lets us transfer data (component props), and reconcile trees so that the client state as well as DOM focus/scroll/state doesn’t get blown away.

- Isn’t static generation better?
  - Static generation is great for some use cases, and you can run Server Components at build time for that.

- Do I have to read my database directly from components?
  - No, although it might be convenient when you’re starting up. 
  - The goal is to be able to scale up or down, and let you move freely between direct database access, microservices, or other approaches without rewriting your app. 
  - You can also build JavaScript abstractions that let you manage batching queries and provide authorization layers.

- What is the response format?
  - It’s like JSON, but with “slots” that can be filled in later. 
  - This lets us stream content in stages, breadth-first. 
  - Suspense boundaries mark intentionally designed visual state so we can start showing the result before all of it has fully streamed in. 
  - This protocol is a richer form that can also be converted to an HTML stream in order to speed up the initial, non-interactive render.

- How does this relate to Suspense?
  - The Server Components data fetching APIs are integrated with Suspense. 
  - We use Suspense to provide loading states and unblock parts of the stream so that the client can show something before the whole response is done.

- How does this relate to Concurrent Mode?
  - Concurrent Mode is a set of optimizations across React and also integrates with Server Components. 
  - For example, Concurrent Mode lets us start rendering Client Components as their data streams in, without waiting for the whole response to be finished.

- How do you do routing?
  - We don’t know yet. It’s an active area of research. 
  - There is a missing feature similar to Context for Server Context that we need to build into React first.

- Why not use async/await?
  - The React IO libraries used in the demo and RFC follow the conventions we've discussed previously for writing Suspense-compatible data-fetching APIs. 
  - Suspense-compatible APIs return data synchronously when it is already available, throw if there is an error, or "suspend" to indicate to React that they are unable to return a value. 
  - The mechanism for Suspending is to throw a `Promise` value. 
  - React uses resolution of the promise to know when the API may be ready to provide a value (or that it has failed) and to schedule an attempt to render the component again.
  - One new consideration in the design of Suspense from this proposal is that 
    - we would like to use a consistent API for accessing data across Server Components, Client Components, and Shared Components. 

- Are Server Components refetched whenever their props change?
  - No, Server Components in the middle of the tree won’t refetch when a parent Client component re-renders.
  - From the Client’s perspective, there are no Server Components at all
  - When a Server component needs to update, such as a result of a mutation, React will refetch the whole Server Component tree output that renders from top to bottom (though finer-grained invalidation is an active area of research). 
  - Currently, the Server Component tree starts at the root of the app, but we plan to allow more granular refetching from explicitly chosen entry points.

- Are you always refetching the whole app? Isn’t that slow?
  - We are planning to introduce a more granular refetching mechanism so that you have the option to refetch only a part of the screen, 
  - but it is not available yet.

- What are the performance benefits of Server Components?
  - Server Components let you put most of your data fetching on the server so that the client doesn’t need to make many requests. 
    - This also avoids client network waterfalls, which is typical for fetching in useEffect
  - Server Components also let you add non-interactive features to your app without increasing the bundle size. 
    - Moving features from the client to the server decreases the initial code size and client JS parse time. 

- Doesn’t always re-fetching the UI make interactions slow?
  - You can (and should) use Client components at any level of the tree for fast interactions. 
  - Also, you don’t want to always refetch — the fetched trees can stay in the client cache and be reused for navigations like back button.

- How is this different from PHP/Rails/etc?
  - You can reuse some components between Client and Server for use cases with different tradeoffs. 
  - E.g. Markdown renderer that offers live preview on the client but is rendered for consumption on the server. 
  - This is possible because they’re written in the same paradigm and language.

- Why not Rx?
  - Rx is a great solution for managing streams of data. 
  - Rx is a good fit for implementing a transport layer to receive the stream of rendered UI chunks that React creates on the server and stream them to the client.

## [pr: React Server Components](https://github.com/reactjs/rfcs/pull/188)

- One of the reason I loved hooks is that it solved REAL problems for us that were currently preventing scale in our React applications, 
  - where-as I feel like for me personally this doesn't solve real problems I'm currently facing in my React projects.
  - For me personally, I wouldn't trade a fractional increase in performance for the complexity this brings to a project, especially when I have many other levers I can pull before pulling this one.

## [RFC: React Server Components](https://github.com/reactjs/rfcs/blob/2b3ab544f46f74b9035d7768c143dc2efbacedb6/text/0000-server-components.md)

- Server Components allow developers to build apps that span the server and client, 
  - combining the rich interactivity of client-side apps with the improved performance of traditional server rendering
- Server Components run only on the server and have zero impact on bundle-size.
  - Their code is never downloaded to clients, helping to reduce bundle sizes and improve startup time.
- Server Components can access server-side data sources, such as databases, files systems, or (micro)services.
- Server Components seamlessly integrate with Client Components — ie traditional React components. 
  - Server Components can load data on the server and pass it as props to Client Components, 
  - allowing the client to handle rendering the interactive parts of a page.
- Server Components can dynamically choose which Client Components to render, 
  - allowing clients to download just the minimal amount of code necessary to render a page.
- Server Components preserve client state when reloaded. 
  - This means that client state, focus, and even ongoing animations aren’t disrupted or reset when a Server Component tree is refetched.
- Server Components are rendered progressively and incrementally stream rendered units of the UI to the client. 
  - Combined with Suspense, this allows developers to craft intentional loading states and quickly show important content 
  - while waiting for the remainder of a page to load.
- Developers can also share code between the server and client, 
  - allowing a single component to be used to render a static version of some content on the server on one route
  - and an editable version of that content on the client in a different route.

- Basic Example

```JS
// Note.server.js - Server Component

import db from 'db.server';
// (A1) We import from NoteEditor.client.js - a Client Component.
import NoteEditor from 'NoteEditor.client';

function Note(props) {
  const { id, isEditing } = props;
  // (B) Can directly access server data sources during render, e.g. databases
  const note = db.posts.get(id);

  return (
    <div>
      <h1>{note.title}</h1>
      <section>{note.body}</section>
      {/* (A2) Dynamically render the editor only if necessary */}
      {isEditing 
        ? <NoteEditor note={note} />
        : null
      }
    </div>
  );
}
```

- This is “just” a React component: 
  - it takes in props and renders a view. 
  - There are some constraints of Server Components - they can’t use state or effects
- Server Components can directly access server data sources such as a database

- **Motivation**
  - Server Components address a number of challenges in React that we’ve seen across a wide range of apps.
  - These challenges fall into two main buckets. 
  - First, we wanted to make it easier for developers to fall into the “pit of success” and achieve good performance by default. 
  - Second, we wanted to make it easier to fetch data in React apps.
- Zero-Bundle-Size Components
  - Developers constantly have to make choices about using third-party packages.
  - While advanced features such as tree-shaking can help somewhat, we still end up having to ship some extra code to the user.
  - Server Components allow developers to render static content on the server, taking full advantage of React’s component-oriented model and freely using third-party packages while incurring zero impact on bundle size.
- Full Access to the Backend
  - There are many great approaches to data-fetching with React, and many great databases and data stores to choose from.
  - We wanted a solution that would both make it easier for anyone to get started and that could tame(易于控制；驯服) complexity in larger apps too.
  - RSC能提供切换后台数据存储访问方式的灵活性
- Automatic Code Splitting
  - Common approaches are lazily loading a bundle per route and/or lazily loading different modules based on some criteria at runtime.
  - there are two main limitations to existing code-splitting approaches. 
  - First, developers have to remember to do it at all, replacing regular import statements with `React.lazy` and dynamic imports. 
  - Second, this approach delays the point at which the application can start loading the selected component, offsetting some of the benefit of loading less code!
  - Server Components address these limitations in two ways. 
    - First, they make code splitting automatic: Server Components treat all imports of Client Components as potential code-split points. 
    - Second, they allow developers to make the choice of which component to use much earlier, on the server, so that the client can download it earlier in the rendering process. 
- No Waterfalls
  - A common cause of poor performance occurs when applications make sequential requests to fetch data.
  - one pattern for data fetching is to initially render a placeholder and then fetch data in a useEffect() hook
    - When both a parent and child component use this approach, however, the child can’t start loading any data until the parent component finishes loading its data. 
    - One upside of fetching data in individual components is that it allows an application to fetch exactly the data it needs
    - We wanted to find a way to avoid sequential round trips from the client while still avoiding over-fetching of data that wouldn’t be used.
  - Server Components allow applications to achieve this goal by moving sequential round trips to the server.
    - The problem isn’t really the round trips, 
    - it’s that they are from client to server. 
    - By moving this logic to the server, we reduce the request latency and improve performance. 
  - Even better, Server Components allow developers to continue fetching the minimal data they need directly from within their components
- Avoiding the Abstraction Tax
  - UI frameworks in “static“ languages can exploit ahead-of-time compilation to compile away some of these abstractions, but this option isn’t available in JavaScript.
  - we initially experimented with one approach to ahead-of-time (AOT) optimization — Prepack — but ultimately that direction did not pan out. 
  - Specifically, we realized that many AOT optimizations don’t work because they either don’t have enough global knowledge or they have too little
  - Server components help to address this by removing the abstraction cost on the server.
- Distinct Challenges, Unified Solution
  - a theme of these challenges was that React was primarily client-centric
  - Ultimately, we realized that neither pure server rendering or pure client rendering were sufficient. 
  - Server rendering allows applications to easily access server-side data sources and to quickly show static content, 
  - while client rendering is critical for rich, interactive features where users expect immediate feedback. 

- **Detailed Design**
- Simplified Loading Sequence
- Update (Refetch) Sequence
- Capabilities & Constraints of Server and Client Components
- Sharing Code Between Server and Client
- Naming Convention for Server/Client Components
- Open Areas of Research
  - Routing
  - Bundling
  - Pagination and partial refetches
  - Mutations and invalidations
  - Pre-rendering
  - Static Site Generation
  - Developer Tools

- **Drawbacks**
  - Introducing a new form of components means more to learn.
  - This approach requires a convention for distinguishing server, client, and “shared” components, which may be confusing or off-putting.

- **Alternatives**
  - Client-only rendering
  - Server-only rendering
  - “Server-side rendering” (SSR)
  - Static Site Generation
  - AOT compilation
- none of these techniques alone is sufficient to achieve the combination of familiar developer experience, user experience, and features achieved by this proposal.

- Adoption Strategy
  - using Server Components will require integration with an application’s routing system and bundler.

- [Introducing Zero-Bundle-Size React Server Components](https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html)
- [server-components-demo](https://github.com/reactjs/server-components-demo)
  - The demo is a note-taking app called React Notes.
    - It uses a Webpack plugin (not defined in this repo) that allows us to only include client components in build artifacts
    - An Express server that:
      - Serves API endpoints used in the app
      - Renders Server Components into a special format that we can read on the client
    - A React app containing Server and Client components used to build React Notes
  - This early demo is built on top of our Webpack plugin, 
    - but this is not how we envision using Server Components when they are stable. 
    - They are intended to be used in a framework that supports server rendering — for example, in Next.js.
- [server-components-demo-no-db](https://github.com/pomber/server-components-demo/)
  - a fork of the original demo without the Postgres dependency
  - you can run the demo app without needing a database.
  - you won't be able to execute SQL queries (but fetch should still work).
# pieces
- Cool, React can now do what PHP has been able to for decades.
  - PHP is definitely an inspiration, but there are a few different nuances:
    - Being able to *refetch* a Server tree without blowing away the Client state inside of it.
    - Being able to choose to run the same component on the server *or* on the client (for fast interactions).

- ## What do React Server Components mean for the ecosystem and frameworks like Next.js?(from vercel dev)
  - https://twitter.com/leeerob/status/1341818958794657795
  - Server Components reduce client bundle size and improve startup time. 
    - Since they run on the server, you can access data sources like databases and file systems directly.
    - This will simplify data fetching and enable future performance improvements (e.g. Concurrent Mode, Streaming SSR).
  - You will no longer need to choose client or server-rendering on a per-app basis. 
    - Server Components will unlock this at the *per-component level.*
    - For example, Next.js can only access the backend on a per-page level (e.g. `getServerSideProps`).
  - How will you share state between the client and the server?
    - The server is stateless. 
    - However, the React team intends to add something similar to the Context API. 
    - This state would be passed between the client and the server.
  - What does this mean for hosting?
    - It's still early. Obviously, you will need a server. 
    - Since React components are JS, initial backend support would also be JS. 
    - That doesn't necessarily mean Node, but something similar.
  - How will this improve Next.js?
    - Any pages that use SSR will have smaller bundles and faster response times. 
    - Using Server Components will be incrementally adoptable with newer versions of Next.js.
  - How is this different from SSR in Next.js?
    - With SSR in Next.js, all component code is sent to the client in the JS bundle. 
    - Server Components will allow you to choose "zero-bundle" or "whatever bundle you need".
    - This will improve performance and startup times.
    - My understanding is startup time(initial render) won’t be improved by server components because server components is just a different implementation of SSR which Next is already doing. 
      - I can see time to interactive to improve because of smaller bundle size

- If you don’t care about perf, you don’t have to bother with either Server Components nor SSR. 
  - https://twitter.com/sebmarkbage/status/1341768759585943552
  - If you do, it’s probably worth investing in either SSG CLI or a JavaScript server infra. 
  - I suspect Server Components will be the first thing you’ll want to adopt and close second SSR.

- CSR is not going away! Server components aren’t totally changing how we build React apps. 
  - They are an optimization you can use for better UX.
  - https://twitter.com/flybayer/status/1341465457799344136

- one thing I personally find cool about Server Components is that their output is jumped over while diffing / “re-rendering” when re-rendering due to a state change above. Because it couldn’t have possibly changed — it comes from the server!
  - https://twitter.com/dan_abramov/status/1342130504464666625
  - Now if only we had an auto-memoizing compiler for the parts that *do* have to stay on the client... that would be rad(棒的).
  - In other words reconciliation also becomes faster?
    - Yes because the code in between doesn’t need to rerun (it’s on the server) and the props to native elements have not changed.
  - It’s not the main objective of RSC but in this it is more performant than React.memo 
    - because React.memo still needs to do a diff of the component’s props 
    - and it’s gonna be re-rendered if there’s a change in its state or context.

- ## Can someone help me understand who React Server components are for?
  - https://twitter.com/RyanCarniato/status/1341485603695730688
  - I get what they do. I get how they work. 
    - But you could clearly fetch/stream data isomorphically. 
    - Partial hydration can be accomplished other ways. 
    - Why render the component on the server after the fact? 
  - So layout components driven by readonly data can be excluded from the client bundle
  - It is good to a lot of hight conditional (i18n, AB, theme) read-only data, like newsfeed
  - It’s good for the cloud providers who will now make more money from all the compute associated with the Server side Components rendering

- evan you
  - https://twitter.com/youyuxi/status/1341124009858052104
  - React server components are very interesting, but the coupling to a specific server setup seems quite a cost to pay. 
    - Incidentally I've also been doing some research on more aggressive elimination of bundle/hydration cost, but with the goal of being applicable to both SSR/SSG.

- our research into zero-bundle-size React Server Components
  - https://twitter.com/reactjs/status/1341072021099327489
  - The difference with LiveView is we refetch more coarsely — not sending updates, but the result. 
    - (We need to add granular refetching, but it would be based on subtrees rather than diffs.) 
    - The upside is that the server is fully stateless.

- Sharing app views between server and client is magical:
  - https://twitter.com/DavidKPiano/status/1341391171176816644
  - LiveView (Elixir - Phoenix)
  - Turbolinks (Ruby - Rails)
  - Livewire (PHP - Laravel)
  - Server Components (Node - React Soon)
  - In the future, we can (hopefully) do the same for app logic, regardless of language 
  - We do this in our platform (low code tool for building apps quickly). 
    - What’s even more interesting is that modeling the app logic in a language independent visual way allows for automatic calculation of dom diffs as well. 
    - And we have visual state machines
  - That would be awesome, kind of like if markdown was it’s own independent that can be used in any other “real” language and we all agree on the spec
  - It’d be cool if we had a standard for the intermediary representation for the components 
    - and then we could share components across frameworks/libs/languages.
    - Judging by some of the comments under the RFC that's definitely on their mind
    - I wonder how web components fit into all this (or can they fit even).

- The eventual future is server-side with a sprinkle of client-side for instant interactions
  - https://twitter.com/mxstbr/status/1198627346955350021
  - 关于服务端计算还是客户端计算的争论
  - I don’t buy it. User experience happens on the client side.
    - Native apps are fucking 900% superior to web apps and they dont server render shit
    - I mean if we're talking web pages, then by all means, have it cho way. But apps. Pushing it all to the server is defeat.
  - But my colleagues on the native side have been server rendering significant chunks for years for a variety of reasons. 
    - So it’s not completely unnecessary. Just less commonly needed.
  - The performance and UX is always better on apps that don’t server render. 
    - That said, for apps that need to render across dozens of devices like Netflix and YouTube 
    - there is value in server rendering, especially when the device is low powered

- As noted in RFC, frameworks such as Rails were one of many inspirations for React Server Components. 
  - We’re not swinging the pendulum(钟摆；摇摆) fully to the server: 
  - we’re acknowledging that neither server- or client-rendering are ideal for all cases. 
  - Choose *per component*, not per app.
