---
title: thread-pm-app-marketing-office-saas
tags: [marketing, office, saas, thread]
created: 2023-10-10T14:19:05.850Z
modified: 2023-10-10T14:20:13.855Z
---

# thread-pm-app-marketing-office-saas

# guide

# discuss-stars
- ## 

- ## 在 CRUD Boy 很便宜的环境里，做本质上用来取代 CRUD Boy 的 Retool，肯定是不那么直观的。
- https://twitter.com/CatChen/status/1717648929679114356
  - 美国公司进行 IT 采购时，往往会先看 Gartner Report 上这个领域的竞品都有什么，然后发 RFP。中国公司如果上不了行业报告，别人根本不会发 RFP 给你。
- 在国内，大企业不会采购，小公司的采购会把你转化为外包公司

- ## Immutable software means people *can* create workflows, can learn, become experts, and optimize their experiences through automation. 
- https://twitter.com/andrestaltz/status/1433782109458649102
  - Software should become a foundational building block for productivity habits, not a "service" that changes every year. 
  - SaaS has poisoned software.
- There is now a real opportunity for the "please don't change this software anymore" monetization model, simply because the pursuit of endless ROI drives business to force bloat onto the same piece of software. This has to stop, but under capitalism, it cannot stop.
  - This is the reason why FOSS alternatives are rightfully filling the gap, because SaaS is making software become worse over time.

# discuss
- ## 

- ## 

- ## 💰 今天约了聚水潭（ERP SaaS）的人来现场，我以为是顺带演示的，
- https://twitter.com/thecalicastle/status/1726925858705908220  
  - 结果过来跟我说专业版一年 ¥8888，要大老远跑过来亲自说，不能微信一句话解决？官网也故意不明码标价，一定要联系上门。
  - 我记得金蝶也是如此…国内 SaaS 故意的吗？很少看到有随时可以取消订阅的那种，定价方案都故意不写的。
- 企业SaaS的Price on Request的做法其实国际通用，尤其是走按月订阅的，需要看客户体量和需求灵活定价，也顺便找找product-market fit，而且会比如先让你免费试用x个月然后直接锁一年。一些个人/power users级别的SaaS，$100以下的一般都会明码标价。
- 他们家的收费比较迷，最近两年为了上市，搞了很多收费方式。如果没有生态问题，可选还是挺多的。销售不演示倒可能是人员质量参差吧。这类产品遇到好的销售很难

- 不同渠道价格不一致，所以没有办法标在网上；过来见面说，而不是微信，是因为怕你不是诚心买而是打探消息
- 很多B端业务还是很依赖线下的沟通和客情维护的。不过连个演示都没有未免有点离谱了，好歹也应该线上调研完需求再带着方案来。估计是一个不靠谱的渠道商。

- ## how did Dropbox end up looking more like Microsoft than Microsoft?
- https://twitter.com/blankresident/status/1725475017767428479
- They had a great product, got greedy and took on lots of capital to build a mess that no one wants

- ## 云计算最近十年确实过热了，热到无脑上云的地步，
- https://twitter.com/skywind3000/status/1718599103565742409
  - 创业公司业务变化大，可以理解，但业务稳定后需要下云缩减成本时，
  - 很多常年被云服务宠坏的人似乎已经失去了独立搭建完整服务的能力了，其实从购置服务器开始，徒手弄好线路接入，vlan，虚拟化和容器，文件和对象存储，数据库和缓存等东西还是很好玩的。
- 业务初期最好做个数据中间层，比如你需要一个分布式文件系统，那么别直接用云服务的，自己封装个 http 接口，后面可以对接云服务，也可以随时切换成自己的服务，不用改业务代码，还有个好处是，前期及本地开发时可以对接内部的轻量级分布式文件系统，比如用 mongodb 的对象存储模拟一个，既简单有轻量
- 购置好服务器，总得找机柜吧，这就得和运营商打交道，还要把服务器运到机房。如果想搞点灾备和多活还得快递到异地。维护起来更费劲，有问题可能还要跑到机房重启。零零总总，体力活是少不了的。

- 云计算现在很大问题在于，成本如果按照3-4年前计算还行，但是这2年服务器CPU、内存、磁盘的成本都大幅下降了，固态存储和内存今年已经是白菜价，但是云服务价格完全没有下跌。

- 从云计算原理，需要计算资源的高度共享和充分复用才能产生效益，而现实世界的运行并不都适合现在的云计算来解决问题，所以云计算回归常态也是正常的。在没有巨型电子商务平台业务来填满云平台时，其资源有效利用率不支持价格降低的

- 云计算使很多人创业起步简单了（看似）

- 准确来说，人们不是“失去”了自建能力，而是绝大部分人从来没有过这种能力。自建可从来不是一个简单的事情，“徒手”就能做大概是管杀不管埋的水平。至于自建的标准有多高，可能要视项目规模来定。有个很简单的标准，只要核心负责人能承担风险和责任即可。云服务能卖出去的一个核心原因，是责任外包。
  - 包不起，云服务可承当不了这个责任，腾讯云多少次把创业公司的全部用户数据搞丢，你们忘记了么？自己不做数据安全，想靠云厂商责任外包的结果就是把自己公司搞到面临倒闭。

