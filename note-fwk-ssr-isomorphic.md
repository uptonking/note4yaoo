---
title: note-fwk-ssr-isomorphic
tags: [framework, isomorphic, server-side-rendering, ssr]
created: '2020-12-19T13:02:19.041Z'
modified: '2020-12-19T13:05:23.294Z'
---

# note-fwk-ssr-isomorphic

## guide

- ssr的优点
  - seo搜索引擎优化
    - 更多针对toC消费者业务，对企业管理系统没必要做seo
    - 现在的互联网应用是信息孤岛的趋势，微信公众号的文章内容不让百度收录
    - seo针对SPA的问题，谷歌爬虫已经处理，百度也不远了，还是基于prerender
    - dynamic rendering是解决seo问题的另一种方式
  - 加快首屏显示
    - 使用代码拆分和动态(懒)加载也能实现
  - 提升开发效率，使用同构渲染，一套代码可以运行在服务端和客户端

- usecase
  - 针对重消费者业务的seo，偏离市场主流业务
  - 落地页(Landing page)
  - 博客页面(Blog posts)
  - 帮助文档(help and documentation)
  - 营销页面、产品介绍页面(Marketing pages)

- ### [用了react 或者 vue，如何做SEO优化呢？](https://www.zhihu.com/question/51949678/answers/updated)
- 用 Vue 不代表你一定要做成 SPA
  - 对于真正适合做成 SPA 的应用，SEO 反而通常不是问题。
  - 你针对 marketing 的页面应该是静态分开部署的，app 本身则要登陆才能用，SEO 没有什么意义。
  - 少数既需要 SPA 强交互性，又对 SEO 和首屏速度有刚性需求的场景，这时候同构 SSR 就派上用场了。
- SEO的必要性
  - 事实就是这些前端框架最适应的场景就是管理平台，不需要做SEO。
  - 看自己的网站类型及团队架构情况，如果是需要登录才可以使用的，那么SEO意义不大
    - 最多首页放点静态文字和图片让搜索引擎收录即可。
    - 如果是非SPA的，且需要考虑搜索引擎的，要看自己的后端架构，如果是Node，react和vue都有方案。
    - 如果是其它的，可能不太好办，要么给搜索引擎的单独推一套（用户依然体验的是react、vue），要么就用传统的后端直接拍页面方式（放弃react、vue）。
  - seo或许是比较好的网站推广方式，但绝不是唯一的推广方式，还有其他的很多有效的办法的，
    - 以前老说seo是免费的，现在再看，成本已经很高了
    - SEO永远玩不过人民币玩家
  - 如果因为seo的一些限制而造成其他更有价值的东西没办法进展，那就舍弃seo呗
    - 一开始就打算用seo的话就尽量别用这些框架了 不然自己就坑死自己了
  - 比起日益昂贵的SEO，广告联盟反而因为越来越精准而划算
  - 静态信息网站的显示层，通常是直接渲染的，或者干脆就是静态页面。这样方便别人爬取数据。
    - 至于vue，只要用在后台和用户的操作就可以了。比如发布消息，点赞，回复等
- 不说需要维护两份工程，目前百度抓取程序在特定时候会伪装成正常用户，来浏览页面资源，受制于计算和存储资源，百度抓取程序并不能很好的解析JS，会造成站点被百度降低评级；
  - 另外维护一份爬虫白名单，这是个非常细碎的工作，需要UA+IP一起维护，而不是只是维护UA，这样就会非常麻烦。
  - 百度先用公开UA的爬虫来获取页面，然后可能会再模拟用户UA获取页面，如果不一致则判断作弊
  - 可以给用户种cookie，第一次进ssr，第二次就不进了。爬虫即使模拟用户的ua，肯定不会有cookie驻留的功能。
- 对 React 来说核心方法是 renderToString()。
  - 在服务端根据 url 拼出首屏内容发送给前端，到了前端之后就是 SPA 了。
  - 我常用的套装包括 express，react-router 和 redux。
  - 路由交给 react-router，用 redux 的 store 处理 SSR 中的前后数据交换。
  - 如果不用 redux，也有办法实现前后数据交换。原理是把数据拼成一个 JSON 字符串给前端去解析。

- ### SSR vs SSG
- 单页应用不容易实现SEO，近年业界针对此问题提供了两种解决方案：服务器端渲染（SSR）和静态站点生成（SSG）。
- 使用SSR，我们可以在服务器上运行应用程序，它创建由前端获取的HTML。
- 而使用SSG，我们可以在构建时创建应用程序的所有页面，由此，存储在服务器上的文件是静态的，并像标准的非SPA应用程序一样由浏览器获取。
- SSR的最大问题是，在服务器上构建应用程序会占用大量资源，而且速度可能很慢，因此会增加页面加载时间；
  - 而且，每个小的更改都需要重新构建和创建所有应用程序页面。
  - 如果应用程序有很多页面，则该过程很慢且成本很高。
