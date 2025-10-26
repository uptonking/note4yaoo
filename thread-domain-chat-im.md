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
# discuss-discourse
- ## 

- ## 

- ## 

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
