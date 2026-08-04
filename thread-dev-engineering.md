---
title: thread-dev-engineering
tags: [dev, engineering, thread]
created: 2021-01-21T17:51:54.496Z
modified: 2021-01-21T17:52:13.333Z
---

# thread-dev-engineering

# guide

# discuss-auth-account
- ## 

- ## 请问登录接口的 payload 中的密码在有 https 的情况下是否应该加密（比如 rsa ）？
- https://twitter.com/fuergaosi/status/1716812916123742501
  - [网站前端打API 时把密码加密，有意义吗？ - Huli's blog](https://blog.huli.tw/2023/01/10/security-of-encrypt-or-hash-password-in-client-side/)

- 不加, payload需要加个屁，上个前向安全的https就行了。
- 密码这东西从头到尾不就应该是一个hash值而已吗？又不是明文，加密是什么酷炫操作
- 一般都是向后端发送hashed password
- 这有什么争议，自己加密如果比https更安全更方便，那https可以废弃了。
- 加了也没法完全防 mitm 吧，和 ssl pinning bypass 一个道理吧
# discuss-architecture-cases
- ## 

- ## 

- ## 

- ## 

- ## Why Amazon Abandoned Microservices Architecture in Favor Of Monolith?
- https://twitter.com/milan_milanovic/status/1764566784680550654
  - In the latest post (check in the comments), a team that works on Prime Video explained their approach to ensuring that customers receive high-quality content. They use a tool to monitor every stream viewed by customers and use it to identify quality issues.
  - The tool was intended to run on a small scale, so they noticed that onboarding more streams to the service was very expensive. So, they decided to revise the architecture.
  - The initial architecture consisted of serverless components orchestrated by AWS Step Functions. They moved expensive operations between components into a single process to keep the data more transient within process memory.
  - After the analysis, they concluded that the distributed approach didn't bring many benefits, so they packed all the components into a single process. 
  - Moving their service to a monolith reduced their infrastructure cost by over 90% and increased scaling capabilities.

# discuss-exception/restore
- ## 

- ## 

- ## 服务挂了，有人建议要加强 review，我说，一般这种不是要加强 review，而是要有限保证 rollback。
- https://x.com/yfractal/status/1949789540924719204
  - 我们老板说，加强 review 也没错，我说是错的，保证保证不了 rollback，加强 review 就是错的。
  - 我说的很清楚，问题的可能有很多中，rollback 最可行。 然后今天又有人操作失误了。

- 最水的复盘就是“加强责任心，以后会更加注意”
- 加强review可能只是口号，如何保障review的质量？如何保证快速修复，如何规范操作步骤，避免人为的错误和快速恢复才是根本

- review很容易犯于形式，我们通常要求的是必须测试，PR附带测试截图要不然review不给过
  - 职责也不明确，review 过了，出了问题也不好说算谁的。

- 服务器为什么不使用nixos，声明式的图灵完备的编程语言管理配置，系统即代码一键部署，出了问题可以在Boot时选择任意generation rollback或者直接`nixos rebuild --rollback`.
  - 因为有些状态不是在服务器本身，比如数据库的表结构，消息队列的任务

- 出问题了首先rollback止血 事后再RCA解决，rollback这种操作不是很平常吗？
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 软件领域还有一个轮回：
- https://x.com/xicilion/status/2080908639540297914
  所有的软件最后都需要配置；
  所有的配置最后都需要配置文件；
  所有的配置文件最后都会走向工作流；
  所有的工作流最后都会走向可编程；
  所有可编程的工作流最后都会图灵完备；
  这个轮回出现过很多次，现在是另一次。
- 这个规律很早就被发现了：(1)Postscript是个语言而不是格式，所以固化在打印机等机器ROM里的PS解释器不用修改，只要对文档进行PS编程就能实现未来所有文档的需求(2)i386启动时先进入实模式，再执行实模式的代码来配置保护模式的参数，最后再进入保护模式，这样也获得了无限的配置能力

- 是的，配置文件都巨复杂，然后你就发现，他妈的，那已经不是人写的，而是机器生成，然后背后有一套别的什么东西在生成

- ## 我就是在做业务页面开发的! 写表单写表格、调接口、改样式、修兼容!
- https://x.com/hd_nvim/status/1950038562948182443

- ## 项目久了就会有很多性能问题堆积了。你们一般多久治理一次？
- https://x.com/__oQuery/status/1927380807946993856
- 扶老人悖论 -- “不是你写的bug，你为什么要修”，测试不报，从不治理

- 老板非常认可价值&工作舒适: 每个 PR 都尽量注意性能
  - 业务迭代压力大|暂时没那么重要: 劣化到一定程度专项治理
  - 老板不认可价值: let it be

- 能用钱堆机器解决的，绝不去改代码

- 性能问题已经影响到主流程使用了，才会修一下。

- 一般来说，我经手的项目活不到需要考虑性能问题的时候

- ## If you build a similar tool for another ecosystem, don’t just tweak the original name (like Remix to Vemix for Vue).
- https://x.com/adamwathan/status/1906371401608491459
  - Things will inevitably diverge and you will regret it. You’ll have to work way harder to get credit for your original ideas, because it’ll always look derivative.

- ## 学过的最有用的算法： 分治法和穷举法。 
- https://x.com/mrpanda88888888/status/1905894687904342173
  - 小规模问题就用穷举就完事了
  - 大规模问题用分治法个个击破
  - 其中，分治法最为神奇，你可以横着分，也可以纵着分，可以层次分，也可以树状分，总是有各种分法，大道无形，却又变化无常。

- 编程里学到的思维，甚至都有影响到我在生活中如何处理问题。。习惯性的把大问题拆成小问题，逐个解决

- ## 之前在腾讯云/火山云各呆过一段时间。从我的视角来看，二者的 SDK 产品都是有点草台班子
- https://x.com/xiqingongzi/status/1885720224168820938
  - 不过还有所不同。腾讯云的 SDK 实际上是代码生成的，写的时候也没那么用心，导致出现了很多奇奇怪怪的设计。老哥喷的也只是其中一部分，细看会有很多设计很奇葩的逻辑。
  - 火山相比之下好点，是一个牛逼的草台班子
- 其实写sdk这事情技术含量略高。因为是公开的代码，没法隐藏草台。再者这事情不计入kpi，导致没人重视。
  - 是，主要是不计入 kpi，我之前在开放平台 infra 工作，雀实比较难拿到 support

- ## Serverless is dependency injection at the service level. 
- https://x.com/earayu/status/1872487948756873640
  - Users don't want to worry about how services are built - they just want to use them. This is similar to how, at the code level, developers don't care about object construction - they just want to use the objects.

- ## 一个项目过了最佳重构期，再重构就很难了, 用户量一上来全是 breaking，重构零收益，只能缝缝补补走到生命周期的尽头
- https://x.com/Soon_Iter/status/1856958579003330866
- 最佳的重构时间只有在项目设计初期, 已经被breaking折磨了
- 缝缝补补能过就过，有时会发现补着补着还越来越好了

- ## 这些乱七八糟的各种框架究竟有用吗，到底厉害到什么程度？我Uniapp写的App，每一页都是屎山一样的上千行代码
- https://x.com/JohnnyBi577370/status/1848339083925537253
  - 就这样，2008R2 32G内存的服务器，内存也很少超50%啊
  - 所以，这些高大上的框架究竟是给什么项目用的，真的随便一个APP就能几百万用户吗……我是真不懂，所以一直没有动力学习，谁能给我解释解释

- 一群猴子在公司表演。 如果天天无所事事， 会被老板开掉的。 搞搞框架， 搞搞性能优化， 忽悠一下老板

- 对开发体验有影响。 比如大项目从 Webpack 切换成 Vite，体验提升是巨大的（当然也会有新问题）。 再比如从 JS 切成 TS，类型相关的运行时错误也基本杜绝了。提升也是巨大的。 至于用户侧，感知可能不强。

- ## almost all of debugging is
- https://x.com/jarredsumner/status/1842554089751941224
  - why isn’t that function being called
  - why is that function being called
  - why is that variable the wrong value
- If you adopt OOP you can make that list at least twice as long

- ruby debugging is:
  - where is that method defined
  - god damn it where is that method defined
  - giving up and running `RubyVM::InstructionSequence.disasm`

- ## Debouncing everything externally is a pain. Debouncing by default internally would make realtime laggy. 
- https://x.com/gaforres/status/1803137618063868361
  - One usability issue I've discovered with Verdant here is dragging things. With direct manipulation, you get a ton of little changes. 

- ## 最近 10 年，后端 breaking techs 好像并不多。
- https://x.com/yfractal/status/1799662451040092603
  - Docker/Kubernetes，io_uring，eBPF，OpenTelemetry，HTTP2，GRPC。
  - 存储还是老样子，不好用，但也还能用。Redis 依旧单核。
  - RDMA、NVM，工业上几乎见不着。
- rdma其实大厂鸡架落地应该蛮多的。其他team没有落地的原因在于，还有别的kpi可以拿，比rdma要容易。目前其实我感觉正处在系统软件，从“泛化”到“特化”的一个阶段，从数据库市场现在越划越细就可以感受出。
  - 嗯，查了一下，RDMA 确实支持的挺多的，我没留意到
- 特化没有前途，你看高达都是通用型机暴揍特化机。
  - 硬件增长趋于尾声，泛化不能依靠每年翻倍的硬件性能来维持住用户体验，里面有很多不高效的部分。最好的例子就是数据库，以前没分这么多吧，现在TP, AP, 时序，流，向量。
- 历史上特化产品很多时候不知道怎么就死在了能力更强的通用产品上，一条边的纸面数值更高，碰见每项指标都稍微差点的通用六边形战士就很难受（向量产品怕不怕一个 pg？），各种专业的工作站大型机小型机之前单一维度的优秀数值在今天的通用 PC 面前都是渣
  - 特化的专门硬件一般不好卖吧，客户直接被绑死，升级换代只能任宰
- 特化的 infra 软件也很捉急，之前有段时间有 unikernel 的概念，没几年就都死透了，大家都宁愿裁剪通用的 linux kernel 也没人玩专门领域的 unikernel
- 特化也是分程度的，看市场的，我自己也不是很看好向量数据库。不怕碰见pg，因为有pg vector，这里面有他们自己的考量吧，不好评价。

- 这里列举的感觉都是基础层的东西，越来越稳挺是必然的。如同汇编语言上个世纪都同样稳定了如今的焦点应该在更面向业务的层面了。业务需求变化后，后端的变更理论上需求方需要的是一天内实现
- 还有就是性能提升的性价比，假如是逛淘宝，假设我把图片加载从10ms打到1ms，用户能感受到吗？用户愿意为这9ms 付多少钱？io_uring 能打下来一些延迟，但代价是重构整个存储base的代码，没人愿意干的，还必须把需要的内核版本拉高

- 前端也不多啊，AI 部分除外。应该说软件工程可能达到了平台期了。没有明显的短板需要解决了。

- raft/paxos，终于可以不用担心数据库没有及时同步丢数据了

- 因为大厂也不想养造轮子的了

- 三大云infrastructure里面早就全是rdma，nvm，dpu，dpdk

- RDMA已经是AI训练的标配了吧

- ## 不建议使用Serverless的方案，平台绑定性太强。
- https://x.com/ahshengchen/status/1797295416159162443
  - 随便选个顺手的后端开发框架，使用PaaS方案部署，然后再选个云数据库（配合Navicat客户端），这样功能开发完全不受限，也不用运维服务器

- ## 程序员要会的通用技能：
- https://x.com/llennchan2003/status/1796803079159030186
  - CURD（最常见的）
  - 高级CURD（异步，分布式，多线程）
  - Hacking（操作系统底层，数据结构）
  - 数据分析（分类，回归，聚类）
  - 3D（计算机图形学）
  - 感觉会了这5个方面，基本上认知可以覆盖所有软件了，很少会有认知之外的魔法了。（除了PL/编译原理/数据库底层，这个ROI太低而且通常是透明的，感觉不是必须学的）

- 计算机图形学是3D? 欢迎你来到数学物理的世界！光学！矩阵，光追，线代，数分！新世纪的大门在给你敞开！很快你就知道cs只是敲门砖，伟大的物理世界欢迎您的礼炮已经打出

- 我觉得这些都可以在需要的时候补课，而且相关技术栈过时很快。最需要的是抽象能力，其次可能是组成原理、操作系统、数据结构之类的东西。

- 学得再多也没用，如果你不是名校出身，一线大厂工作，CRUD已经完全够用了，你想用其他的也没机会用，普通人就死磕业务能力，把自己牢牢绑在一个可以长期做项目上，这是最好的结果。

- ## 过早的优化是万恶之源。我认同的优化只有一种，让现有代码可以随时被丢弃。
- https://twitter.com/xqliu/status/1777600103987200371
- Docker+PostgreSQL+express+react+iOS+Android一把梭，这技术栈可以支持到赚到$100million的时候，再换k8s。很多人都是业务赚不到几个钱，技术栈高级的不行。

- ## An interesting recurring theme in data infra: protocols/APIs outliving specific implementations.
- https://twitter.com/gunnarmorling/status/1716878504044998914
  - E.g. #Kafka wire protocol (#RedPanda, #WarpStream as alternative providers), S3 API (#MinIO, #Ceph, etc.), #Postgres protocol (too many to list even).
- Dynamodb, Cassandra/Scylladb

- ## 刚读完了这两篇关于 xz-utils 包的供应链攻击说明，攻击者潜伏了三年，很精彩，只差一点点就可以往众多 Linux 发行版的 sshd 注入后门，可用于绕过密钥验证
- https://twitter.com/Blankwonder/status/1773921956615877110
  - 攻击者 JiaT75 (Jia Tan) 于 2021 年注册了 GitHub 账号，之后积极参与 xz 项目的维护，并逐渐获取信任，获得了直接 commit 代码的权利。
  - 初步的研究显示，注入的代码会使用 glibc 的 IFUNC 去 Hook OpenSSH 的 RSA_public_decrypt 函数，致使攻击者可以通过构造特定的验证数据绕过 RSA 签名验证。
  - 只要是同时使用了 liblzma 和 OpenSSH 的程序就会受到影响，最直接的目标就是 sshd，使得攻击者可以构造特定请求，绕过密钥验证远程访问。
  - 幸运的是，注入的代码似乎存在某种 Bug，导致特定情况下 sshd 的 CPU 占用飙升。被一位pg commiter注意到了，顺藤摸瓜发现了这个阴谋并报告给 oss-security，致使此事败漏
- linux发行版要进行全面安全审核太难了，安装了这么多开源软件，每一个开源软件又引用了无数开源库，这其中每一个开源项目都有可能被恶意人士参与注入后门，这样看来，商业公司提供的系统比linux发行版更安全，至少参与开发制作的人数固定，出事了一个都跑不了。
- 看来CPU飙升的程序都得小心

- ## Backend Performance Best Practices 
- https://twitter.com/kamrify/status/1772381600442908865

- ## 没有大段完整时间和直接需求打过来，确实不太容易自己独立写出一个有用的软件。
- https://twitter.com/tison1096/status/1768857505827057935
  - 详情可以参考 BeyondStorage -> Apache OpenDAL 的演变。
  - 尤其是数据系统，很多时候个人想写太复杂的自己也用不上，如果不在团队里，还是写个 Redis / PG 就挺够用的。

- ## 最近上手写 Intellij Plugin，能感受到 IDEA 内部代码有多屎... （甚至还没碰到 PSI）
- https://twitter.com/kirraObj/status/1768567112661152236
  - 文档少得可怜 / 没有参考性，开发过程中几乎是有大半时间是去翻看 Github 现有仓库的实现
  - 翻到贴合我的需求的相关文档有一个参考 repo 链接，上次 commit 时间是十年前。
- 不同版本api的兼容性也很差

- ## What's your favourite coding font?
- https://twitter.com/JoshWComeau/status/1763587415539597433
- It's https://monolisa.dev. I've been jumping on and off different monospace fonts for years. MonoLisa is what finally made me happy. It's a phenomenal font
- Using Hack Nerd Font Mono currently. It's nice. Doesn't have ligatures but not a fan of them personally.

- ## Do people still follow the 80 column width rule for code?
- https://twitter.com/sunbains/status/1762593260927873110
- Yes, it makes the code much easier on the eye. Helps in readability.
- I stick to 80chars pretty religiously. It's easier to read tall and arrow text. Also let's me keep a bunch of stuff visible on the screen at once.

- If you work on a large monitor (>24 inches) most of the time, having a 100-120 column width is reasonable.

- ## I feel automatic dependency management actually does more harm than good
- https://twitter.com/gunnarmorling/status/1759294666699092049
- I wish there would be an option to disable transitive pulling in Maven/Gradle. Would make this a much more aware process to library creators and consumers alike
- Plus Maven plugin dependencies for the same things, in different versions - Yay spaghetti

- ## Nice DuckDB feature. More applications should do this
- https://twitter.com/lukaseder/status/1757693702074450336
- There is a File Leak Detector, a Java agent that collects such info and makes it available to observability tools and users. It would be nice if it was able to automatically augment the exception throws

- ## The Express.js repo got swamped with spam PRs thanks to a YouTube tutorial gone wrong. Hundreds of low-effort contributions flooded in, creating chaos for maintainers.
- https://twitter.com/feross/status/1757463614532071545
- One simple CI bot could’ve cleaned it up and kept it clean

- ## What is the preferred way these days to add dev-only code to libraries? 
- https://twitter.com/buildsghost/status/1757111425129181693
- I'm still using `process.env.NODE_ENV` checks. Keen to know if there is a better way

- Using the development export condition, Which also works for imports.
- Oh good, the three environments "production", "development", and "browser" all mutually exclusive
  - None of them are mutually exclusive. Conditions can be combined using nesting. it works and it's widely supported

- ## 自己的项目里维护一个 TODO点儿md 确实很有用，突发奇想的话就往里面写几笔，有更好的想法了就慢慢细化，等哪几行已经细化到可以动手了，说明就到了能开始TDD的时候了。
- https://twitter.com/geniusvczh/status/1754440582196568066
  - TDD有一个好，就是提前自己的设计到底能否经得起简单的考验。如果连test case都写不出来，那这个设计的API或者业务逻辑，都得扔

- ## 人月神话在现代互联网公司人海战术前是失效的。
- https://twitter.com/tison1096/status/1748561397330436300
  - 我以前一直拿人月神话和大厂人海战术做对比，不幸的是现实的情况就是这里面说的是对的。软件质量在这里面并不重要。
- 前面积累下的债都是要还的，况且最开始其实是赚不到什么钱的，只是在拼命扩大市场份额，等到想赚钱变现的时候发现人月神话是真的，质量差用户不买单，加新功能的工期越来越长，即使是有垄断地位的大厂也逃不掉

- 这个主要是因为之前国内技术跟海外有代差，直接抄跟胡乱堆就能抢占市场。现在存量竞争要做得好才能赢过别人，且技术代差红利消耗殆尽以后，就会进入需要强调工程和创新的阶段。
  - 昨天有位大厂职员跟我提到内部业务老大觉得做技术创新毫无意义，利用垄断地位调个参数就是几个亿的收入。但这是有尽头的。
- 等到了你说的尽头，经济下行，大规模裁员，他们守住存量市场慢慢躺着吃就好了。市场早就被他们连锅都端了。
  - 是啊，我没说他们不行。实际上我当时回复的后半段就是，他们做出这种判断是因为过去十几二十年也没遇到什么挑战。

- ## 要逐行读取1亿条数据的一个大文本文件，然后每行读取后还要写一条数据，
- https://twitter.com/geniusvczh/status/1746882251449835938
  - 折腾了几个小时换了无数种办法，读取速度都上不去，换了Parallel. ForEach(C#)后，直接跑满CPU，1分钟500万条写入
- 很奇怪哎，这种IO密集型的东西，瓶颈怎么会在CPU上，硬盘速度 >单核CPU？
  - 是的，我一开始也很奇怪，后来想明白了，磁盘IOPS 1000K，10万条Bulk一下写库也就1秒，但是1秒读出10万条数据来并处理好，单核还真是难搞
- 在一般的架构设计里，一个core或者cluster的数据口子无法把全部ddr带宽用满。
- 难道下意识不应该试试，先单线程用映射对象读文件，然后一个semaphore控制内存用量做producer consumer，最后多线程处理吗。这样写依然无法最大程度利用硬盘

- ## “云厂商已经做得比自建要好。除非你的体量能达到百万台的机器规模，那就自建” —— 按这个标准，移动联通百度都不配自建了。
- https://twitter.com/GobeUncleWang/status/1746375638662221969
  - 2022年中国算历规模现状
- 满嘴跑火车这是，百万台才下云，那 basecamp hey  完全没必要下云了，但是人每年省了好几百万上千万美元…

- ## 研发资源是真的特别特别昂贵的。 工作里我这十年干的最多的事儿，就是反对技术团队自己造轮子。 传统行业 99% 的场景不配自己造
- https://twitter.com/iamshaynez/status/1743177430377042090
- 有时候单纯把轮子组装起来也很贵
  - 还很异构; 最惨是有现成的，一天上线，然后搞明白比重写时间还长

- 哈哈哈自研过轮子的也觉得这事情绝大多数公司不配也不需要…

- 我支持造轮子，但是只限于自己用，把自己造的轮子藏在看不见的地方。我反对造轮子给别人用，尤其是框架轮子。你何德何能，写个框架让别人往里面塞代码。

- 这里可能有个悖论, 自己造轮子 研发成本高, 不自己造轮子 显不出技术“高明”, 结果是 996 劣质轮子 遍地都是…

01.                        大概率没有开源的好
02.                        造轮子就要维护一个轮子迭代维保团队
03.                        迭代维保团队和其他团队无限的撕逼

- ## Five terms I avoid when naming things:
- https://twitter.com/housecor/status/1742197661837476018
  01.   data
  02.   info
  03.   item
  04.   object
  05.   entity
- I settled to referencing DOM elements with a $ prefix, after tying various things for years, El suffix being one. I think it’s easier to read, it’s faster to type, and better for having good IDE suggestions quickly (one keystroke and it already suggests DOM elements only).
  - Seems like a $ would make it too easy to confuse with jQuery objects and other libraries that prepend with that character.

- I avoid “manager” in names (occasionally it makes sense). Manager objects tend to do way too much. Too many responsibilities.

- user and userEntity might be valuable, where user exists in your domain model, and userEntity exists in your persistence model. Otherwise, you end up having to use fully qualified names, or aliases to differentiate between them.

- ## 🏘️🤼🏻 Realised I make modules/structs/objects much smaller than they need to be in side projects. 
- https://twitter.com/LewisCTech/status/1736887803236282672
  - I think it's in overreaction to all the "legacy code" I've worked with that goes too far in the opposite direction, and this is my brains way of trying to cope with Abstraction Deficiency.
- With time I noticed that all goes into a single global structure; the main reason is that in the beginning its easy to split roles and responsibilities.
  - As soon as you start chasing edge cases the idea of solving everything with messaging begin to sound totally unreasonable: why should I have n components that are involved in a process exchange information with messaging while they all share the same state?
  - And then you clearly understand why Linus Torlvalds opted for a monolithic (but modular approach) vs a microkernel and messaging approach.
  - At the end of they day its just a complex state machine; with state machines anything can be tamed (just think TLA+).

- ## 🟥 请教下大家你们都是怎么用redis的？ 单进程模式？好像20万QPS差不多是个上限，万一不够了怎么办？
- https://twitter.com/plantegg/status/1720257779313856648
- 以前公司（业务量大但没那么高可用要求）：
  - 拆分必做，甚至一开始就做拆分（1 shard），无主从，做下一致性哈希。
  - 主备看 cache 还是 persistence，p 开下 rdb aof 能找回数据就可以，高保业务做主从。
  - 多可用区：不做，挂了就挂了，业务应用都没有容灾呢。
- 现在：交给数据中间件团队或者云厂商

- 我目前做的业务，就是拆分，6台redis，各个场景做了隔离，redis集群模式qps还可以提升，但有一些功能局限性，这要根据业务去判断。
- 拆分是指的按业务拆分还是不同的key hash到不同的redis实例？按业务拆分本来就挺正常的吧，互相不影响，好维护。
- 集群模式下一些功能不支持，比如hyperloglog 不可跨slot计算，这个我们业务用的比较多，我主要是按负载情况和业务场景来拆分。

- 这个主要还是看业务场景，读写比例和用到锁和不用锁差异都比较大

- 要排查大key，看慢请求

- ## ERP软件打成镜像，因为软件包太大到好几个G，所以发明了启动base镜像+初始化拉包。在金融行业还挺流行。
- https://twitter.com/xds2000/status/1725294546727153717

- ## [新人也能懂的调试方法 01 - 通过 syscall 进行定位](https://blog.dreamfever.me/posts/2023-10-24-how-to-debug-01-syscall/)

- ## Twitter现在的代码行数减少了90%
- https://twitter.com/skywind3000/status/1720778734922342786
- 看他们几篇文章，主要是砍掉了两个最近两年臭大街的东西：微服务+云服务，微服务最大的问题就是过度设计，明明一个进程里调用两个函数就能直接解决的问题，偏要做成 N 个接口互相调用；明明一件事情顺着步骤就搞完了，非要弄个管道，分成多个服务多个异步状态来处理，大多数除了让代码量膨胀外别无他用
  - 当然，可能也砍掉了很多内部不能盈利的子项目，子功能。

- 还有一个问题就是滥用异步方法。异步有异步的好处，但不是所有请求都适合使用异步方法，有的调用就应该同步返回一个明确的执行结果，但是很多接口全部做成了异步的，反而引起很多问题

- ## This is why we at Infinite Red have team lead as a fluid position (we call it “primary”). 
- https://twitter.com/jamonholmgren/status/1719588874715042200
  - That is, someone can be a team lead with someone else working with them, and then in the next project their roles can flip. 
  - It’s much less about their experience level and much more about what they want and the project’s needs.
  - Even great team leads want to just code and let someone else deal with meetings and requirements. So we have this one dev who was leading a project for 4+ years. He just wrapped up, and now he’s a secondary dev on a new project and loving being able to just code.
- My employer does something similar by spreading mgmt responsibilities among ICs:
  - team lead: mentorship/advocate for people
  - task lead: PM role, scoped to single project. Still able to code, often also tech lead.
  - Works well, lets people try out roles.
  - Also interesting: project leadership structures ignore the org chart entirely! CEO will report to task leads when working directly on contracts like anyone else.

- ## 说老实话，有实时Preview真的快了好多。
- https://twitter.com/JidanzaiDashan/status/1712063417652011083
  - 打算把项目拆成两个workspace，一个workspace专门preview，iOS 17+ only（不然预览不了UIKit），再搞一个blank project测试一些需要真机手感的东西。
  - 另一个workspace专门负责打包。

- ## Designing an entire MVP without any design!
- https://twitter.com/puruvjdev/status/1710731659535118552
  - Trying something new for once, to ship really fast. Gonna keep this design unstyled while finishing up the logic and everything. And then at the end sprinkle in the style
  - I did this once with neodrag.dev where I built just the unstyled kitchen sink demo, and that shaped the entire website and the logo as well. Hoping to hit that same sweet spot here as well!
  - Update: Added picocss.

- My preferred development order has always been:
  01.         Structure for everything: HTML, content, ARIA, some JS
  02.         Style a component: CSS, interaction states, transitions/animations
  03.         Then make the component functional with JavaScript
  04.         Repeat steps 2 and 3 for each component.

- ## uid 不需要可读性，如果需要可读性可以添加一个新的 id 属性。
- https://twitter.com/ThaddeusJiang/status/1694915724354142678

- ## Nothing beats console.log for debugging.
- https://twitter.com/DwayneCodes/status/1687574301200003072
- closest friend: `border: 1px solid red` ; 
- console.table

- ## Declarative APIs are simpler because they come with a lot of implicit concepts that actually makes them simple.
- https://twitter.com/oleg008/status/1686292446651543552
  - Imperative APIs may be more complex when they expose more direct control of these concepts.
  - Declarative is not better than imperative. Its a simplification.
  - Declarative makes simple things easier, but complex things much harder. Where imperative may make simple things harder than necessary, but then make complex things more doable.

- ## My dev Tips: 使用 docker compose 启动 local db，并把数据存储在当前文件夹 ./local/data
- https://twitter.com/ThaddeusJiang/status/1683697085361836033
  - [docker compose local postgres db](https://gist.github.com/ThaddeusJiang/59afe351b4cb88e5b828d0b99418ab8e)

- ## 才知道VSCode提供了扩展二分查找功能。它能禁用一半的插件，然后问你能否复现问题，再禁用其一半，如此反复，直到找到导致问题的插件。
- https://twitter.com/RikaKagurazaka/status/1682770407634632706
- 对于老司机来说大多数情况是直接用 empty 的 profile，再打开怀疑可能有问题的插件或者设置会更快。这就和 git bisect 一样，当可能有问题的提交数太多的时候，容易把自己搞晕

- ## So, metrics. Push or pull?
- https://twitter.com/gunnarmorling/status/1682454573015871488
- I feel push is more efficient but the nice thing about pull is you can see an explicit log entry for when the pull failed. It’s a little easier to troubleshoot IMO
  - Yeah, also rate limiting seems much easier with pull.
  - That too. But I could see pull at large scale becoming difficult as well managing multiple pull agents. Maybe if 1 pull agent is enough pull is easier. But once you need multiple pull agents push is easier? Thinking out loud
- Pull. Hard to scale histogram with push.
- Pull on long running, push for jobs/tasks

- Prometheus is the answer
  - Supports both actually
- Pros and cons on both. Hybrid.

- Pull, because then the metrics server is in control and has the responsibility
- Async push, synchronous pull

- ## 一般做一件更傻逼的事儿，然后修正，大家会忘记之前有点傻逼的事儿。比如现在，很少有人讨论推特不登陆不能浏览了。
- https://twitter.com/yihong0618/status/1676530968096833536

- ## 最近一直在重构屎山，让我明白一件事
- https://twitter.com/Ehco1996/status/1676513295166246912
  - 你以为的理由：代码实现太挫，风格混乱，缺少 UT
  - 实际上的理由：屎山堆不动了，一加新功能就出 bug 测试一次要两小时起步，再不重构一天到晚全是 oncall，没人力可以交付新 feature 了
- 键是搞这东西对KPI没有帮助，关键业务指标无增长，费力不讨好
- 如果工作量比较大，还是要老板支持才行

- ## Take YouTube as an example. Backend sends all the data in 100ms for the landing page, logged in. Frontend then takes ~1500ms to present that data to the user
- https://twitter.com/nikitonsky/status/1675505359052500994

- ## 以前还很菜的时候就很喜欢过度优化，喜欢学各种高大上的东西，
- https://twitter.com/null12022202/status/1673252095473102849
  - 后来稍微没那么菜的时候知道合适是最好的，目前公司业务的体量，再过些年也用不到k8s这些，后端服务用单体架构就足够公司业务很久了，事少还省心

- ## 我视能不能解决庞大的屎山为新手老手的分水岭
- https://twitter.com/Soulogic/status/1659386692904816641
- 软件工程师 3 个进阶的思考维度，也是任何严肃的系统，从设计阶段就应该考虑的：
  01.             Debugability, 运行中出了错误，是否能快速定位到根本原因？
  02.             Testability, 重构了代码，任何原因修改了代码，是否可以保证没有引入 bug.
  03.             Toolability, 性能有问题，是否可以很快用自动化工具定位到瓶颈。

- ## Tip: Write a design doc (what, why, how, whatever) for any feature you are going to implement. 
- https://twitter.com/evoluhq/status/1261766649679667208

- ## unpopular opinion: I don't like OSS monorepos. They bias toward maintainers over users & contributors.
- https://twitter.com/swyx/status/1292471675712188416
  - git history a mess
  - documentation a mess
  - github issues a mess
  - hard to stay disciplined on dependencies
  - cryptic tooling is a barrier to contributing

- Maintainers are the lifeblood of software, let alone open source. Those downsides are real but optimizing for authors has trade-offs like anything else and often nets out positive all things considered.

- ## I recently got the chance to mentor a few junior developers.
- https://twitter.com/kmuenster/status/1655790446621384704
  - (1) “Return Early” Instead Of Nested Conditions
  - (2) Writing Code For Humans (easier to read)
  - (3) Hiding Information Behind Functions

- ## 这两天技术圈头条的【Amazon的流媒体平台 Prime Video 从微服架构到单体架构”】
- https://twitter.com/haoel/status/1655514399753531392
  - 我以为 Prime Video 遇到不是技术问题，而是AWS  Step Function处理能力不足，而且收费很贵的问题。
  - 如果 可以无限扩展且白菜价，那么他们还会有动力改成单体吗？会不会反过来吹爆 Serverless？
- Microservice 每次 I/O 实在是加了太多 overhead, Monolith 的确更适合这种用例
  - 可能表达不准，想表达文件 I/O。 每次 step function 启动要去 s3 里要文件然后才开始工作，就好比在一个办公楼，一个人去负一楼一百次拿资料走楼梯回到二十楼坐下来工作，和一个人在隔壁拿资料开始工作一个感觉。 他们这种用例就不太适合水平的架构，垂直的更节约成本。
- AWS Step function本来就不是这么用的。任何一个考过AWS developer助理的人都知道step function的应用场景是github action/bitbucket pipeline那种逻辑分步处理。通常单步处理时间至少是秒记。
- Serverless就是为了满足一个极端审美，大多数场景都是反而浪费低效的东西。类似你自己内存的hashmap效率把redis吊打，因为一个就在内存，一个网络通信。
- 上来就serverless太容易出错了. 比较保险的做法是Modular monolith first. Serverless later.

- ## Filesystem watching libraries that assume if the file size didn't change then the file didn't change
- https://twitter.com/tantaman/status/1651584027025915905
  - Wasn't a filesize issue and actually turned out to be a bug in `fswatch` o_O -
- IIRC, `rsync` (fast) does size + modified as a heuristic. To to better than that, you  probably have to hash I think?

- ## If you're a senior JS dev, you should be able to jump in and add a feature or fix a bug in a codebase the first day on the job. 
- https://twitter.com/zachcodes/status/1651057366647939072
  - his is the moment you know you're a senior dev. 
  - It's all just JS / TS in the end, with an api reference for whatever framework is being used.
- When you know how a browser works, http requests, json, html, css, js like the back of your hand….. most projects require zero time for a senior dev to jump in and get going. Especially if it uses a common library like react or nextjs. 

- If the code well written, then even junior devs will able just right in. I find this a really good measurement for how clean your code is.

- ## 之前为了统一接口把所有消息包括外部请求和内部回调都扔到一个channel里, 会增加消息之间等待, 导致该做的事没赶紧做. 
- https://twitter.com/drmingdrmer/status/1650781883943510016
  - 现在把它拆开成内部外部2个channel, 性能提升了1成

- ## 我们一个服务为了性能优化花了30人月全部重构：串行改并行、同步调用改异步调用，效果相当明显整个RT 从200ms优化到了100ms，但是QPS没变，架构师被老板叫到会议室臭骂了，
- https://twitter.com/plantegg/status/1650726735657447424
  - 我们这些小码农也不知道怎么回事，反正这个月我们996班没少加，活完全按照架构师的设计完成了，我也不知道怎么回事
- 应该换个故事，QPS没变，RT也没变，但是省了xx台服务器。老板听了眉开眼笑。
  - 反手就裁掉一波员工
- 这个处理速度上去了，但是上游下发的业务没变。从工程的角度，也不一定是优化，异步的代码维护是个难题
- 不是这个原因，大并发系统直接串行改并行其实大部分时候并不提高QPS的…
  - 因为串行改并行只有在资源未充分使用（比如CPU大量闲置）提高资源利用率，如果本来并发就很高，本来资源就用满，串改并对吞吐量没什么用的。
  - 如果重构目标是单个请求处理时间，他这次重构成功了，如果是吞吐量，显然方法不对
- RT优化体现了编程能力，代码能力，这是程序员指标，代码优化带来的QPS提升远不如架构优化和重构带来的提升，甚至需要反复重构来达到QPS提升，这考验的是架构能力，是架构师指标，所以架构师被骂也不奇怪呀
- 瓶颈如果是在后端数据库的话，那么这些改动是无法提高QPS的，这也是古早年代的异步框架tornado懒得提供数据库异步接口的原因。

- ## 在线文档等Web富应用，在没有经验的时候很容易忽视内存管理，比如DOM数量过多，内存泄漏和内存不合理的使用。
- https://twitter.com/yeshu_in_future/status/1642032791444656129
  - 它们和传统页面的差异在于，应用往往会常驻在标签页中，生命周期更长，用户的使用时间也更长。
- 有一些常见的优化思路：
  01.          关注事件绑定，无论是抽象的event bus 或是 dom 事件，都要在必要的时候解绑
  02.          关注DOM数量，理想情况是不会预期外的增长
  03.          关注一切可复用的变量，比如组件不要反复销毁重建，复用渲染；对象的key如果要用字符串拼接，可能不如拆开几个map 或者用二维数组，比如表示表格单元格的位置和值；避免重复渲染大量svg icon ，基于id 复用，等

- ## When polishing creative work, I can often get into decision paralysis about the priority of things to fix.
- https://twitter.com/aboodman/status/1648835192285704193
  - My solution: embrace that I'm not going to stop until it's perfect, so I might as well start at the start and go through them in interaction order 😂.
  - The mindless "find a problem, fix a problem" loop is much more fun than trying to prioritize. It's also gratifying to see the product start to crystalize from the beginning. After you fix the very first bug, you haven't got much, but at least the very first interaction is perfect ✨.

- ## 以前每次想写点东西总是想把问题的逻辑结构用线性的文字呈现出来, 
- https://twitter.com/drmingdrmer/status/1645063507044605952
  - 类似把平面上的几个点编码到一条直线上再让读者还原几个点的位置, 然而这种降低维度的操作很容易丢失信息而造成解码出错, 以至于要非常小心非常累...
  - 最近突然想写点工作无关的东西, 才发现像gpt那样不用管对错的码字好轻松好舒服啊
- 先写再改，你考虑再周全也抵不住大家基础、背景不一样理解角度不一样，别想这一次到位会轻松很多
- 具体细节的文档懒得看，因为实现永远跟细节有出入，等碰到问题再看代码不迟。描述算法的文档看不懂，因为绝大多数人都基础太差。所以写文档写注释唯一的目标是未来的自己。

- ## 软件工程师就像建筑工程师一样，需要图纸才能把产品完工。
- https://twitter.com/tualatrix/status/1644224900603977729
  - 我终于明白我做了七八成后做不下去的原因了，因为还有两三成没有图纸（脑海里也想不出来）了…赶紧打开 Sketch 开始画图。
  - 本质上我没有「图纸」的原因是我既不愿意和自己沟通，也不愿意和别人沟通，于是就这样卡住了。一旦我和自己和解了，这个任务也能顺利的进行下去了。

- ## 技术研发几大困境：
- https://twitter.com/brabalawuka/status/1643267406255771648
01.     产品要想上新功能，新功能最好做一个技术优化再上，不做技术优化就要上得很丑陋，结果决定先上个很丑陋的版本
02.     技术优化的版本只支持新版本，所所以服务端不得不保存两份代码，或者按照客户端版本写一个很丑陋的if else向前兼容。
03.     重构屎山，漫长的重构中，旧代码不断有人修改，更新添加新功能。重构的部分不断rebase，帮再写一遍代码，心态爆炸
  3.1 为什么上一条要这么干？重构理论上应该不断进行分批merge，但是分批merge不能体现重构整体对于性能，延迟，指标的impact，不得不最后一起merge，然后把整体指标进步摆出来当绩效
01.     unit test 写的跟屎一样，改了一行代码发现几百行的function unit test过不了了，然后画一天时间改unit test，重新写unit test。unit test 层层mock，最后出bug的地方被mock掉了没发现。
02.     改了一行基础库，更新一下基础库版本，发现库里面其他module有breaking change，于是花了一天时间适配。。
03.     客户端说应该服务端应该做，服务端说应该客户端做。产品需求有点离谱。上升到大老板，大老板说两边都应该改，适配起来最好。他选择了没有任何人满意的解决办法～
04.     关系型数据库发展到最后就是一个巨型的blob字段，里面是个大json～ 然后新字段就往里面加，反正一个小需求也不能动数据库不是？

- 我的经验是如果没老板支持，尽量不要做屎山重构。这个支持包括但不限于：
  01. 只定里程碑不看具体排期
  02. 允许小步迭代和返工
  03. 允许拖慢甚至暂停业务迭代
  04. 容忍一定数量的线上故障
  05. 期间不换老板
- 还有个大前提，这是老板主动想做的事，而不是被说服的结果，这样一来碍于面子他就不会轻易变卦

- ## [CSS-only Widgets Are Inaccessible — Adrian Roselli](https://adrianroselli.com/2023/03/css-only-widgets-are-inaccessible.html)
- https://twitter.com/aardrian/status/1639696117490233344
  - Loosely, those CSS-only controls (such as a hamburger trigger that uses the checkbox hack) you see (from every Dribble build or Codepen contest) are generally a problem for many users.

- ## some of my white whales so far in my career:
- https://twitter.com/tmcw/status/1635760871212216323
  - doing untrusted code evaluation
  - predictable geospatial clip/union/buffer operations
  - getting keybindings to work across platforms
  - building consensus around big decisions
  - generating good documentation from source code

- ## 为什么代码水平越来越高，注释写的越来越少就结局都话越来越少？
- https://www.zhihu.com/question/39813913/answer/83671724
- 水平高代码写得好，简洁明了不用看注释就能看懂，所以可以少写一些注释，但是复杂逻辑的注释还是跑不掉的。
  - 注释太多也不好，有时候代码更新了，注释没有更新，这就埋下一颗地雷了
- 会搜索，基本不用问人，只需要偶尔有个人能问下思路是否太偏及时纠正下(小黄鸭[惊喜])，其实心里也有谱，没人能比自己还能帮到自己了

- ## I don’t really know the official difference between a library and a framework
- https://twitter.com/jamespearce/status/1608996890976325632
- You control how you code with a library. A framework controls how you code.
- I like "you call a library, but a framework calls you".

- ## Tips on get a deeper understanding of the library you are using:
- https://twitter.com/lihautan/status/1362791830648016899
  - Try implement the library based on the public API and test cases, figure out how it might be implemented.
  - Peek into the source code if you are stucked.
  - Watch how I did it for #valtio 
  - https://twitter.com/lihautan/status/1361481299970592770?s=19p

- ## 网上很多文章喜欢讲滑动窗口、拥塞算法，在我看来这些不"务实"。内核交给我们控制的是发送buffer(对应发送窗口)/接收buffer, 以及 rt、带宽时延积BDP，这些才是日常头痛可以去改变的，所以今天推荐的这篇文章就是一锤子到底分析透彻、无比实用，一定要看
- https://twitter.com/plantegg/status/1598861467440513024
- [TCP性能和发送接收窗口、Buffer的关系 | plantegg](https://plantegg.github.io/2019/09/28/%E5%B0%B1%E6%98%AF%E8%A6%81%E4%BD%A0%E6%87%82TCP--%E6%80%A7%E8%83%BD%E5%92%8C%E5%8F%91%E9%80%81%E6%8E%A5%E6%94%B6Buffer%E7%9A%84%E5%85%B3%E7%B3%BB/)

- ## For a new project, I’m experimenting with putting test code next to library modules: utl.test.ts
- https://twitter.com/rauschma/status/1584271399606054913
  - Definitely a downside. During development, it mostly doesn’t matter. But it’s important when publishing packages. I’m leaning towards simply publishing the tests, too.
  - `rm dist/ **/* .test.js` 

- I found this pattern more useful and ergonomic than a test folder. I reserved a dedicated test folder for local integration ones that requires fixtures or more complex scenarios. For smaller projects don’t see bigger differences between each other benefits
- This puts an emphasis on unit tests (because where do you put the integration tests that combine multiple modules?).
  - Which is (the main reason) why I prefer the regular "test" folder: because I want to emphasize integration tests.

- I started using this method recently, and it's pretty good. When you see GitHub PR, the code and its test is always a pair. It'd be better if you could store VS Code nesting setting in .vscode/settings.json file so that other engineers can have the same experience.
- I've generalized this into what I've dubbed "the co-location principle", which means that the tighter coupling between two files, the closer they should be in the directory hierarchy. Shared files are moved to the lowest possible level that are in all paths of the consumers.

- I’ve been doing this since forever. I prefer it because:
  01.      It’s very easy to see which files have no tests
  02.      I can easily jump from test to implementation 
  03.      I never have to decide how to name test files
  - IMHO the (anti) pattern of putting test files in a separate folder stems from compiled languages like Java where otherwise tests would end up in the compiled code. JavaScript doesn’t have this issue.
  - Rust is even sillier. It puts the test (optionally) in the same sourcefiles 

- [webmansa on Twitter: "@housecor i have a question how do you manage your test files, do you write the test in the same folder, OR you have a different folder called tests and all the test files are there ?" / Twitter](https://twitter.com/don_csay/status/1598748749781663751)

- ## What is your equivalent to "making a blueprint" before coding? Is it whiteboarding? Diagramming? Writing a spec? Or do you just jump straight into code?
- https://twitter.com/DavidKPiano/status/1550884682014892033
  - By blueprint, I mean the human-level specification for "what" you are building, not the ones and zeros you're sending the computer to actually build the thing.

- I write out a technical design doc for exactly what I'm building, why, and possible ways of implementing it along with my blueprints for how to build it. It usually ends up being me who does the work, but having a detailed plan ensures each step is on time.
  - In the past, I'd just start coding, but I'd end up rewriting multiple times. Spending a bit of time architecting up front helps save a lot of time wasted coding throw-away code. I was never good enough to do this in the past though. Requires understand how the code works.

- depends what I'm making! for UI/UX, wireframes are usually enough once the design language is mostly in place
- Assuming it's a complex problem, straight to code until a POC is ready.
  - Most diagrams feel like an abstraction on top of the problem. I.e, they can hide complexity. Getting close to code immediately is crucial for verifying your assumptions and not getting caught out.
  - Also, ideally the POC should be as quick and dirty as possible - as short a time as necessary to validate your assumptions before actually doing the real thing.
  - Exactly - the thing I'm most scared of is hidden complexity, and I love tools that can help me uncover this. If @statelyai can solve this problem in the diagramming phase it'll be huge.
- Oftentimes: just writing prototype code. It helps me find edge cases that I couldn't think of before. After that, if I have the time, let it sit around for a while - if I'm "primed" like that, I'll just have ideas over the next days.

- Hacking around - usually starting with the interface/api I want to achieve, then types that all `throw`, then the code. Sometimes I iterate a few times at every step. I am unable to do lengthy RFCs & ideas without making a POC along with them.
  - Depends what it is tho, some stuff I start with db modelling instead. Generally it's just hacking around until something feels right 

- A todo list of everything I know about the task, then start working and fill in the gaps as I go

- At work, for large projects we write a design doc that has what we want to do, why we want to do it, and a high level sketch of how we ought to do it and risks involved.
  - Once that has gone through review and feedback, we write a plan of action that details the how.

- for me
  - put all the UI and requirements up on a board 
  - annotate those with data interfaces 
  - sketch out storage requirements 
  - sketch out transport layers
  - attach sticky notes to edge cases/follow ups
  - make a prototype of disconnected bits
  - make an end to end prototype
  - slice the work up into phases
  - make detailed plan for first phase 
  - make rough plan for later phases 
  - collect open questions 
  - link boards to tickets and vice versa
  - along the way, put links and screenshots of docs for relevant 3rd party services and libraries on the board

- ## me 4 years ago: “write a few lines, check if the code works”
- https://twitter.com/jarredsumner/status/1532497943315435520
  - me today: “write 10k loc in 3 sessions, fix the build failures all at once”
  - Not saying one approach is better than the other fwiw. I find I’m faster at shipping this way, but it also means I have to hold a lot of information in my head or else I’ll get lost in the code
- How is bun’s test coverage out of interest?
  - Bun currently has four kinds of tests:
  - 1. unit tests for runtime APIs (& transpiled with bun) 
  - 2. integration tests for the transpiler/resolver that run in a headless browser and run code from npm
  - 3. shell scripts that test basic stuff works end to end
  - 4. zig tests

- ## 80% of software is a reinvented spreadsheet or state machine (or both!) and you can’t convince me otherwise
- https://twitter.com/worldwise001/status/1523150897169432576

- ## Suppose you wanted to create a REST API with Node.js that had OAuth/OpenID authentication. What would you use to build it?
- https://twitter.com/slicknet/status/1521287278420643840
- Seems like @auth0 is the consensus for identity management. Thanks everyone. 👍

- ## 提高编程水平的一个高效的方式: 
- https://twitter.com/ivyliner/status/1519472859239923712
  01. 自己先写一个中等复杂度的项目(在写的时候自己会知道哪些地方写得不够好, 当然也会有不知道的地方) 
  02. 开始学习相关的知识, 看别人的代码
  03. 这时候你会意识到哦原来还能这样用,  嗯用这个 API 看起来更优雅, 我去还能这样写. ..
  - 整个过程自我会感觉到不断精进.

- 我个人最难的是代码边界控制。如何做到适当的业务上可扩展性和尽量缩小业务变更所带来的代码变更问题。

- ## peg.js 真不错，写各种parser很方便，语法的设计很简单而且非常符合直觉。 
- https://twitter.com/TooooooBug/status/1519158038883880960
  - 试了一下，从零基础开始，1个多小时就能写出简单的SQL parser了
- 可惜不维护了，不支持左递归

- ## This is the flowchart of how slack decides to send a notification. 
- https://twitter.com/alexxubyte/status/1514993500709863425

- ## One of my go-to software development tricks: Have 2 clones of the repo side by side
- https://twitter.com/andy_kelley/status/1504657645172449284
  - Implement the a feature the "safe" way in one of them without touching too much code
  - Simultaneously implement the same feature more daringly, refactoring aggressively in a fit of rage
  - Often you can ping-pong between the clones while waiting for builds or tests to run. And there's not really a context switch since it's the same feature.
  - And if the aggro one ends up being too deep of a rabbit hole, often you can still salvage *some* of the diff in your "safer" implementation.

- ## developers at different levels
- https://twitter.com/ZainRzv/status/1502550200396750851
- Junior engineer:
  - Take this tightly defined feature & build it
- Mid-level engineer:
  - Take this vaguely defined feature & build it
- Senior engineer:
  - Take this known problem & figure out how to solve it
- Staff engineer:
  - Take this goal & find the problems we should be solving

- ## TIL you can use "it.only" to run only one test at a time
- https://twitter.com/steveruizok/status/1496052781945397252

- ## One fact that was unknown to me before becoming an open source maintainer is: You have to really understand a contribution before accepting it, as _you_ have to maintain it.
- https://twitter.com/TkDodo/status/1487804403356680201
  - If I'm getting issues for a contribution made by someone else who is now unavailable, what am I gonna do?

- ## 代码中 state 和 status 区别：
- https://twitter.com/ThaddeusJiang/status/1444133176352247810
  * 有状态迁移关系：state，交通灯状态： red -> green -> yellow
  * 没有状态迁移关系：status，付款结果：success、failure
- Search vs. Query
  - Search：在未知的领域查找，比如搜索引擎的搜索 
  - Query：在已经确定的领域内超出某些特例，比如数据库的查询。

- ##  `<num value={123} />` vs `<num>123</num>` which style do you prefer?
- https://twitter.com/jarredsumner/status/1441923089382535173
- my opinion as a developer: `<number value={123} />` is better because it's clearer and there's no ambiguity of what the type is going to be

- ## XSS cheat sheet only with stuff that works in 2021!
- https://twitter.com/SamuelAnttila/status/1358822910526320640
  - [Cheatsheet: XSS that works in 2021](https://netsec.expert/posts/xss-in-2021/)
* Tons of  XSS filter bypasses!
* mXSS Sanitizer bypasses
* URL Schema filter tips
* MIME type exploitation
* Too much stuff to fit here!

- ## 以前经历过的编程模式有：
- https://www.v2ex.com/t/795043
  - Salary Oriented Programming
  - Lingdao Oriented Programming
  - Hongbao Oriented Programming

- ## The danger of open redirects!
- https://scotthelme.co.uk/the-danger-of-open-redirects/
  - 要防止被利用钓鱼
- The absolute first thing I do when I come across any phishing page is report it to Safe Browsing here, as you should too: https://safebrowsing.google.com/safebrowsing/report_general/
- The problem with having an open redirect like the one above is that it can, and will, be abused by attackers in scenarios like this. 
  - The reason these open redirects are useful is that they add legitimacy to the URL in the email itself which helps it to bypass spam filters.
- If an email provider were to check the domain reputation of homes4wiltshire.co.uk then it would come back as quite positive. It hasn't been flagged as being involved in any phishing/malware activity, it doesn't appear on any block lists
- This is what the attackers want to hide and is why the open redirect on a 'good' domain is so useful.

- ## the most valuable thing I've learned in my career isn't a specific skill, but instead the knowledge that "this will eventually work"
- https://twitter.com/Wattenberger/status/1433880202086600704
  - Projects can be seriously overwhelming when you're in the middle of them, but they almost always come together, and usually faster than you think!

- ## Working on open source while also having a full time job is exhausting and unsustainable. 
- https://twitter.com/devongovett/status/1389635869628256259
  - No wonder people are starting companies around this stuff!
- People expect so much for free and it’s not always easy to let that go and not feel bad about it.
- The open source, unfortunately, is on the verge of being broken by the big companies.
  - There has never been a better time for open source companies than now. Elastic is a billion dollar company.
  - the most popular ones are being bought by a limited number of companies. A very limited number.
  - Thankfully those projects maintainers have the ability to choose not to sell. But it begs the question: why do they?
- I've got some news for you. If you quit your job, you just have new problems and need to spend even more time doing things which are not coding.
- The problem is that the github platform promoted open source as free (non paid). 
  - And now everyone expects oss to be free labor, big corps are using software without funding or contributing while making millions. 
  - Getting paid shouldn't be an after thought.

# pieces
- ## 

- ## There is tension between fast startup times (AOT) and peak performance (JIT).
- https://twitter.com/jerrinot/status/1430165270631534602
  - Historically the peak performance was more important for server-side applications.
  - Cloud is changing it, at least partially, and people go a long way to improve startup times. 
- Some examples:
  01.       Design brand new frameworks with great startup times as an explicit design goal.
  02.       Give-up on some language/VM features we used to take for granted.
  03.       Maintain a bunch of descriptors for the sake of a specific compiler.
  04.       Extract JIT compiler into a separate process and run it as a network server.
  05.       Switch to an entirely different language/ecosystem.
- Given all of the above, I wonder how come I don't hear about process snapshotting/checkpointing more.
- Something like Criu sounds like a good fit for "stateless business logic" - That's precisely the place where the fast startup times are most relevant. 
  - The idea is simple: Run a regular JVM, with JIT and everything. 
  - When you need to scale-out then do not start a new process from scratch. 
  - Instead, take a snapshot of an already running/warmed-up process/container and start its clone. 
  - Sure, there'll be many state-related issues.
- https://criu.org/Main_Page
  - Checkpoint/Restore In Userspace, or CRIU is a Linux software. 
  - It can freeze a running container (or an individual application) and checkpoint its state to disk. 
  - The data saved can be used to restore the application and run it exactly as it was during the time of the freeze.
- Yet I don't hear this approach to be discussed too much. I only saw one FOSDEM talk. What am I missing?
  - Native image tool in GraalVM is thought of AOT compiler for Java, but it has snapshotting capabilites. **You have to adapt your code to work with this** well, but maybe that's inherent requirement. Most code bases do not expect that they can be snapshotted.
- [Call for Discussion: New Project: CRaC](https://mail.openjdk.java.net/pipermail/discuss/2021-August/005941.html)

- ## App: Has 83 feature flags.
- https://twitter.com/markdalgleish/status/1429005039452835845
- I often like to think about feature flags in terms of “how many possible versions of this app exist”
  - 2^83 is well, not maintainable

- ## JavaScript build tools measure performance wrong. Roundtrip time — not build time — is what people feel.
- https://twitter.com/jarredsumner/status/1427891371797454851
- What is your definition of round-trip here?
  - For frontend development, that’s ideally how long from saving in your editor to the code refreshing in the page (either through hot reloading or the script loading) — a broader scope than transpilation time
- That makes sense. Incremental changes generally require fewer files to be rebuilt. So the build plays less of a role in that scenario.

- ## Oh God, I've worked with people who made the one function to rule them all. 
- https://twitter.com/BenLesh/status/1424379521525035010
  - The one component to rule them all. The one service to rule them all. Etc. 
  - And then when you finally break it up into tiny pieces, they're like "oh. yeah I guess that's simpler"
- I think the coolest thing about hooks is they get developers thinking like framework developers. Which is sort of weird but cool. "When this component renders, how do I trick it to wiring things up?" ... That's framework developer thinking, normally.

- ## After experimenting with multiple caching solutions and application frameworks to scale our inventory read layer, 
- https://twitter.com/dinquisitively/status/1419145128497737731
  - we finally proceeded to use Hazelcast with near cache support 
  - and Vert. X as this combination offered maximum performance for our use case.
  - [Scaling our inventory cache reads to 1000X](https://t.co/91nSO7NOtU?amp=1)

- ##  Always use profilers to identify performance issues in code. 
- https://twitter.com/d__raptis/status/1419611806557945859
  - I'd never find the problem otherwise.
- It's quite simple (for React at least) : 
  01.      Use this Chrome plugin react-developer-tools 
  02.      Click record
  03.      Reproduce a laggy action
  04.      Check which components/actions are time-consuming
- Now, you've located the issue and you need to check the code to find the real issue

- ## Syncing sign-in state
- https://www.tommoor.com/posts/syncing-signin-state
- Because Outline is primarily for writing documents, we see a use case where users keep many Outline tabs open containing different docs. 
  - Outline is built using MobX for state management. 
  - Local client state is split into multiple stores in the app, for example users, documents, auth. 
  - The auth store contains data related to authentication such as the current user and team – it also manages the persistence and subscriptions. 
- There are essentially three parts to this feature:
  - Syncing auth in MobX state to localStorage
  - Listening to localStorage changes
  - Updating local MobX state from received events

- ## TypeScript/VS Code tip: If you don’t see external type updates in your editor, try opening the changed .d.ts file. That usually refreshes things for me.
- https://twitter.com/rauschma/status/1417285626836160512
- There's also a "TypeScript: Restart TS Server" command that should work too.

- ## Is there a good CI/CD service that provides "visual diffs" of HTML? (and can plug into GitHub CI/CD checks?)
- https://twitter.com/choldgraf/status/1417385474272944152
- https://github.com/cburgmer/csscritic
  - CSS Critic closes the gap in front end testing and makes HTML & CSS testable

- ## Just curious: which package manager/CLI do you use? npm vs yarn vs yarn2 _202105
- https://twitter.com/JoshWComeau/status/1395044829013368846
- [Yarn 1 vs Yarn 2 vs NPM](https://shift.infinite.red/yarn-1-vs-yarn-2-vs-npm-a69ccf0229cd)
- pnpm is supposed to be very good, but since we focus on React Native, it's not an option for us.
  - Yarn 2 is almost an entirely different CLI altogether. I wish they'd just name it Berry (which is its code name) v1.
- I feel your article is misleading in two important aspects:
  01.     Yarn 2+ supports React Native well with node_modules install scheme
  02.     Yarn 2+ perfs are better or comparable to perfs of Yarn 1, both with default PnP installs and with node_modules installs
- I used to use yarn 1. After the acquisition of npm by GitHub I switched back to npm
- I use whatever the project already uses but use npm for anything I start. No real reason though

- ## Test accessibility with more than 1 tool and more than 1 method.
- https://twitter.com/jackdomleo7/status/1414468761860587520
- Accessibility testing tools:
  - Axe
  - Pa11y
  - WAVE
  - Tota11y
  - Chrome's Lighthouse
  - Firefox accessibility devtools
  - jest-a11y
  - Checka11y.css
- Accessibility testing methods:
  - Use a11y testing tools (see above)
  - Unplug mouse
  - Install a screenreader
  - Install a plugin/extension to mock colour blindness
  - Turn on high contrast mode
  - Turn off images
  - Turn off CSS (very useful for HTML structure)
  - Video captions

- ## I feel TDD is focused on backend/business logic, too dogmatic, and lack of clarity on how to test UIs/DOM.
- https://twitter.com/sebastienlorber/status/1414210224001622018
  - You are not allowed to write any production code unless it is to make a failing unit test pass
  - Visual diff tools like Chromatic are much more pragmatic.
  - I don't want to draw a png as my failing test.
  - Nor I want to manually edit a video of the desired animation.
  - testing frontend state/Redux/FSM is only a small part of all the things that can go wrong in a frontend app.
  - TDD should clarify when it can be applied successfully. In my opinion it's not 100% of the time
- I think TDD is more useful when interpreted as "write tests alongside production code code" and not as "write tests before production code".
  - Having a falling test gives you confidence the test is not a false positive, but you can make it fail after writing the production code.

- ## When I do a big refactor to a data structure I like to start by changing the type definitions. Then I fix the red squiggles until they're gone.
- https://twitter.com/kentcdodds/status/1413326124969459714
  - The joy of things *just working* when I finally run the code will never get old.
- This! I have done a few big retractors (~2000-5000 lines of code each) on my current project over the past 9 months without batting an eye. There's a correlation between the red squiggles being gone and the tests passing. TypeScript is the bomb! 
- This is the red-green-refactor cycle with typescript.
- With ts I have no problem on refactors covering tens of files, thousands of lines. 
  - It saved us from having to write a lot of test cases. 
  - More than that I find writing the interface first, I have a clear mental model of what I’m developing and all goes faster

- ## Polishing up a project for release is so much work. I feel like I’ve been working on “finishing” Parcel 2 for the last 6 months. Getting close though!
- https://twitter.com/devongovett/status/1412865291315417089
- Some recent things I've been working on:
  - Automatic module/nomodule
  - Support for reading tsconfig.json to configure JSX settings
  - API consistency
  - TypeScript definitions for public API
  - Improvements for web workers
  - Cache portability
  - Improved diagnostics
  - Lots of bugs
- The last 10% is always the longest half of the project

- ## how to adapt faster in a new squad and a new codebase?
- https://twitter.com/luizpn_/status/1412431905924993030
  - this is my first week working with a new squad and I feel so slow 
- Play with the features, once you understand how the product works you start to make more sense of the code. The rest like architectural decisions made you will pick up on the fly when doing tasks.
- In the beginning, it's normal to be slow. If your teammates help, you'll also learn faster. I'd put emphasis on learning the domain
  - Another great way to get familiar with some codebase is to write automated tests for it.
- Don't worry it's normal
  - First, demonstrate an interest in the project, be proactive, and ask questions. There will be someone that will value your energy and will want to help you
  - Do pair programming, read tests, read the whole code base, and try to understand the big picture

- ## What is the best approaches to provide an uniform API (it could be a function, endpoint or something else) when you have APIs that do the same thing but has different inputs and outputs?
- https://twitter.com/sseraphini/status/1412483649564561408
- I think doing this will just add more complexity, so I'd avoid this if users are devs. Else if they're clients, I'd do a good enough wrapper over the whole thing returning a Frankenstein
  - How would u do instead? Expose 100 different formats to end user?
  - I think a wrapper could work. Enforce the inputs and return an unified output if possible
- A wrapper that receives the "eigen inputs, " a switch case that calls those APIs, and a mapper to return the "eigen outputs."

- ## Open API
- https://twitter.com/peduarte/status/1407710813247389700
  · Flexible, composed, extensible 
  · Can still be abstracted at the app side
  · Use it when wanting to give users more control
- Closed API
  · Opinionated, strict, prop-driven
  · Can be simpler to learn
  · Use it when wanting to limit what users can do
- **They're both good** !
- I use both on a daily basis, I mean the second (UI preset) can be a shortcut for using the first (design system)

- ## I ported Chrome DevTools' inspector to Node.js
- https://twitter.com/privatenumbr/status/1407976142892580867
  - Just run `await inspect(object)` to inspect any value with an inline interactive CLI
  - Great for working with large & complex objects in Node without having to spin up a Chrome debugger

- ## Note: you can't write a test that depends on dynamic import in Jest because Jest runs your code in a vm and dynamic imports don't work in vm due to a Node bug.
- https://twitter.com/matthewcp/status/1407724050638594050
  - Another reason not to have your testing library be a runtime.
- I've used test-framework free solutions quite a few times. Generally they just involve a tiny assertions module, then each test is just a module that exports a test. The actual "test runner" would often just be a simple loop that goes through each test file and runs it.
  - The fact the test modules know nothing about how they'll be run does offer some nice flexibility, in particular it's very easy to whip up versions that run tests in browsers, in workers, or under other constraints.
  - The main drawback I've found is it can be kinda annoying to associate descriptions with tests, especially given it can be a lot easier to have multiple tests in a file. e.g. One thing I've done in the past is have object property names as test descriptions, which isn't ideal.

- ## As someone who ends up building a lot of architectural and infrastructure code, there's one thing I cannot emphasize enough: do the simplest thing that works. 
- https://twitter.com/promit_roy/status/1405912880663433223
  - Do not try to imagine future requirements, or support ill-defined potential use cases. 
  - It will always change later.
  - The problem is that the simplest thing that will work is dependent on how well you already understand the setting. 
  - There’s no single simplest possible approach, and they all differ on how easily they can be extended in different vectors.
- I used to do a lot of planning, and it always turned out to be a waste of time, and I'd have to rewrite large chunks anyway - either because the requirements changed, or because I didn't understand the problem until I actually wrote the code.
- I don't agree, trying the simplest solution will make it harder for you or anyone to extend
  - Yes, do simple things, but not the simplest. 

- ## One driver behind the 'lots of small packages' trend in JavaScript has been the desire to ship the minimal amount of code in web pages.
- https://twitter.com/MarijnJH/status/1397127566503419904
  - Have tree-shaking tools mooted that? Is there still a good point to be made against packages that include a bunch of stuff that many people won't need, as long as it's in a shape where unused code is easy to eliminate?
- Since tree-shaking has been adopted by @RollupJS, I've been shovelling(铲起；挖出) all utility functions that I use across projects into a single monorepo. 
  - Creating yet another package would mean that I'd abandon it at some point.
  - A monorepo forces me to keep it up to date
- I think another advantage of small packages is that all the relevant documentation can easily fit into the README. This makes it pretty straightforward for new contributors to properly document the stuff they add or change, which in turn leads to better documentation overall.
- No. I have found tree shaking to be unreliable when many exports are included in one module, and it is still best to have many small modules to get the best out of the shaker.

- ## has anyone tried both esbuild (or meta build systems like Vite that use it) side by side with Rome?
- https://twitter.com/devongovett/status/1390023696782221312
  - Does/can Rome approach esbuild's speed?
- https://github.com/alangpierce/sucrase
  - Sucrase is an alternative to Babel that allows super-fast development builds.
- vs
  - babel - mutable ast, plugins can mutate the ast, slow af
  - esbuild - immutable ast, filter/link file plugins, very fast
  - sucrase - immutable ast, no plugins, silly fast
- Sucrase doesn’t even have an AST at all. 
  - It manipulates the token stream as it parses. 
  - Much less flexible but skips full parse, ast pass, and codegen.
  - Also mutation itself isn’t the problem. 
  - It’s revisiting mutated nodes that increases complexity from linear to quadratic.
- Rome can get there for sure. sucrase (babel alternative written in TypeScript) is already faster than esbuild for some things.
  - The real bottleneck is multi-threading. 
  - Sucrase only wins slightly in single-threaded mode PLUS the trade-off of non-extensible AST treatment (by design).
  - Future dev machines likely come with 8+ cores and a flexible AST is required for Rome's intended scope.
  - Which is to say... using Sucrase as an example for "JS compilers can be fast if you design it right" isn't particularly accurate because (1) Sucrase is designed to take shortcuts by drastically reducing its scope. Sucrase and Babel are like apples and oranges.
  - And (2) you can't solve JS' inherent problem at multi-threading with compiler design.
- To be fair, ESBuild also takes a lot of the same shortcuts. 
  - No custom transform plugins means it reduces the number of AST passes but wouldn’t be scalable to something with the scope of Rome. 
  - Nothing wrong with being focused one one thing, but they are different approaches.
- Does swc take shortcuts too? If it is comparable to babel and still beats esbuild in performance benchmark, I am even more impressed.
  - It is very similar to babel. Everything is built in separate passes. Does not have quadratic behavior like Babel though.
- Parcel switches to swc (written in Rust) for massive perf boosts

- ## If you do integration tests you don't need to know if the app is using react, redux, redux-saga, or something else
- https://twitter.com/sseraphini/status/1389584078790352902
  - render the app to the DOM
  - interact with the DOM
  - assert the final state of the DOM
- if you refactor from redux to pure react, the test would still pass

- ## I don’t use fake data generators for testing. I prefer using a static dataset instead.
- https://twitter.com/housecor/status/1389386557648482308
  - Tests using local static data are reliable and fast.
  - I can enhance the dataset when I find edge cases.
  - I use the static dataset in mock APIs, unit/integration tests, and Storybook.
- Fake data can be useful for “Fuzz” testing (feeding the app a bunch of random data to see if it bombs), but that’s a separate conversation.
- I would use a faker library to generate useful datasets. Then store that json in a static, committed file.
- Overall I agree with the sentiment: tests should be deterministic. I don't want them to sometimes fail (or falsely pass) depending on randomly generated data; the code either works or it doesn't.
  - We sometimes use static data and sometimes a Faker generator, but with a static seed. Precisely to give us predictable tests. I find that the two versions behave the same in practice.
- For integration tests of components, I prefer to generate fake data 
  - and override parts of fake data with static data  when testing a particular scenario, so the focus on the data remains clear.

- ## If you do code split for each page of your application, you are denying the benefits of building a SPA.
- https://twitter.com/danieljpgo/status/1387149559315550211
- With webpack you can have an SPA with chunk splits dynamically imported to improve performance, and with react you can use suspense
  - Yes, but you will still have to download the bundle for each page, which will not deliver smooth navigation when using your application, which is one of the main features that the SPA brought.
  - render as you fetch solves this
- I would agree that many of us focus on code splitting routes over code splitting features. The latter thinking is more SPA like imo

- ## creating a javascript package is easy
- https://twitter.com/sseraphini/status/1094358825417797633
  - it should run on all node versions
  - it should run both on node and browser
  - it should works on SSR
  - it should works on pure js, typescript and so on
  - it should have lint, prettier setup
  - it should have autorelease process
  - it should work on both react web and react native
  - it should work across frameworks: angular/react/vue
  - it should provide hooks api
  - it should work with webpack, parcel, metro bundler
  - it should cover 100% of edge cases
  - it should have docs and a good readme
  - it should be blazing fast
  - it should have blog posts
  - it should be incrementally adopted
  - it should have tests
  - it should have/provide types
  - it should work on npm, yarn
  - it should have a great logo
  - it should have a changelog

- ## How can I generate a tree, starting from a component to see where it is being used? like A is used in B and C, and D uses B and C
- https://twitter.com/lucasleandrodev/status/1385617694653882370
- [How to easily visualize a project's dependency graph with dependency-cruiser](https://www.netlify.com/blog/2018/08/23/how-to-easily-visualize-a-projects-dependency-graph-with-dependency-cruiser/)
- https://github.com/pahen/madge
  - Create graphs from your CommonJS, AMD or ES6 module dependencies

- ## avoid pages/screens vs components folder structure 
- https://twitter.com/sseraphini/status/1385574397998637058
  - folder-by-type vs folder-by-feature
  - keep components and routes colocated based on their feature example: 
- `<feature>` .
  - all routes of this `<feature>` .
  - all components of this `<feature>` .
  - like sub apps that you can compose
- for both pages and features folder (for a multi-page app)
  - one thing to notice is that a page can use multiple features, so having the page component inside a specific features folder is something that breaks this logic colocation.
- But take next for example
  - Since it's routing is based on the file system, won't that put components to be considered as pages, when they shouldn't be?

- ## AsyncAPI is the OpenAPI for Event Driven architecture 
- https://twitter.com/sseraphini/status/1384490726168227843
  - You can document all your events and payloads, internal and external ones
  - https://www.asyncapi.com/
  - https://github.com/asyncapi/spec
  - https://github.com/asyncapi/asyncapi-react
  - AsyncAPI正在成为定义异步、事件驱动的API的行业标准；您可以将其视为异步世界的OpenAPI
  - 它既提供了以机器可读格式描述和记录异步应用程序的规范，也提供了工具(如代码生成器)来简化负责实现这些应用程序的开发人员的工作
  - 很多框架都支持从代码直接生成OpenAPI，比如SpringDoc等

- ## Forget DRY. It's okay to repeat code sometimes. 
- https://twitter.com/renatorib_/status/1384159371593060357
  - Abstract it when you are sure that it will more help than harm.
  - Repeat first, abstract later.

- ## Request: point me to some good examples of JS libraries that show the TS types for their APIs in the API reference pages? 
- https://twitter.com/acemarke/status/1383503585812508684
  - I'd like to see how other libs organize presenting descriptions vs typedefs in the reference docs.
  - How to present potentially complex and nested typedefs
  - How to maybe hand-wave some of those complex types for readability
  - How to split arg/return value display from the written descriptions
- We dynamically replace the generic type parameters in the docs for generic types with a concrete type where necessary. 
  - No `IEnumerable<T>` but `IEnumerable<INode>` .
  - why not just name the generic parameter something readable (rather than abstract T)? that way you wouldn't have to replace anything - like probably you could just grab the name from `Node extends INode` 

- ## Unpopular opinion: you should write E2E/integration tests *first* , always. 
- https://twitter.com/DavidKPiano/status/1180497113341468677
  - (This mainly applies to applications. For libraries used by developers, the unit tests *are* the E2E tests, a lot of the time.)
  - They should be directly related to business logic (user) requirements. 
  - Only when an E2E/integration test fails should you even think about writing unit tests. 
  - And be willing to delete those unit tests.
- Speaking strictly from the point of view of a library author, it’s the failing unit tests that can give you an instant idea of why the e2e tests are failing, rather than having to go spelunking(洞穴攀爬运动)
- When we first started React Training, we had only one test for the whole website: make sure someone can buy a ticket. As long as that worked, everything else was negotiable

- ## The largest misconception about @webpack is: 
- https://twitter.com/TheLarkInn/status/1017052742039326721
  - Not treeshaking or making vendorbundles is the cause of their web perf issues. 
  - Rather, in _most cases_, the main cause is not leveraging code splitting enough. 
  - You should prioritize code-splitting above the aforementioned.
- The irony here is that to code split, you don't need to configure anything for webpack. 
  - Just use `import()` . 
- I think code-splitting will be more efficient at making your app faster, whether code is tree-shaken or not.
- We use webpack dynamic imports to also lazy load features into our app that only apply in certain config e.g. /config endpoint -> {features:[]} -> for each feature -> import. Works well for us
- Any recommendation or best practices articles  
  - The key is this, if the code you `import` is not needed to produce the initial render of your application (routes, modals, tooltips, dialogues, event handlers, etc.)， then you should use `import()` instead.

- ## Why I code against a mock API:
- https://twitter.com/housecor/status/1256242384075198472

1 I control the speed
2 It's never down
3 No internet required
4 No cross-team dependency
5 I can force it to throw errors to simulate server errors
6 I can write fast, reliable app tests
7 When I find a bug, I can enhance mock data and test it

- ## What challenges have you faced adopting serverless technologies?
- https://twitter.com/flybayer/status/1381743417391255559
- Simulating the environment "locally" for testing/debugging.
  - use case: complex business logic breaking, like a bunch of calculations, how to simulate and debug that to find the error 
  - arc.codes solves that part w a local sandbox
- Realtime, 
  - Connection pools, 
  - Stateful assets(dynamic images et al), 
  - Complex setup (or lose of control)
  - inability to use some tools I love(e.g. mongodb is just poor in serverless)

- ## Don't forget to consider an option to scale horizontally rather than vertically. 
- https://twitter.com/kettanaito/status/1381604735304806403
  - Horizontal scaling is far more sustainable and prone to refactoring.
- let's say when we need to extend an existing function to handle two different scenarios - request in browser or nodejs.
  - instead of pushing the logic through one function `handleRequest` , consider treating each scenario as a standalone implementation, potentially reusing the internal logic that repeats.
- Treating those as two independent scenarios also contributes to much more scoped tests. 
  - That, in turn, allows to reason about similarities and difference and makes it easier to alter logic on a per-scenario basis.

- ## I'd really like to have a thing that wraps every function in my codebase at compile time, it profiles samples of them with minimal overhead, 
- https://twitter.com/fabiospampinato/status/1381569380203573257 
  - it's always on, and over time it tells you interesting things. 
  - Potentially it could work across an entire user base too, that'd be super.
- Different domain and technology, but this idea reminds me very much of pira
  - https://github.com/tudasc/pira
  - Except we don't instrument / wrap every function. We Actually try to minimize the instrumentation to only "relevant" parts -- for different aspects of relevant.

- ## to repeat my favorite software development mantra: "make it work. make it right. make it fast."
- https://twitter.com/acemarke/status/1376969090552725506
- I hate perfectionism, I rather create something initially janky but a really cool thing/idea THEN work on improving it and optimizing it.

- ## I don't use TDD This is what I do instead: code -> test -> docs (CTD)
- https://twitter.com/sseraphini/status/1376636172080922629
- CPT - code > production > test
- Tdd is great but it usually it is not so practical while you are still exploring the implementation space
- I do the opposite: docs code test, DCT
- TDD is interesting for pure functions that you know the expected result and use the test as a tool to automatically check if you are doing it right. Test functions manually are boring if it's not trivial.

- ## it never ceases to amaze me how much some people will resist showing their code after asking a question and saying "this doesn't work".
- https://twitter.com/acemarke/status/1376656948926496768
  - Sometimes I can provide an answer after just hearing a description.
  - but most of the time, I need to see the _real code_ to debug the issue.

- ## Is there any kind of a utility lib that will scan a JS file and identify code that doesn't match a given set of features supported by a target browser?
- https://twitter.com/acemarke/status/1376703719669182471
  - I'm basically looking for something like (notional): `is-browser-safe ie11 my-file.js` .
- eslint-plugin-compat
- eslint-ie11-compat

- ## What's the right process for a library to drop support for IE11/ES5-only environments in its published artifacts? 
- https://twitter.com/acemarke/status/1376381894279987209
  - Should that be a new major, or a minor?
  - Right now our CJS/ESM files are back-compiled to ES5 syntax for IE11 support.
- So "major" seems to be the consensus answer so far, which is reasonable.
- We're planning for RTK Query to be released in RTK 1.6. It's additive only, so that doesn't require a new major.
  - I really want to keep RTK and the new RTK Query features accessible to as many devs as possible. On the other hand... IE11. Ew.
  - Maybe put these out in 1.6, and then begin planning RTK 2.0 that drops ES5-only support?

- ## Where do you put tests and why? same folder vs separate tests/ folder
- https://twitter.com/claviska/status/1375071253753647118
- Separate “tests” folder because clutter etc. 
  - Also if you are concerned that things aren’t getting test, you can also setup code coverage and know for sure.
- Framework's default
  - It's configurable, but I'm looking at one with a tests folder. My concern is, if tests are independent of the things they're testing, it's easy to forget to add/update them (particularly for contributors and large codebase)

- ## If you deploy your app to serverless platforms (Vercel and friends) but you use services (Postgres, Redis, etc) that don’t have auto scaling, then your app is not serverless at all. It’s only an illusion.
- https://twitter.com/flybayer/status/1373824547506511873
- We just shift the bottleneck. Classic manufacturing efficiency optimization problem

- ## I always wondered about Google, how do you push through the internal competition? Android, PWA, Flutter. 
- https://twitter.com/sebmarkbage/status/1373775862219292674
  - I sit here with an amazing community, team, org and management support. 
  - Yet all I can think of before every Monday is the people that don’t believe in me or what we’re doing.
- You have to lead and stand by your decision: Think of Steve Jobs coming back to Apple and bring all that Objective-C guys from Next.
  - It was the better technology - but heck it was unpopular at that time. And despite all the lows he denied all alternatives (Java, Flash).
- I worked at companies where such competition is a norm. 
  - In my experience, that's what helped to avoid such feeling. 
  - Helpful competition promotes stuff that works, kills stuff that does not; 
  - it allows people to focus on the objectivism of the tech not the subjectivism of feelings.

- ## Wondering sometimes if, instead of more libs, we shouldn't offer more first-class copy-and-paste solutions.
- https://twitter.com/mpocock1/status/1372986732354883588
  - Copy and paste an entire component lib and then tweak to your heart's content
- I'm absolutely against this: the good thing about libs is that they are documented and tested configurable blocks. All code should be libs, even our own. Coding for open source enforces code quality (at least at the boundaries).
  - Libs are wonderful, invaluable. But choosing libs for _all_ solutions is perhaps too dogmatic. There should also be space for when you want to grab something pre-built and modify it.
- What you described is the basic idea behind the architecture of Crown. You “install” packages within the framework by cloning with git subrepo. You own the code but can still pull changes from upstream

- ## For tools that don't have multi-versioned docs sites: what are good techniques for how they indicate a particular API or option was added/modified in a specific lib version?
- https://twitter.com/acemarke/status/1373102543371390979
- just a line at the top of the page/section mentioning the version works fine. I think I've seen that pattern in a bunch of pages on Next.js and some other docs.
- api.jquery.com/blur/ Of course that's how things were done back in the day I guess 
  - The version added for a method is always specified, also there are always notes about the differences between versions.
- Kotlin docs show you which version APIs were added in and if they are supported in JavaScript, JVM and/or native

- ## Developers that can't or don't write good comments aren't great developers yet.
- https://twitter.com/BenLesh/status/1372562839475470336
  - Add comments about WHY code exists, not what it does.
- Comments cannot be tested and should therefore be assumed to be wrong.

- ## What's the coolest open source project in the JS or Wasm ecosystems you've seen that's *new* within the last year?
- https://twitter.com/_jayphelps/status/1372249383291457540
- esbuild
- We just finished a show on Remotion and @JNYBGR - how to programmatically make videos with React. It's really excellent and empowering technology.
- css-in-js: SnackUI - the final React style library
  - The smart SwiftUI-inspired UI kit for React Native & Web.

- ## I don't actually show much of my coding work in public, largely because I do most of my coding at my day job.
- https://twitter.com/acemarke/status/1372374988762779649
  - Even then, teammates normally only see "final" code in my PRs, and don't often see how many mistakes I made along the way to get to that final result.
- A couple nights ago I decided I'd see if I could try writing a faster implementation of the RTK mutation detection logic. I did get it passing all our tests.
  - It appears to be like 15x _slower_ than the original.
  - I guess the point here is, consider this your semi-inspirational reminder that everyone screws up - you just don't always see that happening visibly.
  - I am now trying to figure out _why_ my implementation is slow.
  - today I deployed a new build of our app to prod. small app, single server, half-automated deploy process.

- ## What are some times you've needed to keep data synced between two SaaS products? (eg: keep a Trello board synced w/ a Notion table)
- https://twitter.com/geoffreylitt/status/1371509957779148802
  - Looking for example use cases for a sync tool I'm working on
  - Could also be things like "needed to keep this Salesforce data updated in a Google Sheet"
- In design-engineering teams:
  - Figma Comments <> Trello Cards <> GitLab Issues
  - Trello being the middle ground for managers who‘re afraid of Figma/ GitLab
- Personally: Airtable <> Google Sheets

- ## The #1 tech skill to have is comfort in coding, on the fly, in front of other people.
- https://twitter.com/AdamRackis/status/1370875384812740610
  - Expect to be given some silly use case, ie, "write a class that take two strings, and tracks which is longer"
  - Be comfortable talking through the requirements, asking questions, etc.
- Expect to iterate on it, over and over, with requirements being added. Ie, "now optionally take an array of strings, and, if an array was passed, track the shortest string. If just two strings were passed, like before, then ..."
- Most important tip I can give: **think out loud** . Always. Turn the voice in your head you normally think with, off, and think out loud.
  - If you get stuck, talk it through, out loud. Explain why you're stuck. Ask questions. Your interviewer is there to help you. Seriously.
- The worst thing you can do is stop coding, and freeze up, panicking in your mind. Talk it through.
- Expect to be asked questions in your domain to test how deeply you know it. I was asked about everything from arrow functions, to Promises, to web sockets.
  - The deeper you know your stuff, and can demonstrate it, the better.
- If you're asked about arrow functions, don't just say they're shorter syntax sugar.
  - Mention lexical this.
  - Mention lexical arguments.
  - Mention lack of a Prototype and [[Construct]] slot.
  - Show them you're someone who knows their shit.
- You know what I was never, ever asked about, even once? JS Frameworks
  - Oh, you've written apps in React, Svelte, Vue and also Angular? Nobody gives a shit.
  - Companies care a lot more that you have deep language mastery, vs having played with a bunch of different frameworks.
- You know what else I was never asked about? CSS Frameworks.
  - Tailwind seems really, really cool. But maybe learn the fundamentals of CSS before you dive in, there.

- ## friendly reminder that http-only cookies don't protect you from XSS
- https://twitter.com/benawad/status/1370532233698770947
  - if someone can inject code they don't need your token, they can just make fetch calls on that users behalf
- The solution to this is using CSP, right?
  - The solution is "don't trust user input"
  - Yep but not all browsers respect the policy. And if you parse malicious code comming for user inputs it doesn't matter if the browser respect the CSP especially if that code can be rendered by other users too
- Very true. If you've an XSS you're actually flawed and a local jwt should be the least of your worries

- ## Webpack have achieved production server Hot Module Reloading between apps using module federation
- https://twitter.com/ScriptedAlchemy/status/1370555543136301060
  - No cold start, no downtime, no new process. I've seen the future, and its got zero-downtime

- ## Preemptive Pluralization is (Probably) Not Evil
- https://www.swyx.io/preemptive-pluralization/
- What if we just assumed we might have two of everything?
- Before you write any code — ask if you could ever possibly want multiple kinds of the thing you are coding. If yes, just do it. Now, not later.
- But I think Preemptive Pluralization(先发制人多元化) — projecting forward into hypothetical situations when you need N types of a thing — is exempt, even though you are literally optimizing for a future you don't currently live in.
- It is a LOT easier to scale code from a cardinality of 2 to 3 than it is to refactor from a cardinality of 1 to 2. 
- Robust code is optimized for change (more in a future blogpost).
- Let's address two obvious criticisms of Preemptive Pluralization:
  - Increased code complexity: Functional languages and other abstractions can help make array or matrix operations almost as easy to work with as regular operations.
  - Slow performance from doing extra loops: Loops only cost significantly when you have lots of N. By definition, if you are pluralizing prematurely, N = 1.
- Listen up, this is sound advice that I can attest to after years of experience. 
  - You will almost always need two or more. 
  - If you end up not needing 2 or more, the risk/reward is worth it in almost every situation.
  - Just Pluralize It.
- I've made this type of refactor more times than I care to count, and it's always a pain. Absolutely good advice.

- ## 3rd party integrations today are like:
- https://twitter.com/ryanflorence/status/1370405429189046278
  - First, add our 100kb browser SDK
  - Now fetch to your "api route"
  - Now use our server side sdk
  - Now back in the browser use our browser SDK
  - A little config on the third-party dashboard + `<form> ` would have been way simpler.
- But you know that A in JAM is for API and you can make a `<form method=post>` , right?
  - Yes indeed, but so many services require browser javascript and you can't actually process that post on the server.
- `<form method=post>` .
  - automatically serializes data
  - automatically fetches an "api route"
  - automatically changes the page state when complete
  - automatically adds pending indication to the user interface
  - works cross origin if needed
  - This is how you communicate a mutation.
- use `<form>` , Then use `<Form>` , when you've got the time/energy/skill to implement a nice pending/optimistic UI. 
  - Remix doesn't care which one you use, it's all the same!

- ## For a long time, I was always unhappy with my code. I never trusted it, never liked it.
- https://twitter.com/eveporcello/status/1369678978827493376
  - Then I discovered: Testing, Refactoring
  - With both, I worry much less about getting code right initially—I can always improve it later. 
  - Testing also lets me trust my code.

- ## My problem with types added to every function and object is that they occupy my brain when I scan the code when I don't need them. 
- https://twitter.com/oleg008/status/1369956575964782594
  - They are just cluttering the code most of the time. 
  - I want to go back to clean JS code but still have the types hints when I want them.

- ## TIL: passing multiple `-m` options to `git commit` creates paragraphs in the message.

- ## How to identify mistakes in a code structure to learn from:
- https://twitter.com/cse_as/status/1369281929162285063
  - When you go back to a part in the project your team worked on earlier & it takes you more than 10 seconds to pinpoint where the needed code is, it probably wasn't structured in a way that made sense.

- ## A list of basic Linux commands every developer should know:
- https://twitter.com/iamdevloper/status/1368866110951596032
01.    Open your browser
02.    Head to your favourite search engine
03.    Type "how to copy a file to another directory"
04.    Click the first Stack Overflow link
05.    Copy the top voted answer
06.    Blindly paste it into your terminal

- ## When should I (not) use mocks in testing?
- https://dev.to/kettanaito/when-should-i-not-use-mocks-in-testing-544e
- Depending on the software that is being tested, there are multiple things that can be mocked:
  - Environment and context.
  - API communication
  - External dependencies.

- ## Writing software is basically a 2 step process: 
- https://twitter.com/housecor/status/1368569429202792448
  - Ask the computer to do something
  - Verify its response
  - That’s why I believe in creating fast feedback loops. The faster I get a response, the more productive I can be.
- Feedback loops also involve CI, designer-developer collaboration, automated tests, among others. Any improvement that you do in any of those increases your productivity!
- You missed the 3rd step. Swear at the computer when the response is wrong and you can't see the problem.
- What are your favorite techniques for this?
  - Mock APIs
  - Small tickets so I get teammate and user feedback faster
  - Automated unit tests and TDD
  - Build and test small components in isolation
  - Create custom dev tools
  - Use Cypress to avoid interacting with the app manually while coding
- In all seriousness though, this is why I love to write my code using TDD.

- ## is there a "modern" UI for OpenAPI? built with @reactjs that could be very customizable?
- https://twitter.com/sseraphini/status/1367851096421568512
  - I'm like to embed my API inside @docusaurus
  - but redoc takes the full page and swagger UI has some dark mode issues

- ## You can't mock cloud semantics locally but you can mock the API surface. AWS is very stable. 
- https://twitter.com/brianleroux/status/1367851230785990663
  - Folks say you shouldn't use local emulation because of this but I respectfully disagree. It's slower. 
  - Tighten those feedback loops. Test locally AND in an identical staging stack.
- Fwiw, same discussion happened in mobile a decade ago. You can't use an emulator they said. Mostly ppl said that because the emulators sucked. 
  - Ppl don't say that about mobile dev anymore. Cloud will have the same cycle.
- I was firmly in the “don’t emulate AWS” camp until I actually tried using localstack. 
  - If the bits you need to emulate are supported, it works quite well.
  - It's additive too. Work local and then test in a staging stack. Makes step 2 shorter which has higher latency anyhow. 
  - I'm fairly certain this meme happens every new platform because vendors and frameworks add emulation later. It's an excuse while they get their shit together.

- ## 99% of what I do in a large codebase is find pre-existing examples, copy-paste structure, fill in the holes and clean up. That's it.
- https://twitter.com/deech/status/1366859264732635148
  - Relevant skills: find pre-existing examples, copy-paste structure, fill in holes, clean up
  - Irrelevant skills: category theory, able to whiteboard delete for a red-black tree
- This is definitely how big company code works! Sometimes to a surprising effect. 
  - You might check in some random pattern you haven’t given much thought to while filling in some hole. 
  - Then a year later you find your code in a 1, 000 places with tiny changes. Hope it was good code.

- ## Is Webpack's code-splitting just garbage or are there more tricks to implement?
- https://twitter.com/mattgperry/status/1366344701964648450
- Why do you think it is garbage?
  - Because moving a single enum into its own file yielded a 11kb/89% saving.
  - This is incredibly delicate and has implications about how a project should be structured (no more than one export per file). As far as I can tell, for no good reason. It isn't the case with Rollup.
- nope, webpack just offloads more to Terser whereas Rollup do a lot more work on its own, this can make a big diff for some projects, 
  - also - Rollup makes some pragmatic choices sometimes whereas webpack tries to be super strict and safe, which also can make a big diff
  - So do you personally tend towards single-export files?
  - This is a good advice if u want to keep things as treeshakeable as possible - ive thought about creating a rollup plugin that would chunk a project this way automatically. I dont want to split files manually. Never got to it though

- ## As a CS prof, I use binary search practically every day to figure out which part of the paper is crashing LaTeX.
- https://twitter.com/bradreaves/status/1365061879744315398
- I take quadratic computer time to avoid the logarithmic human time for the binary search (a.k.a. re-compile every few keystrokes).
- This is how I used to teach kids to debug. 
  - When a problem is really hard to find, try and reduce code in half, recursively, until the program works
- Divide and comment 😋

- ## Want to find a perf problem? Throw something big at it.
- https://twitter.com/kuvos/status/1364929672652464132
  - 88mb of js will probably do

- ## Integration testing tip: Avoid creating many small tests. Instead, create a few big tests. 
- https://twitter.com/housecor/status/1364584436755480578
  - Here’s why: There’s a lot of overhead in starting each integration test. 
  - So to build a fast integration test suite, favor “big” tests over “small” tests.
  - Example: Imagine I have a todo app. I don’t write separate tests for create, update, and delete. Instead, I create a single test that checks all three. I name the test “should support adding, editing, and deleting todos”.
- And when the test fails, you don't know why.
  - In Cypress that’s clear. It shows what line. And even records and screenshots.

- ## Best CSS debugger: `border: 1px red solid;` .
- https://twitter.com/kyleshevlin/status/1363901000948408320
- I have to say this every time: This is close, but it's NOT the best.
  - It's better to use `outline` than to use `border` . Why?
  - Because `border` affects layout, changing the width and height of its element. `outline` has no affect on layout, whatsoever.
- It's especially important to use `outline` instead of `border` when testing the cumulative layout shifts
- Good call. Its also useful to keep in mind when trying optimize for a better Cumulative Layout Score, if there are larger shifts in elements that could alter the CLS.  Though something as small as a border may not be enough for the algorithm to catch, I am not sure.
- Sometimes, I do prefer using backgrounds, like: `background-color: rgba(0,0,0,0.1)` , I can see how much an element takes, and how they stack
  - But most of the time, outline is the way to go

- ## Imagine if tools like Sketch and Figma let you write expressions the way Excel does.
- https://twitter.com/markdalgleish/status/1363703556109312007
  - e.g. calculating a background based on another element: `=darken(getBackground($ELEMENT_NAME, 10%))` .
- Transpile to CSS vars and ship as code
- Figma could expose the API in editor in addition to using it for plugins. That’d be sweet!
  - It's already done. You can use it in the console.
  - Good point. I think a part of writing “expressions”, not code is making it more approachable. For example, a small thing excel does when writing expression’s is letting you click to select fields and inserting them into the expression.
- It's really clever that Excel doesn't refer to writing expressions as "writing code." More tools should let you "write expressions" rather than underestimating their users' intelligence.

- [Excel is visual programming because you're placing data, labels, variables and calculations in physical space.](https://twitter.com/markdalgleish/status/1363727357169704963) 
- This makes VBA is the javascript of the spreadsheet world
- arent all programming languages like this as well? only difference is that it’s not bound by y and x axis

- ## Sometimes it’s overwhelming to change some complex feature in the existing code.
- https://twitter.com/BenLesh/status/1362762796501401601
- I used to do this. But it's often dangerous. I try to take a more measured approach now.
  01.  Make a couple of PoCs off to the side to see what I learn.
  02.   Carefully improve the code and add tests in the parts of the code I'll be touching, and see what I learn.
  03.   Add the feature.
- I find that after part 2 above, often the approach I take is different and better than what I did in some of my PoC work.
- The main difference between the new code and deleted code: The deleted code has been tested and hardened, if only by users. 
  - It already has behaviors that are expected. 
  - Depending on complexity, a "big bang" rewrite has little hope of recapturing all of that.
- Even when I've had insane test coverage, there were missing corners. 
  - I've found big bang rewrites have a higher probability of regression. 
  - Better to push existing code around until it looks like a rewrite. But this is my experience.

- ## The reason Vite requires .jsx extension for JSX processing is because in most cases plain .js files shouldn't need full AST transforms to work in the browser.
- https://twitter.com/RyanCarniato/status/1362178225493839874
  -  Allowing JSX in .js files means every served file must be full-AST-processed just in case it contains JSX.
- We have been struggling about enforcing this because it makes so much sense, but figured there wouldn't be enough community backing. 
  - But if major tools like Vite go this way that is amazing. It never should have been just .js when you consider compilation

- ## Introducing Blazepack - a super fast dev server powered by @codesandbox sandpack bundler.
- https://twitter.com/ameerthehacker/status/1361615692294852613
  - Supports @reactjs, @vuejs, @angular
-  It is a thin wrapper around the sandpack bundler, so it support React fast refresh, HMR and all the cool stuffs that sandbox supports

- ## How are some of you actually working on _side tech projects_? I'm struggling to even maintain energy for day-job projects lately.
- https://twitter.com/brian_d_vaughn/status/1361520253604421634
- I get anxious without side project. It’s how I relax.
  - When the brain is full of errant(错误的、行为不当的) thoughts and ideas, only way to get anything done at work is to regularly clean the brain.
- don't believe everyone on twitter. Specially in the Dev community.
  -  I have experienced it a lot that people try to talk them selfs better than they actually are. Per se it is not a problem. 
  -  But it promotes a bad reputation for devs. We don't code 24/7

- ## Offline support has been part of the PWA installability criteria since the beginning. 
- https://twitter.com/ChromiumDev/status/1358817467661967365
  - In Chrome 89, we'll warn you if your PWA doesn't have an offline experience. 
  - In Chrome 93, we'll start enforcing the updated install criteria for new PWAs.
- If all you need is a baseline offline fallback page without actually delivering a true offline experience (which, acknowledgedly, many apps don’t need or can’t), then give my article a read
  - [Create an offline fallback page](https://web.dev/offline-fallback-page/)

- ## When learning something new, it’s easy to fall in to the trap of comparing your work to seasoned professionals and think everything you’re doing is wrong. 
- https://twitter.com/steveschoger/status/1358588140328538115
  - Lately I’ve been trying to embrace this learning period because it’s a small window of great discoveries.
- Constant learning from seasoned profs, using my previous dev knowledge mixed with theirs, change code as I find better or more efficient solutions, seasoned profs's solutions are not always right or appropriate for the current app.  Having a blast and always learning.

- ## which companies are using @GraphQL in production nowadays?
- https://twitter.com/mxstbr/status/1358351658078634014
- Frontend teams at Danske Bank use GraphQL, mostly driven through Apollo. 
  - Microservices are still on REST so there's redundancy maintaining a mid-tier just for conversion.
  - GraphQL has most significant advantages when adopted by backend teams which isn't the case at most places.
- Using it in production at @skillshare . 
  - Running Apollo Gateway as API composition layer to allow frontend decoupled monolith -> microservices migration.
- @OrbitalChat uses it for admin-based stuff. 
  - The more interactive part is done with Firebase Real-time database and Firestore direct from the client. 
  - Also @SketchADay is 98% GraphQL and a couple of little plain JSON-over-HTTP bits
- GitHub and Contentful
- @AirbnbEng uses it quite a lot

- ## If you don't know which code is calling your function, use console.trance()
- https://twitter.com/sseraphini/status/1356654950198239233
- I used `console.log(new Error)` 

- I usually also do “console.log = console.trace” to locate and remove some console.log

- ## Hyphens are pretty. Underscores are ugly and don’t belong in URLs
- https://twitter.com/mscccc/status/1355525419152384002
- What about emojis in URLs? 
- [URL as UI](https://www.nngroup.com/articles/url-as-ui/)

- ## "The DOM is bad for apps" makes me laugh pretty hard. 
- https://twitter.com/_developit/status/1355670204366393347
  - It's effectively the same type of abstraction as a scene graph, but because we use it poorly it must be bad!
- I think the dom is very much bad for apps, who in their right mind would say otherwise. 
  - Why else do we have frameworks abstracting it. 
  - Most people don't know or see a dom when they make apps and that is a good thing.
  - That is the same reason why we have rejected a component model built on that pile of perpetual backward compat which is the dom.
- The browsers dom is virtual, bc it's faster. 
  - Every GUI system is split into a logical/virtual & a visual tree, otherwise you wouldn't be able to schedule, or, well, virtualize. 
  - Ever used a virtual list, I suppose you did. 
  - FBs "vdom" has better scheduling than the "dom", facts. 
- aren't some of the most popular apps just app shells with a web-view?
  - that, or react-native which uses a tree abstraction very similar to the DOM anyway
- Well, if we just used fixed height for everything and there was never a need to refresh layout I think most html apps would be as fast as 'native' - as if running apps in a JVM/runtime is native anyway - if it's not assembly writing directly to a framebuffer it's trash

- ## Software tradeoffs
- https://twitter.com/housecor/status/1355144710185230336
  - Build vs Buy
  - Reuse vs Copy
  - Sync vs Async
  - Serial vs Parallel
  - Dynamic vs Static
  - Concise vs Explicit
  - Unified vs Separate
  - Secure vs Convenient
  - Simple vs Configurable
  - Centralized vs Distributed
  - Convention vs Configuration
  - **Avoid picking sides. Think tradeoffs.** 
- I am not sure you want to trade off security for convenient
  - Perhaps, but companies do so everyday. 
  - Using other people’s software is convenient, but adds security risk by trusting other people’s code.

- ## Will Vite replace vue-cli? 
- https://twitter.com/youyuxi/status/1354584410482499585
  - Initially I wasn't sure, but at this stage I believe it will eventually be the case.
  - The main disparity(不同；差异，悬殊) now is just test runner integrations.
- Check out uvu by @lukeed05 . 
  - Native ESM support, very much in the spirit of Vite. 
  - No test compilation step by default, no special integration needed.
  -  When I need to test in the browser, I just start my Vite dev server and use puppeteer in uvu tests. It's refreshingly simple
- We could make a plugin for web test runner
  - It should be relatively straightforward if we can proxy browser requests to some transform API or middleware. 
  - We already have a plugin for snowpack
- There was discussion in vue-cli about letting plugins replace webpack as the builder
- after a few years of running large enterprise apps on vue-cli, I've had to break out of the test runner integrations to avoid the lag time between test runner updates, and vue-cli updates. 
  - vue-cli is still a great tool... 
  - But would love to see a more decoupled approach in vite

- ##  what are your team’s package.json script naming conventions for development mode, your build stage, and potentially running the built thing?
- https://twitter.com/jaredpalmer/status/1353083840424763392
  - I used to be in the ‘start, build, start:prod’ team 
  - but now I’m actually leaning toward ‘dev, build, start’

- ## A little technique we use all the time to audit the layout shifts and avoid performance issues.
- https://twitter.com/smashingmag/status/1352185650091581441
01.  Add * { outline: 3px solid red } to your CSS.
02.  Record the loading of your site/app.
03.  Review it by exploring what happens in slow motion.
04.  Adjust and minimize shifts.

- Great tip, thanks! This one's less visual and more programmatic from the 'Performance' tab in Chrome.
  - You can hover over the 'Moved from' keys and this will visualise the movement in the browser window.
  - And using this method you can even see down to the shift caused by web fonts loading.
- We can also use a `PerformanceObserver` to log elements causing layout shift to the console
- Remember this trick from when i started to learn css.
  - Always use to troubleshoot when some problem arises while postioning elements..
