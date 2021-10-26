---
title: web-latest-trending
tags: [latest, web]
created: '2021-01-01T20:52:04.258Z'
modified: '2021-01-01T20:52:42.088Z'
---

# web-latest-trending

# guide
- watching
  - ssr
  - cjs to esm
  - ~~renderer using sika like flutter~~
  - 华为鸿蒙os的app开发基于js
  - [Technology Preview: Jetpack Compose for Web](https://blog.jetbrains.com/kotlin/2021/05/technology-preview-jetpack-compose-for-web/)
  - [Airbnb’s Server-Driven UI System](https://t.co/XXSpXaztL8?amp=1)
# topics
- viewpoints
  - Payments are moving from batch processing to realtime processing. this changes everything

- new-infra
  - webpack module federation
    - deno url import
  - faas/serverless
  - esbuild/vite bundler

- new-framework-app
  - react server components
  - component story format
  - lowcode/nocode

- hot-now
  - 小程序
  - hybrid
  - flutter
  - 微服务
  - serverless
  - webrtc
  - browser as os, pwa

- engineering
  - 前后端一体化/BFF：blitz, redwood

- animation
  - web animations api

- css
  - CSS Painting API／CSS Layout API／CSS Typed OM
  - css typed om
    - firefox和safari均不支持(202001)
  - css in js依然活跃

- js
  - webgl > webgpu
  - v8 > wasm

- web components
  - react + hooks

- classic
  - viz
  - animation
  - gaming
  - auto testing/monitoring
    - puppeteer
  - compiler

- more
  - WebGL 2
  - Push Notifications
  - anything based on Worklets
  - WebRTC
  - WebP/VP8/VP9
  - WebXR
  - CSS Typed OM
  - Offscreen Canvas
  - ImageBitmap (quickly draw programmatically created images)
  - CSS Typed OM (fast CSS updates from JS)
  - requestIdleCallback
  - ResizeObserver
  - scroll-snap
  - :focus-within
  - new media query options (OS settings personalization)
  - logical properties (block & inline)
  - Sticky Situations
  - backdrop-filter
  - :is()
  - FlexBox gap
  - Houdini
  - Custom properties
  - Paint API
  - Animation Worklet

- ios-missing
  - No Service Worker
  - Can't print or save as PDF
  - No support for GetUserMedia
  - Web Push Notifications (ZOMFG)
  - Audio Worklet
  - Custom Paint
  - Web Animations API
  - Pointer Events
  - CSS Typed OM
  - Web Bluetooth
# products
- natto
  - https://natto.dev/
  - a canvas for JavaScript
# discuss
- ## techs to look out for in the javascript world in 2021
- https://twitter.com/KerryRitter/status/1344039489123934209
  - @stenciljs - web components compiler
  - @tailwindcss - design system toolkit
  - @rustlang - language for wasm
  - @nestframework - 2020s fastest rising framework
  - @deno_land - new JS/TS runtime
- Tanner Linsley 2021 Goals
  - XState
  - Serverless
  - Improve @nozzleio sales
  - 2 years worth of @nozzleio updates
  - React Query Essentials v3
  - React Table v8 (TS rewrite)
  - React Table Essentials
  - React Table/Grid Pro
  - Hopes: Physically attend a JS/React conference
  - There's a good chance this year that I will reimplement React-Charts with airbnb/visx
    - and a slightly smaller chance that React Charts goes away all together.
    - I need more chart types @nozzleio, and not enough time to build essentially what visx has already built.

- ## [Web development and designing trends in 2021](https://twitter.com/Prathkum/status/1347779080259715073)
  - Progressive Web Apps
  - Single Page Websites
  - Accelerated Mobile Pages
  - Voice-Enabled eCommerce apps
  - API-first development
  - Parallax animation
  - Glass and Neumorphism
    - 也称为soft ui，是一种类似于浮雕的效果，有的人说这是新的拟物风格（New Skeuomorphism）
  - Abstract art compositions
  - 3D visuals

- ## [My bold two-year prediction](https://twitter.com/tylerlwsmith/status/1346282659484323841): 
  - 2021 will be the peak of JavaScript frameworks & compilers. 
  - In 2022, tools like Turbo, Laravel Livewire, . NET Blazor Pages and Alpine JS that allow interactivity with little custom JavaScript will become serious alternatives to React & friends.
  - Developers gravitate towards tools that let them build things fast, even if it means letting go of some control. 
    - Bootstrap and Tailwind caught on because they let developers build real apps without tediously writing their own CSS.
    - The same thing will happen to JavaScript.
  - Modern JavaScript is complicated. 
    - Webpack is a challenge for even experienced JS developers.
    - Tools like Create React App ease this pain, but they can force you to put your JS app in a different repo & on a different server, complicating development & deployment.
  - JavaScript is a challenging language. 
    - The "this" keyword, functions vs arrow functions, prototypical inheritance, bind vs call, and immediately-invoked function expressions can be hard to understand.
    - Developers coming from other languages would often rather not learn these.
  - JavaScript's ecosystem has an overwhelming number of choices.
    - React? Vue? Ember? Angular? Svelte?
    - Styled Components? CSS Modules? Emotion?
    - Redux? MobX? XState?
    - JavaScript fatigue can kick in before you write a single line of code. This slows down development.
  - I believe developers will begin to recognize the productivity benefits of writing less custom JavaScript, 
    - and developers with no JavaScript experience will be able to create meaningful interactive/real time web applications.
  - If you are a JavaScript developer and this sounds scary, let me reassure you: there will always be work for JavaScript developers. 
    - However, the tent of web development will become much bigger.
    - Here's to a democratized web

- ## [Serverless能取代微服务吗？](https://www.zhihu.com/question/335301678/answers/updated)
- serverless是一种概念，serverless的目的是让开发者能更专注于逻辑的开发。
  - 云函数是一种可以直接使用的工具。也可以说是 serverless 的一种实现方式（虽然并不完美）
  - 云函数可以用来直接跑主要业务服务吗？看云商的支持力度。
- 微服务是分布式架构, 服务是网状 p2p 通讯, 是比较底层的概念.
  - 云函数是具体实现, 强调 轻量级服务+ serverless(弹性调用), 云函数必然是微服务架构, 而且是 弹性微服务容器架构, 已经是一种saas产品形态了.
  - 历史经验告诉我们, 场景复杂了, 就没有万能的架构, 总是要根据实际情况做取舍.
  - 应用领域有很多复杂的状态问题, 应用冷启动, jit, 状态迁移, 缓存, session , 都制约了应用的弹性
  - serverless目前是云厂商售卖的概念。需要解决的体验问题很多。

- microservices
  - 微服务就是可以组合在一起但是耦合度很松的并且相对独立的小程序，
  - 这些小程序一起合作就是传统意义的某个系统或者应用，只不过在传统的模式下，它们的耦合度很紧密，所以灵活性比较低，而微服务更适用于敏捷开发，以及快速部署等场景之中
  - 独立服务的注册、发现、测试、编排
- 特点
  1、一些列的独立的服务共同组成系统；
  2、单独部署，跑在自己的进程中；
  3、每个服务为独立的业务开发；
  4、分布式管理；
  5、非常强调隔离性。

- ## serverless vs microservices
- https://www.zhihu.com/question/421425308/answer/1498137091
- 我举个例子，midway faas底层，和传统的egg并没有本质区别。只是运行的runtime不一样，serverless省了运维而已。
  - 既然底层都一样，都是后端，为啥不能取代？只是成熟度问题，时间早晚而已。baas基建目前可能还不够理想。

- https://zhuanlan.zhihu.com/p/32536137
- Serverless并不能按字面上理解为无服务器，而是说对应用开发者而言，不再需要操心大部分跟服务器相关的事务，比如服务器选购、应用运行环境配置、负载均衡、日志搜集、系统监控等，这些事情统统交给Serverless平台即可，应用开发者唯一需要做的就是编写应用代码，实现业务逻辑。
  - Serverless最早由Amazon提出，第一个Serverless平台是2014年年底推出的Amazon Lambda，应用开发者只需要上传代码或者应用包，即可发布一个应用。
  - 之后全球各大云服务厂商都纷纷推出各自的Serverless平台，比如Google Cloud Functions，Azure Functions，IBM Cloud Functions，以及阿里云函数计算和腾讯云无服务器云函数等。
  - 在云服务厂商之外，开源社区也涌现出很多优秀的Serverless框架，比如Apache OpenWhisk，Spring Cloud Function，Lambada Framework，webtask等。
- Serverless应用可以细分为BaaS和FaaS两类，
  - BaaS: Backend as a Service，这里的Backend可以指代任何第三方提供的应用和服务，比如提供云数据库服务的Firebase和Parse，提供统一用户身份验证服务的Auth0和Amazon Cognito等。
  - FaaS: Functions as a Service，应用以函数的形式存在，并由第三方云平台托管运行，比如之前提到的Amazon Lambda，Google Cloud Functions等。
- 函数，往大了说可以是一个应用的main函数，往小了说也可以是一个简单的加法函数
  - 如同一个单体应用可以按业务模块拆分成多个微服务，一个微服务也可以按使用场景拆分成多个函数。
  - 比如一个广告微服务，至少可以拆分出实时竞价、展示计数、报表查询等多个函数。也就是说，FaaS中的函数和微服务中的API是同一粒度的。
  - 但不同于API，**在Serverless架构下，每个函数都是独立部署，按需执行**
- 和其他架构相比，Serverless有以下4个特点
  - 运行成本更低
    - 无论是过去的IDC，还是如今的云主机，本质上都是一种包月计费模式
  - 自动扩缩容
    - 一个函数只做一件事，可以独立的进行扩缩容，而不用担心影响其他函数
  - 事件驱动
    - 函数本质上实现的是一种IPO（Input-Process-Output）模型，它是短暂的，是即用即走的。
    - 这点是函数区别于单体应用和微服务的另一个特征。不管是单体应用，还是微服务，都是系统中的常驻进程
    - 函数天然的适用于任何事件驱动的业务场景，比如广告竞价，身份验证，定时任务，以及一些新兴的IoT应用。
  - 无状态性
    - 无状态一方面有助于提高函数的可重用性和可迁移性，但另一方面也带来了一些性能上的损失。
    - 函数只能使用外存（比如Redis，数据库）进行缓存，而操作外存都需要通过网络，性能跟内存、本地硬盘相比差了一到两个数量级。
- 它和DevOps最大的共同点就是帮助企业缩短产品上市的时间。
  - Serverless，从本质上说，它是把Ops外包给第三方平台，让Dev专注于业务逻辑的实现而不用操心Ops相关的工作，最终的结果就是绝大多数企业不再需要Ops这个岗位。

- ## [2020年国内公司前端团队都在搞些什么?](https://www.zhihu.com/question/398940598/answers/updated)
- 我的前端工程化突破点是 webpack5 的 module federation
- 得物作为最近两年的黑马，前端团队也在不断探索新的技术疆域：
  - “no code”、“low code”、“数据可视化”、“前端微服务”、“设计素材中心”、“性能异常监控”、“动画库”、“可视化埋点”、“一站式服务”、“组件 Hub”、“H5 游戏”、“Mock Server”、“前端质量诊断系统”、“BFF”、“前端行为回放”
- 2020年前端团队的新挑战和方向
  - H5(HTML5)+ 原生 ( Cordova、 Ionic、微信小程序)
  - Javascript 开发 + 原生渲染 ( React Native、Weex、快应用)
  - 自绘 U+ 原生 ( QT Mobile、 Flutter)
  - uniApp / Taro

- https://www.zhihu.com/question/398940598/answer/1269685808
01.   建立 开发规范，最重要的就是 git 分支使用规范，至少有个 release 分支对应生产环境，pre 对应预发，qa 对应测试环境
02.   建立统一的项目模版，比如单页，多页，后台管理，组件开发，小程序，Nodejs 项目，然后通过 cli 来选择 项目模版，模版选择后，直接生成项目，然后把调用 gitlab 的 api， 在 gitlab 上创建项目，push项目，这样就收拢了大家创建项目的方式， 自动统一了代码规范
03.   基于上面这个，就可以做基于 gitlab ci/cd，阿里云 oss 的持续集成，完成 push => 构建 => 上传oss（或者静态资源服务器,自动绑定域名，接 cdn，这样一条龙的服务，人手够的话也可以把 2，3结合一起做成基于 GUI 网页的创建，因为这里接管了大家发布代码的规范，后面就可以干很多事了
04.   把内部的 npm 私服搭建起来，做一套内网的 npm 组件开发构建  publish 一条龙服务，建一个组件展示平台，这样人多了，大家接可以互相用起来，方便的很
05.   因为有了上面 3 的收拢，我们就可以上线代码风格校验，检测线上发布是否包含了 sourcemap文件，接着人手够，老板支持的话，可以统计每个项目的依赖，存储到数据库，这样某天某个第三方出了问题（比方包含了挖矿脚本），就能立马找到那个项目依赖了，对于内部 npm 组件，谁使用了，也是很清晰，这样组件更新了，也可以企微，钉钉，邮件的方式自动通知到使用方，再大胆些，还可以每次发布前通过  puppeteer  跑下项目，统计了 性能数据，和之前的数据对比下，偏差太大也可以通知到对应负责人，让他检查下
06.   建立监控体系，监控体系可以简单，可以复杂，看领导的支持度，最基础的功能是，做 pageLoader 监控，意思是页面加载成功后上报下数据，表明当前页面是正常的，这样每次上线后，就通过消息通知到开发去观察 pageLoader 曲线的变化，这样就不会发布后， 2 眼一抹黑，也不知道线上是个什么情况，出了问题，也可以通过 gitlab ci/cd 立马回滚代码，这个是个很强的需求，基本上老板肯定是支持的，那线上出了错也不知道是啥子错，咋办，那我们把 线上错误上报上来，就很直观了，还可以结合 sourcemap 把错误和打包前的文件映射起来，便于定位问题，没人手就用开源的有 sentry，有人手的就自己开发
07.   监控建立起来了，是不是得做个报警机制啊，比方某个桥接更新了，和之前的不兼容，之前运行好好的的页面一直报错，错误上报达到一定量就报警起来，那就去把上报的数据捞起来做个统计分析，还可以结合 prometheus，做个好看展示曲线
08.   既然错误监控都做了，那把页面性能监控也做了吧
09.   哎，咋监控后性能数据这么差，是哪里出了问题，哦，打包文件太大，那 Webpack  得好好学习下，怎么拆分，啊，发现 http 请求时间太常，是不是 CDN 哪里出了问题，是不是资源没开启压缩，那这个链路还不熟，得好好学习下什么
10. 前端的监控都给做了，能不能协助下客户端的同学，把他们的 crash 上报，冷启监控都给做下
11. 要做上面这些，至少需要会门后端语言，会数据库啊，我擦，刚好上手 Egg.js Mysql 开发啊，之前不是学习 Node.js 没有场景使用么，一下子这么多场景来了，刚好带薪学习
12. 我擦，接了前端，客户端上报，请求数量一下子上来了，随手写的垃圾 Egg 代码，性能跟不上了，加班优化吧，不然不被骂死，还不行，加机器吧，加机器要做负载均衡啊，这个不会啊，赶紧学习去，是不是还需要做缓存，那还得学习下 Redis
13. 活动页天天写，可是有很多落地页都是非常简单的，每次都得 copy 个项目，然后改改图片，改改样式，太烦了，没有成长啊，那要不我来整个托拉拽生成页面，把这些页面元素都独立成组件，让运营自己去拖动，生成她需要的，这不就是个就是时髦的 「可视化搭建么」把自己解放出来
14. 简单的落地页可以这样整，那难的活动页咋办，比如 大转盘，红包雨，发现这些活动复杂些，简单的搭建不好解决，但是发现，这些好像也可以抽象，抽象成玩法的概念，那得加个配置中心来配置玩法
15. 发现每个项目组活动页有自己不同的 api，还有些活动会用相同的api，怎么办，每个人还不一样，我擦，这样配置中心用起来太麻烦了，是不是做个服务平台，把这些 API 都包成 BaaS，然后想用的人 自己谢谢代码来组合 api ，那这个要用 Fass 了，额，一步小心，做了个粗糙版的  Serverless

- 上面的 1～6 条是超过6个人前端组都可以干的事，大大节省人力，到现在我发现还有人，是把打包好的文件，拖动服务器上去了，人肉打包机
- 7～12/15人左右的团队必须上了
- 13～15 每个单拎出来都是亮点项目，非常提升人效，也是晋升，跳槽很好吹水的点
- 上面这些听起来没有大家常听的那些时髦，比如 SSR，微前端这些，很多开发者总想着搞些时髦的技术，实际上解决公司当下的一些同事常常抱怨，经常重复的地方，更是我们应该做的，围绕当下业务，解决当下问题

- 没kpi做了怎么办
- 蚂蚁的一整套中台体系就是这样，不过给后来人使用上做了很多限制，个人如果都能实现是很厉害的，也值得学习