- 云服务厂商希望卖给客户的愿景是降低运维成本和更高的SLA。但事实是以99%的公司的业务量而言，差一个点的SLA根本不会对业务带来啥关键影响。而随着基础设施软件的完善，运维的成本和门槛也在持续下降。我们两年前把除了对象存储外的所有云服务替换成了用二手服务器搭的超融合集群，成本着实省了一大块。
  - 是这样，原是关键数据越要掌握在自己手里，何况目前这种硬件成本如此之低，建两个私有数据中成本都远低于云服务器
- 一个云厂商=一个IDC+一个昂贵的软件研发团队。凭啥只卖IDC的钱呢？所以，自己有软件研发团队或者离不开运维人员的业务，用IDC自建绝对比用云服务的成本低啊。但在试错阶段，云服务节省的是开发和集成的周期成本，还是划算的

- https://twitter.com/jeffdylan535/status/1718645675838275679
  - 说到最近dhh放弃云计算的事情，想起来我2019年在某云计算公司思考自己事业前途的问题。当时我所在的team是做tidb的云版本，我思考得到了结论:
  1. 我们套层云皮，不懂底层，如果数据出问题了怎么办?
  2. 什么样的客户会需要集群版MySQL，又比MySQL慢，还不知道底层发生了什么的数据库？
  3. 这么大的数据量，为啥它不自己招几个运维去搭建一套tidb，或者直接用tidb？
  - 想来想去这个工作都很扯淡，还一堆人整天假装很在乎的样子在真加班演戏，就为了年底多一个月年终奖。想了半个月之后我就打算跑路自寻出路了

- 不过从创业者的角度来说我不会选 tidb，更喜欢云厂商的计算存储分离版本：
  1. 便宜，支持单机、扩容到15/16节点已经非常够用了。
  2. 兼容，bug 都能兼容，tidb 之类的 newsql 都是做不到的。
  3. 方便，和云平台的结合更方便，运维一致，比如利用 secret manager 定期自动轮训切密码。

- ## [Zoom introduces Zoom Docs, expands platform for next-generation flexible collaboration | Zoom_202310](https://news.zoom.us/zoom-docs/)

- ## DocsGPT：一个开源的基于GPT模型的文档助手，可和任意文档进行聊天，可本地部署。在处理文本数据方面具有很高的准确性和灵活性。
- https://twitter.com/xiaohuggg/status/1711657836252688443

- https://github.com/arc53/DocsGPT /python/ts
  - https://docsgpt.arc53.com/
  - GPT-powered chat for documentation, chat with your documents

1、适用于多种应用场景：从代码文档到学术论文，DocsGPT 可以应用于多种不同类型的文档，提供广泛的用例覆盖。支持的文件类型包括 MD、RST、TXT、PDF 和 ZIP。
2、文档检索与信息获取：该项目专注于通过自然语言处理技术来改进文档检索和信息获取，能够回答关于项目文档的各种问题。DocsGPT还可以根据你提供的信息和要求，生成各种类型的文档，如报告、简历、信函等。
3、代码示例：如果你需要在文档中插入代码示例，DocsGPT可以帮助你生成合适的代码，并提供解释和注释。
4、界面直观友好：DocsGPT 允许用户通过自然语言查询来检索信息，这使得用户界面更加友好和直观。
5、高度可定制：虽然主要基于 GPT，但其架构设计得相当灵活，因此用户或开发者可以根据需要集成其他LLMs模型或其他功能。
6、支持其他开源模型：除了支持GPT3.5和GPT4，如果你有足够的资源DocsGPT还可以支持Falcon-7b、Falcon-40b和llama-2-14b。
7、本地托管：为了满足数据保密性和安全性的需求，DocsGPT 提供了详细的本地部署指导。对于那些希望在自己的环境中部署 DocsGPT 的企业，该项目提供了个性化的部署支持。

- 我试了很多PDFGPT方案，chat pdf，gpt4langchain以及ChatGPT上所有PDF插件效果都一般，通病要不贵要不就是幻觉严重，目前是10万token以内用Claud2，超过10万token用ChatGPT切成多块喂给Claud2，不知道大家有没有更优雅的方法
- 复杂的表格解析应该还是不行 我试过langchain-chatchat 对于专业性很强的文档包含表格 图 这种现在都做不好 非结构化信息理解不了

- ## 我司 zoom 也开始卷协同文档了，咱就是说你们这些 apps 怎么都长一个样_202310
- https://twitter.com/unixzii/status/1711574302636859759
  - 还接了 AI

- ## 从我加入飞书开放平台开始，眼睁睁的看着这个部门从飞书直属的大部门，一点点被缩减，被合并，最终变成了 aPaaS 下面的一个小部门。_202310
- https://twitter.com/XGHeaven/status/1710940437299761325
  - 回想这一路，不由得为这个部门感到悲伤和难过。开放，本身是一件多么有价值和有意义的事情，最终却……
  - 总人数我不好说怎么变化，但是单块业务负责的人是变少了。另外偏向开放能力的投入也少了，更多的放在了一些有比较直接产出的业务上。
