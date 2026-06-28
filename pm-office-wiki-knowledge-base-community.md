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
# discuss-pm-office/saas
- ## 

- ## 

- ## [飞书为什么大幅裁员？ - 知乎](https://www.zhihu.com/question/650276476)
- 团创始人之一王慧文的一个观点： “中国的toB软件发展缓慢很大一个原因是中国企业分布是头部很大 尾部很多，但腰部企业很少。”
  - 飞书这样做toB生意的办公管理软件，如果做大企业大公司，首先很多大公司内部很可能会有一个团队就在做类似的系统，说服人家抛弃旧的换一套新的系统很难。其次，大公司难伺候，做大公司生意会陷入无穷无尽的定制化需求当中，但是“定制化”这件事是完完全全反规模效应的，字节无法利用自身的流量优势和规模优势，高薪聘请的各种工程师和产品经理只会成为成本负担，做这种生意只会沦为高级外包。 
  - 如果做小企业小公司，首先小公司就压根没有用你这套系统的需求，其次小公司也不具备支付能力。
  - 那做腰部企业呢？对不起，中国的腰部企业太少了。不够供养字节飞书如此之大的体量。

- 这是国内所有行业的问题，基本都是赢家通吃，然后剩下的就是强龙不压地头蛇在当地有着很深的根基但是出去又打不过别人的小公司, 要有腰部公司就一定要有完善的反垄断法，但实际上大boss们并不希望腰部公司多，一两个大公司对他们来说更好管理。
- to b行业但凡觉得自己是号人物的企业，都是定制化的需求。甚至自己公司内部控股子公司投资的子公司就是干这个业务的，所以市场上单纯做to b没有国资背景的民营企业都活不了。我们没有腰部企业，但凡有盈利可能的业务都会被国资收购
- 你觉得它是腰部企业，它觉得自己买单了就是大企业，就要定制
- 中国的小企业社保都不交，愿意为一个软件花钱吗

- 小米汽车：3年、3400人、100亿元；
  - 飞书：6年、巅峰时期8000到1万人、每年研发成本100亿。
- 不能这么比啊，造车模式这么成熟。产业链又不用自己掏钱建
  - 你说造车成熟，那我说飞书做的每个产品行业内有更加成熟的解决方案，文档office Google notion ，会议有zoom以及腾讯会议，聊天沟通有teams，钉钉，slack等一堆软件，所有板块都有非常好的公司作为样板，飞书完全不需要做0-1的创新，很多东西真的太省事了

- 钉钉团队不到2000人
- 钉钉1600人，企微600人，飞书7000人。2023年12月的数据。
  - 企微很多功能模块都是别的团队做的 比如会议和腾讯会议 邮件和腾讯企业有 文档和腾讯文档
- Slack起势的时候团队不过20来人，值200亿美金的时候团队不过百人规模。

- 中国互联网公司的人事管理制度是基于封建军事采邑制发展起来的。每个军事领主都会极尽全力扩张自己部队的规模，因为这个“管理团队的规模”，本就是和“帝国议会”讨价还价的筹码，也是日后把自己卖个好价钱的关键因素之一。
  - 年轻的时候我还纳闷，某些业务不赚钱，领导还热衷于扩张团队规模，怎么会犯如此明显的低级错误？后来发现是我幼稚了，一个封疆大吏，当下有皇帝和宰相的信任支持，不去扩张自己的势力，难道等着安稳进内阁退休吗？
  - 但是，穷兵黩武政策终究是不可持续的，哪一天帝国财政没了源源不断的收入，或者帝国宰相换了人，开始倒查军费，这时候某个公爵的扩张策略也就走到头了。
- 我也是上了两年班才明白，互联网里领导的权利很大一部分来源于下属，特别是下属的规模
- 确实是这样，没有哪个封疆大吏会主动减少自己的团队规模，除非上面一刀切硬性规定，所以每个团队都会按自己的上限去抢HC，然后把HC用足，至于投入产出比，who cares？“先招进来再说，哪怕过来帮忙整理文档也可以啊”
- 上上下下都是利益共同体。我还见过“招不到人说明你们不缺人，明年就不给你们分招聘名额了改分裁员名额”的奇葩逻辑

- 关键B端互联网赚不了快钱哪。。。一个企业三年回本已经算很好了，真正开始挣钱一般都是第五第六年，核心客户都稳定下来了

- 你见过做一个 APP 需要 8000 多人的么？通过内部养蛊淘汰的方式筛选掉不符合字节跳动价值观的人, 最终留下的，身体好、热爱内卷、技术尚可（打螺丝）

- 疫情时候真的拼命砸人进去，一定要成功，如果晚点被甩了。

- ToB要一家一家谈，一家一家落地，一家一家擦屁股，这都不是互联网企业的优势。
  - 所谓办公软件，把聊天文档集成一下基本OK，什么公共知识Wiki这种纯粹是屎上雕花。
  - 至于ERP最看重的事件流、业务流程，纯粹是成本极高的个性化定制，互联网团队过去就是做外包。
- 据我所知，国企用钉钉的都是直接一队人过来做适配，内部再出一队人把已有的应用移植到钉钉上，小公司学不来

- 其实美团是一家 saas 公司

- 
- 
- 
- 
- 
- 

# discuss-file-based
- ## 

- ## 

- ## 

- ## 

- ## [Exploring a folder-as-page approach for file-based PKM : r/PKMS _202601](https://www.reddit.com/r/PKMS/comments/1qdqad1/exploring_a_folderaspage_approach_for_filebased/)
  - I've been thinking a lot about file-based PKM workflows and wanted to share an approach.
- One friction I kept running into was the separation between:
  - project files living in folders, and
  - notes or explanations living somewhere else
  - In practice, this often meant losing context over time, especially when revisiting old projects.
  - So I tried an experiment where folders themselves act as the primary unit of organization, and notes are layered on top rather than stored separately.