- 现在看来，SSG赢了，SSR（几乎）死了。
  - Next.js是一个流行的全栈框架，将SSG设置为默认框架，并添加了增量构建，以缓解每次更改后重新构建所有页面的问题。
- 此外，像Gatsby这样的静态网站生成器会在其产品中添加增量构建。
- ref
  - https://www.zhihu.com/question/433673833/answer/1622039165
  - 我认为，ssg适合中小型应用，不适合超大型应用，
    - 问题在于若内容超级多，则增量构建也会花费大量时间，同时动态交互的计算量也很大

- ### [有必要使用服务器端渲染(SSR)吗？](https://www.zhihu.com/question/308792091/answers/updated)
- 现代框架的服务端渲染和 jsp、php 这些还是有不少区别的。
  - 因为 nextjs 和 nuxtjs 这种不仅仅是服务端渲染，它们还是同构框架。
  - 什么是同构呢？就是一份代码既可以跑在浏览器端，也可以跑在服务端。这得益于 NodeJS 在服务端的流行。
- 传统jsp、php、django这些服务端渲染框架都是返回html字符串，所以就会造成切换页面的时候重新刷新了，用户体验比较差。
  - 而现在流行的前端开发模式都是SPA，这些都是无刷新切换页面带来更好的用户体验。
- 所以 nextjs 和 nuxtjs 不仅支持服务端渲染，还支持 SPA，常用的是对首页进行服务端渲染，其他页面依然保持 SPA 的无刷新访问模式。
- 服务端渲染也不应该滥用。
  - 比如我们的内部后台管理系统就上了Nuxt，现在每次本地构建要花10分钟，非常影响开发效率。

- ### [为什么现在又流行服务端渲染html？](https://www.zhihu.com/question/59578433/answers/updated)
- 互联网市场像知乎、淘宝、视频等toC直接面向用户的站点 占据整体市场的份额并不多。
- 未来，更多的业务还是在于toB端服务型业务建设。
  - toB型业务不需要seo，不需要首屏渲染。要的是低成本开发ios、小程序多端并用
- 现在并没有真正的回归ssr，现在所说的ssr，是结合传统ssr+spa集两家之长。
  - 阿里前端为什么强势，因为他们给公司做了后台技术做不了的贡献。
  - 前后端团队矛盾冲突升级，说白了，就是部分后端开发人员不思进取，又发现被前端蚕食饭碗。
- 作者还是思维局限，没有看到诸多方向下驱动下来的选择，譬如运维成本，服务器资源成本，开发成本，沟通成本
  - 一个项目，要你开发出来pc应用，小程序，App。在传统模式下，你需要多少人？要开发多久？要多少钱？ 客户愿意给你多少钱？
  - 按照传统技术架构，服务端渲染服务端计算，亿万级的访问，需要假设多少服务器？部分计算渲染交给客户端，省了多少钱？
- SSR开发体验、可维护性(包括组件复用性)上的弊端十分明显，之所以至今还没消失是因为能解决某些业务模式的痛点
  - 比如虎扑这种强依赖搜索引擎流量的(spa + puppeteer预渲染 + 分离爬虫流量也能实现，但成本不比ssr低)；
  - 还比如对性能有极高要求的落地页(细微的载入速度差别就能带来营收上的巨大差异)。
  - 技术本质上是需要服务业务的，不管是它的诞生还是以后的发展反向。
- SPA发往浏览器的是一个很轻量的html，以及大体量的javascript，
  - 搜索引擎只能读取这有限的html，没法读取其他动态生成的URL，就很难爬到其他页面
  - 既然爬不到，那能不能直接告诉搜索引擎我有哪些URL呢？
    - 当然可以，如果你是网站的开发者，可以在搜索引擎的console上传sitemap（站点地图），直接通过一定的格式告诉搜索引擎，我这个Single-page application上面有哪些URL，
    - 不过无法读取动态生成的问题仍然存在。
  - 那能不能通过改革搜索引擎来解决呢？
    - 其实一些搜索引擎已经做了，比如googlebot，是支持读取动态生成html的，但是资源有限，不会让你无限地运行下去，对于异步fetch内容的部分，容易超时。
    - 所以服务器渲染才是解决SEO的根本。
  - 搜索引擎是怎么解析一大堆生成的html的呢？
    - 首先找有没有meta标签来描述网站
    - 没有的话就盲猜，比如你h1里面裹的大概是标题吧
    - 可以把meta部分服务器端渲染，然后其他部分依然动态生成，这也是很多大型网站在做的事情。
  - 如果这只是小网站，只有很少的开发者，不愿意搞服务器渲染怎么办？
    - 还有一个小技巧，就是Dynamic rendering
    - 加入中间件，识别这个request是浏览器发送的还是爬虫发送的，
    - 如果是浏览器发过来的，则正常返回，
    - 但如果是爬虫发送的，那就把渲染好的html发回去
    - 另外一个用服务端渲染的页面叫做"我支持的浏览器"，顾名思义，你用的浏览器太破了，无法支持浏览器渲染，请下载Chrome

