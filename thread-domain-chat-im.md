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
# discuss-sms-usecases
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 
  # discuss-sms/sim 📱
  - tips
    - 部分实体卡/esim需要每年在当地一段时间，否则取消, 如giffgaff的封号
    - giffgaff封号后很多用户转向同在英国的voxi, 可能会增加后者的风控, 热门渠道都可能风控
    - 拿到号码别急着买套餐, 先测主流平台如google/telegram/paypal/whatsapp
    - 就算接码了， 也可能封号， 比如google会封禁反代的
    - telegram注册可能收费, 可能接不到其他设备的验证码

  - sim-usecases
    - google, google voice
    - telegram, whatsapp, tiktok, instagram, line
    - paypal, banking
    - alipay
    - wechat

  - sim
    - 激活限制
    - 保号条件
    - esim的条件: skinny优先封号esim, 实体卡封号较少

  - wifi-calling
    - Wi-Fi calling requires both the phone AND your carrier to support it — and specifically, the carrier must support it for your exact device model. 
    - Wi-Fi Calling works in Airplane Mode, as long as you manually turn Wi-Fi back on after enabling Airplane Mode.

  - skinny
    - 刚拿到了 skinny 的卡，在注册 wa 的时候能输手机号，但收不到短信验证码，来电也没有，试了几次就给我弹窗限制了，难受  

  - ## 

  - ## 

  - ## 

  - ## 

  - ## [【问】想注册个美区paypal, 是必须用美国号码注册吗？ _202505](https://www.nodeseek.com/post-342153-1)
  - 用虚拟号码也可以 talkatone gv号 维基百科捐一刀 付款方式选者PayPal 然后在这里面注册 

  - 美国PayPal必须要 美国手机号
  - 手机号不难，关键是怎么过验证不然封号

  - 23年末就用+86注册了美国PP, 现在就要+1才能了

  - ## 📌 [各个国家手机号可以注册的服务（留档） _202607](https://www.nodeseek.com/post-823695-1)
    - 下面都是自己实际注册过的，把下面当作一个备忘录，每买1个手机号就按照顺序看看自己想要注册哪个。

  - GV 我就支持注册PayPal 美区是上个月注册的，我还注册了微信呢

  - ## [请问美区的 AppleID 账号下载的国际版微信能正常使用小程序功能么？谢谢。 - V2EX _202205](https://www.v2ex.com/t/856132)
  - 微信安装包无论 iOS 还是 Android ，都不区分国内版和国际版，它是根据当前账户绑定的手机号来区分服务类型的。大陆+86 手机号注册以后服务是“微信”，非+86 号码注册以后服务叫“WeChat”，二者主要是运营实体不同。如果你用国内+86 手机号注册以后，手动换绑了国外手机号，它也会提醒你微信服务将会迁移至“WeChat”。

  回到楼主的问题，美区 App Store 下载的微信能不能使用微信内的 xxxxx 服务，主要取决于登录的微信绑定的是国内手机号还是国外手机号，以及微信官方的运营策略，和下载渠道没有关系。

  小程序应该都可以使用，之前有说 WeChat 因为无法使用人脸识别，所以不能注册健康码，后来取消这个限制了。

  - appstore 不能根据地区提交不同得包。想要限制一般根据手机号 ip 啥得

  - [关于微信和 wechat 共存的问题 - V2EX _202209](https://v2ex.com/t/877965)
  - 微信跟 wechat 是一个软件，不同国家 /地区的号登录会显示不同的名字，+86 进去就是微信，非+86 进去就是 WeChat ，协议也会跟着变化，互不影响
  - IOS 的客户端都一样，安卓的要注意，Google Play 下载的 WeChat ，国内一众市场下载的是微信，你在 Google Play 下载安装好之后如果被国内的应用商店自动更新一次就会变成微信（中过招），建议将 WeChat 的自动更新永久屏蔽。

  如果你的账号是微信，那么这两个客户端没区别。

  如果你的账号是 WeChat ，那么在微信客户端中，你点击任何服务都会提醒你即将使用的是微信服务，同意协议才能用，比如视频号、更换铃声、打开公众号等等。

  如果你的账号是 WeChat ，那么在 WeChat 客户端中，大多数服务都不需要同意微信协议就直接能用，只有少数比如视频号需要同意协议才能用。

  注意一点，港澳台手机号注册的 WeChat 账号才能使用健康码

  - 

  - ## [记录一下从新西兰🇳🇿带回来的SIM卡 _202604](https://www.nodeseek.com/post-679834-1)
  - 后一共带回来13张，覆盖新西兰四家运营商：
  One NZ：4张实体SIM + 1张eSIM
  Skinny：4张实体SIM（走Spark网络）
  Spark：2张实体SIM + 1张eSIM
  2degrees：1张实体SIM
  这里要特别说一下Spark的坑。Skinny、One NZ、2degrees的卡带回国后都能正常注册网络、接收短信，唯独Spark的卡回国后直接显示"仅限紧急呼叫"，手动选网也注册不上。 最后通过WhatsApp联系Spark客服，客服在后台做了一次network refresh（网络刷新），然后才恢复正常。两张Spark卡都是同样的问题，都需要客服手动刷新才行。
  SIM卡需要在新西兰境内首次激活（插卡拨打运营商客服号），没法回国再激活，所以人在新西兰的时候记得把要用的卡都激活了。
  新西兰SIM卡实名要求很宽松，买的时候不需要护照，激活也很方便。
  如果有去新西兰的计划，路过超市顺手买几张就行，成本极低。

  - 激活都需要实名吗？
    - 不用，转esim需要

  - 这四家好像只有skinny不支持Apple esim转移

  - ONE NZ的二维码还支持复扫好像
    - 是的

  - ## [想用whatsapp接码codex，能否用+86注册whatsapp - LINUX DO _202606](https://linux.do/t/topic/2386780/3)
  - +86 手机号可以注册 whatsapp，但是 OAI 不会给你的 + 86 发验证码

  - +86 的号码 openai 不认，接码是先判断电话号码，再判断要不要发到 whatsapp 的，注册了 whatsapp 也没用

  - 可以先去买个虚拟号再注册 whatsapp，也能长期使用的，不过要是账号丢了手机重置了之类的就不行了

  - 我目前没有遇到 whatsapp 需要二次验证的问题，最稳妥的还是自己有一张外卡。

  - ## [Helium Mobile 免费 Zero Plan 灵车全部坠机 - 运营商 奶昔论坛 _202605](https://forum.naixi.net/thread-12090-1-1.html)
    - 刚收到官方的“死亡通知书”，Helium Mobile 那个 $0/月的 Zero Plan 免费白嫖灵车，终于宣布翻车了！
    - 官方邮件写得挺客气，说什么“不可持续”、“为了提升付费用户体验”，懂的都懂，就是地主家没余粮了，准备开始大规模拔网线割韭菜。6月11号正式到站卸客。
    - 官方最恶心的一招：如果你在 6月11号 之前装死不理它，系统会自动把你强制升级到 $15/月 的 Air 套餐！
    - 之前随便绑了张卡上车的老哥，赶紧去App里解绑或者直接注销套餐。不然下个月账单出来莫名其妙被扣十几刀，直接变成纯种大冤种。

  - 就是收集完你的个人位置及信息了，现在想收割你们的钱包了，两手都要抓全都要

  - ## [Helium 免费美国 eSIM 更改 ToS 需要每个月在美国使用流量 _202510](https://www.nodeseek.com/post-467290-1)
    - Helium Mobile currently offers the Zero Plan free of charge, inclusive of taxes and fees. The Zero Plan includes 3 gigabytes (“GB”) of cellular data, 100 minutes of voice calls, and 300 SMS text messages (sent and received) per billing cycle. Additional data, voice, and text capacity can be purchased for $7.50 per GB via the “Add Ons” section of the Helium Mobile App. Unless purchasing Add Ons, no credit card is required for the Zero Plan.
    - All Zero Plan subscribers must actively use cellular data each billing cycle (within 30 days). Failure to do so will result in termination of Zero Plan at the end of the current billing period. Zero Plan subscribers must show consistent active use of the cellular network to be eligible to earn and redeem Cloud Points.

  - ## [GiffGaff电话卡替换之skinny nz和one nz哪个更好呢 - LINUX DO _202607](https://linux.do/t/topic/2674772)
  有使用过新西兰 skinny nz 和 one nz 卡的佬友吗，可否谈谈实际体验

  我目前只知道，

  保号的话，skinny nz 是 5NZD 一年，one nz 是 10NZD 一年，购买的话，我目前找到的是 skinny 110 元代购加激活；one 卡是 150 元（没有推广，不放链接）

  skinny 要在新西兰激活，而 one 卡似乎可以在国内激活？

  他们两者接 openai 的码是直接接还是 whatsapp？？

  不限于以上问题，有使用过的佬可以随意分享

  - 不如德国沃达丰和 O2，前提是愿意视频 kyc
  - 德国沃达丰和 O2 需要护照，实名 KYC，拦截不少佬友

  - 卖卡的话，不用搞这么含蓄。如果只是为了 openai 接码，我来给一个焚诀，去办菲律宾或印尼的 esim 就好，注册个 whatsapp，接码稳得很，保号成本极低。

  搞新西兰这种贵的，除非是有更广泛的接码需求，看重号码权重。只为了 chatgpt 不值得。

  - 直接携号转网到英国运营商得了，英国一堆保号便宜的。指望厂商不封没有意义，以后封不封谁知道，英国厂商多，被封了携号转网方便，保号也便宜

  确实，不用实名也是优点，而且英国那些都是本地人用的卡，什么旅游卡之类的不能比

  - ## [求教关于短信模块的知识，希望支持 skinny 卡等接收短信 - V2EX _202402](https://fast.v2ex.com/t/1013285)
    - 买了张卡注册 app 用，不想带两个手机。如果手机通过转发 app 的方式，就要求手机长期充电开机，有点安全风险，所以，打算找一个支持接受短信的模块，自己开发个接收短信，转发。 哪位朋友知道有没有类似的模块，给个型号，或者有其他能长期开机接收短信的方案也行。
  - 合宙的 Air724UG 、Air780E 、Air700E ，很小巧，很好用，我的已经稳定运行半年多了
    - 你说的这个 skinny 卡不知道能不能用，Air724UG 可以全网通，其他两个只支持移动卡

  - ## [关于香港开卡，手机号可以填写 GV， paygo， giffgaff， skinny 等非大陆、香港的手机号吗？ - V2EX _202408](https://fast.v2ex.com/t/1064115)
    - 鉴于最近看到很多人说，+86 手机号接到香港的电话后，会引来反诈电话，民警上门等服务。 那么使用非大陆手机号可以作为银行的联系方式吗？

  1. 最好用大陆的手机卡，因为香港银行打电话过来你要是用别的地方电话卡可能借不到电话，银行可能会拒绝你的信用卡等开户申请，有的银行开户需要二次电话确认的
  2. 银行卡可以看看 中银香港和汇丰银行 

  - 当然可以啊，不过那种不需要香港身份证的预付卡，就 MySIM/ClubSIM 之类的，是有有效期的，到期需要再买新的卡号
    - clubsim 到期前一个月买个 6 元短信套餐就行

  - 坐标上海，目前全用的+86 ，经常和+852 打电话，没有反诈打给我。

  建议别用+1 作为银行预留，因为 US 税务身份对银行来说是比较敏感的。

  部分银行（例如 HSBC 、信银）建议用+852 预留，因为你可以把它绑定到云闪付海外版

  - 手机号对于银行卡来说很重要，不建议用 GV 、gg 这些卡，万一号被禁了很麻烦。用 +86 没接到过反诈

  开港卡、海外卡在 V2 都是日经贴了，我把各银行开户需要的教程总结在一起，部署了个网站：提供详细的境外银行开户、港美股开户、境外电话卡、境外收付款、出入金等教程，一起探索数字居民之路

  - 最好是填写国内+86 手机号，因为之前有小伙伴去 HK 开户，填写的非大陆手机号，结果工作人员问他原因。银行开户不要给自己找不必要的麻烦。一个是可能要求你提供更多资料，二个可能影响审核。

  - HSBC 我当时+86 手机号在 HK 一直收不到验证码就换+852 （ clubsim 卡）的了，一段时间后申请蓝狮子卡平邮到广州一直没收到，我猜测是因为手机号问题，后面改成+86 就收到平邮了。关于反诈，我联通手机号直接把汇丰电话拦截了，导致我一直没接听到来电，是我后面去联通 app 拦截电话记录里看才发现的。总结留+86 比较方便

  - 看地区和你的卡吧，汇丰可能会隔一段时间打电话来确认你的信息和你开户是不是吻合，大概 10 分钟的通话，你确定你买的卡接电话不贵就行，我本人是广州联通+86 是没事的，估计老号原因非常稳固，登 tg / 接美国亚马逊 aws 电话和汇丰香港电话，和香港朋友通话都没有引起什么后果，

  - BOC. HK 实测填了 +852 号码，被要求改回 +86 ，理由是非长居香港/在港工作。

  - ## [google voice 能验证 codex 吗 - V2EX _202607](https://www.v2ex.com/t/1225212)
    - 纯虚拟无实体卡的 google voice

  - 不能

  建议整个 giffgaff 的卡，买张实体现成的现在市价在 70 人民币左右，自己想办法注册一个 eSIM 的话就是买张白卡的成本，不到 20 人民币（首次充值 giffgaff 的 10 英镑是免不了的）

  - 正常虚拟卡都会禁用

  - gv 和 hahasim 都过不了验证，gv 提示不支持虚拟号码，haha 提示所在地区不受支持（好像是这个）

  - ## [没忍住办理了一张美esim卡 -- 很坑 _202502](https://www.nodeseek.com/post-261419-1)
    - 注册了paypal，但注册不了GV，TG显示号码被ban，还能注册啥？

  - ## [大佬们：google voice 能转成 esim 吗 _202504](https://www.nodeseek.com/post-315877-1)
  - 不能，只能把gv号转sim，买一张tmo的esim，然后把gv号转到tmo。
  - 要把gv转去运营商，例如转去tmobile

  - 先转实体sim，然后再esim

  - gv转esim得绕路，我上次是先转tmo实体卡再换的esim

  - ## 📌 [热门境外实体卡与 eSIM 选卡指南 _202607](https://www.nodeseek.com/post-844896-1)
  一、 低成本长期保号卡（收码/养号首选）
  香港 hahaSIM（仅实体卡）
  资费/规则：3HK 旗下品牌，每年充值 10 HKD 即可自动延长 1 年有效期。
  亮点：支持购买低价漫游流量包，可正常拨打电话与收发短信。
  短板：近期 3HK 在内地漫游时网络偶尔存在稳定性波动。
  香港 ClubSIM（支持 eSIM）
  资费/规则：香港主流保号卡之一，每年购买一次最低 6 HKD 的本地或漫游服务包即可维持卡片活跃。
  亮点：保号成本极低，支持 eSIM，在内地接收短信完全免费，适合绑定各类境外账号。
  短板：内地漫游时主要用于收验证码或数据上网，基础通话受限。
  菲律宾 Globe（支持 eSIM）
  资费/规则：+63 东南亚号码，每半年充值 15 PHP（约 RMB 2元）即可延长有效期，可直接在官方 App 内开通 eSIM。
  亮点：保号门槛极低，适合有东南亚业务或特定账号注册需求的用户。
  短板：部分国际平台对东南亚号段的风控系数较高。
  * 美国 Ultra Mobile PayGo（支持 eSIM）
  资费/规则：+1 原生美国号码，月租为 3 USD（约 RMB 21元）。
  亮点：账号权重高，完美契合对美国原生号码有强需求（如美区金融、特定服务注册）的用户。
  短板：相比其他地区卡种，长期持有成本稍高。
  荷兰沃达丰（Vodafone NL）（eSIM）

  二、 高速直连流量卡（免FQ直连）
  澳门 CTM（需实名 / 支持 eSIM）
  亮点：内地漫游体验梯队顶尖，支持中国移动与中国联通双 5G 接入，网速可冲破 1Gbps，稳定性极佳。
  短板：无优惠活动时整体资费偏高，适合对网速和网络质量有极致追求的使用者。
  中国电信澳门蓝卡（需实名 / 仅实体卡）
  亮点：主打流量永不过期。内地漫游走中国电信网络，延迟极低；支持内地主流支付方式直接充值，保号成本亲民。
  短板：实名认证审核较为严格，且不支持 eSIM。
  香港 3HK DIY（无需强制实名 / 支持 eSIM）
  亮点：性价比大流量代表，常见套餐如 268 HKD 包 45GB 中港澳三地共享流量。支持内地支付工具付款，开卡便捷。
  短板：近期漫游线路偶有不稳定情况。
  中国电信香港蓝卡（无需强制实名 / 仅实体卡）
  亮点：资费模式延续澳门蓝卡逻辑，但分配香港 IP 与 +852 号码。网络延迟低，且随卡附赠通话分钟数。
  短板：综合表现均衡，暂无明显短板，仅是不支持 eSIM。
  马来西亚 Celcom（预付卡）
  亮点：提供大流量及包月无限流量套餐，内地漫游支持移动/联通 5G，性价比突出。
  短板：需注意长期在非本土环境漫游可能会触发运营商的漫游时长限制。
  英国 CMLink UK（无需强制实名 / 支持 eSIM）

  三、 低成本通话卡
  如果身处内地有频繁拨打/接听境外电话的需求，中国电信澳门蓝卡 与 中国电信香港蓝卡 是目前境外预付卡中资费最划算的选择，内地漫游拨打电话折合每分钟仅需 0.38 - 0.78 当地货币。

  - 德国O2 德国Vodafone 荷兰Vodafone

  - Globe那个6块钱保号倒是真便宜，就是有些平台看到+63直接拒，注册tg都费劲。

  - 这个信息应该是24年的 因为我看过和这个一样的sim卡排版评测

  - 沃达丰德国已经不支持自助认证了 只能线下或者视频

  荷兰simyo转账最低10欧起

  - ## 📌 [eSIM 折腾留存记+一点补充心得 _202606](https://www.nodeseek.com/post-783926-1)
    - 还需要考虑地区的不可替代：美区 PP 就必须要美国手机卡，港区支付宝就必须要香港手机号，包括维护港卡也是刚需。

  Tello　T-Mobile · ❌
  互联网小公司，当时不知道它的风控那么厉害，5 刀 / 月不要 KYC，尝试 wificalling 以及修改 911 地址好多次才成功，结果不久就被封禁，好在联系客服后都可以退款，转而放弃持有。

  Redpocket（红包卡）　AT&T · ✅
  AT&T、T-Mobile、Verizon 御三家网络任选，但好像合适我们的只有 AT&T。免 KYC，最低 30 美元 / 年，自带全球漫游 100 分钟通话、100 条短信，以及 1G 美国住宅 IP 流量。

  Redpocket 对非原生 eSIM 套卡的风控也很严格，不过这次我选择实体卡，使用感受非常完美。

  注册 Telegram / Gmail / Instagram / WhatsApp / 美区 PayPal 等非常丝滑，每个月自带的 1G 流量有奇效
  365 天到期续费即可保号，eBay 买充值码就行
  Ultra Mobile 紫卡　T-Mobile · ❌
  在弄到红包卡之前踩的坑，据说公司被收购，所以尽管是实体卡依旧难逃被封。3 刀 / 月，免 KYC。

  要注意一下，美国手机卡对非原生支持esim的套卡很敏感，目前仅有少量牌子能稳定写入不封号

  giffgaff　🇬🇧 · ❌
  大热门，免 KYC，介绍和攻略很多不赘述。当时实体卡转 eSIM 可以用抓包方式拿到编码，现在不知道咋回事。中规中矩，注册软件时不好用，考虑到价格因素也就释然了，要啥自行车。180 天消费保号。
  2026.7.28更新
  最近大规模坠机，GG已经被彻底薅坏

  voxi　🇬🇧 · ❌
  免 KYC，跟 gg 卡差不多，被白嫖得挺狠。

  ⚠️ 重要补充：以前的 voxi 联网删除就会自动发新二维码，目前用第三方套卡的小伙伴切莫随意删除，它不会再发二维码，只能联系客服直接绑定原生支持 eSIM 的手机设备。
  2026.7.28更新：使用三方套卡不慎删除后，无法收到新二维码短信

  CTExcel　🇬🇧 · 🔹
  中国电信英国分公司产品，常年在小红书推广，有微信客服，官网套餐比较多。原则上需在英国基站激活才能在国内使用，实际可以偷渡开通使用。我选的是 50G / 年的回国年套餐，英国当地主流网络，完全可以当英国住宅 IP 流量使用，直接漫游不过墙。需 KYC，90 天消费保号。

  换设备3英镑

  Vodafone de　🇩🇪 · ✅
  沃达丰德国分公司产品，注册极其复杂，需要 KYC 签订合同，但比想象中好用很多，注册丝滑，漫游信号稳定，收发短信非常高效。90 天消费保号。

  换设备联通删除 扫注册邮件中的原始二维码即可

  esimgg　🇪🇪 · ❌
  爱沙尼亚号码，不需要 KYC，低价王者，但注册不好用，单纯接码还行吧。联网即可保号。

  Vodafone nl　🇳🇱 · ✅
  不要 KYC，基本没用它，吃灰状态。最初可以转账 0.01 充值，后来隐藏入口。

  建议不要去找那个入口，wise 转过去的 0.01 那边是人工入账，猜测有一定风险。
  最新使用体验还是很不错的，不愧是沃达丰。

  club esim　🇭🇰 · ✅
  香港保号热门神卡，不用多说，需要 KYC，365 消费保号。
  7月3日更新：6元短信包下架，保号成本来到15

  ⚠️ 这卡有一点要注意：每年只能网络自助补卡一次，再想补需要人肉进港。

  CTM　🇲🇴 · 🔸
  需要线下到澳门购买 KYC 激活，5G 漫游流量，不够还可以续费，澳门 IP 看 YouTube 没广告，用不完的流量可以留存。180 天充值保号。

  globe　🇵🇭 · 🔸
  菲律宾最大运营商，需要 KYC，但早期极不严谨，拍个猴子斑马什么的也能过，现在新卡审核严格了一些，而且容易出 bug。适合开通 GCash 和 Maya，可以绑定菲区苹果 ID，支付例如 ChatGPT 等，享受菲区低价汇率。最新体验极差，globe one 的 OTA 码都难以接到。365 充值保号。

  one nz　🇳🇿 · ✅
  新西兰沃达丰的前妻，当地第二大运营商，不需要 KYC，注册软件极其好用，纵享丝滑，甚至可以支付宝生活缴费充值。365 充值保号。

  号码质量（重点）
  别只看价格和"能不能收码"。手机号不像 IP 有公开的黑名单 / ASN / 机房识别那套体系，普通人看不到号码的综合质量分。号好不好用，取决于平台怎么看它：运营商、地区、号段历史、是否易批量获取、有没有被拿去营销 / 诈骗。

  几类坑：

  免 KYC、可批量、低成本的号：你觉得香，工作室更觉得香，薅烂后被风控盯上，普通人再用就很难受。
  野鸡卡：国家 / 运营商权重天然偏低，更容易受号段滥用波及。
  回收号：可能是带封号 / 风控历史的"背锅号"。会有各种各样的问题，比如提示已注册、收不到码、无法换绑、注册成功秒风控等。
  冷知识：+86 三大运营商权重其实挺高，挺好用，只是大家折腾海外号是有别的需求。

  价格重要，但绑重要账号时稳定性更重要。

  重要账号（ChatGPT、Apple ID、Gmail、TG、WhatsApp、LINE、PayPal、X）：选主流国家 / 运营商、保号规则清楚、迁移明确的号，贵点无所谓，别突然失联。
  小号 / 测试：便宜卡，丢了无所谓。
  野鸡卡：别绑重要账号，拿来应付野鸡商家、临时平台正好。

  - 有关于港卡club esim 6hkd 短信包保号再补充一下 这个套餐貌似只能在港内地使用 只能拿来保号

  hahasim每年最少可充值10hkd 但这个是充值到余额的 可消费 其余的就没什么了

  - 设备支持的话 可以直接买esim
  我真后悔买了这个破xesim 如果是estk就直接用，转运实体卡老费劲了

  - globe拉完了 收不到短信, 登录app 都没办法登录

  - 几天前买了esimgg的爱沙尼亚卡，拿来接码有时候都接不到，真是拉完了

  - ## 📌 [海外手机卡大汇总，低成本保号神器（验证码、账号绑定必备） - 运营商 奶昔论坛 _202601](https://forum.naixi.net/thread-9305-1-1.html)
  1. 美国卡（兼容性强，适合美区服务如ChatGPT）
  Ultra Mobile PayGo/Purple Card

  优势：真实号段，接收验证码无敌（X、TG、Google等）；月租3美元（约21元），包含基本通话/短信；Wi-Fi Calling免费。

  成本：购卡100-200元，月租3\r\n（可隔月充值保号）。

  保号：自动续费信用卡绑定，避免冻结。

  获取：淘宝搜“紫卡”，官网激活。

  缺点：月租稍高，但稳定。

  Tello

  优势：支持eSIM，月租5美元（约35元），适合美区注册；实体卡也行。

  成本：官网购eSIM免费，实体250元；年保号约420元。

  保号：月租自动。

  获取：官网或淘宝。

  Redpocket/T-Mobile

  优势：零月租，纯短信稳定。

  成本：购卡低，保号需偶尔使用。

  保号：半年使用一次。

  Helium Mobile

  优势：完全免费美国号，App下载，支持短信；兼容性高，无需实名。

  成本：0元（邀请码如MWBGPQX）。

  保号：连接基站自动续。

  获取：App免费申请。

  缺点：可能需梯子。

  2. 英国卡（零月租王者，超长保号）
  Giffgaff

  优势：零月租，免费收短信；英国O2旗下，稳定接码；一次充值可用20年。

  成本：购卡50-80元，初始10磅+赠5磅（约100元）；年保号0.6磅（约6元）。 保号：每180天发条短信（0.3磅/条）或充值。

  获取：咸鱼/淘宝买空卡激活（官网关国内通道）。

  缺点：最近有封号反馈，建议备用。

  3. 新西兰卡（零成本保号，性价比高）
  Skinny

  优势：零月租，无需实名；第一年无需充值，支持国内信用卡；纯短信稳定。

  成本：购卡150元，年保号5新元（约25元）或互转0成本。

  保号：每年充值5元或活动送通话。

  获取：淘宝买实体卡，本地激活更便宜。

  缺点：无eSIM，收不到某些码如WhatsApp。

  4. 香港/澳门卡（近距离，便利，部分原生IP）
  CSL

  优势：激活简单，接收短信免费；支持中文APP；附711兑换券。

  成本：购卡58港币（含28余额），年保号6港币（约5元）。

  保号：买大陆澳门流量套餐（6港币/年）。

  获取：香港711买，APP激活。

  My3 (3HK)

  优势：包年45G流量+原生IP，无需大陆实名；港澳实名可用。 成本：268港币/年（约240元）。 保号：包年自动。 获取：官网或淘宝。

  Club Sim

  优势：零月租，纯短信。

  成本：低，但反馈收不到TG/Google码。

  保号：偶尔使用。

  缺点：兼容性差，避免。

  中国电信香港Easy+

  优势：月租90港币，附内地号；省心。

  成本：月90港币（约80元）。

  保号：月租。

  获取：官网。

  5. 欧洲卡（eSIM友好，低成本）
  沃丰达 (Vodafone DE)

  优势：预付费，无月租；eSIM，支持全球验证码。

  成本：购eSIM低，年保号0.01欧元/季度（约0.07元）。

  保号：季度最低充值。

  获取：官网+ Xesim桥接（国行iPhone需）。

  爱沙尼亚卡

  优势：365天，无月租；5分钟激活。

  成本：40元一次搞定。

  保号：永久。

  获取：实体eSIM+教程。

  Simyo.nl(荷兰)

  优势：0月租，免实名。

  成本：5欧元购买（约40元）。

  保号：半年发短信或缴费。

  获取：官网。

  6. 其他亚洲/太平洋卡
  马来西亚Celcom Life
  其他网站看到的拿过来分享

  海外手机卡大汇总：X上博主亲测推荐，低成本保号神器（验证码、账号绑定必备）

  最近在X上看到很多博主分享海外手机卡的经验，尤其是用于接收验证码、绑定X/TG/ChatGPT账号、降低封号风险的低成本方案。作为AI创作者或出海用户，一个稳定海外号能省不少心。

  一、全部海外手机卡汇总大全
  1. 美国卡（兼容性强，适合美区服务如ChatGPT）
  Ultra Mobile PayGo/Purple Card

  优势：真实号段，接收验证码无敌（X、TG、Google等）；月租3美元（约21元），包含基本通话/短信；Wi-Fi Calling免费。

  成本：购卡100-200元，月租3\r\n（可隔月充值保号）。

  保号：自动续费信用卡绑定，避免冻结。

  获取：淘宝搜“紫卡”，官网激活。

  缺点：月租稍高，但稳定。

  Tello

  优势：支持eSIM，月租5美元（约35元），适合美区注册；实体卡也行。

  成本：官网购eSIM免费，实体250元；年保号约420元。

  保号：月租自动。

  获取：官网或淘宝。

  Redpocket/T-Mobile

  优势：零月租，纯短信稳定。

  成本：购卡低，保号需偶尔使用。

  保号：半年使用一次。

  Helium Mobile

  优势：完全免费美国号，App下载，支持短信；兼容性高，无需实名。

  成本：0元（邀请码如MWBGPQX）。

  保号：连接基站自动续。

  获取：App免费申请。

  缺点：可能需梯子。

  2. 英国卡（零月租王者，超长保号）
  Giffgaff

  优势：零月租，免费收短信；英国O2旗下，稳定接码；一次充值可用20年。

  成本：购卡50-80元，初始10磅+赠5磅（约100元）；年保号0.6磅（约6元）。 保号：每180天发条短信（0.3磅/条）或充值。

  获取：咸鱼/淘宝买空卡激活（官网关国内通道）。

  缺点：最近有封号反馈，建议备用。

  3. 新西兰卡（零成本保号，性价比高）
  Skinny

  优势：零月租，无需实名；第一年无需充值，支持国内信用卡；纯短信稳定。

  成本：购卡150元，年保号5新元（约25元）或互转0成本。

  保号：每年充值5元或活动送通话。

  获取：淘宝买实体卡，本地激活更便宜。

  缺点：无eSIM，收不到某些码如WhatsApp。

  4. 香港/澳门卡（近距离，便利，部分原生IP）
  CSL

  优势：激活简单，接收短信免费；支持中文APP；附711兑换券。

  成本：购卡58港币（含28余额），年保号6港币（约5元）。

  保号：买大陆澳门流量套餐（6港币/年）。

  获取：香港711买，APP激活。

  My3 (3HK)

  优势：包年45G流量+原生IP，无需大陆实名；港澳实名可用。 成本：268港币/年（约240元）。 保号：包年自动。 获取：官网或淘宝。

  Club Sim

  优势：零月租，纯短信。

  成本：低，但反馈收不到TG/Google码。

  保号：偶尔使用。

  缺点：兼容性差，避免。

  中国电信香港Easy+

  优势：月租90港币，附内地号；省心。

  成本：月90港币（约80元）。

  保号：月租。

  获取：官网。

  5. 欧洲卡（eSIM友好，低成本）
  沃丰达 (Vodafone DE)

  优势：预付费，无月租；eSIM，支持全球验证码。

  成本：购eSIM低，年保号0.01欧元/季度（约0.07元）。

  保号：季度最低充值。

  获取：官网+ Xesim桥接（国行iPhone需）。

  爱沙尼亚卡

  优势：365天，无月租；5分钟激活。

  成本：40元一次搞定。

  保号：永久。

  获取：实体eSIM+教程。

  Simyo.nl(荷兰)

  优势：0月租，免实名。

  成本：5欧元购买（约40元）。

  保号：半年发短信或缴费。

  获取：官网。

  6. 其他亚洲/太平洋卡
  马来西亚Celcom Life

  优势：每天3G原生流量，超稳如梯子；适合高强度使用。 成

  本：购卡150元，月148马币（约250元）。

  保号：月租。

  获取：淘宝。

  日本Povo/SoftBank

  优势：免费或低成本，游客友好；回国漫游收短信。

  成本：Povo免费（需日本身份），Osaka eSIM 370日元/3天无限。

  保号：半年试用。

  缺点：需在日激活。

  Nomad亚太eSIM

  优势：短期流量，无号码；中国可用。

  成本：低，短期plan。

  保号：无（非长期）。

  ESTK（Lite/Plus/Max版）

  优势：自带Bootstrap流量，无WiFi也能激活/写入；界面详尽，固件优化中；颜值高，功能强大。

  成本：13-26美元（升级版），Max版200港币。

  容量：4-60张（视版本）。

  写卡器：官网套餐带读卡器，支持iOS/安卓批量写入/备份；极客爱用。

  获取：官网 https://store.estk.me/ ，9折码YUZONG。

  缺点：iOS操作偶卡顿，偏极客风格；低价版库存少。

  通用Tips
  写卡器通用：USB/蓝牙类型，15-20美元；用于导入eSIM，避免机型限制；纯iOS选内置款。

  亲测：Xesim和esimfan最常用，前者丝滑后者实惠。

  兼容：测试机型（如iPhone 15 Pro），三星/小米有坑；多备安卓机。

  用途：结合海外eSIM（如沃丰达）收码，防封号。

  - helium不是政策变了吗

  - ## [32元永久使用爱沙尼亚esim（乌龟）卡，并写入到实体sim卡 _202507](https://www.nodeseek.com/post-392871-1)
  - 最近因为注册某些app需要用到海外的电话号码，目前海外大部分国家都支持esim，且部分国家的电话号码并不需要实名（上传护照等信息），但国内大部分手机都是不支持esim的，所以还需要把esim写入到实体sim卡，这里我就选择了爱沙尼亚的esim.gg卡（俗称乌龟卡），3.8欧（32元）即可永久使用，不用实名且可以免费收短信。
  - 前排提示，国内的esim标准和国际不一样，所以国内手机/设备是无法写入海外esim，同样，海外手机也无法写入国内esim，ara-m（证书）不一样
    - esim.gg俗称乌龟卡，他们家主要是爱沙尼亚的esim卡，其他地区的也有，但是太贵了，这个爱沙尼亚（区号为+372）的最便宜。
    - 说下具体资费，一次性购买费用3.5欧，然后最低需要充值0.38，合计一次性支付3.8欧，相当于32rmb。为什么说是永久使用呢，因为除此之外就没有套餐费，收短信免费，在国内接听电话也免费，只要自己不发短信不开流量，当个接收短信的号码完全0额外成本。
    - 他这个保号规则也很简单，只要1年只能连接上一次基站，就可以延长1年使用期（或者余额有变动也可以延长1年），所以平常接收完验证码，直接拔卡就行，一年内连上一次基站，实现0额外成本一直使用。
    - 只充值0.3欧所以可选的免费号码比较少（嗯靓号也是要收费的），最后支付宝完成支付，这个非常贴心，直接用支付宝就行。
    - 支付完成后就可以下卡了，自己账户里面就会出现这个号码，选择install esim，就会出现二维码，此时用支持esim的手机扫描就可以下卡了，如果自己手机不支持esim，就需要写入到实体sim卡。
  - 所谓的写入实体sim卡，是自己购买euicc卡，然后通过软件或者读卡器把esim信息写入到euicc。
    - euicc就是一个能写入多个esim的实体卡，不同euicc卡片容量不同，能写入的数量也不同，一般都是500k，可以写20个esim（可以不同运营商），这样当你需要哪个卡的适合就直接切换到对应的esim，一个卡顶20个传统卡。
    - 可能大火有听说过5ber/9esim这种，其实都是euicc卡，只是前者有牌子，卖的非常贵，普通euicc卡俗称小白卡，即小作坊产品，质量不好说（有人写入一次就炸鸡），但是非常便宜，40不到就能拿下（500k容量）。需要注意的是，安卓目前写入和切卡（切换euicc内的esim信息）非常方便，但是苹果只能切卡，而且需要特定的euicc才支持，这类euicc也要贵几块钱，如果自己用苹果的建议买海外esim版的。
  - 这个能不能写入国内的esim，不行，因为国内国外esim标准不用，ara-m不兼容。ARA-M是eSIM Profile 的 Region/Type 标识符之一在 eSIM（嵌入式 SIM 卡）或 MNO（移动网络运营商）分发配置中，ARA-M 往往代表："Authorized Reporting Authority – Mobile"它用于标识 移动网络配置文件的授权来源，也可出现在 eSIM profile 或运营商域名（如 SM-DP+）中。写入esim信息的时候是需要验证ara-m的，如果不对是直接拒绝写入。但是国内ara-m签发是和国外不一样，这就导致国内的esim设备无法写入海外esim信息，反过来国外设备也无法写入国内esim，因为没对应ara-m，苹果也不例外，但好像海外版可以额外导入国内的ara-m。
    - 安卓写入需要用到一个叫做“easyeuicc”的app，这个自己谷歌下载，安装好后可以运行检测下，前三项能通过就没问题，基本上大部分手机都可以通过，我这好几年前的红米都可以，至于后面几项不用管。对了，有些手机只能sim卡1槽才支持写卡，卡2槽不行
  - 上面的检查没问题后就可以准备把euicc卡插到手机准备写卡，但是，我要说但是了，如果是小米手机，请务必关闭手机查找功能，这玩意会插入新的sim卡自动发短信，乌龟卡发一条就会扣0.24欧，给我气的，我一共就冲了0.3欧，一下子就被小米给花了0.24欧？？？？？？然后小米还会偷跑流量，我干，后面又给我跑了0.3k流量扣了0.0001欧，本来就不富裕的家庭更是雪上加霜。
    - 肯定是有人想拿这个上网，，，，怎么说呢，也能用，但是流量费肯定是贵。
  - 回到正题，插入euicc后，打开easyeuicc app，我这个是从没写入过esim，所以是空的，点击右下角的+号，扫描刚刚乌龟卡的esim二维码，确认写入的sim卡以及esim信息，就可以写卡了。
  - 安卓写卡完成后，可以直接通过easyeuicc app切卡，想要哪个启用哪个卡就行。
    - 至于苹果，可以通过stk切卡，也就是说，你可以安卓写卡后放到苹果里面用，要么就是买sim读卡器写卡。
  - 可以自己禁用乌龟卡的发送短信和通话功能，防止误操作扣费。

  - 接电话免费？
    - 看faq，在中国是免费（不是计费地区）

  - 不用怀疑，就是国人开的

  - 👷: 不用怀疑，我开的。为什么不是 ee 呢，因为 ee 被另一个经销商占了，不过他家卖更贵，而且主要面向乌克兰俄罗斯这块（他们有独占协议）。
    - travelsim.com / travelsim.lt / esimplus.me / esim.ee / popcorn.tel 和我这个其实都是一个上游，如果对方同意也可以转入，你要是有其他爱沙尼亚上台卡也有权转入（前两个本家的签字就会放行）。
    - 可以对比一下资费，我这边应该是最低的了，政策其实基本都一样，真的倒了 TravelSIM 本家也可以接盘

  - 能接受谷歌验证码吗
    - 看faq今年3月谷歌就不给这个区号发验证码了

  - 小白卡有推荐的不
    - 淘宝pdd随便买，都差不多，只要用ara-m就行
  - 我这个就是小米啊，无esim，所以只能写到实体卡

  - ## [ONE NZ不适合长期使用, 这是真的吗，用过的人说一下 _202608](https://www.nodeseek.com/post-850103-1)
  - 都不支持长期漫游，就看人家管不管
  - tos这么写那就是真的，跟gg一样，管的时候就全杀了

  - ## [刚购买onenz, 国行手机可用吗？ _202609](https://www.nodeseek.com/post-913652-1)
  1. 国行iphone 可以wificalling吗？
  2. 没有wificalling可以收短信吗？
  3. 这个卡每年必须有消费记录，可发送一条短信解决？
  4. 每年需要最低充值10新币保号？

  5. 开启wifi calling有手就行
  6. 应该可以，漫游效果不错，我这甚至有5G信号
  7. 好像没说，充值应该就能保号，不过你要是真1年都用不着一次，直接抛了也不是不行
  8. 是，现在app最低充值就是10NZD

  - ## [新西兰的skinny or one 卡稳吗 _202609](https://www.nodeseek.com/post-871176-1)
    - 这2个卡稳吗，想入一张外面卖130

  - 不太行，skinny之前杀过漫游的，onenz可以国内激活感觉会泛滥

  - onenz我24年一月用到现在，可漫游，wificall很好拉

  - skinny esim要死了 实体卡不知道

  - ## [在giffgaff封禁长期漫游、Skinny封网的前提下，到底什么esim值得长期拥有 _202608](https://www.nodeseek.com/post-896178-1)
  最近在重新考虑海外号码的配置，目标很简单：低成本保号 + 收验证码 + 能长期漫游，基本没有通话需求。现在手上的号码比较杂，但反而越来越不知道该怎么组合了，想听听大家的建议。

  目前的情况：

  giffgaff

  刚开了没几个月就莫名其妙被无故封禁了。虽然最近论坛里似乎又有一些解封的消息，但经历过这次之后，心理上已经不太敢把它当长期主力了。

  Skinny

  刚刚又在论坛看到 Skinny 也开始掐网络，所以原本考虑的方案也不太敢继续上。

  esim.gg

  目前手里还有一个，但实际使用下来，有些验证码平台不发爱沙尼亚号码，所以感觉适用范围还是有限。

  Voxi UK

  目前还保留着一个，整体来说还是比较好用，但现在也会担心以后会不会出现类似 giffgaff 的情况，所以不太敢把鸡蛋全放在一个篮子里。

  香港 CSL + Hahasim

  这两个目前都有。个人感觉香港运营商应该不会像一些海外 MVNO 那样随意掐长期漫游，但也不太确定，想听听大家的实际使用情况。

  比较奇怪的是，这两个香港号码拿来注册 TG，都遇到了需要额外付短信费的情况，不知道是不是线路/节点的问题。其他国家的号码目前还没遇到这个情况。

  另外一个比较明显的问题是：香港号码对于一些 AI 服务不太友好。所以如果只留香港号码，感觉还是缺一个能注册 AI 服务的海外号码。

  Google Voice

  也有一个，但感觉比较尴尬——平时用不上，真正需要的时候又不一定好使，属于“有比没有强，但食之无味”的状态。

  所以现在比较纠结两个方向：

  方案 A：香港双持 + 一个支持 AI 的海外号码
  比如 CSL + Hahasim 负责长期低成本保号，再找一个成本比较低、支持 AI 注册的号码作为补充。

  优点是成本低，而且香港两个号可以互相做备份；缺点就是需要维护三个号码，而且那个支持 AI 的号码同样存在以后被封/掐漫游的风险。

  方案 B：直接上美国实体卡/正规美国号码
  稳定性和生态可能会更好，AI、TG、Google 等兼容性也比较省心。

  但问题就是：长期持有成本明显更高。
  我现在比较纠结的是： 既然主要需求只是保号 + 收验证码，没有通话需求，是不是没必要为了“一个全能号码”去承担美卡的长期成本？
  是不是更合理的思路是： 香港号码负责低成本长期保号，再单独找一个支持 AI 的号码作为功能号。
  大家如果有类似需求，尤其是长期在国内漫游、主要用于保号/收验证码、注册 TG / Google / AI 服务的，比较推荐什么组合？

  - 我的评价是 唯一稳定方法只有门槛 德国沃达丰 要护照 simyo nl 要IDEA支付 现在这两根本没有容易的方法用上 不过对于你 我觉得你可以去澳门开CTM 50mop半年 澳门号码还是干净一些的 尤其是禁止大陆云开后

  - 德国o2和沃达丰目前都要护照+视频认证，门槛比较高可以看看。

  - 最近也在研究这个，看了一圈，反正都有缺点，紫卡也有封号风险，tello又有点贵，T-mobile好像收垃圾短信也会扣费，等等

  - 区别不大，热门的好多人冲，然后低成本保号，厂商赚不到钱，最后就掀桌子。还有好多博主推荐的，也不说政策，很多都是只给本地人使用或者禁止长期漫游，我现在只招那种没写这种政策的，小众一点的，不用kyc的，多备几个。

  - one NZ 这卡的esim最开始2年不用保号，后面每年保号一次就行。我现在用第三年了注册都能收到验证码

  - 是的，就像前段时间我看油管疯狂推skinny，疯狂吹，都抢断货了，我还可惜没抢到，然后没几天都开始杀号了

  - ## [咨询一下用过onenz的老哥，skinny号码能转过去吗 - eSIM 奶昔论坛 _202608](https://forum.naixi.net/forum.php?mod=viewthread&tid=15139&highlight=skinny)
    - 我的skinny跟我的生日很接近，我还挺喜欢的，想问一下onenz能不能把号转过去，我找到一个卡商，价格也还能接受，就是想保留一下这个号码
  - 转esim要签证或者pr，开老版的onenz还可以开但不能转，新版的只能卡商激活后给你带回来
  - 转不了的，要证件
  - 人在国内不好办

  - [skinny能转移号码吗 - eSIM 奶昔论坛 _202608](https://forum.naixi.net/forum.php?mod=viewthread&tid=14978&highlight=skinny)
  - 按照官方要求必须护照和签证
  - 首先你转esim需要护照，这一步就给你卡死了

  - ## [skinny现在有什么渠道 _202606](https://www.nodeseek.com/post-784697-1)
  - 实体卡现在只能在新西兰激活
  eSIM有一段时间是可以在内地下单激活。但是eSIM是永远无法转移的，除非你在新西兰或者有新西兰的护照。有人拿新西兰签证也被拒了，必须到新西兰去才能转移。现在最新情况不清楚了。

  - 要我说esim不如实体卡，安装了就转移不了，实体卡好歹能拔下来换手机。
    - 优点就是可以通过增加余额保号，两张卡相互转一次，增加一年有效期，理论上永久免费保号。

  - ## [关于skinny _202608](https://www.nodeseek.com/post-882998-1)
    - 买了一张26年6月10日在新西兰激活的skinny实体卡，听说有一个规则是三个月不连新西兰本土基站就封禁，确有此事吗 
  - 没有的事，放心用（目前是）

  - 实体卡 新西兰本土激活目前没看到大规模封号的

  - 在ns发帖收，130r左右应该可以收到

  - ## [skinny实体卡陨落！白扔了100块 _202608](https://www.nodeseek.com/post-891065-1)
  - 早上发现没信号，一登陆官网，果然“Your Skinny SIM is currently blocked from accessing the network.”
  之前封esim的时候还在侥幸，感觉这波应该波及不到我，还是年轻了

  6月买的gg，7月被封，损失10英镑
  8月买的skinny，8月被封，损失100RMB

  - 如果一台手机激活了太多卡，就会被封。看你的卡是怎么来的，如果是买的卡商的，估计也是批量激活的

  - 检查了一下我的skinny还活着，不过我23年底买的，当时还可以国内激活
  之前skinny封过一波转esim的，现在封实体没看出有什么规律
  本来skinny不能转esim我都打算弃了，giffgaff封卡后我打算留着，看它能活多久

  - one nz依旧坚挺，本地激活后一直用wificalling

  - ## [请问skinny和GG卡的区别是啥, 能替代GG卡吗 _202607](https://www.nodeseek.com/post-846780-1)
  - skinny现在能买到的不稳，因为需要在本地激活，除非你买到去年24年9月之前激活的
  - Skinny去年还是前年砍了海外激活，如果以后滥用加剧，不排除和gg卡一个下场

  - ## [昨天skinny电话卡大规模封号 _202608](https://www.nodeseek.com/post-871657-1)
    - 最近受到giffgaff封号影响，到处找接力棒，上了skinny的车，以前流传3个月不连接基站就封杀，经TG群友和官方沟通，没有这回事，以为是谣传上车了，卖家用的VOWIFI激活的esim，还没稳定几天，油管突然冒出推skinny卡破解方法的视频，有天杀的二狗子看到，不做人事，故意去官方对线，举报，昨天开始SKINNY官方大规模封杀异地漫游的账号。

  - 根本就不会有稳定的卡这一说，尤其是跟你讲几块钱能保你几年甚至十几年的，根本就不可能。你在国内保号一张卡，电信一年都要60了，其他几家要96，凭什么认为国外的漫游还比你便宜

  - ## [skinny电话卡 _202608](https://www.nodeseek.com/post-864001-1)
    - 插上卡没信号怎么办，重启过了，飞行模式也开关过了，还是没信号，安卓手机，买的激活好的成品卡
    - 我的是显示没激活，客服说重新给我邮一张
  - 插卡一开始是没信号的，等个几分钟就有了。
  - 把自动那里改成中国移动（中国联通）然后等3分钟，收到skinny的短信，就表示正常了 

  - 是不是一个设备激活太多被风控了，运营商那边都能看到哪个imei的手机激活的，你想同一个手机激活几百个手机卡靠谱吗

  - 你可以去skinny官网上尝试激活一下这个卡号，我这个就是在网上查了显示未激活（可能激活了的就直接发验证码了？知道的老哥可以回复一下），我联系客户他说给我重发。

  - 今天到手的两张已激活实体卡都能正常收到短信

  - ## [skinny 如何激活？ _202608](https://www.nodeseek.com/post-850405-1)
  - skinny在前年就改为新西兰境内基站激活了
  - 只能新西兰蜂窝基站激活

  - esim用wificalling激活。
  sim本地基站激活

  - 可以wifi calling激活的，那些个在卖esim小白卡skinny的就是在大陆激活的
  - esim可以 国内激活 但是要手法 不清楚 哪些卡商咋弄的

  - ## 📌 [【中国玩家宝典】新西兰Skinny Sim卡详细介绍 _202604](https://www.nodeseek.com/post-696319-1)
    - [skinny 新西兰电话卡 · 常见问题与要点 ](https://faq.nbsn.co/#skinny)
    - [KakaSkinny ](https://kakaskinny.com/)
    - [2degrees 新西兰电话卡 · 常见问题与要点 ](https://faq.nbsn.co/#2degrees)
  - Skinny 是新西兰的一家实体运营商，属于新西兰电信（Spark）旗下的虚拟运营商，提供无月租费的手机卡，免费接收短信，保号费用低廉。
  零月租：日常使用无固定费用。
  免费接收短信：无需额外费用即可接收短信。
  Skinny 从 2024 年开始只能在新西兰激活，我们改卖 One NZ 很久了，直接买 One 就行，也是零月租。

  保号便宜：每年仅需充值一次，费用约为25元人民币，或通过互转1新西兰元实现0元保号。
  支持多平台注册：可用于注册 推特、Telegram、ChatGPT、TikTok、Google、Discord 和 WeChat 等平台。

  如何保号？
  充值保号：每年充值 5 新西兰元（约 25 元人民币），卡片有效期从充值日起延长 12 个月。
  互转保号：通过互转 1 新西兰元的方式实现 0 元保号。持有两个 Skinny 号码（或与朋友互转）即可来回转余额延期，无需额外充值。
  ==注意事项==：未激活的卡有效期为9年；激活后有效期为12个月，需要在到期前充值以延续使用。

  如何查看有效期？
  网站：登录后，在右下角查看。
  App：点击右上角小箭头，查看上次充值时间，加 12 个月即为有效期。

  如果忘记保号导致过期怎么办？
  30天内：可联系在线客服处理，可能较为繁琐，建议及时充值避免过期。
  超过30天：号码将被回收，无法找回。
  Skinny 的卡有效期为最后充值时间的后一年，在软件界面可以看到 Expiry Date。在这个有效期之前都可以正常使用。
  如果超过了这个有效期，最后有一个月的缓冲期，如果过期不超过一个月的话是可以重新激活。
  当过期后，你只能通过 Voucher code 方式加值激活，但是以前 topup 的网页已经停止服务了，所以首先需要购买 Skinny 的 Voucher code（可以使用 Visa 卡从 nz 的 gift card 网站购买的）

  Skinny 电话卡在国内能使用吗？
  在国内使用此卡为国际漫游，该卡主要适用于新西兰旅游或留学等目的。
  支持哪些手机？
  除锁卡手机外，其他正常手机均支持。Skinny SIM 卡支持所有尺寸的 SIM 卡槽。

  Skinny 卡从 2024 年 9 月 11 日起，需要在新西兰境内激活。经过测试，==在新西兰之外（比如在中国）无法激活==，无法激活只能接收部分短信，大部分功能无法使用。
  目前 Skinny 支持 esim，可以由物理 sim 转换为 esim。但是需要验证身份。为此，您需要 A：有效的新西兰驾照或（其他国家）护照，B：一部手机，用于通过短信完成身份验证。手机必须有可用的摄像头。

  中国漫游资费如何？
  发送短信：0.8 新西兰元/条。
  拨打国内电话：2.3 新西兰元/分钟。
  接听电话：1.15 新西兰元/分钟。
  漫游流量包：17 新西兰元/1GB（有效期一周）。

  国内漫游使用哪个运营商？
  Skinny 在国内漫游支持联通和移动，显示任一运营商名称均属正常。可在手机设置中手动选择。

  支持 WiFi Calling 吗？
  支持，在国内使用 Skinny 电话卡可以开启 WiFi Calling 功能，待运营商图标处出现 Wifi Calling 的图标即可。在 Wifi Calling 状态下通话费率按照本地通话计算
  如何充值？
  自助充值：使用信用卡（VISA、MasterCard、AE）在 Skinny 网站或 App 上充值。
  代充服务：如无信用卡，可联系 Skinny 客服代为充值。

  - 游全球，冲就行了，或者淘宝咸鱼
  多花几块钱

  - 这是激活后的卡吗？
    - 对，是已经激活了的卡
    - 发出的时候就已经是激活的了，到手即用

  - nz本地激活拿回国卖

  - 楼主没有esim卖吗
    - 没有esim，你需要拿到物理sim后到官网去转esim。

  - 求一个简单直接，支持写卡的新西兰esim（已经有空白卡和写卡器）
    - Skinny就支持，5新西兰币套餐就行，之后取消。
  - 麻木了，买了套餐，二维码也有了，也扫码写入sim卡了，也改到新西兰定位了，结果插卡后拨打456激活不了，提示无法连接到移动网络
    - 肯定啊，刚买的esim，等同于新卡激活，需要在新西兰境内激活才可以。别被误导了

  - ### [one nz 新西兰电话卡 · 常见问题与要点 ](https://faq.nbsn.co/)
    - [Kaka Shop - 新西兰手机卡与充值 ](https://kaka-shops.com/)
    - [KakaOne](https://kaka-one.com/)
  - 新西兰三大运营商之一，前身 Vodafone NZ，2023 年更名 One NZ。本卡是它的 Prepay 预付费卡，无月租、免费收短信、保号便宜，号码为新西兰原生实体号码。
  - 零月租：Pay & Go 没有固定费用，不用不扣。
  - 免费接收短信：在中国漫游收短信不收费，这是保号卡的核心用途。
  - 保号简单：一年充一次 $10（约 45 元人民币），不需要互转、不需要第二张卡。
  - 支持多平台注册：可用于注册推特、Telegram、ChatGPT、TikTok、Google、Discord 和 WeChat 等平台。
  - One NZ 的规则很严格：360 天一到，账户失效、号码回收、余额清零、SIM 内存储的一切一并丢失，条款原文是「We cannot reactivate a number once you lose your allocated phone number due to account inactivity」——没有补救途径。
  - +64 开头的新西兰实体号码，注册与激活无需实名认证，比 GV、接码平台更好用。
  所以唯一的办法是不要过期：把到期日记进手机日历，提前一个月充。

  - 🌹 One NZ 电话卡在国内能使用吗？
  可以，在国内是国际漫游状态。收短信免费，接打电话和上网按漫游资费计（见第 9 条）。
  可以长期放在国内用：Prepay、Mobile、Prepay Roaming 三份官方条款里都没有「长期在海外即停机」的条文。官网上唯一的时长限制（连续 90 天、需常住新西兰）属于 Daily Roaming，只对 Pay Monthly 合约用户适用，与本卡无关。

  - 自助充值：My One NZ App 首页按「Top up」，或网站 one.nz/topup，输入手机号，Visa / Mastercard 支付，最低 $10。
  代充：不想绑自己的信用卡，可以联系店主代充，充完在 App 里看余额即可。

  - 如何激活 One NZ 电话卡？
  须在新西兰
  激活要把卡插进手机、在新西兰有信号的地方，打开 one.nz/activate 输手机号、收验证码短信、选套餐；或拨 777 按语音提示。未激活的卡在国外注册不上任何网络，收不到验证码，在中国无法激活。

  我们出售的卡已在新西兰激活并注册过网络，到手插卡即用。

  - One NZ 支持 eSIM 吗？
  支持，Prepay（含 Pay & Go）可以换成 eSIM，但需要到 One NZ 门店办理并核验身份。人在国内无法操作，建议保留实体卡。

  - 支持 WiFi Calling 吗？
  支持。在国内连 Wi-Fi 开启 WiFi Calling 后，运营商图标处出现 WiFi Calling 标志即可。官方说明：没有月套餐的 Prepay 在海外也能用 WiFi Calling，按标准 Prepay 资费计（打新西兰号码 49c/分钟、短信 20c/条，不按漫游价）。

  - 支持哪些手机？
  除锁网手机外均可。卡为三合一尺寸（标准 / micro / nano），支持所有卡槽。

  - 国内漫游使用哪个运营商？
  手机会自动搜到中国移动 / 联通 / 电信之一，显示任一名称均属正常。连不上时按第 14 条手动选网。

  - Prepay 的号码由激活时分配，One NZ 不提供在线选号。想要特定号段只能换卡。

  - ## [Lebara UK eSIM 国内 Wi‑Fi Calling _202608](https://www.nodeseek.com/post-874249-1)
  - 其实说白了，就是只能首次wifi calling 激活后， 后面就是£0.49/ 80天（还是90天，记不得了）保号

  - wificalling可以接打电话发短信 昨天我刚跑通的
  结论就是不折腾！！！
  飞行模式，全局英国节点下载esim且显示wificalling后，不要去折腾他。此时看着拉成功、但后台还在激活。大概1小时后，就可以给英国电话打电话、发短信。
  同时，不要关闭飞行模式，不然就要重新删除esim重复上述流程。

  - 这个又贵又麻烦，就有点劝退了（侧面说明薅羊毛的更少，祝楼主好用

  - 我啦giffgaff、voxi、Vodafone、ctexcel、cmlink都没问题，就是lebara没拉起来，全局也不行

  - ## [Lebara 疑似也要黄 _202608](https://www.nodeseek.com/post-863917-1)
  - Lebara老草台班子了，客服全是印度人，这卡之前蝗虫已经过境一次了 之前Roam like home能用30G没过多久就下掉了

  - Lebara 所有国家都要本地激活的, 你们不看就上车吗?

  - lebara异地激活有bug, 偶尔才可可以
  这个卡在本地都是免费领的

  - 和另一家 ASDA Mobile 比不算便宜吧？

  Lebara 保号周期90天，最低充值5英镑，发送短信 0.49 英镑。

  而 ASDA Mobile 180天充值一次最低2英镑就可以了，也可以发送短信0.1英镑。
  但 ASDA Mobile 我用了 2 张卡支付都被拒了，据说需要 Paypal 英区卡支付。

  - 这家慎选，在国内有信号，但是每次开启这卡要等一个多小时才会来信号
    - 每个地方好像都不一样，我这里硬切几次才能出信号，挺烦人的

  - ## [VOXI eSIM 在国内只有开 WiFi Calling 才能发短信打电话，关掉就不行，有解吗 _202609](https://www.nodeseek.com/post-903761-1)
  如题，voxi的esim已激活，人在国内。开着wifi calling一切正常，一关掉短信就发不出去，电话也打不了。

  按理说漫游下走本地网络打电话是常规操作，难道vodafone跟国内运营商没语音漫游协议？

  出门没wifi的时候真挺难受的，收验证码倒是无所谓，主要是得能主动发短信打电话。有同款卡的佬吗，还是说wificalling就是唯一解

  - 你充值了吗
  第一个月，开着wificalling能免费发短信
  充值后只要曾经拉过1次wificalling，即使关了，以后都可以发短信（要扣余额）
  - 那倒还没有，昨天刚开，就订了个10磅套餐

  - 关掉wificall，漫游状态使用，要注意：
  漫游状态，要关掉“wlan通话”或者“无线局域网通话”
  另外卡内有余额，才能正常使用

  - 有没有套餐无所谓，你再充值5磅就可以正常发短信了，套餐漫游不行的，你得有额外的余额。

  - 我装三星外板手机Wi-Ficall随便拉，不要英国IP都行，到了外板iPhone怎么都拉不起来Wi-Ficall

  - ## [VOXI怎么申请实体卡？ - 运营商 奶昔论坛 _202603](https://forum.naixi.net/thread-10329-1-1.html)
  - voxi实体sim卡只能邮寄英国境内，不发往海外地区，想要卡只能找代收或者找人买

  - 找 在英留/在英国的盆友/转运（UK Post Box）发回来

  - 没啥意义啊 现在一张esim白卡才十几块钱 转运费都不止

  - ## ⚠️ [voxi使用条款 _202607](https://www.nodeseek.com/post-847319-1)
    - 让GPT查了一下，也有说长期漫游注销啊。

  - UK运营商都不支持长期漫游，都有所谓的公平使用规则

  - voxi也ban的话就再携号转网转回giffgaff不就行了吗？

  - ## [voxi 只用来收短信需要 WiFi CALL 吗？ _202608](https://www.nodeseek.com/post-868157-1)
  - 不需要，漫游可以收
  但是注意：VOXI也不支持长期漫游

  - UK运营商都有长期漫游政策（FUP）
  CTExcel和cmlink，有回国年套餐，可能会好点

  - 目前明确可以长期的只有 lebara 卡

  - 你保号得用wificall

  - 发短信得wifi-calling
  - 用wificalling又不是为了收短信，是为了保号

  - ## [【voxi居然要实体卡才能转PAYG？】 _202607](https://www.nodeseek.com/post-845908-1)
  - voxi不需要实体卡，可以取消套餐就行了，快180天时候充值5英镑
  - 我是直接找客服说（我是因为忘记取消套餐，到下一个账单周期了，扣20英镑），假期出去旅游了，不在Uk，帮我停止一下套餐，就ok了

  - giffgaff客服还说giffgaff只能英国本地激活呢你信了吗，这家直接等套餐过期就行，过期自动转pay as you go，自动转不用管客服

  - 官方说明，到期自动转入pay as you go

  - [voxi客服说是不用切换 _202602](https://www.nodeseek.com/post-616735-1)
    - Please keep in mind that your number will remain active for the next 180 days until you add credit to your account and send a standard text or make a call once within the next 90 days. This will be considered your usage with VOXI and will keep your number active (if you do not wish to add any plan unless you're in the UK)
    - We will disconnect your mobile services and you will forfeit(失去, 放弃) any credit held on your account if you do not do so within 90 days of receiving the text because you have not followed this Agreement or have not used the services for 270 days. When you return to the UK, you can add plan from your online account. This is an ideal process of keeping your number active with VOXI.

  - ## [关于VOXI保号的相关条款 _202603](https://www.nodeseek.com/post-662258-1)
  VOXI： 沃达丰旗下的子品牌，更像是青春特惠版，激活时必须选套餐（有优惠券首月免了）。但套餐到期后可以不续订。
  Vodafone PAYG： 标准预付费卡。然后PAYG还分 Simply（即用即付，用多少扣多少）和 PAYG 1（按天计费，当天有消费则扣 £2 封顶，不使用不扣费）。
  需要注意的是，VOXI 官方条款里明确写了只要超过 180 天无活动，官方就有权直接注销。所以那额外的 90 天宽容期并不是 100% 稳的“免死金牌”。为了防翻车，建议大家还是老老实实按“半年动一次”的频率操作，一年保两次最安全。(哦还有个bug，如果想270天保号你得充值保了，因为180天后会把你暂停通信，剩下这90天理论上你得充值保号了)

  - 只要目前持有的 VOXI eSIM 已经有信号，正常用着就行，完全没必要去转 PAYG。转网不仅需要联系人工客服，还要重新下发和扫描 eSIM。至于保号，安全起见，建议老老实实保持180天保一次的频率最稳妥，当然胆子大的老哥也可以试试第一次270天充值5￡保，剩下还是180天消费保最划算了。

  - ## [0元手把手教你申请VOXI英国手机卡eSIM _202601](https://www.nodeseek.com/post-590905-1)
  - giffgaff：虽然卡免费，但激活必须充值 £10 (10磅)，成本较高。
  - VOXI：申请免费，最低充值仅需 £5 (5磅)！
  - 拿到卡后，别在 VOXI 官网充大额套餐！如需保号登录账号后先暂停套餐然后再进行充值
  - 利用 Vodafone 底层接口，支持最低5镑充值保号

  - 保号周期：每 180天 需要有一次消费记录（余额变动），否则号码会被回收。
  最省钱方案：在中国漫游状态下，发一条短信给任意英国号码（比如你自己的英国号或接码号）。

  超低成本：实测漫游短信费用低至 8p/条 (约£0.08)！
  注：相比之下 giffgaff 漫游短信通常要 30p，VOXI 这一点赢麻了。

  - ## [谷歌账号被封控，登陆要求填手机号接码怎么办？ _202609](https://www.nodeseek.com/post-920125-1)
  - 下次验证还是第一次接码的号码，必须建议绑定长期可接码的号码 。

  可以开个voxi UK eSIM, 自用一年多，目前很稳定。

  手机原生支持eSIM更好，不支持可以在多多上花20不到买个“小白卡”写入eSIM。

  充值5英磅理论可保号30年, 使用优惠码后0元开通，支持转paygo。就算不充值，也能用200多天。

  之前没注册过voxi，强烈建议买成品号，因为优惠码一旦使用注册过程中出现任何问题就不能重复使用了
  VOXI 保号方式

  Paygo 状态下任意余额变动（例如充值、通话、短信），即可刷新有效期再延长 180 天。

  VOXI 的最低充值金额 £5 GBP，号码失效的前 90 天会收到短信通知。

  中国发短信成本仅为 0.08 GBP ≈ 0.8 RMB / 条，在 WiFi Calling 下仅为 0.01 GBP 约等于一毛钱！
  充值一次理论可以做到保号30年！
  最简保号方式建议：
  最佳保号方式是每 180 天内主动发送一次短信。

  - ## 📌 [长期出：15块/个voxi优惠码、35块/个voxi成品号，目前GG（giffgaff）被封后 ESIM的不二之选！可用于chatgpt(codex)等主流服务接码！附注册、扫码、Wifi Calling、转移详细开通教程 _202607](https://www.nodeseek.com/post-847659-1)
    - [AI事多的小店 - 链动小铺 ](https://wzyp.cn/shop/faka)
  - 

  - ## [voxi 怎么搞 pay as you go _202603](https://www.nodeseek.com/post-642158-1)
  - 能接短信
  但是拉不起来wifi calling的话，不能发短信
  也就是没法保号了

  - 这张卡已经没啥用了 国内无漫游 只能接不能发
    - ios加上尾插可以拉wificalling拉好了就有信号了，中国联通的也可以发短信

  - ## 📌 [GG卡GG了，其他可用的卡汇总 _202607](https://www.nodeseek.com/post-843142-1)
  Ultra Mobile PayGo
  美号，也就是常说的紫卡。官方售价 US$13，含卡和首月，国内没法直接卖，我找到最便宜的是180包激活包邮。月租 US$3，中国漫游收短信 US$0.10、发短信 US$0.50，不支持漫游数据，也可通过 Wi‑Fi Calling 收码。近期似乎有风控，可能无法激活，欠费超过 60 天可能销号。

  Red Pocket
  美号，也就是红包卡。官方eBay年卡 US$46/360天，含美国境内无限通话短信。国内不能买，需要找商家买和激活，卡+首年资费价格应该在五六百？年包到期续费即可保号。最近资费有很大变动，此前每月1GB国内能用的漫游流量只剩下10MB了，原本30U的年费涨到46U（感谢#10楼补充）了。额外 100 分钟或100条短信均为 US$5，1GB 数据 US$20（这个资费AI查的）。

  HAHASIM
  香港 +852 实体卡，由丰泽销售、3HK 提供服务，官方售价 HK$50并含等额余额。不能直接买，需要找商家。接收短信通常免费，发短信约 HK$3.5/条。

  Club SIM
  香港 +852 卡，CSL/HKT 体系，支持实体卡和 eSIM。似乎可以在线购买eSIM，然后使用港澳通行证实名开通。每365天购买一次任意套餐包，最低为 HK$15/30天短信包（感谢楼下指正）。大陆漫游通常可以免费接收短信，但不能拨打、接听或发送短信。纯接验证码时算是比较省事的？

  Skinny
  新西兰 +64 卡，Spark 旗下品牌。实体卡只能在新西兰购买或寄送，eSIM虽然免费单页必须在新西兰激活，所以在国内只能购买已经激活的卡。每12个月至少充值NZ$5即可保号。大陆收短信通常免费；发短信 NZ$0.80/条。

  VOXI
  英国 +44 卡，可以免费寄SIM到英国地址，也必须在英国激活，所以还得电商找商家。连续180天没有充值、套餐或收费通信会暂停，再过90天可能彻底销号，可以150天发一次收费短信。中国漫游发短信 £0.08/条，收短信免费。

  CTExcel UK
  英国 +44 卡，中国电信欧洲运营。官网可以直接购买实体卡，激活需要用UK🪜。“回国年套餐”有365天保号时间，价格是50G流量 36£/Y，15G流量 22£/Y。现在有5折优惠。

  T-Mobile Prepaid / Connect
  美国 +1 原生运营商卡，必须在美国购买或通过官网/eSIM App开通，并在美国完成首次激活，so 卡商走起。具体套餐资费 佬们可以补充一下，我记得成本不低。

  Tello
  美国 +1 卡，支持实体 SIM和eSIM。此前都是挂🪜激活的，现在似乎不一定能成功。中国漫游短信 US$0.01/条、数据 US$0.01/MB，也支持 Wi‑Fi Calling接收普通短信和银行验证码。具体规则 佬们可以补充一下。

  我最后选了CTExcel的 22£ 回国年套餐，考虑是我能自己官网直发购买和续费，激活用🪜似乎不麻烦。22£折合大概203rmb一年，现在在付款页用优惠码“DEAL50OFF”可以首年五折，也就是102左右。套餐内带的15GB流量是可以上外网的。

  - 香港卡确实省事，可惜不能验证gpt

  - 有些信息已经过时了

  Red Pocket已经被砍了

  clubsim最低15，没有6的了

  - 红包卡现在是46刀了，价格涨了套餐砍废了，没法说划算了. 通信税和州税之类的东西加起来就是十几刀，还有什么管理费和delivery配送费（反正esim也不知道哪来的配送费）

  - 紫卡听说风控很严苛，商家都劝我别买

  - ## [想买个海外号码，长期接短信验证码用，有推荐吗？ - V2EX _202505](https://www.v2ex.com/t/1133396)
  - talatone 不建议长期使用，即使你付费，他家经常会无故封号。 收发短信的话建议还是德国沃达丰或者 giffgaff 。

  - clubsim 香港 每年 6 港币消费保号 可转 esim
  hahasim 香港 每年充值 10 港币保号 可转 esim

  giffgaff 英国 激活充值 10 磅 每半年消费一次保号 可转 esim

  - clubsim 好像要实名验证, 挺烦的
  - hahasim 要实名了。。

  - 新西兰 Skinny 保号成本最低，使用方便，实体卡

  - 英国 giffgaff：注册接码性价比神卡，0 月租，无实名，实体卡，支持 eSIM 和 WiFi Calling ，收短信免费，每半年发一条短信保号（发短信 0.3 镑/条），用 Visa 或万事达卡充 10 镑（ 90 多人民币）就能激活成功，激活成功后获得一个随机+44 号码（实体号码，非虚拟号码）；本月正好有限时活动充 10 送 10 ，到手 20 镑余额，发短信保号的话可以用 30 多年了。

  - 有 eSIM 就是 T-Mobile 3 刀乐穷鬼卡
  没有 eSIM 就上淘宝上买个出境卡，比如斯里兰卡 Dialog ，没有淘宝所说，店家会卖给你实名认证的，每次充值 LKR 1, 000 以上（ CNY 25.00~）延期一年有效期。

  - google voice ，这个好处是真的免费，但是需要花钱买，最便宜可能 10 块左右的，坏处就是容易被识别为虚拟号，有一些无法接到短信，不需要手机接收信号，用 app 来收短信就行。

  helium mobile ，真 0 元美国卡，需要上传护照申请，可以用我邀请码 M8LHDL3 ，缺点是需要你手机支持 esim ，如果没有 esim 的话，就需要写卡，这个是另外花钱的，

  - 还不如直接新开国内的卡，只用来接受短信。号码也不告诉任何人。电话一律自动拒接。

  - 使用建议专机专用、开 wifi calling （过梯子别直连），同时国内移动+国外卡 esim （也是漫游到移动）被当地电话询查，漫游信号也变成“紧急服务”、wifi calling 直连会被墙。

  - ## [gv除外，mjj都用什么国外手机号 _202403](https://www.nodeseek.com/post-79266-1)
  - Vodafone UK，
  Skinny NZ，
  Hahasim HK。
  都比较便宜。
  另外，giffgaff的aff太多了很多人推，而且首充多了点，就没用这个。

  - [现在性价比最高的国外手机号方式是什么啊 _202402](https://www.nodeseek.com/post-71296-3)
    - 持有成本最低当然是 Google Voice，不需要购买设备，缺点是 VoIP 会无法接收某些验证码，用来注册某些服务风控也会比较高，但它最大的优点是可以做到完全免费，所以性价比是无穷的。
    - Giffgaff 是目前实体卡持有成本最低的，并且也有作为实体 SIM 卡的优势。但考虑到首充就得10£。最大的缺点就是很难说后期会不会因为成本考量强制要求现有用户购买更贵的套餐，或者要求使用者在一定时间后必须在回英国使用一次才能续期。

  - ## [需要一个外国手机号，有持有成本低的吗？ - V2EX _202511](https://www.v2ex.com/t/1173159)
  - 我有香港的卡，好几种，最低一年充值 10 块钱就能长期使用
  - HAHASIM 不仅能收短信，还有可以接受的流量价格，好像还能接电话，不在香港用还不用实名
  - hahasim 香港卡，可以接打电话和短信。 冲 20 港币保一年，不需要消费。 可以开一日流量包用来上网。
  - GG 卡还是性价比挺高的，如果有港卡的需求，买个 clubsim 也可以的

  - 不知道外贸要求高不高 高的话美国实体卡
  3 刀/月 美国实体卡 ultra paygo

  - 港澳卡是最好的选择，从激活到售后，都是最适合国人宝宝体质的，就算是再有什么问题需要跑一趟，也比去一趟国外的成本低

  - skinny 保号一年一次，可以发短信，也可以两个号互转 5$ 左手倒右手，这样就不花钱保号了
  giffgaff 需要半年发一次短信给英国手机客服发一次短信，目的也是让账户变动
  这两个卡都不需要月费，只要运营商还在，政策不变，按时保号，可以用 10 年+

  - 你的需求是上网还是收发短信
  上网可以用 esim+firsty
  收发短信可以用 gv
  都是免费的

  - ## [哪里能购买到能在国内接码的美国手机号？ - LINUX DO _202609](https://linux.do/t/topic/2840847/17)
  - 美国手机号码也封号的。哈哈哈 感觉境外手机卡就没有很稳定不封号的说法

  - UltraMobilePayGo，3$ 月租，每月交月租保号，有公众号卖这个的

  - 京东买 t-mobile 3 美元月租的就行，U 卡可以充值。但是注意不要买那种只能通过商家充值的，不太稳定，容易封号。自己能充值就意味着这个号完全由你自己控制。
  坏处是较贵，接一条短信 0.1 美元，刚用头一两个月经常收垃圾短信…… 后面注册了联邦反骚扰名单，营销短信就绝迹了

  - saily 用了小半年，除了停车场收不到短信其他地方都没问题，而且国内卡支付的有正规账单可以走报销

  只是手机要有 esim 才行，没的话买个好点的白卡不便宜

  - 可以搞个 voip 的虚拟号，google play 上有很多这种 app，美国号码基本在 19.9-29.9 刀 / 年。
  也可以搞 saily 的 eSIM，是我目前手里性价比最高的美国 eSIM 卡，最便宜的 1.99 刀 / 月 5 条短信，有抵扣券可以用

  - saily 和 1psim 都可以网上申请 esim。

  - 后面的佬千万不要买 20 多的那个小白卡，有概率丢失号码，但是 xesim 价格太贵了，所以还是推荐买一台支持 esim 的手机。

  - ## [有好用的美国手机号可以注册美国银行的吗 - LINUX DO _202605](https://linux.do/t/topic/2219193)
    - 有人知道有什么好用的美国手机号不是虚拟号的哪种，可以注册美国银行卡，保号越便宜越好，最好能支持 esim 的，目前了解有 gopay 或者 T-mobile 是 2.5 刀 - 3 刀的每个月感觉还是好贵，但是其他的像 google voice 又是虚拟号有的银行不接受虚拟号办理银行卡，好纠结呀，好烦呀，像 giffgaff 我感觉就很好，充值 10 刀能用十年这样子，每条短信才 0.03 英镑。
  - 用来做银行业务的美国手机号基本就这些了，最便宜的都是 2.5 美元，这些严格来说都不是实名手机号
  有些要 caller id 的都 20 美元 / 月起步

  - ## [费用低容易获取的美国手机号，如何申请？ _202512](https://www.nodeseek.com/post-557302-1)
  - 美国保号就没一个便宜的
  tello 5刀
  ultramobile t-mobile 3刀

  - 有电话短信需求优选ultra mobile 3刀
  没电话短信需求优选T-mobile 3刀
  其次新出的红包2.5刀套餐，无限通话和短信
  再其次优选tello 5刀

  - 我选了一个ultra mobile 3U，但是每次充值都收我手续费，真烦。我都填写免税州了

  - ## [两款美国esim保号卡，可能包含虚拟号码（无AFF） - LINUX DO _202608](https://linux.do/t/topic/2829880)
    - https://www.phonevalidator.com/
    - 输入手机号进行检测，只要结果显示手机号的类型是 CELL PHONE，那就说明是实体手机号；如果显示的是：VOIP ，那说明是虚拟手机号。
    - Truth Social 懂王自己创建在社交网站，访问需要挂载美国节点。注册需要美国实体手机号。
    - 大厂 NordVPN 旗下出品，适合作为低成本美区接码主力备用卡。+1 美国号码，适合长期保号、接收短信验证码以及注册部分美国平台（美区 paypal，tg，WhatsApp）。购买技巧（只包含接收短信，发送短信和接打电话需要另外购买）：先在手机上下载 app 注册账号，选择只获取手机号码，在结算页面选择使用抵扣金便可实现首月 $0.6，后续一个月续费 $0.99。
    - 1PSIM 使用 T-Mobile 网络，适合需要长期保留一个美国手机号、接收短信验证码、注册海外平台的人使用。官方目前提供 eSIM 和实体 SIM 两种形式，并支持 Wi-Fi Calling。 其中比较适合长期保号的是 PayGo eSIM：官方目前显示 $30/12 个月，包含 100MB 流量 + 100 分钟通话 + 100 条 SMS，折算下来约 $2.5 / 月。建议先购买 1 到 2 个月体验再决定是否长期续费。

  - 通过两个号码的检测结果可以看出我拿到的 saily 号码是介于虚拟和实体号码之间的。虽然可以注册懂王的网站，但是仍被一个网站定义为虚拟号码。1psim 的号码是使用 T-mobile 网络且检测结果全为实体号码，所以 1psim 的号码大概率为实体号码。

  - saily 身份证就可以了，1psim 不需要 kyc。

  - 用的 Saily，945 号段，懂王能收验证码，但是 ws 获取不到验证码

  - 买了两个号 都注册不了 whatsapp

  - 反正 945 段。openai 也不行。

  - ### [美国1pesim+实体卡，每月2.8美金 _202509](https://www.nodeseek.com/post-450742-1)
    - 优点：Esim方便，不是虚拟号，实体卡香港发大陆快，套餐便宜，1刀保号，可随时转入转出。
    - 缺点：只支持Wifi Calling，6个月套餐才有优惠，1刀保号收不了短信。
    - 我其它美国虚拟号有-永久免费Talkatone：每月保号1次，永久免费Hushed：半年保号一次

  - Talkatone好用，基本都识别为实体卡，能注册很多东西，另外一个和谷歌call一样是虚拟的，很多东西注册不了

  - ## Nord VPN Saily [仅需一美元获得一个实体美国手机号 - V2EX _202606](https://www.v2ex.com/t/1219929)
    - Nord VPN 旗下的 eSIM 服务 Saily 现推出每月仅需 1 美元的美国专属电话号码。您可以使用 Saily 号码注册账户、接收包裹、访问仅限美国用户的服务，以及创建第二个 WhatsApp 账号等各种用途。
    - 目前该手机号月租为 1 美元，可以免费接收短信，发送短信和打电话需要开通相应的套餐。
    - kyc 对国内用户非常友好
  - esim 了，肯定是实体

  - 昨天注册 折腾了半天

  Google Voice 无法收到短信验证码

  Telegram 可以收到短信验证码

  OpenAI 短信 发送报错提示

  WeChat 可以收到短信验证码

  WhatsApp 无法收到短信验证码，但是可以收到语音验证码

  - 先注册好 WhatsApp 然后再注册 openai 通过 whs 来收验证码就好了。

  - 肯定不如 giffgaff 的，giffgaff 可以发短信，可以流量上网。
  - pdd 白卡+ giffgaff esim, 首次搞完也就 100 块，还不要月租

  - 还是贵了，目前手上 gaffga 和 vodafone 都是零成本持有。

  - 一般情况下美国卡要填写 e911 的，并且大部分运营商首次激活要在美国本土连上基站才行。买卡 1$，激活很麻烦的，100 ￥起吧

  - 散了吧，亲测 PayPal 收不到验证码，拿 Telegram 试了可以收到
    - 我这刚试了下 paypal 没有问题

  - 注册后查询是实体号码，绑定 Paypal 没有问题，正好 GV 被回收了 

  - ### [0.99刀一个月开通了一个美国实体手机号-内含AFF _202606](https://www.nodeseek.com/post-773332-1)
  - 貌似已经涨价了。 刚才测试，打开默认就是显示 每月US$1.99
    - 好消息是官网下单还是 0.99，可以试试水

  - 号码1刀每月，接短信需要另买套餐最便宜的是 5条短信1.99刀每月。可以扫二维码下载esim，已经删了不划算。

  - 实体号码，刚测试了一下美国银行短信也能收
    - 一切正常，坐标江苏
    - 接收短信是免费且无限量的。 Saily 的美国手机号（+1）功能最近推出，明确支持“Users can receive unlimited SMS messages without an active plan”（即使没有激活通话/SMS 套餐，也能无限接收短信）。楼下的大兄弟在哪儿看到的收短信也收费。。。。

  - 坐标华北 联通电信都收不到短信 其他没信号

  - 这几年弄了两个美国手机号, 最后都被封了, 不给中国的用, 现在用tello贵点起码稳定

  - kyc需要刷脸吗 还是上传一下就行
    - 需要刷脸

  - 
  - 
  - 
  - 
  - 
  - 

  - ## [求教，目前能用于Google接码验证的手机号买哪里的最便宜？ _202509](https://www.nodeseek.com/post-451234-1)
  - 电信有个5元保号，现在不知道还有没有

  - ## [分享几个短信接码平台 - LINUX DO _202605](https://linux.do/t/topic/2202877)
    - 号码类型查询 https://www.freecarrierlookup.com

# discuss-google-accounts
- ## 

- ## 

- ## 

- ## 

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
- 有救 过七天再试 我就救过两个
这期间不要再试了
试一次再延长
可以下个月再试 大概率就不提示了

- 我之前问过客服
你等 7 天 + 以上 现在不要登录了 你越登录 越麻烦

- 巧了，我最近也在折腾这个问题，有一个买的账号掉登录了，然后我登录输入手机号前几次还能等，但是那时候可能我携号转网问题收不到，最近看激活了重新登录输入验证码就一直显示次数过多，我隔了，3, 4 天去还不行，我今天早上又试了一下重新登录居然直接让我输入新的手机号，我换了个手机号收到验证码登录之后告诉我被封号了，然后我现在在申诉

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

- ## [反重力需要扫描验证怎么解决 - LINUX DO _202609](https://linux.do/t/topic/2855971)
- 找个装谷歌框架的安卓手机，有 play，登录一个老账号，然后用相机直接扫就行

- YouTube 扫个码就过了，我有两个号也报二验，扫完就 OK 了

- 直接扫就行啊，扫完跳转谷歌系任意一个登录过的 app 确认一下就行了

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

# discuss-email
- ## 

- ## 

- ## 

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