- The core ideas of this approach are:
  - each folder functions like a “page”
  - the folder structure stays exactly as it is
  - notes are written in Markdown alongside real files
  - files or subfolders can be referenced directly from the page
  - search works across both file names and note content
- This isn’t meant as a replacement for existing PKM tools like Obsidian or Logseq. It’s more about exploring whether annotating the file system itself can reduce friction in certain workflows.
- Conceptually it’s very similar to how index.html works for a directory. Each folder can have a corresponding Markdown note (stored as a regular .md file in that folder), which acts as the “page” for that folder.
  - The main difference is UX: creating or removing that note is exposed as a simple action in the UI, so users don’t have to think about managing the file manually if they don’t want to. But the content itself is still just a normal Markdown file living in the folder.
  - From a storage perspective nothing special is happening — the UI just reduces the manual overhead.

- I use obsidian. I’ve come across the idea of using a moc (map of contents?) idea.
  - This would look like something like: Fundamental heading List of fundamental ideas- basically linking the page
# discuss-patterns
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What's the benefit of date stamp or Zettelkasten-style id prefixes for digital notes? : r/PKMS _202606](https://www.reddit.com/r/PKMS/comments/1ugc2lk/whats_the_benefit_of_date_stamp_or/)
  - I'm just wondering what the advantages/disadvantages are for prefixes for notes such as YYYYMMDDHHmm or Zettelkasten ID. To me it seems less useful for digital notes but I'd love to hear opinions.
- Its a matter of preference if you need it as a prefix. But timebased UID is very useful and gives your note a fixed adress. I prefer YYMMDD-hhmm. 260626-1852 is instantly readable and tells a story. 202606261852 not so much.
- what happens if you need to update? Do you update the time and date stamp as well?
  - Its in the bottom of all markdownfiles with the tags, and never changes, so the file have a fixed position from start. I normally only have titles/filenames without UID to make things more relaxed. For me the only way to make sure I always have the date of a file.

- I like having a creation date and time stamp in the text body of my notes, just for the sake of knowing when I had the thought or whatever.

If the note is of the type where the date and time of an update is important, I might add that to the update text.

Both of these things are easily done in Obsidian, with templates and hotkeys.

A ZK id really isn't needed for a digital ZK system. LInks and Backlinks take the place of the ZK id in digital systems. The id is a holdover from analog, paper based systems.

- I don’t prefix note names, and can still sort my notes by date(文件系统本身就提供了mtime)
- My understanding of Zettlekasten-style prefix is to relate notes to each other

- ## [Karpathy's LLM Wiki setup : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1uai1w2/karpathys_llm_wiki_setup/)
  - I've been using Karpathy's LLM Wiki setup (Obsidian + Claude Code) for about two weeks, and I'm pretty impressed so far.
  - It feels like a different approach to knowledge management. Instead of spending time organizing notes, I'm focusing more on collecting information and letting the AI handle much of the structure and linking.
  - For those who've been using it for a few months or longer, has it meaningfully improved your work or thinking? What do you use it for, and what benefits or drawbacks have you discovered over time?
- Honest question - if you now only collect information and all the linking, refining etc. is done through the AI - how exactly shall this improve your thinking? Its a good technique for managing code documentation - but i fail to see how this, in any way, improves pure knowledge work. 
  - The goal here is not to improve your thinking. It is to improve the LLM's knowledge of you and its memory and thinking. Obsidian in this model is just a tool for the LLM to store detailed memories of you and your projects.
  - It is also building a memory that is not agent-dependent. It can go with you between different AI agents.
- The goal of OP was stated clearly : does it improve your work and thinking.
- You must never forget: This is a great way to separate what's important from what's not. But it's not a way to learn at all. To learn, you have to connect your own neurons—not the AI.

- Karpathy’s method is a context-management strategy for LLMs. It’s not “shortcut Zettelkasten.” A Karpathy-style wiki could be a useful reference source. You could draw from it or be inspired by it. But the manual part of note-making and connection-finding in, say, an evergreen notes approach is the whole point. A tool for thinking by definition can’t do the thinking for you. It’s the difference between learning from watching a computer play chess and playing chess yourself.

- Karpathy took a point of view that the agent manages the wiki. He thought it would be too onerous for a human to do it. But I've been maintaining a second brain/wiki for 5 years before AI showed up. In my case, I am letting AI write and read from my second brain which makes it incredibly useful - it's like a "shared brain". I wrote about my perspective here if useful: From Second Brain to Shared Brain
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Migrating from folder-based storage to Paperless-ngx – need advice on structure : r/Paperlessngx](https://www.reddit.com/r/Paperlessngx/comments/1nt4xg0/migrating_from_folderbased_storage_to/)
  - I’m moving my documents from a traditional folder-based system into Paperless-ngx.
  - Here’s how I’m thinking of mapping that into Paperless:
  - Correspondent → the last folder before the files (e.g., Dr_Smith, 1stAve, 2ndAve)
  - Tags → the broader folder (e.g., Medical, Apartment Rent) + any extra context I might need later
  - Document Type → something specific like Lab Report, Lease, Rent Payment, etc.
  - Title → not sure what the best practice is here. What would you recommend?
- Just keep title detailed. I've recently migrated. Still trying to figure out things. Paperless can add tags from folders and subfolders automatically for docs in consume folder. So then you can go later and make that into correpondent, doc type, tags... Just don't overdo anything unless you see it working... Itself main use case is finding docs fast

- Very timely topic for me as well and will follow this conversation. Just started and trying out different ways. Now I'm using more and more workflows to set the Doctype first, then Correspondent, Path and Tags. In tags using OCR word matching.

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