- ### [“Single-page” JS websites and SEO](https://stackoverflow.com/questions/7549306/single-page-js-websites-and-seo)
- In my opinion, SPA is done right by letting the server act as an API (and nothing more) and letting the client handle all of the HTML generation stuff. 
  - The problem with this "pattern" is the lack of search engine support. I can think of two solutions:
    - When the user enters the website, let the server render the page exactly as the client would upon navigation. 
    - Let the server provide a special website only for the search engine bots. 
- There are two ways to make sure a single page application is SEO friendly
  - Dynamic rendering is the easiest way. 
    - requests coming from bots are forwarded via a service that can execute JS and render your SPA into a plain HTML page readable by any search engine bot. 
    - This can be done using a headless browser. 
    - An example of such a service is Rendertron that uses headless Chrome. 
    - These days it's probably the best option, and you can easily install it on your server along with your web server (Apache, Nginx, or whatever you use).
  - Server-side rendering (SSR) may appear to be a bit more complicated. 
    - the pre-rendered SPA is also a plain HTML for search engines, 
    - but on the other hand, it's a fully functional application that can continue running once it's loaded into a browser. 
    - SSR probably brings no advantages for SEO compared to dynamic rendering. 
    - Still, a pre-rendered SPA may load faster for users, especially on a slow mobile device, because the device will not have to execute all JavaScript before the user sees the first page.
- ref
  - [SEO with single page application](https://stackoverflow.com/questions/30789799/seo-with-single-page-application)

- ### [google: Implement dynamic rendering for SEO](https://developers.google.com/search/docs/guides/dynamic-rendering)
  - Currently, it's difficult to process JS and not all search engine crawlers are able to process it successfully or immediately. 
  - we recommend dynamic rendering as a workaround solution to this problem.
  - **Dynamic rendering means switching between client-side rendered and pre-rendered content for specific user agents**.

    - Dynamic rendering is good for indexable, public JS-generated content that changes rapidly, or content that uses JS features that aren't supported by the crawlers you care about. 
    - Not all sites need to use dynamic rendering, and it's worth noting that dynamic rendering is a workaround for crawlers.

  - Dynamic rendering requires your web server to detect crawlers (for example, by checking the user agent).

    - Requests from crawlers are routed to a renderer, requests from users are served normally
    - Where needed, the dynamic renderer serves a version of the content that's suitable to the crawler, for example, it may serve a static HTML version. 
    - You can choose to enable the dynamic renderer for all pages or on a per-page basis.

  - Googlebot generally doesn't consider dynamic rendering as cloaking

    - As long as your dynamic rendering produces similar content, Googlebot won't view dynamic rendering as cloaking.
    - When you're setting up dynamic rendering, your site may produce error pages. 
    - Googlebot doesn't consider these error pages as cloaking and treats the error as any other error page.

  - Using dynamic rendering to serve completely different content to users and crawlers can be considered cloaking
  - To setup dynamic rendering for your content, follow our general guidelines. 

    - You will need to refer to your specific configuration details, as they vary greatly between implementations.
    - For a hands on approach, try our new Implement dynamic rendering with Rendertron codelab.
    - Install and configure a dynamic renderer to transform your content into static HTML that's easier for crawlers to consume. 
      - Some common dynamic renderers are Puppeteer, Rendertron, and prerender.io.
      - Rendertron  is an open source solution based on headless Chromium.
    - Choose the user agents that you think should receive your static HTML and refer to your specific configuration details on how to update or add user agents.
    - If pre-rendering slows down your server or you see a high number of pre-rendering requests, consider implementing a cache for pre-rendered content, or verifying that requests are from legitimate crawlers.

  - Configure your server to deliver the static HTML to the crawlers that you selected. 
  - There are several ways you can do this depending on your technology; 

    - Proxy requests coming from crawlers to the dynamic renderer.
    - Pre-render as part of your deployment process and make your server serve the static HTML to crawlers.
    - Serve static content from a pre-rendering service to crawlers.
    - Use a middleware for your server 

## ref

- [google: Deprecating our AJAX crawling scheme_201510](https://developers.google.com/search/blog/2015/10/deprecating-our-ajax-crawling-scheme)
  - We are no longer recommending the AJAX crawling proposal we made back in 2009.
  - In 2009, we made a proposal to make AJAX pages crawlable. 
  - Today we are generally able to render and understand your web pages like modern browsers. 
  - Serving Googlebot different content than a normal user would see is considered cloaking(隐蔽欺骗), and would be against our Webmaster Guidelines.
- [How do you use React.js for SEO?](https://stackoverflow.com/questions/28252768/how-do-you-use-react-js-for-seo)
