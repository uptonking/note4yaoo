---
title: thread-domain-chat-im
tags: [chat, im, instant-messaging, thread]
created: 2024-01-04T01:28:02.550Z
modified: 2024-01-04T01:28:58.097Z
---

# thread-domain-chat-im

# guide

- chat-products
  - discord: 侧重语音/gaming
  - slack: 侧重企服/工作流, 类似有teams/mattermost
  - telegram: 侧重私人与短信，但已逐渐偏离短信
  - [15 Best Open Source Discord Alternatives 2024](https://rigorousthemes.com/blog/best-open-source-discord-alternatives/)
# draft
- rewrite discourse with apache-answer/NodeBB
# discuss-stars
- ## 

- ## 

- ## 

- ## 社交媒体的历史一图流
- https://x.com/oran_ge/status/1852562550522826925
  - 这里面的几个常青树都不简单, 还有个极速增长的 reddit, 怪不得现在都去 reddit 获客, 为什么中国的论坛没有这样的机会？
- 当然是监管的原因。当年我的论坛也有日活十万贴，月访问量三千万的光辉历史记录。被降维打击了一把，转眼也成了云烟。
- Pinterest 这个形态在国内也是没有。

- Instagram、Reddit、TikTok三大流量巨头，国内小红书、b站、抖音。

- ## 🔁 [Why isn't Bluesky a peer-to-peer network? | Paul's Dev Notes _202401](https://www.pfrazee.com/blog/why-not-p2p)
- The indie hacker spirit was strong in the NodeJS & Web community in 2014. There was a brief surge of interest in CouchDB and the potential for CouchApps. WebRTC had just stabilized and was being fiddled with.
- A couple of things then happened all at once:
  - Distributed systems theory became more mainstream
  - Bitcoin showed that novel protocols could make waves
  - DJB's NaCl became widely available, and, with it, more compact public keys
- This led to the formation of IPFS, Secure Scuttlebutt, Dat and WebTorrent at all roughly the same time.

- The BitTorrent variants
  - BitTorrent uses a Merkle Tree to represent datasets. 
  - This means that a torrent represents one static collection of files. 
  - Each project looked to replace the Merkle Tree with a new data structure which would still benefit from shared hosting and strong authentication while adding support for more dynamic data.

- IPFS: the Merkle DAG
  - IPFS still focused on content-hashes, but essentially broke each chunk of data into its own torrent that could be cross-referenced by the hash. 
  - A public key or DNS name could point to a hash to support dynamism. 
  - It used a DHT to look up and connect machines.

- SSB: the append-only log
  - SSB used an append-only log which was modeled as a signed linked list. 
  - Back references were content-hashes, making the HEAD a rolling hash. 
  - It used a gossip model to distribute data and "pubs" to connect peers.

- Dat: the merkle log
  - Dat also used a signed append-only log, but it used a merkle tree to reference nodes rather than a linked list. 
  - This gave a nice performance benefit over SSB, since it was able to verify signed heads against partial datasets using the tree structure. 
  - It used a DHT to look up and connect machines.

- My personal timeline
  - I joined the scene in 2014 by the good graces of Dominic Tarr, who allowed me to join him as the first application developer for SSB.
  - in 2016 I paired Electron with the Dat protocol and declared it a "peer-to-peer web browser."  I then stuffed in APIs for reading and writing the p2p files and started pitching it as the Beaker browser.
  - in 2017 Beaker supported the ability to "fork" p2p websites, so an indie social network called Rotonde briefly emerged on it where you created accounts by forking existing user sites.
  - in 2018-2020, The Beaker team experimented heavily with baked-in APIs for interacting with user data on the Dat network. This included an indexer in the browser which would create computed views from user data.
  - in 2021, Discouraged with the outcomes thus far — for reasons I'll explain shortly — I embarked on the another social networking project CTZN which I livestreamed. I began experimenting with hybrid p2p & server models.
  - in 2022, I joined Bluesky with a pocket full of dreams and a huge backlog of failed projects learnings.

- What went right
  - P2P makes some things extraordinarily easy. Beaker browser demoed one-click website creation and the ability to fork other people's sites. 
  - You could write entire applications as SPAs that would simply read & write files instead of relying on a server.
  - The data structures built by each protocol evolved significantly. There were some very innovative improvements in each technology.

- What went wrong
  - The pure p2p model suffered from an introductions problem (how do two users meet for the first time?) and so reliable delivery of events such as replies or likes was never solved. 
  - It didn't take long to hit data-scales that an individual device couldn't manage.
  - We never solved multi-device synchronization in a way that preserved the convenience of the technology. Same for key backup/sync.
  - DHTs were not reliable or performant. We were way too optimistic about device discovery and NAT traversal.
  - Doing everything on the user device opened new and difficult questions about resource management. When is it safe to clear cached data? How many connections can we keep open? How much CPU and RAM can our daemon eat before people notice? Mobile was a non-starter.

- By 2022, a number of us in the community had begun to re-examine our original premises from 2014. We generally agreed that device-hosted network software was simply infeasible, but we still saw a lot of potential in the data structures we had been using.
- Hosting agility
  - The general benefit from p2p we looked at preserving was hosting agility. 
  - Host-based addressing (the Web's traditional model) means that data published under a server's name becomes immovable from that server. 
  - Redirects may be suitable for an individual page, but large datasets will cross-reference records extensively and those references cannot be reliably migrated every time a user wants to move to a new server.
- Cryptographic structures
  - User data is encoded in a cryptographic structure called a Merkle Search Tree which was chosen for optimal proof sizes. This is a direct carry-over from our peer-to-peer work, and is what drives hosting agility.
  - In protocol terminology, we call this structure a "repository."
  - The repositories are designed to be highly cacheable and efficient to replicate.
  - A downside of this model is that the entirety of the repository is meant to be broadcast publicly. Selectively-shared data will require a separate channel within the protocol.

- Host discovery
  - Once we moved to the PDS model, the requirements for looking up hosts from cryptographic identifiers got less intense. 
- Aggregation data modeling
  - The data model we refined through the p2p era was an aggregation-based indexes. Users would subscribe to each others' datasets and ingest them into local indexes. Those local indexes could then be queried to provide a view of the application state.
  - This works well because it preserves the fact that each user's own dataset is an isolated space.
  - This model also benefits from eventually-consistent convergence. 
  - With Bluesky, the major difference from our p2p work was deciding that these aggregations would happen via large services (the AppViews) rather than on each user's own infra (their PDS or their device). This makes it possible to provide the high-scale networking that people expect from social experiences.
- Not quite P2P, not quite Federation
  - We ended up calling the AT Protocol a "federated" network because we couldn't think of a more appropriate term
- You can see why we settled on the name AT Protocol. In the technical sense, AT — Authenticated Transfer — references the use of the cryptographic structures, data which is inherently authenticated. 

- ## [Support ActivityPub for GitLab (&11247) · Epics · GitLab_202308](https://gitlab.com/groups/gitlab-org/-/epics/11247)
  - The goal of those documents is to provide an implementation path for adding fediverse capabilities to Gitlab.
  - Among the push for decentralization of the web, several projects tried different protocols with different ideals behind their reasoning (some examples : Secure Scuttlebutt or ssb for short, Dat, IPFS, Solid). 
  - But one gained traction recently : what is known as ActivityPub

- ## ⚖️ [FAQ | AT Protocol - Why not use ActivityPub for bluesky?](https://atproto.com/guides/faq)
- 🐛 Account portability is the major reason why we chose to build a separate protocol. 
  - We consider portability to be crucial because it protects users from sudden bans, server shutdowns, and policy disagreements. 
  - Our solution for portability requires both signed data repositories and DIDs, neither of which are easy to retrofit into ActivityPub. 
  - The migration tools for ActivityPub are comparatively limited; they require the original server to provide a redirect and cannot migrate the user's previous data.
- 🐛 Other smaller differences include: a different viewpoint about how schemas should be handled, a preference for domain usernames over AP’s double-@ email usernames, and the goal of having large scale search and discovery (rather than the hashtag style of discovery that ActivityPub favors).

- ## ⚖️ [Why not RDF in the AT Protocol? | Paul's Dev Notes](https://www.pfrazee.com/blog/why-not-rdf)
- There is a problem of semantic and schematic agreement.
  - Semantic: what names(属性名或路径) do we use to identify the types of data.
  - Schematic: how do we model the data — or more simply, what fields do we expect and how do we expect them to be defined?

- RDF was invented to solve these kinds of problems. 
  - You can see it used in ActivityPub, DIDs, Verifiable Credentials, SOLID, and a variety of other protocols designed for multi-vendor environments.
- RDF uses an elegant model of graph triples. Everything gets distilled down into nodes and edges between those nodes.
  - However, because these definitions are per-field, there are some additional work that's necessary to establish the schema in the full "document" sense. 
  - If it is important that pfrazee.com output both schemas.com/name and schemas.com/job, then you need to use additional systems inside RDF such as SHACL.
- RDF is notorious(臭名昭着的) for having a bad developer experience. While it is conceptually elegant, the heavy use of URIs inside the data model clutters(使乱成一团; 杂乱) a lot of the code.
  - it can be verbose and difficult to understand. JSON-LD and Turtle are two examples of this. 

- I think it's fair to say that you can model two separate systems correctly without preplanning thanks to the generality of RDF. However, very few systems natively use a graph model and programmers are not often familiar with it. The closest mainstream technology might be GraphQL.
  - I looked very closely at RDF during the AT Proto's initial design phase. One of the initial drafts for our schema system was based on RDF.
  - My belief is that a highly opinionated language (akin to Turtle or JSON-LD) which drops some of the features of RDF in favor of a more concise language could actually be effective. 
  - I ran out of time while exploring this option

- I believe that a document-oriented model is more intuitive for software engineers. 
  - The request/response bodies of HTTP and RPC systems are documents. 
  - Moreover, ATProto's data model is fundamentally a document store. 
  - Therefore, a document-oriented model seemed to be the best choice.

- The second draft of our schema system used JSON-schema, which did not solve any semantic concerns but does solve all of the schematic ones.
  - To solve the semantic element, we introduced the notion of a namespaced identifier (NSID) which is simply a form of reverse-DNS.

- We eventually conceptualized our target as a kind of "d.ts for ATProto" — that is, a type declaration language for all of the interfaces and data-types on the protocol.

- Using namespaced IDs is somewhat pointless if you can simply define all the schemas in the core protocol spec and call it a day.
- the other significant point of evolvability (that's in practice now) is the RPC methods. New ones can be defined, returning new schemas, and so on.
# discuss-forum-vc/market
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [L站估值多少？ _202603](https://linux.do/t/topic/1693851)
  - 差不多2亿，看到有人问始皇出去年包多少突发奇想
- 全员翻墙违法，没收违法所得。资产为负

# discuss-ai-customer-service/客服
- ## 

- ## 

- ## 

- ## 我至今还是觉得AI 客服这个领域，是我做过的最棘手的智能领域，可能没有之一。
- https://x.com/wwwgoubuli/status/1988098099299184909
  - 从最早提示词到RAG，然后后来尝试 agent，到现在又用路由模型分配机制， AI 客服这个事有个永恒的痛点。 用户对及时响应的需求太高了。
  - 实际落地里，我和合作伙伴们想过各种办法，现在效果其实还凑合，更好的交互，提示，缓存，或者把一个任务故意拆成几轮对话，不追求一步到位。
  - 方法很多，跑了这么久了，其实效果可以做的还行。不是说做不了。但总归还是比较难做。
  - 如果做一个 deep research，我大可以简单点用一些动画，把thinking step的 summary 放出来慢慢播放，反正用户预期本来就没指望一下子做完。
  - 但客服这个领域真的有点不太一样。客户不会有耐心等你那么久的。尤其是售前售后的领域不同，叠加上时刻变动的库存啊，SKU指标也会变化，还有销售部门的需求干预，客户往往又不满足于AI只做边缘上的一些服务。
  - 最后都会变成一个长得像AI客服，其实是贯穿销售和产品全领域的巨无霸。
  - 一方面有前台的及时响应的需求，一方面大量的离线任务在后面跑，还有一堆和现成系统的对接。

- 我们想的办法是把类型给他提前框出来，然后给用户选择，然后再来下一步交互
  - 我也是用AI根据业务类型前置预生成了很多路径，提前兜住。
- 我其实还做过一个方向，我给用户需求打标签，分类型，再来根据这个再来做下一步，然后中间设计一个链路返回给用户询问他是不是这个问题，然后再来进行下一步
  - 先雕花，然后把这些trajectory都记录下来拿去做RL

- 用户要的是替我说话、理解我、帮我办事

- 我也想做ai客服，问题非常重复就几篇知识库能完全解决，描述好问题rag搜索一下就行了。
  - 可是难点就在于很多用户无法准确描述出自己的问题，怎么让ai跟用户聊把真实问题弄清楚呢（真人客服也是这么做的）

- 需求巨大的领域，但是，仔细想下，客服是最不应该采用AI的领域

- 我在做我们公司内部的aiagent ，主要工作是配置报价，产品答疑，目前做的demo解放专业售前部分生产力，但是我的预期是这个agent是销售可以直接访问咨询获取报价。这样对初次准确率要求就很高，请问我该怎么做呢？固定销售提示词？可是即使提示词一样 每次也不同反馈。

- 关键是不敢给AI放权限，特定行为必须人类负责

- 我不是科技业者。在我们的公司里，关于AI客服最令人满意的不是用在chatbot, 而是用AI游览CRM给客户较全面和有利的电邮回复
# discuss-chat-credit/rewards
- ## 

- ## 

- ## 

- ## [LDC服务临时下线 - 运营反馈 - LINUX DO _202603](https://linux.do/t/topic/1770169)
  - 几十万积分无限兑换100E卡这太吓人了，LDC已经走偏了。
  - 从这个服务上线的第一天，就一直在强调，它只是社区活跃的积分，不是数字货币，更不是真实货币。但慢慢的还是在供需关系中走偏了，这是大家可以看到的事实。

- 亟需完善LDC的规则~ 必须打破这个 大米→E卡→LDC→E卡→大米 闭环~

- 京东可以直接买e卡，应该是为了用公益站专门买的，然后兑换 ldc 去换公益站余额

- [真理越辩越明 关于积分提出个疑问 - LINUX DO _202603](https://linux.do/t/topic/1770440)
- 支持态度吧，每日限额就能解决的问题
- 我觉得没利益的东西做不长的，不仅有理想世界，还有现实世界

- 禁止和金融活动挂钩，是为了防止洗钱。至于公益回血，本身就违背了公益的精神

- 三角洲的哈夫币还能变现呢，总不能也触犯法律吧

- 仔细想想看，梦幻西游的游戏币也是作为一种相当稳定的“货币”而存在，并且变现，dnf也可以变现。似乎，这并不涉及合规问题。

- 规模大点的都有经营许可证之类的吧

- ## [LDC 积分通货紧缩的情况，是市场的必然导向 - 积分乐园 - LINUX DO _202603](https://linux.do/t/topic/1688617)
- 现在 ldc 升值是在回归其原有价值，50ldc 的 team 在咸鱼卖 5 到 10 块，考虑到人工倒卖成本，ldc 与 rmb 汇率应该在 10 到 20 之间，现在才哪到哪呀

第一，ldc 为什么升值

从实际价值来看，以 gpt team 作为参照物，ldc 与 rmb 实际价值应当在 10 到 20 之间
从供需来看，很多 ldc 并不参与到市场流通。比如说，头部拥有 ldc 的佬友还不愿意出手收购京东 e 卡，这可能是因为 ldc 升值趋势导致的。从底部来看，可能有很多佬友还没有进入到 ldc 交易市场，或者手上的 ldc 还没有积累足够，所以没有出手
ldc 是有交易税的，每次交易市场上的 ldc 都有一定比例被回收到市场之外
第二，ldc 升值有利于谁，不利于谁

ldc 升值有利于广大持有 ldc 头部佬友（拥有大量 ldc）和底部佬友（拥有少量 ldc），不利于急于卖出京东 e 卡换取 ldc 的佬友
ldc 升值有利于广大持有 ldc 的佬友，为什么要强行引入干预机制，阻止 ldc 升值呢？这不是伤了最广大佬友群众的利益和热情吗？
第三，什么时候需要干预

只有当出现炒作，人为干预从中牟利时才需要干预。不过，这种情况很难发生，因为 ldc 的交易税很高，如果炒作干预市场，不说是否获利，几轮下来 ldc 全部拿去填补交易税了
因此，现在看不出来需要干预 ldc 升值，也没必要干预
综上，ldc 升值是在回归其本身价值所在，有利于广大佬友，没有干预 ldc 升值的需要

- 我觉得这也是始皇当时限制邀请码价格的主要方法。实际上LDC市场上，供给最大最有价值的东西就是邀请码，人为限制到500LDC一个客观上推高了LDC的需求，当然也大大降低了交易量。对于货币来说这不是好事，会导致抛售，但是LDC好就好在不是货币，大部分佬友都没有变现的需求，相当于有稳固的基本盘（笑）。同时推高LDC价值也能让低级别佬友获益. 其实始皇还有很多方法推高LDC价值，都还没用呢，比如邀请码可以设置500LDC一个，LDC又能蒸蒸日上了

- 升值的主要原因是流动性不足，大伙对于公益站和其他需要ldc服务的需求又很旺盛，最快的途径就是拿京东e卡换，但是因为大量ldc都掌握在少数的佬手里，形成买方市场，卖方为了出手只能不断压价，所以ldc对于e卡的汇率就不断上升

- 如果你觉得LDC积分购买力没那么高，那么就把东西搬到闲鱼上去赚差价
  - 如果LDC积分没那么低，那么就赶紧在论坛卖东西

- 一开始就说了，积分就是个玩具，是个情绪价值。只是因为佬友信任后给出一些有价值的东西，才会流通的。你不能将其看做一种真的货币，那你看啥都是价值了。虽然现在看上去好像是个等价物？其实不然，你就没考虑过ldc直接改规则呢？实际上已经调整过几轮了，你没来的时候已经权衡了，只要越界的帖子就会被删。说到底，还是你把ldc看得太当回事了。当大家都不拿东西来兑换时，ldc也就那个回事，啥用没有。
# discuss-discourse-tools
- ## 

- ## 

- ## 

- ## [上班逛 L 站的摸鱼神器，Word 主题风格 L 站 - LINUX DO _202608](https://linux.do/t/topic/2770736)
  - https://github.com/gbxhq/discourse-word-ui /js
  - 搞了个油猴插件，可以假装看 Word 的形式逛 L 站。
  - 总共花了几分钟，就一两次问答让 AI 搞出来的，可能有不好用的地方，有体验的欢迎大家提问题或者提 PR 哈。

- 更需要类似 cli 终端或者 VSCode 那种风格的
- 所以有没有 VScode 风格、Excel 风格的插件

- 侧边栏可以做成章节目录，感觉不违和还隐蔽
# discuss-discourse
- ## 

- ## 

- ## 

- ## 

- ## 

- ## ["Suppressed from latest" category vs. "muted" category. What is the difference? - Support - Discourse Meta _202603](https://meta.discourse.org/t/suppressed-from-latest-category-vs-muted-category-what-is-the-difference/158567)
- With muting, you can mute topics, tags, categories, and even users. Each context is a little different, though:
  - Topic: You will never be notified of anything about the topic, and it will not appear in latest.
  - Tag: You will not be notified of anything about new topics with the tag, and they will not appear on your unread tab. (Note that there is a remove muted tags from latest site setting to tweak muted tag behavior).
  - Category: You will never be notified of anything about new topics in the category, and they will not appear in latest. Muted categories are placed at the end of the category list on the Categories page and appear much less prominently.
  - Users: Suppress all posts, notifications, and PMs from a user

- ## [Can't edit my post? - Site feedback - Discourse Meta _202305](https://meta.discourse.org/t/cant-edit-my-post/267632?tl=en)
- The default edit time in discourse per trust level are
  - tl0/tl1 - 24h
  - tl2/tl3 - 30d
  - tl4 - unlimited

- ## [建议调整connect中“获赞: 单日最高数量”的表述 _202510](https://linux.do/t/topic/1060299)
  - 一开始以为 connect 中 “获赞：单日最高数量” 是指 “一天内最高获得 N 个的赞”，但实际并不是这个意思
  - 理解，应该是指 “获得赞的天里，天数达到 N”，可能是直接英译的缘故，导致中文意思偏差太大了，建议调整，例如调整为 “累计每日获赞天数”、“累计获赞天数”。

- 过去 100 天中获得赞的天数

- 翻译是硬编码在 Discourse 程序里的，疑似不行。

- 符合信任级别 3 要求，凌晨 4 点升级

- ## [不小心免打扰的帖子怎么取消免打扰 _202410](https://linux.do/t/topic/247306)
- 找到了，在 个人用户中心 - 偏好设置 - 跟踪 - 下面的已设为免打扰，点那个 “显示” 就会跳转到你设置免打扰的帖子列表页
  - https://linux.do/latest?state=muted

- ## [Understanding Discourse Trust Levels _201806](https://blog.discourse.org/2018/06/understanding-discourse-trust-levels/)
  - Sandboxing new users in your community so that they cannot accidentally hurt themselves, or other users 
  - Granting experienced users more rights over time, so that they can help everyone maintain and moderate the community

- Users at trust level 0 cannot …
  - Send personal messages to other users
  - Post more than 1 image
  - Post any attachments
  - Flag posts

- Get to trust level 1 by…
  - Entering at least 5 topics
  - Reading at least 30 posts
  - Spend a total of 10 minutes reading posts

- Get to trust level 2 by…
  - Visiting at least 15 days, not sequentially
  - Receiving at least 1 like
  - Replying to at least 3 different topics
  - Reading at least 100 posts
  - Spend a total of 60 minutes reading posts
- Users at trust level 2 can…
  - Invite outside users to PMs making a group PM
  - Daily like, edit, and flag limits increased by 1.5×
  - Ignore other users
  - Edit their own posts for up to 30 days after posting

- To get to trust level 3, in the last 100 days…
  - Must have visited at least 50% of days
  - Of topics created in the last 100 days, must have viewed 25% (capped at 500)
  - Of posts created in the last 100 days, must have read 25% (capped at 20k)
  - Must have received 20 likes, and given 30 likes.*
  - Must not have received more than 5 spam or offensive flags
  - Must not have been suspended or silenced in the last 6 months
- Users at trust level 3 can…
  - Recategorize and rename topics
  - Make their own posts wiki (that is, editable by any TL1+ users)

- Get to trust level 4 by…
  - Manual promotion by staff only
# discuss
- ## 

- ## 

- ## [Please don't use Slack for FOSS projects (2015) | Hacker News _201911](https://news.ycombinator.com/item?id=21415463)
- What's wrong with Discord?
- Everything that's wrong with slack, and more.
  No IRC gateway.
  Developers are extremely hostile to 3rd party clients.
  Centralized control.
  Ownership of your data.
- Slack has no public API for 3rd party clients; it's strictly for bots. The EULA says they can ban you if you use a 3rd party client. The clients I've seen require you to open browser web dev tools in the browser and copy your API key from the browser session. Even browser CSS modifications are apparently frowned upon.

- I think one often overlooked alternative is riot.im, basically discord/slack but with the ability to host custom servers and an emphasis on security.

- ## [Looking for a rocketchat alternative : r/selfhosted _202402](https://www.reddit.com/r/selfhosted/comments/1arc7wi/looking_for_a_rocketchat_alternative/)
- is there a user limit to mattermost for the free self hosted option?
  - No, but there's a setting for max users per team. It's set to 50 by default but you can change it.
  - but for both options, no sso included in the free version

- You can self host matrix/synapse (apache2 > AGPL)

- We use Zulip and it's great, we picked it over all main alternative (slack an the like). Fully open source so free self hosting

- "Nextcloud Talk is a fully self hosted, on-premises audio/video and chat communication service."

- ## 淘宝：钉钉，抖音：飞书，拼多多：knock，腾讯：企业微信，京东：咚咚，美团：大象，苏宁：豆芽。。。每个大厂都要把IM放在可控环境里
- https://x.com/ken_xu/status/1801577638961811562

- ## 我对 telegram channel 的新看法
- https://x.com/ThaddeusJiang/status/1798904722373664775
  1. 单向信息传递：所有者发布内容，订阅者消费内容。不适合我，我更喜欢相互碰撞，而不是单方面输出。
  2. 不够开放，对公共社区提供价值受限，甚至不如 http://X.com。http://X.com 上发布的内容可以在搜索引擎中找到。
  3. 有通知。我讨厌一切通知，我更喜欢异步生活和工作，我更喜欢 email 和 RSS。

- ## 🤔 近期在纠结 #Slack 和 #Discord 作为社群 IM 平台的选型。
- https://twitter.com/tison1096/status/1763774282914742550
- Your goal is to build a robust community not to choose a tool.
- Yes, full history without extra cost. Besides, discord has:
  1. Better threads support (easier to use than slack)
  2. One account difference profiles in different servers (no need to "find my workspace")
  3. Good permissions support (it’s still free!)

- Rust 社区用的 zulipchat 呢？
  - 太 Geek 了，我自己的项目我敢用，有一定大众需求的项目还是算了。另外一些集成方面还不如另两个丰富，直接的就是我要把 activities 接到 CommonRoom 上，另两个直接有集成，Zulip 理论上我可以自己写，但是实际上不太可能有时间写好。

- 感觉 Discord 跟企业微信的存在有点像，目的是跟用户对接，而非内部成员之间的联络

- 前段时间看到once出的campfire似乎也不错，299刀买断，有源码可以自托管

- ## [Is there any Slack self-hosted Alternative? : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/p8ahom/is_there_any_slack_selfhosted_alternative/)
- Matrix is great! Its a chat protocol that has many front ends your users can choose from. The most popular front end is Element. Why use matrix? At its core, the protocol is just for routing messages between clients and servers. This means you can join multiple servers (hosted by other matrix users). There's also bridges between other chat services so you can do all your communication in one place. Also, with Jitsi integration you can do video calls directly in the app.

- https://revolt.chat is open source (and in rust), and is easily selfhostable

- ## [Slack alternatives? : r/Slack _202307](https://www.reddit.com/r/Slack/comments/15180dl/slack_alternatives/)
- take a peak at this: https://zulip.com/plans/ . You can use a self-hosted one with all the features included.

- Mattermost, Rocket.chat, Zulip

- ## [Rocket.chat leverages the Matrix protocol for interoperable communications | Hacker News_202205](https://news.ycombinator.com/item?id=31535034)

- ## [Telegram: 700M users and Premium | Hacker News_202206](https://news.ycombinator.com/item?id=31802245)
- Telegram blows my mind. Say what you want about their security; 
  - they have the absolute best UX of any (primarily 1-on-1) messaging app, bar none.
  - And it’s lots of small features and details such as built in translation for messages in a foreign language, all the smooth animations, quick look and summaries of channels with aggregated links media etc, a super fast and responsive UI etc. 
  - And their stickers are actually ridiculously fun to play with (I used to not be into that, telegram converted me).

- Many people are asking what are in Telegram that aren’t anywhere else?
  - It offers you to simply share an alphanumeric handle and you can connect with anyone in the world. I can do a voice chat or normal chat really quickly and easily. It is the only famous truly Instant Messenger there is. And I can do it without sharing my name (unlike FB), email address, or phone number (unlike WApp).
  - The video quality in chats is really high. In Android, only Google Duo came close.
  - ONLY chat app in market with an excellent desktop app for Linux. Also Windows.
  - I love their non-SJW-everything approach to allowed stickers. 
  - UI/UX is excellent. Really love chat themes and how I can edit them. Many components are customizable. Chat bubble colors, radii of rounded corners, etc.
  - I like the fine-grained control over notifications from different chats (groups and persons).
  - I like the lack of E2EE. I just like logging in and having access to all my chats. I don't have to be with the same device to be on the same chat.
  - The simple yet effective image editor is nice. So is the text formatting with no fuss.
  - I often use the auto image resize feature to downscale images.
  - It is so seamless. It has replaced email when I want to transfer small files to my own devices.
  - I am a selectively social person. It's good that even with 700 mn people, not many people are in it. The people with whom I don't want to interact more aren’t yet in Telegram. That's an appeal to me.
  - Developing bots is a bliss. So easy and effective.

- Telegram chats are encrypted to and from the server, they're not E2E encrypted, they do not claim to be by default. They do offer E2E chats you can opt into, and there has not been a single example of an E2E message being cracked.

- Telegram doesn't encrypt any more than Discord: through https. Telegram offers a 1:1 e2e encryption option, but few use it, because it does not propagate to other devices.

- Telegram now is more akin to Discord and Twitter with bots, channels and public groups. It's been some time Telegram has moved from personal chatting app as WhatsApp.
  - The problem is just that Telegram still advertises itself, and people expect it to be a messaging app.

- ## [Gitter is open source | Hacker News_201707](https://news.ycombinator.com/item?id=14694283)
- Gitter is a great idea in theory. In practice it's just been a place for my questions to go unanswered.

- While I applaud the initiative of Gitlab to opensource Gitter I think the target audience for self hosting is rather small. I think alternatives like Zulip or Mattermost are probably better suited for most organizations.

- Asking users to run mongo, es, neo4j, and redis is a tall order. Mattermost just needs (AFAIK) a relational database.
  - Gitter is not intended to be a replacement for Mattermost, Slack or other team collaboration tools. We see Gitter as a community instead.
  - we use neo4j for suggesting rooms.
# discuss-telegram
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [关于tg封号和养号，老哥们有什么建议？ _202605](https://www.nodeseek.com/post-731929-1)
- 什么都不做放一个月

- ## [tg注册养号求助 - LINUX DO _202604](https://linux.do/t/topic/1911531)
  - 拿美国 + 1 虚拟号成功注册的 tg 之后，手机电脑和网页三端都登录 tg 之后，连中文搜索机器人还没加上就被拿下了。现在注册成功后有什么不容易被封的操作方法？只在一端使用比较好？哪个地方的号码更不容易被封？

- iPhone 注册，注册完什么都不做，先放一阵子（如果是 Android + Google voice 24 小时死的概率极高）

- 注册新号放一周，一周后添加官方机器人发送 start 看正不正常。

- 登网页端干嘛？新号不要登网页端，设置好 2 步验证就可以放着了

- 稳定节点登录后挂机 12 或 24 小时即可，我的号就是这么整的，目前啥问题也没有

- 我都是拿实体手机号先注册，然后换绑虚拟号，这样好像就很稳定

- 注册完 ip 不能乱跳和立刻加一堆群什么的，可能是滥用的太多了，tg 现在风控很严，最近注册了个号，固定 ip + 注册好关注了一两个频道 一个群都没加，等了两三天之后慢慢加群和频道没有触发风控

- 什么都别干，就晾在那，晾一段时间再说。你一来就加群私聊什么的，90% 被 ban

- 注册完之后，在手机上要一直保存着，有时候电脑会掉，只要你创建完别乱订阅频道/私聊别人一般不会封禁

- ## [关于 TG 账号安全与养号，你该知道的都在这里了 - LINUX DO _202604](https://linux.do/t/topic/2015217)
- 注册未满 7 天：新注册未满 7 天暂时双向，满 7 天后自动解除！
双向撸毛号：不能主动私聊别人，其他正常，后续可能会解封。
通讯录限制：无法通过手机号搜索用户，其他功能均正常。

- 无论是自主注册的还是购买的账号一定先绑定邮箱和设置 2FA 密码
  - 号到手别急着做任何事，改头像换名字改简介改用户名养几天再操作，不要急着加群如果急的话不要短时间内加入很多群，不要一进群就秒发言，不要秒私信别人，几分钟内不要私信很多人，总之号到手不要使劲造，干啥都慢一点。

- 避坑指南
干净 IP 环境
干净的设备，彻底清楚 Tg 应用缓存
无论新老账号，登录安稳养号。

- 
- 

- ## 📌 [关于TG注册以及权重问题 _202601](https://www.nodeseek.com/post-585334-1)
- 大部分网友在注册TG的时候时常会遇到SMS FEE或者绑定邮箱（一般情况代表号码差）
出现这个问题有3个原因，一个是IP，一个是国码，一个是号段
先说国码
TG对于注册号码的国家是有一些分层的，等级越高的号码越不容易被风控或要SMS fee
一般来说高权重国家一般分布在西欧，中东
西欧有奥地利、比利时、保加利亚、克罗地亚、塞浦路斯共和国、捷克共和国、丹麦、芬兰、法国、德国、希腊、匈牙利、爱尔兰、意大利、拉脱维亚、立陶宛、卢森堡、马耳他、荷兰、波兰、罗马尼亚、斯洛伐克、西班牙、瑞典、冰岛、列支敦士登和挪威等
东欧有乌克兰，摩尔多瓦，格鲁吉亚等
亚洲有日本，韩国，新加坡，台湾（需要sms fee)，文莱
中东有巴林，沙特，卡塔尔，阿联酋等
大洋洲有澳大利亚，新西兰

普通权重国家有：加拿大，美国（虚拟号段），英国，罗马尼亚，爱沙尼亚，香港，泰国，越南等
低权重地区有菲律宾，缅甸，哥伦比亚，萨尔瓦多，洪都拉斯，蒙古，南非等
一般情况下高，中权重地区号码注册无需sms fee（部分因为短信成本原因和号段原因需要）
低权重地区号码需要sms fee且注册后换设备需要当地IP，否则会封禁，典例菲律宾
sms fee和号码关系还是大的，比方说南非，什么IP注册都要收费，然后账号稳定性和风控的话，号码属国和号段是最重要的因素 

sms fee出现的另一个原因是号段
号段差的表现除了出现sms fee的页面有时也表现为不收费但是要绑定邮箱 或 被需要更好的IP

- 最后也是最重要的原因——IP！
一般情况下当注册IP的风控值大于80%且为机房IP的话会导致所有国家号码的注册行为都会弹出sms fee
当注册IP风控值小于40%但IP为机房时高权重地区不收费，中权重地区部分不收费
当注册IP风控值小于35%且为原生住宅IP时，高，中权重地区大部分注册无需付费
以下国家注册需要本地纯净IP注册才不会要sms fee（概率问题）：爱沙尼亚，罗马尼亚，斯洛文尼亚
以下国家付费也不发验证码：蒙古

- 如果遇到收费怎么办
换好一点的IP是个好办法，或者用低版本的telegramX（高版本该注册不了的还是注册不了，报错400）注册从根源解决问题
养号时尽量不要用多个设备登录一个账号，不要用劣质IP，不要大量私信，不要用同一个IP登录不同账号

- 
- 
- 
- 
- 
- 
- 

- ## [TG解封文本 _202605](https://www.nodeseek.com/post-753245-1)
  - 第一步：点击 ：@spambot
  - 第二步：点击：this is a mistake
  - 第三步：点击：Yes
  - 第四步：回复 complaints

- ## [【请教】为什么有些佬友偏好TG，相比大陆的社交软件，TG有什么优势吗  _202603](https://linux.do/t/topic/1755448)
- tg server不开源

- 机器人生态丰富。
- telegrambot申请只要几秒钟，而且不会封，就这么简单

- 你估计没有体会过微信消息发不出去。自己这边显示发出去了，对面啥也收不到。

- 用斜杠命令方便呀
  - 而且群组功能生态也更好
  - 感觉tg和discord都明显比飞书好用，qq那边还没试过

- 就两个字，好用。又流畅，又有涩涩，甚至可以当网盘用

- 首先是隐私问题，然后就是openclaw的tg机器人方便，/命令有补全，还能交互，很方便
# discuss-accounts-tencent/腾讯
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [国际用户如何注册QQ ?  - LINUX DO _202606](https://linux.do/t/topic/2431020)
- 你真正需要的其实还是中国香港澳门的台湾手机号码
您可以通过网页版进行注册账号： QQ 账号注册
但说实话，国际注册的账号风控会高许多，其实用程度还不如您结交一个真正的中国朋友，让他给你一个注册过的 QQ 账号。

不推荐您购买账号，风险会高很多

- 现在是两个人了。 刚注册了一个 麻烦的狠

- ## [请问下海外手机号怎么注册QQ - LINUX DO _202503](https://linux.do/t/topic/521877)
  - 确实是支持美国手机号注册，但是一直提示当前环境不安全，一美国华人朋友想注册 qq 一直不成功遂来求助

- 只能国内手机号注册换绑
  - 换绑提示无法跨区换。。。。
- 现在已经不行了 只有以前换过的或者海外本土号才行
- 换个方法而已，你就手机号登陆，然后问你这个号是不是你的，你选择不是，就会默认解绑（一年只能一次）解绑之后就可以绑定国外手机号了

- 刚看了下，目前新注册网页只支持大陆以及港澳台的手机号了。
以前是可以的，我有一个 QQ 号，是用 google voice 注册的，还能用，但平时很少打开。
还不如让你朋友注册 wechat，更好用呀，也没有手机号限制。

- 注册不起来，之前用 gg 卡试过

- 

# discuss-accounts-us/payment
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 💰 [关于Gemini Pro 会员一年 Pixel 的优惠的购买 小坑 希望各位注意 - LINUX DO _202607](https://linux.do/t/topic/2605544?tl=en)
最近 用学生认证的几个账号 Gemini pro 会员都掉了，
然后闲鱼 20 元购买了 2 个 分别找的 2 个商家，Gemini pro 会员 整个认证都比较顺利 先去掉支付，然后开启验证器.
但有个小坑就是商家用的支付信用卡是 PaysafeCard 英国的，把我的 2 个美区账号都变成了英国支付信息了，也导致了无法加其他的美区账号到家庭组，本来还想自己在加几个号到家庭组进来，结果全都不行！
算是一点注意事项，分享出来。不知道哪有美区信用卡的商家 一条龙搞定想在买几个

- 你重新转回美区，或者把美区账号转到英区
  - 转不了美区了，必须要去掉 Gemini Pro 的订阅才能转，订阅没到期不能转 是按照 Google play 商店地区的

- 你把支付资料删掉，重新加一次就行了。其实不加也行，梯子挂美国节点就可以加了。 家庭组是看 Google play 商店地区的
  - 支付资料不能删，必须去掉订阅才可以删除 转不了美区了，必须要去掉 Gemini Pro 的订阅才能转，订阅没到期或不取消订阅 不能转

- 非常简单，我教你。直接去支付资料中吧地址随便改为一个美国就行了，然后吧家庭组关闭，然后你就可以更改为美国了，然后打开家庭组 就 OK 了！ 哈哈哈我昨晚也是
  - 听我的，不需要取消订阅 也不需要美国卡！
  - 受不了了，给你喂到嘴里。来来。首先去 https://payments.google.com/gp/w/u/0/home/settings 点击 国家 / 地区，填入一个美国地址。然后，去家庭哪里，把所有人踢出去，然后关闭共享，然后去 https://play.google.com/settings 这里就可以把地区改为美国了。然后打开家庭共享 拉人 OK

- 感谢 。
你第一个链接就是我截图的那个页面 点击 笔杆子后就会出现 Create new profile 链接 然后新添加一个美国地址， 在删除家庭组，然后在切换 Play store 的地区， 然后在创建家庭组，然后还有点击 start share 分享 google pro 套餐功能
注意 切换地区后原来的英区支付信息会删除，而且再次进入支付信息页面需要接短信验证码验证 如果无法接码的要注意一下！

- 两个号都关闭支付资料不就好了，又不会取消订阅，两个号同地区 ip，哪怕国内归属地的账号都能加 

- 可以转，先申请转区再删家庭组再去 play 上改支付资料到美区（需要一张美区信用卡做认证），然后再建家庭组即可

- 其实可以直接取消订阅然后删掉支付资料的，取消订阅不会取消 pro

- ## [A Comprehensive Guide to Tax-Free Shopping in Portland | Portland _202601](https://webpromo.com/blog/jammybear/3/en)
- Oregon has no sales tax, so you pay the exact price listed on the tag at checkout.

- Portland's shopping destinations can be broadly categorized into malls, department stores, outdoor outlets, and farmers markets, each with its own distinct appeal.

- The most historic indoor shopping mall in Portland is Lloyd Center.
Opened in 1960, this mall was one of the largest in the U. S. at the time and features an indoor ice rink, making it especially popular with families.
Located in the Lloyd District in East Portland, it hosts a variety of brand stores ranging from Mexicos to casual fashion.
It's a great space to casually stroll and compare various brands in one place.
The ice rink inside operates year-round and offers skate rentals, serving as a recreational space for local residents.

Located in the heart of downtown, Nike Town is a symbolic shopping destination given that Nike's headquarters is nearby in Beaverton. You can experience Nike's entire lineup firsthand, and limited edition collections are frequently released, making it a must-visit for sneaker enthusiasts.

Pioneer Place, also in downtown, is a representative shopping mall of Portland, featuring an Apple Store and high-end brand shops. The mall connects various stores and a food court from the basement level to the fourth floor, allowing for a comfortable shopping experience even on bad weather days.

- When talking about outdoor shopping in Portland, the REI flagship store cannot be overlooked. Given that Portland has a strong hiking and biking culture, the REI store is quite large. You can purchase everything from camping gear to hiking boots and bike accessories in one stop, and most of the staff are outdoor enthusiasts, making it easy to seek advice.

Additionally, Portland is home to the headquarters of Columbia Sportswear, and the flagship store located downtown holds seasonal sales.

- The standout farmers markets in Portland are undoubtedly the Portland Saturday Market and the PSU Farmers Market. The Portland Saturday Market, which started in 1974, is one of the oldest outdoor craft markets in the U. S., held every Saturday and Sunday near the downtown waterfront.
You can purchase various handmade items, jewelry, textiles, and prints from local artists, making it a perfect spot for travel souvenirs. It operates from March to December, especially busy during the holiday market period.

The PSU Farmers Market takes place every Saturday morning near Portland State University's Park Blocks. It operates seasonally from May to October, selling fresh produce, cheese, meat, jams, bread, and flowers directly from Oregon farms. It is one of the markets that represents Portland's food culture, and local restaurant chefs are known to come here to buy ingredients. There are also many booths selling freshly prepared food, allowing you to enjoy breakfast while shopping.

- If you're planning to shop in Portland, it's worth keeping an eye on seasonal sales events. With a tax-free environment and additional discounts during Black Friday or the holiday season, you can save significantly.
# discuss-apple-accounts
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [无限@icloud.com邮箱 _202607](https://www.nodeseek.com/post-817277-1)
- 由于注册gpt的邮箱使用域名邮箱容易风控，所以当你有icloud+服务的时候你就有无限邮箱了。
  - 通过逆向 iCloud Web 接口和 IMAP 邮件协议，实现 Apple iCloud 隐藏邮箱别名的创建、列出和邮件收取功能。

- ## [2026 年使用 邮箱 在 设置 中注册 任意地区 新 Apple ID 保姆级教程，解决注册风控问题 - V2EX _202604](https://www.v2ex.com/t/1207433)
- 一台 iPhone 或 iPad
- 注意：注册地区 = 当前装置的系统地区设定，请在注册前先确认装置地区是否正确
  - 注册期间不要更改装置地区，否则可能导致注册地区与预期不符
- 前往 设置 → 通用 → 语言与地区 → 地区，语言无需修改，确认地区与你想注册的 Apple ID 地区一致。
- 使用现有邮箱注册, 输入你的邮箱地址（如 Gmail / Outlook ）
- 验证手机号码

- 若注册后无法登录 App Store ，检查付款方式是否需要设置为「无」

- 
- 

# discuss-google-accounts
- tips
  - 接码和发短信验证会风控同一手机设备的扫码次数和同一手机号的接码次数，最好准备多个设备和多个号码轮流验证, 多次尝试了还是可能失败

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [佬们求谷歌号注册新方法 - LINUX DO _202608](https://linux.do/t/topic/2835435)
  - mac，梯子挺好的之前在手机上能注册成功，电脑上想注册个新号一直不可以，要么是让我拿手机扫码，要么是手机验证过不了

- ios 设备注册几乎是随便注册，也不知道谷歌为啥要给苹果开后门（对了，pixel 也能随便注册）
- iPhone 随便注册 Gmail，只要手机号能过关就行。手机号绑定的账号不能过多，近期没有频繁验证就行。
- iphone 的邮箱直接创建，手机验证都不要
- 用 iPhone，烂 IP 一样能过，甚至跳过手机接码

- 用手机 gmail 中注册，注册之后再登录
- 建议你在谷歌商店里注册，虽然注册后有概率被临时封禁，但是申诉一下就解了，成功率更高。web 端因为各种原因，还需要输入手机号
- 安卓手机很容易申请呀佬。我在 Gmail 里面申请，每次申请完隔两个星期，断断续续手里快 50 个号了，基本没被封过，不过刚申请下来会立马封禁，但申诉就可以了，申诉很快就过

- iphone 自带的邮件呀，里面添加账号谷歌，注册就行了，手机验证都免了

- ## [苹果手机Gmail登录多个账号方法 - LINUX DO _202605](https://linux.do/t/topic/2214695)
我前面使用 Gmail 登录 google 账号的时候，登录 10 个就无法继续登录了，提示超过了最大限制，后面偶然一次发现一个方法：

先正常登录，当后面继续登录的时候，提示超过了最大数量的时候
打开 Safari 浏览器，打开 google.com，点击右上角头像
可以看到有很多登录状态的账号，基本跟你的 Gmail 邮箱登录的账号一样
点击退出全部账号【不影响 Gmail 已经登录的账号状态】，然后点击删除账号，将上面登录了的账号都删除掉 【直接去 safari 设置里清除历史记录与网站数据也行，比较快，不介意历史记录的可以操作】
返回 Gmail App，重新添加 Google 账号，即可继续添加了
楼主目前登录了 30 几个，我看到有佬友登录 50 多个的

时不时注册一个，但是基本都要手机号，25 年下半年之后，没有手机注册的基本都跳手机验证了，有的手机号，过几个月又可以注册了，然后用了家人的手机

- 直接去 safari 设置里清除历史记录与网站数据也行，比较快

- Google 本来就没禁止多账号啊，只是不让批量注册而已，正常环境登录上百个没事

- ## [多个google账号怎么管理比较好？ _202605](https://www.nodeseek.com/post-750862-1)
  - 陆续注册了10多个google账号，但是IOS的gmail App不让继续登录新账号了。大家都是怎么管理多账号的？
  - 另外，google的风控真严格。弄了pixel自助认证，Google发现异地登录，立马退出了账号，再登录就显示被风控了。坑爹的是，解除风控的手机号不记得了，辅助邮箱也没设置
  - 干净的 ip➕ iOS gmail 客户端，分分钟出来，但不能连着注册

- 有没有安卓备用机 安卓gmail我登录了15个了 还没有提示上限
  - 有的。看来安卓对数量限制没那么严格，回头试试看

- 我安卓登录30多个没啥事。就是老手机有点卡

- ## [时隔两年，旧事重提下：一部手机最多能登录几个google账号 - LINUX DO _202610](https://linux.do/t/topic/3061131)
- iPhone 上的 gmail 最多是 8 个号

- 目前登录了 6 个，有个奇葩问题，手机验证用别的号验证，重新登录，手机号还是旧的（大号的）
- 非常多 我目前登了 13 个号 没事的
- 22个目前还没出问题，有被封禁的但都是别的原因

- 不知道现在能不能像两年前 EIF 佬的壮举，chrome 多开，一开 10 个号，再加上 edge 浏览器 10 个号，实现一部手机 60 个号

- 每个窗口 4 个号，差不多 200 个号

- 换了设备之后就很容易风控，我之前的好多号都丢了

- 和账号注册有关系的，和登录没关系，手机电脑同时登录 20 多个很久了，一直没事。

- ## [谷歌提示设备验证次数过多怎么解 - LINUX DO _202611](https://linux.do/t/topic/3119610)
  - 在网上看到其他解决方案，已经用上了：ios 登录 google one 和 YouTube，使用同一个谷歌账号，然后反重力提示扫码用 Google one 扫码，跳转 YouTube 直接认证登录！

- 换设备扫码验证就行，不用发短信，他这个会验证扫码手机的 sim 卡，或者你可以把卡先换一下再扫

- ## [Stuck in Google Anti-Bot QR / MO-SMS Verification Loop on PC ("Device used too many times") when authenticating Google Antigravity / Gemini Code Assist : r/googlecloud _202609](https://www.reddit.com/r/googlecloud/comments/1wr91td/stuck_in_google_antibot_qr_mosms_verification/)
  - sceenshot the qr code and send the photo to family to scan it .. that worked for me
- Worked for me too! Thanks 

- ## [Goole 验证二维码【放弃】 _202610](https://www.nodeseek.com/post-985556-1)
  - The device you used to scan the QR code was used too many times for verification
  - 设备：苹果 小米
  - 网络：家宽 搬瓦工
  - 我tello 成功过一次 后面在验证就不行了 操蛋

- 让你换设备就是IP脏了，换一个节点吧！
  - 一个sixtynet家宽 一个搬瓦工 
- 我这里瓦工的IP，一直就是设备不支持提示，连找回密码操作都不可以做。换了个莫名其妙的节点，就好了。

- ## [谷歌账号弹扫码 _202611](https://www.nodeseek.com/post-1023541-1)
  - 对方号码是 244444， 96831 这些，发不出去

- 用 hk 节点登录，手机扫码的也是同 ip，就会发短信到+852， 国内或者香港手机号都可以发

- ## [现在在国内还有办法注册 Google 账号吗？ - V2EX _202606](https://www.v2ex.com/t/1218362?p=2)
- 美国节点扫码会让发短信到 96831 ，这时用 giffgaff 发不出去。节点切换到香港节点，会让发短信到 85264522353 ，这时候在号码前面加 00 ，即：0085264522353 ，就可以发出短信了。
  - 感谢。我这边中国的+86 ，切香港节点后成功了

- 之前用美国节点短信接收方是000590104，96831，244444，这种发送不了

- ## [谷歌账户要验证手机，这步怎么过跟各位求教 - LINUX DO _202610](https://linux.do/t/topic/3026673)
  - 绑了 2FA，也能输密码过验证，但就是最后登陆之前，它要我做验证。
  - 国内手机我用了，发短信到 //96831？是什么鬼，我发了，但没效果。求佬友支招  
  - 点了试试其他方式，仅此一种方式，点了还是这个页面，还是手机扫码。

- 用手机 /ipad 下载 Google app，打开手机设置里的谷歌服务选项，在 Google app 里登录一个
正常的谷歌账号，用 google app 内部的扫码功能扫码即可

- 这个我前些天刚过了。我的操作是：
手机开全局的美国加宽梯子；
下载谷歌（注意，这是谷歌，不是 Chrome）；
用谷歌这个软件扫就行了，就不会让你发验证码了。

- mobile 端下载 google app (非 chrome) 以及 youtube
用 google app 扫码
跳转后然后点击确认登录地址即可

- ## [关于gmail防封以及被封后申诉问题（分享） _202404](https://www.nodeseek.com/post-88578-1)
近期看到很多mjj因为gmail的封停烦恼，作为一个号商来说，简单分享一点防封技巧和被封后申诉技巧

首先，谷歌近期对于不活跃账号和批量注册打击很频繁，封号逻辑大致就下面几个
新号不活跃，或者IP不干净（机场为例），一个IP注册多号被关联，频繁切换设备
防封技巧，多号话，PC端用指纹浏览器，比特或者HUB等等免费的就可以，批量新建环境，可以一个静态IP配置3-5个账号使用
或者使用那些动态住宅IP。（核心技巧，动态住宅IP范围一定要圈定在某一个国家的某个城市，养号期间，每次登录可以变换IP但是范围不要改变太大）
操作上，定期登录gmail邮箱，固定养号一段时间就可以活下来。

移动端：如果有安卓设备最好，没有的话，用模拟器，批量新建环境，IP同上，模拟器手机型号可以随便改。养设备
模拟器里安装上谷歌PLAY，把号都登录上去，可以批量操作随机下一点app，新号初注册，每两三天登陆一次谷歌PLAY

防封主要就是一个IP和活跃度问题，下面说说申诉技巧。

一般批量关联的号都是IP导致，用统一话术申诉就行。（自行翻译成英文）
你好，我的帐户是xxxxx@gmail.com .
我位于china，我必须使用VPN代理才能访问谷歌产品。由于VPN的不稳定和频繁切换，我的帐户可能已被暂停。这个账户对我来说非常重要，我使用它来进行工作和生活，我希望你能帮助我解决这个问题。非常感谢。
话术很老套，但是很管用。
申诉一般24-48小时内就回收到回复。如果没有，间隔几天继续申诉，话术不变，换一种文本翻译就行。不要用简中。

- 应该是人机，谷歌这么大体量，人工搞不过来。
不过我测试过用脚本批量申诉，用这个文案成功率高点。
人机审核的应该，我用批量申诉脚本测试过，欧美这些地区语言成功率相对高的多。

- 简体中文申诉也可以通过的

- ## [谷歌账号被停用，该怎么申诉？附申诉小作文 _202409](https://www.nodeseek.com/post-156129-1)
  - ~~谷歌账号被停用，只有两次申诉机会。~~ 

- I must use a vpn proxy to use Google products. The account may be abnormally disabled due to vpn instability and frequent switching. This account is very important to me. I hope you can help me solve it. Thank you very much.

- I reside in an area with restricted internet access, and due to unstable VPN connections and the need to switch frequently, I’m confident that I haven’t violated any Google policies. Could you assist me in restoring my account? Thank you very much!

- I live in a region where internet access is limited, and I often have to switch servers due to VPN connectivity issues. I am certain that I have not breached any of Google’s rules. Could you please help me reinstate my account? Thank you!

- 

- ## [反重力登录 CPA 问题 - LINUX DO _202610](https://linux.do/t/topic/2969943)
  - 提示这个是什么问题啊，目前只能卖家给的 RT 在反重力能用。

- 我当时也这样，rt 登录过几天就不会这样了

- ## [多个谷歌账号怎么管理养号 - LINUX DO _202609](https://linux.do/t/topic/2923259)
- 也不算多吧，我电脑主浏览器登了 7 个号，指纹浏览器有二十来个号分散在四个窗口中，感觉没这么容易风控，有的一个浏览器挂三十多个号都没啥问题，我的是没被封控过，后续准备把一些号往主浏览器切换
  - 没问题的，官方支持 profile 自然有他的道理，不放心就放指纹浏览器，放心就一个号建立一个 profile，我看站内有的人一个浏览器挂三十多个 profile 没出问题，别一个 profile 登一堆号就行

- 普通 chrome
我挂 30 多个没事
ip 随便飘。
尽量不要登录手机
就在电脑上用。
- 浏览器不是只能挂 10 个吗，怎么挂三十的。
  - 添加 chrome 个人资料, 具体能加多少个不知道, 最多见过挂 50 多个的
- 小了，我直接 100 多个挂在一个上面

- 我手机 gmail 登录了 40 个号，一直就这么用着，没啥问题

- ## [google账号注册邪修 - LINUX DO _202608](https://linux.do/t/topic/2769212)
  - 网页注册 google 账号，会弹出扫码验证，不好操作～
  - 邪修：手机下载 youtube 可以直接跳过，后续操作国内手机正常接收验证码就行～

- google play 也可以，在里面注册不弹手机验证什么的

- 我是在 Google 邮箱 app 中注册的，第二天封了，然后我申诉之后又解封了。

- [现在还有没有什么方法好注册美区的google邮箱呀？ - LINUX DO _202608](https://linux.do/t/topic/2694067/5)
- 手机上 gmail 客户端注册账号，干净节点就不会要求
- 在 iPad 上用 gmail 客户端注册没要手机验证，但是不要短时间内连续注册多个会被封号，我当时是注册了三个，虽然后面申诉回来了

- 安卓手机上用 Google Play 注册，节点用干净点的，也不用特别干净，基本不会遇到验证手机号，不要注册太多，一周最多 1-2 个。然后过 2 天就会告诉你要你验证手机号，可以用国内的号，但不论用哪里的号，都会先封号；然后写小作文申诉，可以让 AI 写，用英文写满，大意就是因为网络问题不稳定，需要切换节点啥的，后续保证会正常使用账号。基本都能解封，解封后就正常了，可以正常绑国内的手机号，不会再封了。其实也不用特别追求非要美区的，功能上都一样的。

- ## [【折腾心得】手持30多个Google AI Pro，在反重力IDE里无痛轮换长任务 _202609](https://www.nodeseek.com/post-926622-1)
GPT 不如直接撸了在论坛里卖，Claude 退款退多了银行关户杀全家，两家对破限越来越严，能爽用的只有 Google AI Pro。现在 5 小时额度越来越少了，丢个大项目或者跑个搜索，一两次额度就见底强制结束任务，单个号长任务根本不够用。

我白嫖了 30 多个 Google AI Pro 号（主要靠美国社区大学学生送 12 个月、印度 Jio 送 18 个月，以前 Pixel 送 12 个月现在好像不能搞了），通过 Chrome 在反重力 IDE 中轮换。

尝试过CPA搞反代会 48 小时内封反重力登录。

Chrome 单个 Profile 最多能同时登 10 个 Google 账号。建 3~4 个独立 Profile，把号全塞进去。在反重力里要用的时候，直接点它弹出的 Chrome 原生账号列表，哪个有额度点哪个，秒切不用输密码。一个 Profile 的额度榨干了，反重力里换下一个 Profile 目录继续点。

全程都是本地真实 Chromium 环境，不触发风控，稳用半年没掉过号。记得偶尔发一些邮件保号，Google 会冻结不活跃账户。

我用的带Google全家桶的机子，没有发验证码这一步

IP不送中，不是被制裁国家就行，用不了大概率需要账号改地区

- ## 💡 [松了口气，100多个谷歌号全部存活，逃过昨晚的大面积追杀 - LINUX DO _202609](https://linux.do/t/topic/2882364)
  - 昨晚至今没收到封号邮件，一大早先挨个检查号池，居然都活着，一个也没死。 100 多个号有买的，有自己注册的。有 free 号，有 pixel 号，有学生认证号，昨天又新开了几个 jio 号。 全部都在反重力反代，一部分在 aistudio 反代。
  - 因为我用反重力的 Claude，那个额度太太太少了
  - 反重力反代本来就不封号呢，只会封使用 code assist 的权限
  - 我这些是从去年到今年慢慢攒的，如果想批量注册，被封号的可能性就很大
  - 其实前阵子买的号也被封了很多了，剩下的可能都是耐活王吧
  - 趁没人看偷偷小小炫耀一下 (不敢发主楼怕立 flag)，这批号里有一部分号，甚至神奇地养出了高权重账号，高权重账号的表现就是有前两个月免费的 YouTube，Google pro1.9 美元折扣价，使用反重力的 Claude 从不 429/503，还有就是白嫖 gcp 的 300 不需要交押金。
- 建议有条件还是自己注册吧，尽量用苹果设备，干净家宽 ip，刚注册的那几天老实一点，过上几个月就能养出我上面说的高权重号。
- 我以前特别喜欢买号，买过很多。以我从去年到今年买号的经验来看，我感觉号贩子手里的优质账号越来越少了，我去年买的号，现在还活着，至今不需要绑定手机号。以前买号默认是没有绑定过手机号的白号的。
今年买的号质量越来越差了，上去不是 gcp 被封，就是 YouTube 频道被封，连邮箱被封的都有。然后慢慢发展到了买的号都绑定过手机号了 (大概率就是已经被封过一次的号了)。
只能说买号越来越不划算了。
- 我没批量注册啊，从去年开始隔三差五注册攒到今年的。目前除了贩子还没听说有人能批量注册谷歌，手工注册都要大概率被封，别说批量了。贩子批量注册的号，最近也被谷歌追着杀，杀到了 2020 年了都
- 如果要你发短信，那肯定是环境有问题啊，要不就是你这个设备注册失败次数过多，要不就是 ip 不干净
- 我感觉也没有很大的花销，ip，指纹浏览器这些都是可以白嫖的，家宽的话，搞点伪的就行，好像谷歌识别不太出来真伪。
- 我是多个设备注册的，家里刚好设备多，旧手机旧 ipad 啥的，还有家人的 iPhone。注册完不是用手机养，而是在指纹浏览器养号。
一个指纹浏览器窗口可以挂多个账号，五六个没问题，不过只要窗口能白嫖，多挂几个总是更好的。
你要把手机的换到电脑上没啥问题，掉登录就再登就是了。总之就是一个原则，尽量不跳设备和 ip，如果要跳，一次只跳一个。跳设备不跳 ip，跳 ip 不跳设备。如果非要同时跳，就尽量跳同城 ip。说白了就是模拟正常用户的使用轨迹。
- 我不是写代码的，主要 gemini 用在养 Hermes 打理多台服务器 (维系号池)，还有就是 Claude 用来玩酒馆 rp 的。
反代不会直接导致封号，会导致封你的 code assist 权限 (cli+antigravity)，如果被封号了，大概率还是有其他原因触发了风控的。

- agy 第一次使用都需要验证的，无论是 jio 还是 pixel 还是 free 号
  - 最简单的办法就是手机上要有 Google app 和 YouTube，用 Google app 扫码，它会自动跳转 YouTube，点确认就可以了，不需要绑定手机号。
  - 如果这个办法行不通，你就去 Google cloud 的 console，右上角有个 shell，点了以后它会让你验证，选接码验证，用任意 + 86 手机号即可接码。接码后反重力就不用验证了。
- 我是指反重力验证的时候的接码，那个之前是不会绑定到账号的，只用作验证反重力。现在不确定有没有改这个政策。 
如果是指注册时的接码，我都是尽量不接码，环境好可以跳过接码。
- 佬，上面那个焚决是针对反重力第一次验证的，不是针对注册的，注册的话没有焚决，就是看环境，环境干净了就能跳过接码。

- 佬接码用的都是自己的手机吗？
  - 当然是用接码平台啦，我没有那么多手机号
  - 大部分都没接过码的

- 我一直重试都不行，佬有试过账号权重后续能提升吗？我这个号用指纹浏览器其实养了挺久的
  - 可以给你提供大致思路：1. 在有谷歌体系的手机上养，关定位，ip 固定。2. 经常刷 YouTube，尤其是要刷 shorts，像正常人那样刷。3. 经常使用 Gemini app。
  - 但是很难，我这个帖子前面探讨的养号都是指让号活着不被封，基本上这个我已经做到了。但是怎么把低权重号养到高级权重我至今成功率不太高。我确实养出了一批高权重号，但基本都是号的体质问题，从注册时就天生的，如果是贩子那里买的低权重号，我想刻意养，成功率挺低的。
- 我在贩子那里买的号，只有挂在我安卓手机上的六个号全部都被养成高权重了。你换手机养试试看吧。
顺便提供鉴定谷歌号是否高权重的方式 / 福利：1. 打开 Google one，plus 和 pro 都有优惠价格，价格越便宜说明权重越高。我目前看到最便宜的是 pro1.99 美元一个月。2.youtube 有 1-2 个月的免费 premium。3. 反重力用 Claude 从来都不 503。4.gcp 白嫖 300 赠金不需要付押金，可直开。

- 想请教下管理这么多号的经验，一个浏览器里登录多少个号？
  - 那必须得指纹浏览器啊，一个浏览器的话，我最高记录是五个还是六个吧，然后由于这五六个是我的常用账号，我经常活跃使用，反而这五六个都活的好好的，权重也不低。
  - 所有指纹浏览器都支持多个谷歌账号登录，包括 roxy
- 不需要管理工具啊，就放指纹浏览器里挂着
- 指纹浏览器我是把我能下的全下了，到处白嫖窗口，随便哪个都可以用，我觉得没有区别。ip / 代理这个我不太方便推荐哈，肉身墙内比较谨慎，不敢乱推这个。但是可以告诉你，伪家宽就可以，不需要多么纯净的，然后稳定以后，人少的机房 ip 养号也没问题。

- 你手机注册再放到电脑的指纹浏览器吗？那手机上号留着一百多个谷歌号登录吗？
  - 怎么可能， 分散再不同设备上，模拟器也有的。

- 收邮件的话可以设置邮箱转发，都转到自己常用的邮箱就可以了。

- 佬一般一个手机放多少个谷歌号比较安全？话说安卓模拟器能养号吗？之前试过好像环境不太行，佬用的是哪款模拟器？
  - 我最多放过六七个吧，但是六七个不是上限，下面佬说放几十个的也有。模拟器不能养号只能注册，注册好了要么就直接上指纹浏览器，要么就直接上凭证。

- 你们都用的这么小心吗？
我就是一个电脑上 chrome 登录几十个
随便用啊
ip 就是蹭免费的机场，到处飞
账号有显示中国，有显示日本，美国都有
账号没一个封的
但 google cloud 有封的，以前同时开太多项目拿 gemini 免费 key

- 请教一下每个账号接码注册好之后都设置了哪些 2FA，身份验证器，辅助邮箱，辅助手机号这些
  - 我是 2fa 和辅助邮箱，辅助电话不需要。

- 这么多号怎么看有没有被封的？一个个登录看吗？然后建议登多少号换一个 IP 好呢？
  - 打开指纹浏览器看就好了，都是保持登录的。或者直接看 cpa 号池，刷新一下一目了然。ip 的话只要干净的 ip，登录十几个没问题，不过最好别再同一个浏览器，也别同一个时间一起登录。

- 用 + 86 接码总是被提示用过太多无法再用了。
  - 这个一般是环境不够干净，比如 ip 风险值较高，同一个 ip 和浏览器登录了多个账号等等，一般一个手机号可以绑定 3-5 个 google 号（不能连续绑，一般隔一个月以上绑一次）

- 100 个号，每个指纹浏览器窗口登 5 个，那不得 20 个 ip，还是 20 个静态且能够长期持有的 ip，“没有很大花销” 是如何做到的？指纹浏览器免费的很多，20 个静态 ip 是怎么做到低成本长期持有的
  - 首先我不是 100 个号全部养着的，很多号我注册出来直接上反代，拿到凭证就不登了。其次并不是一个 ip 只能养一个窗口，我自己的 vps 的机房 ip 就养了七八个窗口 (但不是每个窗口都五六个号)。最后静态 ip 肯定是要花钱的，但是我觉得不能全算在谷歌账上，其他地方也都要用，我还有好几个 codex 号池，grok 号池也要用，Claude 也用但是已经被封了
- 固定代理一般也没事，就怕老跳 ip

- 请问下出现这个手机验证的话账号还会要二验吗
  - 纯看环境的，我之前有阵子喜欢用模拟器注册，注册的时候就得验证手机号，注册完了秒封，我解封后一直用到现在有小半年了，基本上跳 ip 也没风控过。但是环境不好的话有人刚绑了手机号，第二天就出二验或者再次封号，封号也需要验证手机号才能申诉的。你最好先解决环境问题再绑手机吧。

- 佬，你的学生 pro 反重力用 claude 模型会提示 Our servers are experiencing high traffic right now, please try again in a minute 吗？我昨天加了两个账号全都给我显示这个软封禁，都是接过码的
  - 这个是号的权重低就会一直 503，大约半个月前，低权重号一直 503，但是反复重试，还能出字，最近谷歌明显是又严格了，重试也很难很难出字了。

- 
- 

- ## [谷歌账号要求指定手机接码的解决方案 - LINUX DO _202507](https://linux.do/t/topic/794812)
  - 等半个月就好了
半个月里不要尝试登录（这点很重要！）
之后再去登录就可以使用任意号码接码（这是第一次验证）
但是接码后可能会提示账号被停用，需要申诉
申诉通过后，需要再次接码（这是第二次验证）
第二次验证强制要求第一次验证时的手机号
所以，在第一次验证时，要用能重复接码的手机号，比如 + 86

- ip 经常换，尤其不同国家之间反复横跳，容易触发验证

- 实测有效，1 个月不行就 3 个月，中间可以隔一个月登录看看，但是不要频繁登录

补充一点，新登录，用新的浏览器，和好一点的 ip

我现在卡在申诉了，一直过不了，哭

- 实测半个月后，沐浴焚香，iphone 重置，安装 t-mobile esim 美国原生 ip, 安装 gmail, 里面登录
依旧要发验证码到原号码
结论：洗洗睡吧，谷歌无情，

- ## [谷歌账号登录提示 谷歌账号手机号验证次数过多 还有救吗 - LINUX DO _202608](https://linux.do/t/topic/2819955)
  - 登录就会让验证手机号，然后用自己的手机号就会提示 手机号验证次数过多，点试试其他方式也没有用。之前大概半年多没登录过，结果最近登录，接了一次验证码，然后就又提示这个了。
  - 当时是隔了大概半年多没用过，然后登录。第一次成功接码，然后让我再输了一次手机号，这个时候又被提示风控了。

- 登录要手机号，是人机验证的手机号，一个手机号大概会被系统记录 3-6 个月
接太多就会，提示使用次数过多，只能等

一般第一次接码之后，第二次还是会要你这个手机号接码。不应该再让你输入手机号的

这个只是登录验证，没啥问题，能过就行

实在不行，改个密码吧，或许异地登录，或者 ip 不好，被风控了

你现在是登录不进去，还是登录还需要输入手机号？

- 有救 过七天再试 我就救过两个
这期间不要再试了
试一次再延长
可以下个月再试 大概率就不提示了

- 我之前问过客服
你等 7 天 + 以上 现在不要登录了 你越登录 越麻烦

- 巧了，我最近也在折腾这个问题，有一个买的账号掉登录了，然后我登录输入手机号前几次还能等，但是那时候可能我携号转网问题收不到，最近看激活了重新登录输入验证码就一直显示次数过多，我隔了，3, 4 天去还不行，我今天早上又试了一下重新登录居然直接让我输入新的手机号，我换了个手机号收到验证码登录之后告诉我被封号了，然后我现在在申诉

- 我的号也是提示短信验证次数多，隔了一个多星期，今天用家宽的 IP 发验证码成功了，但提示号被封了，看看能不能申请回来 

- ## [关于google登录的时候，提示当前号码次数过多的解决方法 _202609](https://www.nodeseek.com/post-925119-1)
  - 很多人看到这个就换手机号，换完发现还是不行。可能就会考虑，接码，家宽，换852之类的
  - 其实这个就是ip问题，换个ip即可，也没有限定一定要家宽，随便一个机房也可以过。

- 刚试了试 换了仨ip也不得行，要是行的话我估计早建烂了。一个设备差不多注册6-7个谷歌账号就会被风控

- 提示此号码无法用于验证才是ip环境问题，次数过多换手机号就可以解决
  - 👷 刚才试了换ip还是不行

- 风控换ip也没用 一定要静止 和换设备

- ## [gemini和Antigravity有什么区别 - LINUX DO _202609](https://linux.do/t/topic/2870744)
- Antigravity 是开发工具，有 agent、cli、ide
Gemini 是 AI 模型
理论上买的就是 Google One Pro 会员，但是你要反代当心谷歌封号

- 应该买带 antigravity 权限的 pro 订阅账号，如果给自己的号开 pro 会员，先检查一下自己的账号的归属地区，是不是谷歌提供服务的地区（最好是美国）。如果不是，就先把号养好后，再开会员（一般 aws 节点就行了），否则你开了 pro 订阅，账号也不会有 antigravity 权限的。
谷歌杀 cpa 反代根据自己模型能力和算力来的，之前 2.5pro 3.0pro 时期，你反代露头就秒，现在路边一条水平，只反代 gemini 系列模型被杀的几率不大。但反代 antigravity 里的 opus4.6 你被杀号风险还是很大。
反正你这操作我建议买个号或者新建养个号，别用自己主号去开福利 pro 订阅了

- 不买包 antigravity 权限的 google 账号，那可能你就用不了 antigravity
只能在网页端 app 端用 gemini
号商都是挑出去然后涨价卖

- ## [google账号被封后，申请解封了，需要原手机号验证 - LINUX DO _202508](https://linux.do/t/topic/836576)
- 意思就是等着，多试几次之后就不用原手机号了

- 等半个月，期间不要登录这个号

- [google账号风控，要求用之前接过码的手机接码验证，没有这个手机号怎么办 - LINUX DO _202607](https://linux.do/t/topic/2644627/4)
- 先放着不管，一个月后再尝试登录，或许就能换手机号接码

- 等半个月就好了 半个月里不要尝试登录（这点很重要！） 之后再去登录就可以使用任意号码接码（这是第一次验证） 但是接码后可能会提示账号被停用，需要申诉 申诉通过后，需要再次接码（这是第二次验证） 第二次验证强制要求第一次验证时的手机号 所以，在第一次验证时，要用能重复接码的手机号

- ## [公司有一批非常重要的Gmail帐号，如何低成本养号呢 _202503](https://www.nodeseek.com/post-294121-1)
- 因某个业务只能使用Gmail所以没办法更换域名邮箱
目前方案是指纹浏览器+独立IP，但是每个月IP成本太高了，又经常使用这批帐号进行授权登录
还经常蹦出来二次手机号验证，目前也没找到好办法
有没有什么办法能低成本的养住这Gmail，尽量少挂掉

评论里几乎没有一个说到点上，大多都是3，5个帐号的，50个以下帐号的不要回复了，当然不用考虑养号的问题

我们的场景是给学员注册某个平台，但是我们要有邮箱帐号管理权限，平均一个学员5个帐号，对于不严格的平台，我们直接用outlook或者Getmx域名邮箱了，但是有些平台比较严格只能Gmail，连outlook都不可以

只用来收验证码，不发件，但是偶尔可能要操作授权，所以目前转发也无法满足我们的需求
偶尔需要授权登录

成本主要是IP，目前一个固定IP一个月也最少10块钱, 还不是家庭的

『gmail又不管你一个ip登录几个号』这个是不正确的
养的是Gmail，业务有独立的方案，业务会依赖Gmail收验证码
『建议多花钱，都管学生了，又不是没钱』我问得是如何能省钱，不谈成本得到利润都是耍流氓

- 指纹浏览器+假家宽都嫌贵，那说明还没有那么重要。。随便弄弄吧

- 既然 非常重要, 就没必要 低成本 吧
  - 每个号一台pixel3、4、5，三百块一台，绝对安全
- 买谷歌pixel 手机。正常可以一机搞十来个号

- 我一个chrome浏览器就登了5个账号，啥事没有啊，要哪个账号点哪个
- 我gmail的app登着十多个账号呢，用了快十年了还没碰到被封。
- 这个不用养吧？我10几个号，都是直接在同一个浏览器里一键切换

- IP可以买CC或者RN之类的年付十刀左右，自己搭建用机场统一管理，然后试试多少号一个IP能稳定一些，这样就只有指纹浏览器的成本了。

- 养的应该是业务不是gmail吧，gmail又不管你一个ip登录几个号，所以楼主需要的是指纹浏览器开N个实例+N个住宅IP，其中N>=你的业务账号数量。

成本就是指纹数量和ip数量，这些量大的还得能自动托管指纹和ip对应关系，防止串号或串指纹，指纹浏览器一般都支持这些功能的。你就是整个学校一万学生它也能管下来。

自己实现也行，开N个浏览器沙盒，配置N組Agent和硬件指纹，会把你累坏的。就这些。要么花钱省事儿，要么省钱花功夫。建议多花钱，都管学生了，又不是没钱

- 有款软件叫AYCD可以帮你养号, 也会帮你模拟一些操作. 如果你aws有高cpu的话, 这款软件也能一键帮你生成代理
  - [Automation Done Right | AYCD ](https://aycd.io/)

- 一台香港4H4G的优化线路30多块一个月，带宽不需要多高，然后使用docker部署jlesage/firefox浏览器，既简单又方便，然后通过vnc连接浏览器可视化使用，一台机挂5个账号，这样算下来，50个账号300多块，500个账号3000多块，需要接码就打开对应机器的vnc连接查看网页就行了，关闭vnc的话浏览器也会一直后台运行，相当于你的账号一直是登录状态，网页也一直是打开状态，然后可以搞个小本本记录下来哪个IP地址登录了哪5个账号

- ## 💡 [反重力教程登陆教程 此教程只针对个人使用定制 _202608](https://flowus.cn/share/edefab75-e89b-4c48-85df-343715d71664)
  - 关于不能跳转和反重力没资格的问题的问题 用tools管理工具登陆
- 谷歌号停用被封申诉模板: 
  - 要围绕自己用，不得不用网络代理，账号里面有重要数据 展开
- 申诉原因
  1. 中国人或者美国人居住在中国**
  2. 特殊原因必须要网络代理才能使用到谷歌服务**
  3. 自己只有这一个号**
  4. 凸显出账号的重要性，例如要与国外的朋友联系、账号内有很重要的东西、公司重要账号等**）
- 申诉后一般 24–48 小时会有回复
  - 如果没回，可以隔几天再发一次，内容主旨不变，换一种英文说法即可

- [Gemini 成品号使用教程 - Feishu Docs ](https://my.feishu.cn/wiki/N43PwSarpi5XGGkhwe0cmOOanve)
- 登录上去正常使用，养了6-10天之后，可以逐步修改账户信息（建议不要一次完成，分几次）：
  - 添加辅助手机号、邮箱号
  - 添加两步验证
  - 修改密码

- ## [关于谷歌AntiGravity反重力扫码二维码验证手机号风控 - LINUX DO _202608](https://linux.do/t/topic/2772871)
- 扫码好解决
搞一台能登 Google play 的 包括谷歌套件都全的
把号登上
然后扫码的时候用 Firefox 扫
国产手机不要用自带浏览器扫 大概率扫不出来
Firefox 会提示打开谷歌的应用
能打开 + play 号登着的（多号的情况要把号切过来）
就能过

基本上现在 cpa 是能拿到 JSON 的
但是调用得
在 agy 里面登一下看看是不是真的能进去
或者这个过程中会告诉你有哪些问题要解决

- 一个手机可以重复扫不同的账号吗，手机电脑要一样才可以吗
  - 其实可以的 只要 play 登的不同的号就行
- 可以的，我扫了五六个都没事，只要手机上面登录了就行，会自动跳转

- ## [反重力需要扫描验证怎么解决 - LINUX DO _202609](https://linux.do/t/topic/2855971)
- 找个装谷歌框架的安卓手机，有 play，登录一个老账号，然后用相机直接扫就行

- YouTube 扫个码就过了，我有两个号也报二验，扫完就 OK 了

- 直接扫就行啊，扫完跳转谷歌系任意一个登录过的 app 确认一下就行了

- ## [antigravity反重力绕过二次验证 - LINUX DO _202609](https://linux.do/t/topic/2855717)
对于新账号和刚订阅 Pro 的用户来说 登录 antigravity 可能会触发风控 导致无法反代到 Codex 里 以下是解决方案：

用新的谷歌账号登录一下以下网址

https://shell.cloud.google.com

会弹出 扫码界面 然后用常用手机扫码即可（不需要登录新谷歌账户）

原理：Antigravity 登录用的是它自己的 OAuth 客户端，风控更容易升到 设备二维码验证。

Cloud Console / Cloud Shell 是 Google 自己的网页产品，挑战经常还是老一套：密码 + 手机短信 / 提示。
两条路的风控档位不一样
我这个闲鱼上买的方法，没注意看论坛有没有

- 奇怪，我用同个账号，手机也登录了这个账号，扫码依然要手机号和发短信

- ## [Google验证让发送短信验证码 - LINUX DO _202609](https://linux.do/t/topic/2935692)
- 下载 google app 和 youtube app
然后在 youtube app 登录这个账号
再用谷歌 app 扫码

- 我今天也遇到了 antigravity 需要二次验证（白嫖的学生账号之前用了几个月都没事），然后一上午就在不停的折腾：
1、用 iPhone 相机扫码，跳转发短信，虽然我 google 账号本来就绑的 86 的号码，但要发的那个 244444 显然是个美国的号码，所以无法发送成功，失败！
2、用没装卡登陆 google 账号的 google pixel4 原生安卓手机相机扫码，提示需要 sim 卡，失败！
3、用大家都说好用的 google shell，我进去直接登陆成功，就没触发验证，但切回 antigravity 还是提示要验证，失败！
4、在 iPhone 上下载 google app 和 YouTube app，并都登陆账号，然后用 google app 扫码，自动跳转 YouTube 验证后，成功！！！

- ## [antigravity的账号验证要怎么过啊，要我扫码发短信 - LINUX DO _202605](https://linux.do/t/topic/2215836)
- 我也是好多个号卡在这扫码了，自己设备已经扫的超限了，最后花钱解决的，几分钟就搞定，要不是还想用 gemini 模型，真想扔了它

- 最简单直接的办法就是闲鱼找人代扫，20 以内一般

- 我遇到过同样的问题，让发送短信，结果短信根本无法送达，后来用谷歌 app 还是谷歌浏览器扫码，会跳出来打开方式，打开方式有【google play、以及其他几个软件】，选择 google play 打开就好了（谷歌这神人交互真是绝了）

- 我前几天也遇到了这个问题，刚充套餐的时候风控了，用 + 86 和租的 + 1 号发都没反应，搞了两天都没搞好。期间我是直接用的 agy cli，这个虽然会显示检测失败但是依然能直接用套餐里的模型。结果有一天发现 cli 没有显示检测失败，然后再登 antigravity 就发现已经不用验证了。

- ## [近期反重力antigravity无法登录等问题可能的解决方案 - LINUX DO _202608](https://linux.do/t/topic/2804240)
  - 闲鱼入手 jio 渠道的邀请的 pro, 说是 18 个月，但是这玩意不要抱有任何希望，几块钱能用一天都是赚. 
  - 然后故事就来了，因为是一个注册了半年的 google 账号，通过链接开通了之后。登录 antigravity, 提示 verify . 点击之后需要手机扫码发送短信，而且没有其他的验证方式.
  - 核心问题，google 账号可以 oauth 跳转到 antigravity, 但是显示 verify 点击会显示 需要扫码发短信
  - 通过 https://console.cloud.google.com/ 开启 console 的时候的 verify 他是在 web 端进行验证的，会给出第二个选项，就是通过手机号码接收验证码。而不是必须要手机扫码二维码。这时候就通过一个手机号码接收验证码就行了
- [【安卓 反重力登录验证码问题】+【Google AI Plus+400G存储免费白嫖12个月】+【Antigravity 反代api】 - LINUX DO _202608](https://linux.do/t/topic/2746638)
  - 激活终端：在控制台页面右上角的顶部导航栏，找到并点击 “激活 Cloud Shell” 图标（图标形状类似 >_）

- 方法可行，+86 的也可以验证成功

- ## [antigravity反重力过二次验证 _202609](https://www.nodeseek.com/post-911507-1)
  - 对于新账号和刚订阅Pro的用户来说 登录antigravity可能会触发风控 导致无法反代到Codex里 
  - 用新的谷歌账号登录一下以下网址 https://shell.cloud.google.com
  - 会弹出 扫码界面 然后用常用手机扫码即可（不需要登录新谷歌账户）
- 原理：Antigravity 登录用的是它自己的 OAuth 客户端，风控更容易升到 设备二维码验证。
  - Cloud Console / Cloud Shell 是 Google 自己的网页产品，挑战经常还是老一套：密码 + 手机短信/提示。
  - 两条路的风控档位不一样
  - 亲测有效

- ## [Google One AI Gemini Pro $99 家庭5人拼车 _202601](https://www.nodeseek.com/post-566540-1)
  - 在 Google One AI 高级版（家庭方案）中，虽然空间（如 2TB 存储空间）是共享的，但 AI 功能的使用权是按人头独立计算的。
  - 独立计算： 您的家庭成员（最多 5 人）中，凡是年满 18 岁且符合条件的成员，每个人都拥有自己独立的 Gemini Pro 使用权限。
  - 不共用额度： 假设您今天用完了 3 个视频生成的额度，这并不会消耗您家人的额度。他们依然可以生成自己那部分的视频。
  - 隐私保护： 您的生成历史、提示词（Prompt）以及积分消耗情况，其他家庭成员是看不见的。

- ## [【网页版操作】解决谷歌家庭组地区不同 - LINUX DO _202602](https://linux.do/t/topic/1611408)
  - 支付方式改成美国了，为什么 play 里面显示法国呢

- 有个【+ 添加支付方式】选项，试试这里添加个 fake CC，billing address 改 US

我之前的小号没有添加支付方式。

- 加了，之前有个法国的支付方式，我删除了，然后加个一个假的就过了

- [Google One家庭组地区不匹配解决方案（Gemini pro优惠共享） - LINUX DO _202511](https://linux.do/t/topic/1206323/2)
- 其实，关闭付款资料，用美国 IP 就 OK 了

- 大部分只需要发起邀请时的 ip 一致就可以啦

- ## [Google 家庭组切换后 12 个月内可以自己再创建吗 - V2EX _202604](https://fast.v2ex.com/t/1203654)
  - 我之前作为家庭成员加入了别人的谷歌家庭组，上的 YouTube 会员车，结果车主跑路了。 谷歌官方说的是 12 个月内只能切换一次家庭组，现在还没到 12 个月，我想自己开车创建家庭组再去邀请别人，这种操作会受 12 个月的限制吗？
- 自问自答：试过了，不行，更换和创建统一受 12 个月的限制。

- 我亲身试过，之前上别人车，翻了下车上车又翻，车主说还有办法拉我，我怕有问题，就自己开了个车，正常拉人用到现在
  - 为啥谷歌提示我 12 个月内只能变更一次，服了

- 找客服说你的室友搬家了之类的, 第一次非常容易过

- ## [无法加入 Google One 家庭组？全因这 3 个“地区”搞乌龙！ _202602](https://www.nodeseek.com/post-606792-1)
  - 核心问题：订阅或加入 Google One 家庭群组时，提示「地区不匹配，无法加入家庭组」。
  - 根本原因：Google 账号体系里有 3 个不同的地区概念。家庭组匹配的是「Play 商店地区」，而不是你当前的「IP 地区」。

地区类型	👀 在哪里查看	💡 定义是什么
Google Play 商店地区	play.google.com右下角	付款资料中的地址 (家庭组看这个)
当前 IP 地区	policies.google.com/terms	你现在用的代理节点
账号注册地区	Google 账号设置	注册时的 IP

- 地区类型	定义与作用	关键限制与特点	特别备注
Play 商店地区	• 决定商店应用及定价 • 家庭组判定依据	• 需绑定该区本地支付方式 • 限制严，每年仅可改一次	⚠️ 家庭组匹配这个 (成员地区必须与家长一致)
当前 IP 地区	• 访问网络时的物理/VPN位置 • 实时变动	• 直接影响搜索结果 • 决定区域限制内容 (如流媒体)	-
账号注册地区	• 创建账号时选择的地区 • 属于账号的基础属性	• 通常不可随意更改 • 影响部分基础服务

- 操作名称	操作位置	作用	解决地区问题用哪个？
移除付款方式(Remove payment method)	Google Pay > Payment methods	仅仅删除了卡号，地区锁定依然存在。	❌ 不行
关闭付款资料(Close payments profile)	Settings 页面最底部	彻底重置账号的支付属性和地区绑定。	✅ 必须用这个

- 要确认账号真实的 Play 商店地区，以 Google Pay 的 Payments profile → Country/Region 为准。

- [google 账号是美国 但是无法加入美国组的解决方案 - V2EX _202601](https://v2ex.com/t/1184393)
  - 账号已经申请改资料变成了美国 但是还是没法加入美国群组
  - 右下角能看到支付国家 就是因为这个地址和上方账号地址不一致导致无法加入
  - 设置->支付资料->设置->滑倒最下面 关闭资料即可
  - 支付资料银行卡卡什么都可以随便填 但是国家一定选美国 点击确定保存资料 是不是成功无所谓 这时候再去看支付国家就会变了

- 不用改区，
1 、挂美国的梯子，开启 tun ，然后 https://play.google.com/store/games 查看确认是否是美国
2 、关闭支付资料
我地区是 香港的，一直没改成功，手动填写申诉理由，不给审核。
在咸鱼上买的服务，满足这两个也加入 家庭组了。

- ## ["Can't join family group It looks like you're not in the same country as the person who invited you" - Google Drive Community _202508](https://support.google.com/drive/thread/369037540/can-t-join-family-group-it-looks-like-you-re-not-in-the-same-country-as-the-person-who-invited-you?hl=en)
- To ensure a 'Payments profile' is the same 'COUNTRY/REGION' as the family manager who invited you:
  - https://policies.google.com/country-association-form

- Ensure the 'COUNTRY/REGION' shown in the 'Payments profile' matches those of the family manager (parent account).
  - https://payments.google.com/settings

- ## [分享一个注册谷歌账号不用验证手机号的方法 - LINUX DO _202607](https://linux.do/t/topic/2535158)
  - 主要是最近谷歌风控严重，要么就是让你用手机扫码然后给它发短信（但是发送失败），要么直接让你填验证手机（但是+86手机提示不支持），要么用免费机场注册的账号立刻被封，总之各种失败。
  - 这个方法很简单，先挂好US梯子（反正我挂的是US的），在安卓手机中下载好Google app（不是chrome，也不是google play），点击右上角账号登录，然后选择创建新账户，一路进行下去，就注册完毕了，不会问手机。然后去浏览器中登录gmail的时候只会要求填写辅助电话和邮箱（不会发验证码验证），还有地址（跳过即可）。然后就登上了。

- 我一般是在IOS的Gmail、Youtube这些APP上面注册，隔一段时间就能不用验证手机注册一两个号，慢慢的攒了好几个号了

- 是可以，用play一样的。但过两天就风控了，不过写申诉就行了， 基本都能申诉回来
- 我也是 在Gmail的安卓app 隔一段时间就注册一个 已经注册7-8个 想起来就注册，不过还是会封，随便申诉必过

- ## [Removing old phone number from account : r/GoogleSupport _202601](https://www.reddit.com/r/GoogleSupport/comments/1qhc02x/removing_old_phone_number_from_account/)
- Login to your Google account in a browser. Select: Security and sign-in: Click on "Recovery phone": Delect the old number and delete it.

- Totally understandable concern, this usually happens because Google treats phone numbers added at signup as “historical recovery info” and sometimes the UI doesn’t let you fully remove them even after adding a new one.
  - People usually handle this by relying on stronger recovery options or periodically auditing what data is actually usable for sign-in; a common mistake is assuming an old number alone can grant access when in practice it’s just one weak signal among many (websites like Delvia org can help you sanity-check what recovery paths are exposed, but it’s just one option).

- ## [How do a remove a phone number I no longer have access to from my account when there isn’t an option to? : r/GoogleSupport _202603](https://www.reddit.com/r/GoogleSupport/comments/1rs21v2/how_do_a_remove_a_phone_number_i_no_longer_have/)
- The reason you do not see the trash can icon is that Google still considers that old number as your active 2-Step Verification or account recovery method. You cannot delete it from the personal info page until you replace it in the security settings.
  - Since you are already logged in on the device you took the screenshot from, go to your Google Account settings and click on the Security tab. Scroll down to 2-Step Verification. Add your new phone number there and verify it. Once the new number is set up for 2-Step Verification, you will be able to remove the old one from that list. Also check the Recovery phone section under the Security tab to make sure your new number is updated there too.
  - After you completely remove the old number from the security and recovery settings, the trash can icon will finally appear on the page in your screenshot so you can delete it for good.

# discuss-email-hosting
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [问下各位关于25端口的问题 _202610](https://www.nodeseek.com/post-966645-1)
是不是一般25端口入站vps都是放开的，不会特意屏蔽

但是出站的要求明显更严格

但是25端口出站+rdns组合只有少数vps服务商才会提供
比如我所知的dartnode

- 绿云全开，但有部分在黑名单列表里。

- 绿云开 25 出站这点确实少见，不过 IP 段在黑名单里等于白开。想自己发信的话建议先用 mxtoolbox 查一下 IP 段的信誉，很多商家的段早被 Spamhaus 列过。真要稳，发信走 SES 或 Resend 的中继，VPS 只收信，比养 IP 省事得多

- ## [[闲聊]现在都有哪家廉价的VPS服务商支持自建邮箱？ _202607](https://www.nodeseek.com/post-839395-1)
cloudnium（可发，不能收）
DediRock
cc
RN
CCS
delux
netcup

- cloudnium啊~3块多一个月~
出站 25，是通的
入站 25，不通
❓ 实测都能收

- 25端口开的就行，没rdns进垃圾箱的概率会高一些

- ## [有佬知道dedirock支持rDNS _202604](https://www.nodeseek.com/post-687338-1)
- 支持，但是面板配置不会生效，工单申请

- ## 💡 [DediRock RDNS 要多久啊 _202604](https://www.nodeseek.com/post-703882-1)
  - 有没有兄弟工单申请了，DediRock 的 RDNS，要多久啊
  - 通过了
  - 他们家不需要理由，我工单写的： `请帮我修改xx.xx.xx.xx的rDNS指向，xx.xx.xx.xx to mail.aaa.com` ，你的域名首先要正向解析过去，然后他才会给你添加反向解析。

- 我看了下似乎可以直接添加？
  - 可以加，但是不生效，要工单加才行。

- 好奇问一问如果做邮件服务器的话，使用mail.xx.xx作为发信域名，是不是也要用mail.xx.xx来做rdns呀？
  - 是的，至少我用的是iRedMail，是需要rDNS mail. 域名的

- ## [杜甫都开25端口吗 _202512](https://www.nodeseek.com/post-533971-1)
- 有些商家不给开，有些要发工单开

- ccs的25端口和rdns都是支持的，不过后者要发工单申请

- 怕碰见滥用，滥用会导致单个IP或者整个asn会被拉黑名单，要交钱才给删黑名单，应该是怕这个
据说4000多人民币

- ## [折腾了一晚上自建邮局，最后还是选择托管 _202602](https://www.nodeseek.com/post-608741-1)
  - 整了一晚上Stalwart，搭在RN上，mailtest 9.1分，实际只有QQ邮箱能收，gmail进垃圾箱，outlook根本就是拒收，最后还是甲骨文托管邮局了。

- 进垃圾箱其实跟用什么邮局无关
  - 配置正确是基本条件，IP，域名信誉，邮件内容都有影响

- stalwart为了秀肌肉，实际根本不是给人用的东西。
见过最烂的文档没有之一。
如果你有机会，可以试试Mox，配置简单，且遵循RFC标准，目前拿所有支持的测试都是10分。

普通的邮件交流目前投递Gmail和Outlook都没进垃圾箱

- 甲骨文做邮局好弄吗
  - 免费龟龟里面的，每天200封，每分钟限速10封，够用。

- 之前用阿里企业邮箱，满分，不进垃圾邮件

- 哈哈太真实了，自建邮局就是这样，技术上能跑通但实际送达率是玄学。大厂对小IP的信誉度要求太苛刻了，花时间养IP还不如直接托管省心。

- 已经在mox禁用ipv6了。

我第一次发信测试qq、outlook 进垃圾箱了，查看发信ip、mox的dmarc列表，才知道用了ipv6，spf校验没过~

- 建议还是把v6发信关闭吧 只有坏处没有好处

- 企业邮箱服务是要多点部署，防止单点故障，stalwart支持分布式部署，承载百万甚至千万级别的发件量

stalwart是企业邮箱方案，个人使用确实过于复杂，也不必全部否定

- ## [使用 Stalwart 自托管邮局服务 | Dejavu's Blog _202601](https://blog.dejavu.moe/posts/hosting-mail-and-collaboration-server-with-stalwart/)
- Rust 编写的高性能邮件与协作服务器，兼顾了极致的运行效率与从个人到企业级的扩展灵活性。
- 空闲状态下 RAM 占用约 100MB，是资源受限系统的理想选择。
- 并发处理：系统默认设置为全协议共 8192 个连接，更高并发场景下，也支持多节点负载均衡部署。

- 选择 25 端口开放、支持 rDNS 解析 的云服务提供商，这是自托管邮件服务器的基本门槛。
  - Netcup 全系产品原生开放 25 端口，无需提交工单申请。若是新购买的 G12 代产品，只需登录 SCP 控制台手动删除默认的防火墙策略即可。
  - 在 Netcup 客户面板，设置 rDNS 记录

- 本文以 mail.via.moe 作为测试邮件域名，我们将获得类似 helo@mail.via.moe 的邮箱。
- 在设置服务器的 rDNS 解析之前，先完成域名到服务器 IP 的解析。
  - 请勿开启任何 CDN 来代理此流量，DNS 记录全球同步需要一些时间，趁着这段解析空档，我们继续下一步。

- Stalwart 遵循「安全即默认」原则，系统内部已集成了针对暴力破解、账户枚举、漏洞扫描及 SYN 泛洪攻击的防护机制。
- 我们将采用官方推荐的 二进制安装 方式（而非 Docker）。通过官方提供的 Shell 脚本，可以快速完成部署。后续升级只需手动替换单个二进制可执行文件，维护压力极小。

- 在 Cloudflare 控制台 新建一个用户 API 令牌，这将用于 acme.sh 用于 DNS 验证

- 官方文档逻辑混乱，Web Admin 控制台操作反直觉、用户交互体验差、维护和更新困难，我认为它远未达到生产级别的可用水平。

- 👥 

- 现在用的是cloudflare提供的域名邮箱，后面接的是自己的微软邮箱，体验上不错，对外展示是自己的域名，后台可以随意切换实际收信邮箱
  - 不能发信，只能收信

- ## 🌰 [邮件服务器系列教程 - 香菇肥牛的博客 _2025](https://qing.su/mailservers)
  - [Stalwart Mail 邮件服务器的单服务器部署 - 香菇肥牛的博客 _202501](https://qing.su/article/stalwart-mail-single-server-nginx.html)

- ## [关于自建邮箱 - LINUX DO _202501](https://linux.do/t/topic/378090/2)
- 自建容易但是收发信极容易被拉黑的，因为你的域名和 ip 之间只有 mx 解析没有反解。建议还是用第三方吧，量不大的话腾讯企微就可以了

- 个人搭建的话，如果不是很熟悉自建邮箱，比较推荐 mailinabox.email, 这是一个成熟的一体化套件，所有东西都给你装好安排好了，包括备份、文件储存、日历、DNS，等等，很适合新手。

如果想要体验新的功能，这里必须得推荐用 Rust 写的 Stalwart mail, 可以进行极其精细的自定义，而且超级轻量，速度还快。Stalwart 应该是去年以来国外最火的自建邮箱解决方案了。我现在也已经从 mailinabox 搬到 stalwart 了。不过这个东西配置的时候坑特别多，不建议新手用。

普遍意义上的域名邮箱主要有三个部分，1 是 MTA （可以理解为 SMTP 服务器），2 是 MUA （可以理解为 IMAP/POP3 服务器），3 是客户端软件（比如基于本地的 Thunderbird, EM Client, Foxmail，基于网页的 Roundcube, Snappy, SquirrelMail 等等）。

技术层面，除了一些商用闭源软件外，市面上用得多的 MTA 主要是 Postfix 和 Exim, (Mailinabox, Poste, iRedMail 等等用的都是 Postfix)，这是二十多年前 C 语言写的程序，现在还是主流。最近几年发展起来的比较新的 MTA 有用 Java 写的 Apache James 和用 Rust 写的 Stalwart.

市面上用得最多的 MUA 是 Dovecot, 和 Postfix 一样，这也是二十多年前 C 语言写的程序，现在依旧是主流。最近几年发展起来的比较新的 MTA 有用 Java 写的 Apache James 和用 Rust 写的 Stalwart.

客户端软件就有很多了，用得最多的开源网页邮件客户端还得是 Roundcube, 用 PHP 写的。个人更推荐的是轻量的 Snappymail 或者功能更丰富的 SOGo.

- Serv00 个性邮局打造过程（调试详细步骤）
lark
自建 找开放 25 端口的小鸡
买别人的服务 比如 mxroute

- ## [【分享】Mailu&Poste.io自建邮局的比较及避坑指南 _202503](https://www.nodeseek.com/post-296754-1)
  - 为了充分利用闲置的Vps，用Mailu和Poste.io分别自建了一次邮局，其中也踩了一些坑，特分享一下。
  - 推荐支持设置rDNS（一般是找提供主机或VPS的厂商设置，部分厂商在控制台也可以自行设置）
  - 顶级域名（TLD）推荐使用 .com、.net或各国缩写的后缀，不容易被列入不可信的TLD名单中，此项主要影响发出邮件后产生的垃圾邮件评分
- 推荐使用Cloudflare等比较大型的DNS解析商配置，会比较清楚，Cloudflare还提供了针对Email配置的DMARC Management，帮助你检查DNS的配置情况。
- Mailu和Poste.io的比较
Mailu是开源全免费的，Poste.io也是免费使用但部分功能需要专业版解锁
Mailu支持自动根据Let's Encrypt证书生成TLSA记录，Poste.io需要自行生成，当然TLSA生效的前提是域名需要支持DNSSEC
两家都支持反病毒和反垃圾邮件的功能，其中反垃圾邮件Mailu支持对收、发的邮件都进行扫描，Poste.io对发的邮件进行扫描是专业版服务，如果你的邮箱不止你一人使用，想避免被滥用发送垃圾邮件可能需要关注
Mailu支持用户直接注册，Poste.io的免费版本不支持，只能帮助创建用户，用户登录后自行修改密码
两家都支持管理后台，Poste.io的管理后台颜值更加高一些
- 一些坑点
在配置DNS的MX记录的时候，name可以使用@代表你的域名，一些比较正常的解析商如果你输入yourdomain.com在name里也没问题，但一些比较蠢的DNS解析商会帮你解析为 yourdomain.com.yourdomain.com，导致一直解析不对
如果用Cloudflare做解析，记得与Mail相关的解析记录都不能开代理，包括Mail对应的那条A记录、CNAME记录等
部分域名解析商的DNSSEC是收费服务，免费版本无法开启
如果使用的主机或者VPS内存比较少，可以开一下Swap，也是可以跑起来的
完成后记得用mail-tester之类的工具测试一下发送邮件的得分，如果一切正常应该会得到如下结果

- 补充下：我是用的netcup1o鸡部署的，域名也是用的de的域名，都是没问题的（之前用过top的，会被扣分）
我自己最后留的是poste.io，主要原因是2个，一个是我一台机器先后部署的不高兴动了，二是poste.io的后台管理端颜值确实高点

- 还有一条重要提醒：1个月以内的新域名不能用来发信，不然直接黑名单。

- 有什么其他便宜稳定主机推荐自建邮局吗？
  - 主要是需要放开25端口，有放开的一般都可以的，查了下RN、OVH之类的都行
  - 常见的有nc、rn、cc这些吧
- 哪个更适合低配置vps
  - 2个占用都不高的，不开扫病毒就行，我的netcup1o鸡内存占用60%，swap用了300m，cpu更是只有个位数占用

- 最好把邮局和网站分开，因为你网站可以套个CF开小黄云保护源站，但是邮局开不了小黄云，这样会暴露源站ip
  - 我现在就是网站之类的web服务一台VPS，邮局专门弄了netcup的1o鸡，解析的时候在一个主域名下分开

- 前几天我也在1o上部署了poste.io，用的是nginxproxymanager做的反向代理，需要把.well-known同时挂载给poste.io容器才行，不然smtp这些端口申请不到证书。
虽然写在博客里了，但是还是贴一下配置吧，需要使用docker volume create well-known先创建卷。

- 测试了下，当https都由nginx反代提供的情况下，poste使用nginx的反代很方便，mailu非常麻烦，webmail那边总是502。

- ## [分享一个，和论坛邮箱类似功能的，来自simplelogin，我也是最近学习到的 _202607](https://www.nodeseek.com/post-805996-1)
  - 能注册，能push，但是只能10个别名
  - Proton 家族背书： 2022 年被大名鼎鼎的隐私邮箱巨头 Proton 收购了。现在和 Proton 体系深度整合，稳定性有绝对保障，不用担心小厂跑路。
  - 100% 开源 + 支持自建 (Self-host)： 它的代码完全开源
  - 支持自定义域名 (Custom Domains)： 这是高级版最香的功能。你可以绑定自己的域名，开启泛解析（Catch-all），配合它的目录（Directory）功能，实现无限后缀别名。
  - 支持 PGP 加密： 极客福音。它可以把收到的邮件用你的 PGP 公钥加密后再转发，这样即使是你的主邮箱提供商也看不到邮件的具体内容。

- 论坛有个佬自建了simplelogin，很多人交易都用的 https://app.yuanyou.de/auth/login
  - 我试过了 他是把创建的别名邮箱收到的邮件转发到你的注册邮箱里 逻辑跟seek.li不一样

- ## 🌰🌰 [教程：使用 mailu 搭建LINUX DO Mail同款域名邮箱服务器 - LINUX DO _202502](https://linux.do/t/topic/453502)
  - Mailu.io 是著名的基于 Docker 的邮件服务器管理系统，它的前身是著名的 Poste.io 系统。与 Poste 相比，Mailu 的功能更加丰富，在服务器集群部署的环境中也有较好的可拓展性，但资源占用较高，且部署起来没有 Poste 那么直观。相对来说，Poste 更适合小团队，而 Mailu 可以用于较大规模的团队和社区的部署。
- 本篇教程总共包括下面的几个部分
搭建开始前的准备
域名 DNS 的设置（第一部分）
Reverse DNS 的设置
生成 Mailu 服务器配置文件
安装 Mailu
域名 DNS 的设置（第二部分）
添加用户与其他域名
测试邮件收发
配置 MTA-STS (可选)
设置 SMTP Relay (可选)

- 用下面的命令判断 25 端口是否被阻断。
  - 如果收到类似 220 smtp.mail.yahoo.com ESMTP ready 的回复，说明 25 端口正常，可以发信。
  - 如果超时，且防火墙没有禁止 25 端口，则说明 25 端口被阻断。 示例信息 telnet: Unable to connect to remote host: No route to host
- 如果您使用第三方 SMTP 中继服务来进行发信（比如 Linux.do 使用了 MXRoute 作为中继），那么 25 端口的开放就不是必须的。

```sh

telnet smtp.aol.com 25
```

- 给服务器设置一个单独的子域名，作为邮箱服务器的服务器名，这里将假设为 mx.linux.do.
- 如果您使用 Cloudflare 作为您的 DNS 服务器，请关闭上述 A 记录的 CF Proxy 功能（把解析记录边上的小云朵关掉），否则会导致收不到邮件。

- Reverse DNS (rDNS) 是邮件服务器必不可少的配置。
- Reverse DNS (rDNS) 的作用是将 IP 地址指定为一个子域名。如果您的发信 IP 地址没有设置 rDNS，发送的邮件将会被很多邮件服务器拒收。
  - rDNS 需要在您的服务器的主机商处设置。几乎所有的国外主机商都提供了自助设置 rDNS 的服务，您需要在您的服务器后台设置，一般会出现在 "Network" 或者 "IP Address" 等地方。如果您找不到相关的设置，请发工单给主机商，他们会帮你设置好或者告诉你在哪里可以自助设置。
  - 当然，如果您使用第三方 SMTP 中继服务作为发信节点，那么就不需要给你自己的服务器设置 rDNS 了。

- 之前，我们已经设置好了邮件服务器需要的大部分 DNS，包括 MX, SPF, DMARC 等。搭建好邮件服务器之后，我们还需要根据系统生成的 DKIM 密钥来配置 DKIM 记录。
  - 进入服务器后台 https://mx.linux.do/ , 点击左侧 Mail Domains，可以看到如下图的域名管理界面。
  - 生成 DKIM key 记录。您需要添加这条 TXT 记录进您的域名的 DNS，用来 DKIM 签名。注意不要把 DKIM 的内容复制错了，如果复制粘贴出错了，会导致 DKIM 验证失败，导致发送的邮件被拒收。
如果您需要支持各种客户端的自动配置，也可以按照页面的提示设置好 SRV 记录（不必须）。
如果您的域名支持 DNSSEC, 那么也可以按照页面提示设置 TLSA 记录（不必须）

- 全部设置完毕后，我们来添加用户。也可以添加其他的域名。
  - 进入域名管理界面。在 Manage 模块中找到 User, 可以新建邮箱用户

- Mailu.io 支持配置 MTA-STS. 启用 MTA-STS 可以硬性要求发件方往你的邮件服务器发送邮件时使用 TLS 安全链接，这样可以在一定程度上提升邮箱的安全性，防止中间人攻击。

- 
- 

- ## 🌰 [自建邮局 | Poste.io邮箱服务搭建教程 _202308](https://www.nodeseek.com/post-20417-1)
- [Poste.io邮箱服务器搭建教程 _202410](https://www.nodeseek.com/post-169958-1)
  - 无ptr/rdns

- [【教程】使用Docker快速搭建邮件服务器 _202501](https://www.nodeseek.com/post-253926-1)

- ## [想自建邮件 有哪家服务商能帮助配ptr吗 _202606](https://www.nodeseek.com/post-767798-1)
- ccs独立服务器，日本樱花，德国netcup这三家能做ptr

- aws ec2 可以prt

- ## [迷上了自建邮局，请问服务器选哪个好？ _202609](https://www.nodeseek.com/post-919365-1)
  - 要求开25端口
- DediRock(CCS系) 或者 NetCup 或者 正价瓦工 或者 EuGameHost的 UK

- 自建推荐加1或2个备用邮局服务器 这样主mx炸了也不会丢件

- 我用的cloud mail，直接CF works+resend，收发信都没问题
  - 没办法imap smtp

- cloudnium的服务器默认开25端口而且控制台就能设置反向dns，我搭了3个stalwart

- RN的都可以开25端口，支持工单改PTR解析
你觉得哪款便宜配置够就用哪款

- ## [最近已经把邮箱全迁到自建邮箱了 _202406](https://www.nodeseek.com/post-125892-1)
- 第一是，总会在后期想换更好的域名，就会变更邮箱，巨麻烦。
第二是，有时候你从未想过出售或者放弃，但是人就是很奇怪，想把这个域名扔掉，但是你发现很多地方绑定的这个邮箱，你会记不住，最后发现登录不上去某个站，损失惨重。
第三是，域名邮箱和专业的邮箱服务、功能、各方面差距实在是太大了，折腾来折腾去，我最后还不如用专业的邮箱服务。
所以最后又全都折腾回去了，现在我的域名邮箱仅仅用来收些特殊的邮件。

- 去年我和你做了一样的事，把所有邮箱全部变成自建，然鹅，上个月把所有域名邮箱全部改回了outlook。。。。这给我累的。

- 域名邮箱我都用来注册各种盗版网站

- rn, ccs, naranja都不限制（我印象）

- 對公用域名郵箱，對私用 outlook or Gmail

- qq上面最多能添加3个邮箱
# discuss-email
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Tuta邮箱感觉比proton还坑啊！ _202402](https://www.nodeseek.com/post-67981-1)
  - 刚想注册个这个Tuta(Tutanota)邮箱，发现这货6个月不登陆就删号，注册的时候还得勾选只有一个免费账号和不能用于商业用途的选项。

- 所以我收机碰到稀奇古怪的邮箱我都不收

- 这玩意主打隐私，不适合日常使用
另外proton之前泄露过用户ip，算有前科不太敢用

- 

- ## [我的Google邮箱有点多，辅助邮箱填相同有影响吗 _202501](https://www.nodeseek.com/post-246558-1)
  - Google邮箱添加辅助邮箱，能不能都填一个，或者两三个邮箱填相同的，有没有影响啊？

- 我五六十个gmail 大部分填一样的 没啥大问题 不过最好还是做下区别

- 我outlook也害怕填相同的出问题，所以都填了不同的，不过可能只是自我安慰，毕竟经常用同一个IP和浏览器登录，就看微软啥时候心情不好开杀了

- 几十个邮箱 辅助邮箱都填的qq邮箱 最近QQ邮箱老给我弹xxx谷歌邮箱两年没登录让我登录 我现在用的也不是之前的设备和IP了 搞得之前的一堆账号也很难登上去

- Outlook 可以添加邮箱别名。我是一个 GMail 对应一个别名。除非两家的数据串到一起，否则应该很难查出来吧。

- ## 💡 [How to ACTUALLY mark all of your emails as read in your inbox (2025) : r/GMail _202507](https://www.reddit.com/r/GMail/comments/1m78zti/how_to_actually_mark_all_of_your_emails_as_read/)
- I went down this rabbit hole and could not for the life of me figure out how to mark all my emails as read. I'm sure you guys have followed the most commons steps:

1. Go to your google inbox

2. is:unread in the search bar to populate all of the unread emails

3. hit the check mark in the top left above the first email and a message "select all conversations that match this etc" will pop up

BUT wait - it doesn't pop up, no matter how long you wait.

4. This is the secret, key step. In the top right of your inbox, you will see your email sorted by "Most Relevant". You can only mark all of your emails as unread if the emails are sorted by "Most Recent".

Once you make this switch and follow the above steps, it WILL work. 

- This method works in the iOS app:

To mark all emails as read in the Gmail app, open your inbox, tap and hold the first unread email to select it, then tap the "Select all" checkbox that appears at the top to select visible messages, and finally tap the open envelope icon (Mark as Read) at the top right. For a very large number of emails, you might need to scroll and tap "Select all" multiple times, or use the desktop version for easier bulk actions, as the mobile app handles them in batches.

- iOS only allows me to select 30 emails when I have several thousand

- ## [求gmail邮箱账户的购买渠道 - LINUX DO _202609](https://linux.do/t/topic/2857425)
  - 最近公司想买一批 gpt 账号，找好了代充但是要我们自备邮箱，听说 gmail 耐用一些，想问问佬友们哪里可以买得到靠谱的 gmail 邮箱账户？自己创还要养有点麻烦，暂时不考虑
- 代充是怎么个代法？
  - 给session

- 不要买新号 现在老号很多存量的 直接买老号 我说的就是老号的价格 10 块到 20 块左右

老号它的风控没那么严 不用验证手机号了

- 可以开通 google workspace，一个账号可以生成 30 个邮箱地址。收费版比较稳定。

- mail.com 只有注册比较吃 ip（更建议直接买邮箱然后换密码） 其他的风控什么的都还好 并且 mail.com 自动化更容易
  - proton 的话也挺稳的 但是 proton 接码自动化没做好的话容易导致邮箱被封 邮箱风控相对高一点
  - 我目前卖的成品号量大的也都是走 mail.com 的

- 买的 gmail, 买后不要立刻修改密码 只修改 2fa, 并绑定手机和辅助邮箱，过一周后修改密码 基本不会出现 2 验，或者也有些邮箱申请的时候就没绑定手机，二验也只是输入辅助邮箱名称 不影响 我年前买的 当时 2-8 块左右 有学生认证的贵一些 现在倒无所谓了 我看还有 10 块一下的 不过我没买过 不知道质量怎么样

- 之前也买过 10 来个，都正常，然后突然有一天开始陆陆续续挂了 4 个，其中三个在同一天挂，IP 与其他存活至今的完全一致，有关指纹也正常，全都是曾经有过异地设备并已经剔除和挂失的即有关绑定全部换新并且还闲得没事去油管搜索播放过 

- ## [gmail邮箱购买经验求指导建议 _202607](https://www.nodeseek.com/post-808947-1)
  - 昨天买了一个 Gmail 邮箱，然后上去一顿操作，然后被封了。上去我就改了密码，然后修改了辅助邮箱，添加了 RFA 验证。这一顿操作猛如虎，然后直接挂了。

- 新号改了环境上去不要改敏感信息 一周后再改

- 重要警告（必读）
禁止立刻修改密码！ 登录后请勿立即更改密码，否则极易触发风控导致封号。因登录后立刻改密导致的封号，不提供任何售后！

请勿频繁切换登录！ 不要频繁登入登出，建议在固定设备上保持登录。

养号期（7-30天）： 建议始终使用固定且纯净的IP（推荐美国IP）登录使用，稳定使用 7-30 天后再进行修改密码、绑定手机等敏感操作。

- 购买后先不要着急改这些信息，先去设备里面看，如果设备里面显示有三星手机登录的痕迹，很遗憾，百分之99这个号是号商使用模拟器接码注册的，哪怕你绑定自己的手机，后续风控了也要求验证原始手机，号直接废了，需要等几个月有概率让你重新绑定手机。

- ## Proton ["Account is no longer available due to inactivity" : r/ProtonMail _202411](https://www.reddit.com/r/ProtonMail/comments/1gl35ek/account_is_no_longer_available_due_to_inactivity/)

- [Inactive accounts | Proton  ](https://proton.me/support/inactive-accounts)
  - If you’re on a Proton Free plan, your account must stay active to avoid deletion. To keep your account active, sign in to Proton and use one of our services at least once a year.

- ["Account is no longer available due to inactivity" even though I opened my account before this policy change took place : r/ProtonMail _202411](https://www.reddit.com/r/ProtonMail/comments/1gtefcg/account_is_no_longer_available_due_to_inactivity/)
- Multiple people complaining about their emails gets deleted 2 years before April 9, 2026 is the problem.

- I had the same thing happen. I created another account, and used it to contact them about the original account, providing the details. After a few back and forth emails they restored the original account.

- ## [How can i use more than 10 gmail at a browser? : r/GMail _202512](https://www.reddit.com/r/GMail/comments/1pd5niu/how_can_i_use_more_than_10_gmail_at_a_browser/)
- With chrome, you can set up different profiles - one for each google account. I often have 5 or 6 chrome sessions open with each logged into a different account. I flip to the chrome session of interest to do something, and then flip to another.

- [Maximum Number of Accounts : r/google _202502](https://www.reddit.com/r/google/comments/1izo9mi/maximum_number_of_accounts/)
  - Is there any way to add more than 10 accounts to a single Google profile? I work for an agency and have 15 clients but can only have 10 accounts on my profile at a time.
- Setup profiles in your browser for each client to help prevent data leakage.
  - I have a dozen or so Google accounts, so far, each with their own Chrome browser profile. I also have each one remember the tabs I had open on them, and set to send my main email notifications if the account is at risk of deletion due to inactivity. Also have 2FA on each.

- ## [How many gmails can be opened under one number? - Google Account Community _202502](https://support.google.com/accounts/thread/324205080/how-many-gmails-can-be-opened-under-one-number?hl=en)
- You can create up to four Gmail accounts using the same phone number for verification. Opening a second Gmail account for work purposes is both possible and safe. Having multiple Gmail accounts is common and can help separate personal and professional communications.
  - While Google allows you to create as many Gmail accounts as you want, the limit of four accounts per phone number is a security measure to prevent spam and abuse. If you need more than four accounts, you'll need to use a different phone number for verification. Using multiple Gmail accounts is safe as long as you follow good security practices like using strong, unique passwords for each account. Having a separate work account can actually improve your overall email security and organization.

- ## 💡 [How many Google email accounts can I have? : r/GMail _202601](https://www.reddit.com/r/GMail/comments/1qc58lb/how_many_google_email_accounts_can_i_have/)
- You can use multiple addresses with a single account using plus addresses. If you have joesmith@gmail.com, you can give addresses to multiple sites as joesmith+site1@gmail.com, joesmith+site2@gmail.com, etc.
  - The last time I checked, Google didn't have any hard limit on the number of accounts you have, but it does seem to have a hard limit of how many accounts you can set up with a given phone number. That limit is 4.
- There is no limit off Google accounts but if you use it for free storage then Google can disabled your account but if you do not use to store photos on the account there can not be anything wrong. i have 13 Google accounts and have on 2 accounts Google One paid. but beware doent use your free account for "Free" storage because Google then will disabled your.

- ## [outlook邮箱注册分享 - LINUX DO _202604](https://linux.do/t/topic/1996756)
  - 纯手工注册，仅仅测试玩玩，
  - 环境：win11、outlook客户端、日本节点
  - 一口气连续注册好几个都成功了，信息都随机填写，关注下机器人验证那边，步骤如下：
  - 纯手工注册，一般可以连续成功8个左右，出现异常，就换个节点

- 谢谢佬友分享！之前用网页端注册无论怎么换节点、用指纹浏览器、开无痕模式都经常被机器人验证卡住，改用outlook客户端注册之后非常丝滑，不换节点也可以连续注册多个邮箱。
  - 再补充一点踩坑经历：clash网络设置使用系统代理时，outlook客户端注册弹窗会报错0x80190001。需要把clash网络设置改成虚拟网卡模式（TUN模式），代理模式改成全局。

- com注册简单，主要想注册几个别的国家后缀的，一直没成功
  - 注册outlook时账户信息的国家填你要注册的邮箱后缀的国家，然后在outlook设置里添加邮箱别名，就可以选择国家后缀的邮箱。
  - 比如你想注册@outlook.sg后缀的邮箱，那么注册outlook时国家选新加坡。注册完成后，打开以下页面添加邮箱别名，后缀可以选择outlook.sg。https://account.live.com/names/manage

- 嗯嗯，一个节点过段时间也可以注册多个，反正邮箱肯定够用的；另外cloudmail+indevs.in域名邮箱也可以注册好多账号

- [outlook为什么注册门槛这么低？ - LINUX DO _202603](https://linux.do/t/topic/1761522/15)
  - 因为微软强制win11 oobe注册这个，想想如果打开新买的电脑然后注册不上进不了系统

- [现在outlook.hotmail注册对于我来说真的太难了。那个人机验证按麻了都不行 - LINUX DO _202604](https://linux.do/t/topic/2081470/2)
- 下载APP啊，用app注册，最慢3分钟都能注册一个出来了

- 别折腾了 几分钱一个的东西 甚至还能用支付宝红包，直接买你会快乐很多
- 3分钱一个的东西这么自己干什么呢，随便到处买的呀
- 以前是三分，但是后来大家都用这个来注册oai以后，涨价了好多倍了 

- 别走代理，用指纹浏览器，每个窗口只注册一个号，从来没弹过人机验证
# discuss-zulip/mattermost
- ## 

- ## 

- ## 

- ## [Slack Alternatives, broken trust : r/selfhosted _202405](https://www.reddit.com/r/selfhosted/comments/1cv2gpd/slack_alternatives_broken_trust/)
- Rocket.chat did some shady licensing shiningas not so long time ago, they backed out, buuuuut, i wouldn't trust them.
- Mattermost has weird licensing too. They have two releases, a binary MIT one, binary only, and an agpl source one

- I wanted to use Mattermost, but they charge for oidc. Ended up doing matrix with element.
- The free version can be used with Gitlab authentication (only the auth module, not full Gitlab). We use our >400 person Mattermost instance with that to attach it to an AD.
  - Same here. One can either setup a docker oauth server making the connection to ldap / ad or use Keycloak.

- ## [Now that RocketChat 6.5 limits to 25 users or less what are you moving to? : r/selfhosted _202312](https://www.reddit.com/r/selfhosted/comments/18a2624/now_that_rocketchat_65_limits_to_25_users_or_less/)
- Zulip. They are open source and even offer an importer for RocketChat
- We run zulip and mattermost. The tech behind zulip is nice, but the user interface needs work. Most people prefer the mm interface. Think this is the main issue it is lacking popularity.

- Mattermost has no 2FA and SSO in the free version, you also can't change the ToU from default, and a bunch of other restrictions (unless I'm wrong)

- ## [After Slack made it's last pricing change... : r/ProgrammerHumor _202209](https://www.reddit.com/r/ProgrammerHumor/comments/xedo3k/after_slack_made_its_last_pricing_change/)
- Zulip is the only text comm tool I know of which supports topics in channels (streams) and I think it’s pretty cool. I haven’t tested it enough yet though.

- GitLab bundles Mattermost in their Omnibus installation/package. You can take that as an indicator of quality, and/or probable good maintenance in the future. (I can not personally attest to either though.)

- I have to use zoom

- ## [Mattermost – open-source platform for secure collaboration | Hacker News _202206](https://news.ycombinator.com/item?id=31858829)
- They decided to up their price per user by a significant amount not too long ago... our self-hosted instance suddenly became more expensive than Slack but with an obviously not nearly as polished product as Slack. So we moved over to Zulip because at least they do their own thing, we haven't had any regrets over the switch to Zulip.

- My former company adopted Zulip because we were in the cybersecurity space and needed an on-prem solution. When I first saw it I thought "oh god this is going to be awful" - very ugly UI compared to Slack and others. But after getting used to it, I found that the UX is excellent.
  - When everyone on the team learn to use Topics, it's life changer.
- And not only that, Zulip is 100% FOSS, whereas Mattermost is Open Core, so the Open Source portion is missing key features.

- Zulip has a "public access" view, which I wish more open source projects would adopt (:eyes: kubernetes.slack.com) since it allows search engines to index into the threads
  - > Web-public streams do not yet support search engine indexing. You can use zulip-archive to create an archive of a Zulip organization that can be indexed by search engines.
  - 202406仍不支持
- You can export all message types and none of them require any special licensing or payment: https://docs.mattermost.com/manage/bulk-export-tool.html.

- Mattermost v7 was released on Thursday and includes video conferencing functionality! 

- Mattermost does not provide a good way to archive topics. 
  - Another wishlist would be to be able to hide or block people.

- Mattermost is nice in that communication and project management is all in one tool, but doing anything within Mattermost is very sluggish (even on a very overspecced server with only 1 Mattermost user online). Using their Focalboard plugin resulted in multiple seconds of wait time between various actions like modifying a task. 
  - On the other hand, Zulip has been consistently snappy even as we've onboarded users onto our instance. 
  - Seeing it in use at large organizations such as Rust's Zulip instance instilled confidence that it'll continue to perform well even well beyond our scale.
- Zulip's threading model is really nice to use once you and your team gets the hang of topic separation

- ## [We Switched to Mattermost | Hacker News _202108](https://news.ycombinator.com/item?id=28044235)
- Mattermost is great, but I wish they natively supported the Matrix protocol to enable federation. Or — at least — made it possible to integrate a "natively-looking" third-party bridge, similarly to how Gitter does it.
- There is Matterbridge that supports many different protocols including Matrix.
  - Yes, but it’s not the same as native or near-native experience.

- A couple things stand out to me about Mattermost:
  1. It's the most expensive chat out there, at $10/month and no free plan.
  2. Focalboard is being integrated to be part of the chat. Focalboard doesn't currently do much that I find interesting, but I have hope that it will with time.

- It's open core. There's a bunch of features that aren't in the open source version, such as LDAP authentication and 2FA enforcement.
- Mattermost is open core. There are features that aren't available in the open source version and which you have to pay for

- We used MM in the past and switched to Zulip. The docker upgrade path of MM is a pain and lacks support. (They switched to a new postgres version without providing any upgrade tutorial.) But honestly if you like to use a team chat to get work done Zulip works the best. The thread tagging inside a group and the keyboard support makes it easy to follow different conversations in a stream.

- The only gripe I have now (besides collapsed threads looking awful: which seems to be fixed in the latest beta!) is that the data (i.e. chats) is stored unencrypted in our MySQL database. Being a tech company lots of ours engineer 'theoretically' have access to this database. I believe MM suggests to some higher level db encryption to solve this, but this is not ideal.

- The only thing I missed is FOSS LDAP connector, I am strong believer that at least in some basic form it should come in such products - after all, you don't use such tools if you are not in enterprise and not having at least login is seriously problematic. We finished using Gitlab auth instead of it but I don't like that we are coupled to it.

- ## 🎯 [Mattermost 1.0 released – open-source Slack alternative | Hacker News _201510](https://news.ycombinator.com/item?id=10386847)
- The takeaway I'm getting from this story, and Mattermost, is: 1. Export your critical data from SaaS services if you're business cannot exists without them. 2. Test that this works before putting years of data into a service.

- > Every conversation in Zulip has a topic, so it’s easy to keep conversations straight.

- Overall I like it because they closely follow Slack's UI. However I question the choice of fully supporting Markdown. A comment isn't supposed to be documentation. Supporting things like bold, italic makes sense for emphasis or making code easier to read. But headings? When would one ever want really large text in a comment?
  - Mattermost team here, We had dozens of community members upvote a feature to add markdown and we added it because it made sense. Now we really love it and can't go back

- The main issue with IRC is that you have to stay connected all the time to receive messages, and you have to leave your IRC client to see and search the logs (unless you have some intermediate IRC client server that runs all the time). It's just not as nice.

- ## [Trying to decide between open source web chat platforms such as Mattermost, Zulip, Matrix etc. in 2022 : r/selfhosted _202209](https://www.reddit.com/r/selfhosted/comments/x8dsma/trying_to_decide_between_open_source_web_chat/)
- I would recommend using zulip over mattermost. While mattermost community edition might be suitable for most, but if lacks some of the most basic features and requires license to enable them. It's fucking ridiculous lol.

- There's Nextcloud with Nextcloud Talk.
# discuss-slack/discord/telegram
- ## 

- ## 

- ## ✨ [Select multiple chat messages to create a thread from – Discord](https://support.discord.com/hc/en-us/community/posts/4405512392727-Select-multiple-chat-messages-to-create-a-thread-from)
- just now discovering what Discord is & does, & cannot believe this isn't already a feature

- ## [Slack Is Going Public at a $16B Valuation | Hacker News_201906](https://news.ycombinator.com/item?id=20228689)
- Their product-vision was clear, their execution focused on what mattered... and they didn't need to bend or break laws to succeed.
  - Advertising companies like Facebook make their revenue by selling to advertisers, not individuals- they are emphatically a B2B company.

- Discord has essentially the same app but better voice/call support and other various features. But they seem focused on the gamer market.

- I think Discord is more a replacement of IRC than Slack could ever be.
  - Slack is enterprise and workflow-oriented, Discord is community oriented.

- ## [Discord vs Telegram vs Slack vs others : podcasting_202310](https://www.reddit.com/r/podcasting/comments/171cczn/discord_vs_telegram_vs_slack_vs_others/)
- Discord and it’s not even close. Hardly anyone in the US uses telegram (may not apply to you) and slack is something by people associate with business.

- I'll be completely honest, it all depends on your audience. 
  - People between the ages of 18-25 prefer discord. 
  - Older audiences prefer telegram. It all depends on how savvy your users are with tech.
  - you want to use the platform your audience is already using. 

- I prefer Slack over Discord generally speaking, but it lacks the ability to do any sort of moderation, which should disqualify it from community-building platforms. 

- Discord, hands down. Beyond the great options for chat (linking Patreon/membership tiers to certain channels/roles, searchable, threads within channels, etc), there are watch party stages and voice/video chats. Tons of bots to handle basic moderation, event reminders, polls, etc

- ## [Discord Vs Slack Vs Telegram : discordapp_201808](https://www.reddit.com/r/discordapp/comments/98wvrb/discord_vs_slack_vs_telegram/)
- discord's marketing/ui are more geared toward gamers, which might drive companies away from it. 
  - personally, i think discord is the better of the two being completely free and having more features. 
  - i haven't used telegram.

- Slack is generally the de-facto "business" chat platform. 
  - It looks and feels very similar to Discord, as Discord was seemingly heavily inspired by Slack. 
  - Telegram is... okay, but certainly not something I can recommend for a company
# discuss-mastodon
- ## 

- ## [Why Bluesky and not something like Mastodon? : KnowledgeFight_202307](https://www.reddit.com/r/KnowledgeFight/comments/14tawvg/why_bluesky_and_not_something_like_mastodon/)
- Mastodon's cool but it seems to confuse a lot of people, so the choice of Twitter replacement platform to reach a large audience is likely Threads vs BlueSky
- Bluesky is easier to setup (provided you get an invite) and will eventually be part of the fediverse.

- ## [What are your thoughts on those who use Mastodon alongside Bluesky : Mastodon_202308](https://www.reddit.com/r/Mastodon/comments/160vzob/what_are_your_thoughts_on_those_who_use_mastodon/)
- Mastodon's decentralization, including Activity Pub which has approval of the W3 consortium, is what can help make sure there isn't another Elon in the future.
  - The developers at Damus (the NOSTR client) regularly post about the problems they have with ActivityPub as a protocol, and yet they still fairly quickly implemented Mastodon relays.

- ## 🆚️ [Everything happening on Bluesky | Hacker News_202305](https://news.ycombinator.com/item?id=35830612)
- > Although Bluesky is currently hosted on only one server under the control of the Bluesky team, its intention is to eventually become a decentralized protocol for a multiplicity of federated servers with a variety of different moderation practices

- Bluesky made some key decisions that are different from Mastodon:
  - Profiles and posts are portable across hosted instances. If you have a problem with your admins, etc, you'll be able to hop away without much fuss.
  - Moderation is decoupled from hosting. They're still working out the details, but the overall vision is that the global firehose is public, and you'll be able to opt in and out of different moderators which operate on that stream. If you don't like what a moderator is doing, you'll be able to just turn them off for yourself. Moderation doesn't prevent people from posting, it allows people to prevent themselves from seeing.
- As far as I can tell, this is only with cooperation of the server owner; since their "DID Placeholder" relies on a server to provide a string of identity updates. ActivityPub can do the same thing with HTTP redirects; and Mastodon supports cooperative profile redirection, which is morally equivalent. Polycentric is a tad more decentralized than this, AFAIK it's specifically designed to make cryptographic keys first-class identities (so called "sovereign identity"). No clue if they've managed to solve the obvious pitfalls of cryptoidentity.

- Journalists are flocking to Bluesky, and not Mastodon because Bluesky allows retweets—which Mastodon doesn’t allow. Oh, and about hashtags, direct messages, and post edits not being available on Bluesky? Journalists don’t need them.

- ## 🆚️ [Blue Sky Server? : BlueskySocial_202304](https://www.reddit.com/r/BlueskySocial/comments/12nqfgz/blue_sky_server/)
- There is actually a lot of documentation for the ATP. It doesn’t cover the recent changes they’ve implemented, but there’s more than enough there to develop against the protocol and to understand the differences between it and AP.
- The major differentiators are also documented:
  - Data portability. Your data is stored in a self signed structure similar to a git repository. You own your data and you can move it around seamlessly without needing a 3rd party to verify it.
  - Algorithmic choice. It’s built around the idea that algorithms are useful and we need them, but users should be able to choose them.
  - Moderation. Moderation selection is also built into the protocol, although it’s still under development. Uses will be able to subscribe to different moderation providers separately from their host.
  - Performance. The performance cost of the protocol is a top priority and it’s something that was ignored with AP. They are designing it around the idea that low power hardware should be able to run an implementation of the protocol. AP is very… chatty, and it costs a lot to keep servers in sync with the federation.

# discuss-bluesky/threads
- ## 

- ## 

- ## 

- ## 

- ## [Threads or BlueSky, which is next? : cybersecurity_202307](https://www.reddit.com/r/cybersecurity/comments/14srryy/threads_or_bluesky_which_is_next/)
- Meta can’t launch Threads in the EU yet, that’s all I need to know about that.
  - 最初，Threads暂未在欧盟推出，是因为欧盟极为严苛的数字服务监管系统。

- Bluesky is like a merging of Twitter and Reddit. It's amazing, and the conversations there are very organic.

- ## 🪶 [Bluesky migrates to single-tenant SQLite | Hacker News_202311](https://news.ycombinator.com/item?id=38171322)
- I'm not opposed to this setup at all and it does have its place. But we are running away from schema-per-tenant setup at warp speed at work. There are so many issues if you don't invest in it properly and I don't think many are prepared when they initially have the idea.
  - The funny thing is that about a decade ago, the app was born on a SQLite per tenant setup, then it moved to schema per tenant on Postgres, now it's finally moving to a single schema with RLS. So, the exact opposite progression.

- Interesting... I like the strategy of having each user be 1:1 with a DB. What would be done for data that needs to be aggregated across users though?
  - To summarise the relevant details, the "AppView" service is responsible for the sorts of queries that aggregate across users, and that has its own database setup - I think postgres but I'm not 100% sure on that.
- You're right, as usual. AppView is on a Postgres cluster with read replicas doing timeline generation (and other things) on-demand. We're in the process of moving it toward a beefy ScyllaDB cluster designed around a fanout-on-write system.
  - The v1 backend system was optimized for rapid development and served us well. 
  - The v2 backend will be somewhat less flexible (no joins!) but is designed for much higher scale.

- Can someone that knows more about bluesky explain what data is stored in sqlite and not? Because i assume it isnt messages etc between users.
  - It's all your posts and replies as a user. While they currently host the only* PDS themselves, the end goal is for every end user to have their own PDS. Inrupt/SOLID calls this concept a "pod".

- This seems like a very misleading title, the Bluesky PDS is the meant-for-selfhosting thing they distribute, not the bluesky service as experienced and used by most of its users.
- AFAIK there's only one version of the software so "the service" runs the same thing that you self-host. SQLite seems like it will simplify the single-user case though.
  - That's right. This is the same code Bluesky is running on our new PDS hosts. It's all open source.
  - The main motivation in moving from a big central Postgres cluster to single tenant SQLite databases is to make hosting users much more efficient, inexpensive, and operationally simpler.
  - But it's also part of the plan to run regional PDS hosts near users, increasing performance by decreasing end-to-end latency.
  - The most experimental part of this setup is using Litestream to replicate these many SQLite databases (there are almost 2 million user repositories) to cloud storage. But we're not relying on this alone, we're also going to maintain standard SQLite ".backup" snapshots as well.

- I am curious, does the HN folks know if bluesky is more active than nostr or the mastodon network?
  - Less active than Mastodon, I'd assume more active than Nostr.
  - But the interesting thing for me isn't activity — it's the people on there.
  - Of the cohort who had >100k followers on Twitter, I think more of them post regularly on Bluesky than post on Mastodon. Bluesky definitely has a more cohesive feel, especially because there's currently just one instance & mod team.
- My bet is regardless of any initial good intentions, since BlueSky is a company, market pressures will inevitably force them into dark patterns like we see on every other commercial social network (going back to the early days of the companies, Facebook, Twitter, and even Google looked really good early on until all were corrupted by profit motive). My belief is that the profit motive is necessarily at odds with free communication.
  - To me, the ActivityPub network (Mastodon and friends) is relatively unique in the social media space in having no direct commercial pressures (the protocol is developed by W3C) and therefore being inoculated against the causes for these dark patterns.

- Why not use Postgres with RBAC (Row Based Access Control).
  - simpler db client
  - simpler cloud architecture
  - simpler resource management
  - simpler partial backups/restore
  - simpler compliance with law enforcement
  - partitioning might be easier
  - maybe simpler billing for storage ("just" size of DB)

- ## [Can you bookmark posts in BlueSky app?_202305](https://mrhack.io/can-you-bookmark-posts-in-bluesky-app/)
- as of now, bookmarking posts on BlueSky is not possible.
  - The only option available for users is to like a post.
  - After liking a post, it will be added to your list of liked posts. But, unfortunately, you cannot see your own likes as well.
- here are some tips to keep your favorite posts organized:
  - Use the "save post" feature on your device. This will save the link of the post, and you can easily access it again.
  - Use a third-party app to manage your bookmarks. Many apps are available on app stores that allow you to save and organize your favorite links.

- ## ✨ The official Bluesky app for Web, iOS, and Android is now open-source_202305
- https://twitter.com/addyosmani/status/1658228255328190464
  - Powered by @reactjs & @expo w/thanks to @pfrazee

- ## [First Impressions of Bluesky's Brand New iOS App | Hacker News_202303](https://news.ycombinator.com/item?id=35009723)
- Why would they expect anyone to build on top of their new social networking protocol? It is owned and will be driven by a private company and it’s desire for profitability, ⚖️ ActivityPub is an open standard that has been around for ~5 years and battle tested and already in use across different platforms.
- Maybe their efforts will be co-opted, but judging by the team's background -- André Staltz with Secure Scuttlebutt, Paul Frazee with dat/Beaker/Hypercore Protocol -- I think it's pretty clear the driving motivation for much of the team behind Bluesky is not profit.
- Bluesky's answer is this
  > Account portability is the major reason why we chose to build a separate protocol. We consider portability to be crucial because it protects users from sudden bans, server shutdowns, and policy disagreements. Our solution for portability requires both signed data repositories and DIDs, neither of which are easy to retrofit into ActivityPub. The migration tools for ActivityPub are comparatively limited; they require the original server to provide a redirect and cannot migrate the user's previous data.
  - > Other smaller differences include: a different viewpoint about how schemas should be handled, a preference for domain usernames over AP’s double-@ email usernames, and the goal of having large scale search and discovery (rather than the hashtag style of discovery that ActivityPub favors).
