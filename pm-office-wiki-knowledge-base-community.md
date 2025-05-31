---
title: pm-office-wiki-knowledge-base-community
tags: [community, knowledge-base, pm, wiki]
created: 2021-07-27T16:34:27.575Z
modified: 2021-07-27T16:35:20.057Z
---

# pm-office-wiki-knowledge-base-community

# guide

# pattern: Zettelkasten
- [Zettelkasten? | Hacker News _201910](https://news.ycombinator.com/item?id=21208196)

- https://github.com/Zettelkasten-Method/10000-markdown-files /201601
  - 10, 000 markdown files. Useful for stress testing note-taking tools.
# pattern: Memex
- [Vannevar Bush - The Memex](https://lemelson.mit.edu/resources/vannevar-bush)

- [The Secret History of Hypertext - The Atlantic](https://www.theatlantic.com/technology/archive/2014/05/in-search-of-the-proto-memex/371385/)

- [Memex Explained: Everything You Need to Know - History-Computer](https://history-computer.com/memex-guide/)
  - The Memex was a conceptual system created by Vannevar Bush for storing data and retrieving it in an easy and organized manner. 
  - The system was to provide easy access to the large amount of knowledge that was already recorded. 
  - Building on the technology of his time, Bush described a new kind of device which was a sort of mechanized file and library system. He called it a “memex.” The word memex came from combining portions of the words (mem)ory and (ex)tender. 
  - Even though Memex was never actually built, the concept was used as a guideline in the process of creating our modern-day internet. 
# pattern: Xanadu
- [Project Xanadu](https://xanadu.com.au/ted/XU/XuPageKeio.html)
  - Project Xanadu is the name for Ted Nelson's hypertext work since 1960. 
  - We foresaw world-wide hypertext, clearly and specifically, even in the sixties when almost nobody could imagine hypertext
  - We long ago foresaw the problems of one-way links, links that break (no guaranteed long-term publishing), no way to publish comments, no version management, no rights management.  All these were built into the Xanadu design.
- Xanadu is a specific structure which we want everyone to understand, both as an abstraction and as an answer to what is still wrong with the Web.
- Xanadu is a specific structure which we want everyone to understand, both as an abstraction and as an answer to what is still wrong with the Web.
  - Lotus Notes, created by Ray Ozzie
  - HyperWave(tm), created by Hermann Maurer
  - MicroCosm(tm), created by Wendy Hall
# pattern: bulletjournal
- [Bullet Journal](https://bulletjournal.com/)
  - Bullet Journal® (aka Bujo) is a mindfulness practice designed as a productivity system. 

- https://github.com/bastianallgeier/bulletjournal /202112/js/inactive
  - https://bastianallgeier.com/projects/bulletjournal
  - This little HTML file is nothing more than a scratchpad for your weekly tasks and notes.

- https://github.com/fulgor/bulletjournal.md /202003/python/inactive
  - Python script to create a bullet journal in an plain textfile with Markdown formatting
  - It is about the idea of using the concept of a bulletjournal in a plain textfile. The second idea is to use markdown-formatting. 

- https://github.com/singerdmx/BulletJournal /202306/java/ts
  - open source platform for notebook keeping, ledger management, task/project management

- https://github.com/weekend-project-space/moon-note /202303/js/vue
  - https://weekendproject.online/journal.html
  - 数据全部存放再您的个人设备上，可以点击右上角导出，支持离线使用
# discuss-bulletjournal
- ## 

- ## 
# discuss-kb-ai
- ## 

- ## 

- ## LlamaIndex 是不是最合适自部署的知识库工具？最近真的得花点时间做起我的自助客户服务平台了，不能再当人工客服了。
- https://x.com/tualatrix/status/1882307965249884460
- 是, 作为从零撸了RAG, 再迁移用Langchain撸了一个, 最后再用llamaindex重构了一个大型项目的老板, 强烈推荐llamaindex --- 前提是你有比AI更强的能力, 不然遇到好几个坑, 你不会读文档读源代码, 是解决不了的
  - 很多企业也找我们做To B的知识库/智能客服接口, 这生意太累我就先没做

- 一般的 QA 需求，套个向量库，手写个 RAG 不需要几行代码。有新想法改起来也很容易。
  - 也是，先用基本的工具实现，有必要再上大型框架。
- 大型框架一定是没必要的，越晚下车越吃大亏。

- 我喜欢 LlamaIndex 的抽象，我们基于 LlamaIndex 在做企业级产品开发。可以灵活选择哪一层面用它，哪一层面裸，哪一层面用别的。

- 不是。LlamaIndex和LangChain都代码和用法都非常垃圾。大量使用依赖注入，非常难以定制化开发。建议使用CrewAI来做。 [一日一技：为什么我很讨厌LangChain | 谢乾坤 | Kingname _202412](https://kingname.info/2024/12/14/hate-langchain/)
  - 依赖注入是解决大型项目协同依赖问题的，没人能完全搞清楚所有依赖的组件，也不需要完全搞清楚，不屏蔽实现细节，每个人都会被累死，代码也没法看。难道Spring生态不支持扩展和定制？你这个理由很牵强。

- LlamaIndex 文档好，例子多，验证想法快。但是没什么扩展性，深入定制就得复制源码来改了。 
  - langchain 的 Langgraph 文档一般，但是框架灵活，可以结合其他框架一块玩。比如某个node 换成LlamaIndex，所以我选了Langgraph..

- dify 的license 禁止多租户，禁止saas 产品
# discuss
- ## 

- ## 

- ## The best way to preview PDFs at scale:
- https://x.com/pontusab/status/1924091702832517357
  ◇ Generate PNG
  ◇ Cache in Vercel CDN
  ◇ Use `<Image />`

- don't like Vercel `<Image/>`, litteraly a wrapper around `<img />` but it charges you money and doesn't work if you deploy out of Vercel
  - Next.js will still optimise your image using sharp
  - it’s definitely more than a wrapper. you can also create a loader function not controlled by vercel (well documented). we use it with great success on a self-hosted instance too

- If PNG will not be enough, try to generate SVG is much scalable. I'm using it for photobook building in UI, than generatin same PDF for printing.

- ## 大家觉得企业文档管理最好的产品是哪个？ _202501
- https://x.com/waylybaye/status/1877307423142146266
- 这个问题我比较有资格回答，申请答题：
  - 小团队可以尝试：Notion、Coda 这类轻便性管理
  - 大团队比较注重权限，可以看看 Confluence
  - 如果喜欢套件，飞书、Google Workspace 都可以
  - 这里不存在绝对最好，文档这个行业我做了那么多年，很多想法都是想通的，主要看你自己顺手哪个而已

- Confluence+Jira的生态基本无敌。

- 与其做文档，还不如先做一个更好用的ai写作编辑器，先做点再做面吧？感觉文档太多上下游和生态整合之类了… 比如微软用azure devops wiki居然很多，然后还有word和loop实时协作，然后基于sharepoint可以用copilot在teams里面检索，这整个生态链一旦一个企业用上就很难跳出了。

- 欧美企业用的最多的一定是sharepoint. 微软一贯的打包做法基本没对手。我遇到过的欧美中大型企业都用，反正打包在Microsoft 365里面。然后做技术的企业一般就是confluence。

- nextcloud也不错 主要是喜欢账户系统  随便设置共享 还有note 邮箱 群聊 视频通话等等很多功能 在线共同编辑也行

- ## [Paperless-ngx – Open source document management system | Hacker News _202310](https://news.ycombinator.com/item?id=37800951)
- one thing that keeps me coming back to DEVONthink: a learning classifier.
  - Paperless uses tags and will auto tag based on previous scans. IME it works very well (as long as you have a decently sized library of tagged documents) and seldom do I have to add my own tags. It’s not perfect, though, and sometimes I have to go in and fix some of the tags.

- 🐛 Paperless-NGX doesn't have document version history, unfortunately.
  - Right now I am looking at OpenProDoc(java) and bitfarm-archiv as document management possibilities.
- I am just rcloning my paperless-ngx document volume to s3 deep glacier every night for this.

- ## 企业内部知识库系统，带个 RAG 这种，很长一段时间将只会是免费开源的天下。
- https://x.com/wwwgoubuli/status/1867976505697165417
  - 我知道有一些商务的例子，我当然也知道永远都会有。但这没法成为一个可靠稳定的商业需求目标。
  - 搜索与召回是个狗都能写，但要提升一点点点点都极其困难。
  - 剩下看模型。怎么看都是开源免费的天下。

- 我觉得知识库最难的在于你怎么把系统内的文本做有结构化的组织。搜索跟召回更大程度的依赖与你给予的语料，而语料是从你处理过的数据中来的。而不是直接拿的原始的数据。
  - 所以说这个事情几乎不存在什么通用解，每个业务中都要精心地来构造对应的二次语料，这事儿能干，但不轻松

- RPA可以是RAG数据输入或输出外设，延伸了RAG和模型的应用场景
  - 机会一直有。能找到客户，满足需求，有付费意愿

- ## 🧩 [如何具体实践Zettelkasten卡片盒笔记法的？ - 知乎](https://www.zhihu.com/question/424376132)
- 卡片笔记法三大核心：
- 卡片及时记（建立卡片库）。它可以是一句话，也可以是一个灵感，也可以是一片文章
  - 卡片模板架构：唯一编号（编号+日期+标题）+出处+摘录+复述（一事一记）+链接（主卡入口）。这个步骤叫做信息录入。
- 深度思考及时理（建立永久库——你的知识体系）。核心强调一点：深度思考+关键词标签。
  - 我们需要对卡片内容进行深入思考，去其糟粕留其精华，并且对该内容贴上分类标签。这个步骤叫做信息加工。
  - 永久库模板：标题栏+短文+知识链接九宫格+参考文献+引用目录
  - 永久库的标准：深度思考后的信息，要做到后期再调取使用时立马可以用。
- 卡片笔记库的核心：目录。
  - 一个是永久库的清单目录。一个是内容的主题词目录。使用超链接功能，将目录与永久库链接，实现信息对接。这也是我们随取随用的关键。该步骤目的是为了方便信息提取。
- 以上就是卢曼卡片笔记法的骨架三部曲。

- 卡片笔记写作法的流程。
  - 通过阅读、反思记录闪念笔记。
  - 每隔2-3天将闪念笔记与卡片盒中的笔记进行联系，思考，整理成永久笔记，存入卡片盒。
  - 在卡片盒中将笔记与笔记建立连接。
  - 不断生长的卡片笔记逐渐自然生发，产生想法集群，形成主题，并建立索引。
  - 将主题进一步发展，产生洞见，写成文章或者著作。

- ## [Wiki.js | Hacker News_202007](https://news.ycombinator.com/item?id=23904193)
- Now, it is fair to complain that VisualEditor is difficult to get running on your own local Mediawiki instance, as it requires the suite of local node.js microservers (RestBase and Parsoid) that aren't part of the core PHP platform. That said, this is about to change! The upcoming Mediawiki 1.35 is supposed to move Parsoid into core PHP, and so VisualEditor is going to become a lot more default-accessible. : D

- Mediawiki has some UX and RBAC challenges that makes it difficult to scale to large organizations.

- Wikis also don't need (or indeed, even permit) cumbersome Git and PR-based workflows just to get changes into the "wiki". Better for it to be a single-page app that actually implements a wiki, than to provide a service that doesn't actually support wikis but has no qualms about throwing the word around anyway.

- I tried DokuWiki at first (has flat file db which is cool). It's simpler, but I ended up going with MediaWiki which is more powerful, and aside from Wikipedia using it, I noticed most big wikis I use also use it
  - MediaWiki lets you choose Sqlite as an option, so I have one big wiki/ folder sitting in my Dropbox folder symlinked into my iCloud folder and local fs
  - The problem with most apps is that they just become append-only dumping grounds where your only organizational power is to, what, create yet another tag?
  - My advice is to just look for the text files scattered around your computer and note-taking apps and move them into wiki pages. As you make progress, you will notice natural categories/namespaces emerging.
- I did start similar things over 10 years ago. Where I am at these days is just text files ( markdown ) nested into folder structures. I've found this the most sustainable for quite a few years and it's been super useful. Main thing is, do whatever, as long as you find it easy to sustain.

- My two biggest complaints about MediawWiki are 1. PHP, and 2. no well-supported way to opt-in to a different syntax like Markdown or AsciiDoc or pretty much anything that isn't MediaWiki-flavored wikitext.

- ## 如何看待语雀付费策略？_20221026
- https://www.zhihu.com/question/562238887
  - 从2022年11月3日实施，个人版开始收费了，最低年费 99 元
- 对于免费用户，主要做了 2 个限制：
  - 总文档数不能超过 100 篇（包含小记、文档、数据表、表格、画板等）
  - 不具备互联网公开分享能力。

- 我觉得最大的原因在于：语雀自身定位改变，从内容社区变为工具定位，过程执行有点粗暴，从而带来的用户心智冲突。
  - 从创作者角度看，你是内容社区，我来帮你填补内容，互惠互利，所以你要给我一定的激励，可能是积分折扣或者需求反馈优先级等方面，然后我也很愿意为增值部分付费。
  - 但对基础的社区分享交流能力的限制，这很不互联网精神，语雀你之前标榜的『解决知识的孤岛』的初心哪去了？就会觉得非常的匪夷所思。
- 这 2 个新的限制，恰恰是对这类人的一个非常大的惩罚，或者说背刺。
  - 100 篇文档能够个啥？尤其这是包括小记的。调整后的 100 篇/月会好一些，但我觉得也不应该把『小记』纳进去，它违背了语雀小记的初心 - 从碎片化到结构化的信息记录工具。"亲，你这个月脑爆太多了，休息下吧"？？？
  - 不具备互联网分享功能 -- 创造的产出无法被分享，无法被评论和交流，这是对创作者最大的惩罚。
- 从语雀平台的角度看，现在准备改为工具定位了，我是在帮你们创作者更好的创作内容，所以你付费是天经地义的
- 现在既然语雀本身不做社区了，那对于流量分发环节得提供一些便利些吧？譬如：
  - 更好的 Markdown 导出能力？目前只能说勉强可用。
  - API 是否会重启维护？因为我们需要通过自动化的手段来降低分发成本。
  - 甚至支持一键发布到知乎等多个平台？这些你们是做还是不做？
  - 文档的标签功能呢，这也是工具的基础能力。

- 效率工具推荐
  - 大纲编辑器：幕布、Workflowy
  - 在线 Office：金山文档、腾讯文档
  - 灵感收集工具：@flomo浮墨笔记
  - 轻量级便签：SideNote
  - 知识管理工具、在线协作中心：FlowUs 息流笔记@FlowUs
  - 白板笔记：Heptabase、氢图@氢图
  - 写作软件：Effie、Ulysses、Writeathon
  - 思维导图工具：MindNode、Xmind
  - 白板工具合辑：微软白板、Apple Freeform

- ## 语雀知乎上怎么这么多说好用的，看文章好像已经是同类产品的top1了？
- https://www.zhihu.com/question/434578818/answers/updated
- 语雀强大，但是有其局限性，比如：
  - 适合搭建知识库，但是更多的是做线上“杂志”；
  - 按钮复杂，对小白很不友好；
  - 知识的流动性较差，就算基础功能强大，也不适合日常记录；
  - 仍旧是office word逻辑，也就是说说office - word没有解决的问题，它也解决不了
- notion & wolai
  - 块随意拖动，用设计的思维打造美丽页面
  - 父子结构，打破传统认知，让知识更成体系
  - 双向链接，让知识流动
  - 超级多内容格式的支持和强大的模板中心
- 语雀体验
  - 强大的知识库，内容平台中清流
  - 强大的社交属性，知识交友
  - 复杂的界面设计，和过于繁琐的操作
  - 没有逃脱的Office“魔咒”

- 语雀是只貔貅，只进不出，单向封闭的生态

- ## No XML space exports from Confluence 5.5
- https://confluence.atlassian.com/alldoc/confluence-documentation-directory-12877996.html
- From Confluence 5.5 we will not provide XML exports of the complete Confluence documentation.
  - The documentation has grown very large and contains content drawn from a number of other spaces for features that are shared between products (for example user management, application links, the universal plugin manager and more). 
  - This has made for a poor experience for users accessing the documentation locally (from an export that has been imported into their Confluence instance).
  - We will continue to provide PDF exports of the documentation for all major versions of Confluence. 
