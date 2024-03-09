---
title: lib-collab-community-sync
tags: [collaboration, community, synchronization]
created: 2022-11-29T20:41:00.894Z
modified: 2022-11-29T20:41:25.566Z
---

# lib-collab-community-sync

# guide

- 协作方案参考
  - Liveblocks, synced-store, FluidFramework, gun, pouchdb
  - automerge(2017), yjs(2015), sharedb(2013)

- 成熟的解决方案一般都会设计和公开自己的同步协议
  - database: mysql, pg, couchdb, rxdb
  - framework: meteor-ddp, feathers-sync, gnu, realm/Atlas-Device-Sync
  - editing: yjs-protocols, automerge-sync

- sync-tips
  - 基于缓存实现sync有点类似于react-query
  - 参考vlcn

- sync实现要点
  - client发送内容op/patch/changes, 发送时机，接收内容
  - server接收，发送内容

- 考虑到客户端升级的问题
  - 同步前一定要检查一个version，参考indexeddb upgrade
  - logux支持客户端不同version

- 支持offline的架构
  - 还可以考虑使用多级缓存，不一定全量数据库，类似react-query + indexeddb
# sync-protocols
- [Building an offline realtime sync engine references](https://gist.github.com/pesterhazy/3e039677f2e314cb77ffe3497ebca07b)
  - figma, linear
  - pouchdb, fluid, watermelonDB, Liveblocks

- https://code.briarproject.org/briar/briar-spec/-/tree/master
  - [Bramble Synchronisation Protocol, version 0](https://code.briarproject.org/briar/briar-spec/-/blob/master/protocols/BSP.md)
    - BSP is an application layer data synchronisation protocol suitable for delay-tolerant networks.
  - [A Quick Overview of the Protocol Stack](https://code.briarproject.org/briar/briar/-/wikis/A-Quick-Overview-of-the-Protocol-Stack)

- [Fossil: The Fossil Sync Protocol](https://www.fossil-scm.org/home/doc/trunk/www/sync.wiki)
  - The "bag of artifacts" data model used by Fossil is apparently an implementation of a particular Conflict-Free Replicated Datatype (CRDT) called a "G-Set" or "Grow-only Set". 
  - [The Fossil Sync Protocol | Hacker News _202402](https://news.ycombinator.com/item?id=39464938)

- [Pushpin | Generic Realtime Intermediary Protocol](https://pushpin.org/docs/protocols/grip/)
  - GRIP makes it possible for a web service to delegate realtime push behavior to a proxy component
# blogs-sync
- [MongoDB Realm: Device Sync Protocol](https://www.mongodb.com/docs/atlas/app-services/sync/details/protocol/)
  - Atlas Device Sync uses a protocol to correctly and efficiently sync data changes in real time across multiple clients that each maintain their own local Realm files
  - The Realm SDKs internally implement and manage the sync protocol, so for most applications you don't need to understand the sync protocol to use Device Sync
  - Changesets are the base unit of the sync protocol.
  - Synced realm clients send changesets to the Device Sync server whenever they perform a write operation. 
  - The server sends each connected client the changesets for write operations executed by other clients.
  - 👉🏻 The Device Sync server accepts changesets from any connected sync client (including changes in a synced MongoDB cluster) at any time and uses an **operational transformation** algorithm to serialize changes into a linear order and resolve conflicting changesets before sending them to connected clients.

- [PostgreSQL: Documentation: 16: 55.4. Streaming Replication Protocol](https://www.postgresql.org/docs/current/protocol-replication.html)
  - To initiate streaming replication, the frontend sends the `replication` parameter in the startup message.
  - it tells the backend to go into physical replication walsender mode, wherein a small set of replication commands, shown below, can be issued instead of SQL statements.
  - In either physical replication or logical replication walsender mode, only the simple query protocol can be used.
  - [PostgreSQL: Documentation: 16: 55.5. Logical Streaming Replication Protocol](https://www.postgresql.org/docs/current/protocol-logical-replication.html)

- [MySQL 8.0 Reference Manual :: 17 Replication](https://dev.mysql.com/doc/refman/8.0/en/replication.html)
  - Replication enables data from one MySQL database server (known as a source) to be copied to one or more MySQL database servers (known as replicas). 
  - Replication is asynchronous by default; 
  - you can replicate all databases, selected databases, or even selected tables within a database.
  - MySQL 8.0 supports different methods of replication. 
    - The traditional method is based on replicating events from the source's binary log, and requires the log files and positions in them to be synchronized between source and replica. 
    - The newer method based on global transaction identifiers (GTIDs) is transactional and therefore does not require working with log files
  - [MySQL: Replication Protocol](https://dev.mysql.com/doc/dev/mysql-server/latest/page_protocol_replication.html)
    - Replication uses binlogs to ship changes done on the master to the slave and can be written to Binlog File and sent over the network as Binlog Network Stream.

 ## [RxDB replication protocol](https://rxdb.info/replication.html)

- 支持websocket、graphql、couchdb、p2p
- The RxDB replication protocol provides the ability to replicate the database state in realtime between the clients and the server.
- The backend server does not have to be a RxDB instance; you can build a replication with any infrastructure. For example you can replicate with a custom GraphQL endpoint or a http server on top of a PostgreSQL database.
- 👉🏻 RxDB resolves all conflicts on the client so it would call the conflict handler of the RxCollection and create a new document state D that can then be written to the master.
- The default conflict handler will always drop the fork/client state and use the master/server state.
  - This ensures that clients that are offline for a very long time, do not accidentally overwrite other peoples changes when they go online again. 
  - You can specify a custom conflict handler by setting the property `conflictHandler` when calling addCollection().
- It is not possible to do a multi-master replication, like with CouchDB. RxDB always assumes that the backend is the single source of truth.

## [Different approaches to p2p data sync](https://status-im.github.io/bigbrother-specs/data_sync/p2p-data-sync-comparison.html)

- [Different approaches to p2p data sync · status-im/bigbrother-specs_201903](https://github.com/status-im/bigbrother-specs/blob/master/data_sync/p2p-data-sync-comparison.md)
  - 支持partial replication的有: Matrix, Swarm, Briar, Bramble

- Briar Bramble
- Matrix
- Secure Scuttlebutt (SSB)
# discuss-external-sync
- ## 

- ## 

- ## [Joplin/Obsidian笔记软件同步问题：如何在不能装网盘客户端的电脑上同步？ - 知乎](https://www.zhihu.com/question/471377032)
- 方案一： 官网Sync服务
- 方案二：Remotely方案
  - Remotely 是一款 Obsidian 第三方插件，你可以在插件中配置使用DropBox/OneDrive / WebDAV/S3/OSS/COS 等网盘及云存储服务来使用，常见是使用OneDrive或者阿里、腾讯的云存储做中转；WebDAV 的支持上，国内坚果云暂时是不支持的。 
  - 使用Remotely需要配置第三方的中转，现在功能还在完善中，还不能同步Ob的插件和主题，因些同步文件后，插件和主题要自己在第二台设备上安装
- 方案三：Rsync的方案
  - 基于开源的Rsync方案，可以实现Win/Mac/Linux与移动端的文件增量同步功能，需依赖同一局域网中的SSH协议进行文件传输

# discuss-stars
- ## 

- ## 

- ## 

- ## 🧭💡 [web端如何无感共享屏幕？ - 知乎](https://www.zhihu.com/question/565779619)
- 如果单纯共享屏幕，那还不涉及协同问题，更加简单。
- 一种是基于服务端，如果你很早以前接触过一个叫browsersync的工具，它主要是用作一些开发测试场景用的，如果想要用到生产，需要自己基于它做深度开发，不过好处是你不需要改当前网页的代码，靠服务器端注入脚步来同步两端界面。可以了解一下liveview这个项目，你可以把它理解为云渲染，所有状态存储在云端，浏览器只不过是界面的控制台输出
- 第二种是基于浏览器的。这种途径，需要同时收集界面、鼠标、键盘输入等信息，管理起来复杂一点。也有多套方案，根据架构可借助服务端或者基于webRTC的点对点通信
- 既然要无感，那么弹出权限询问显然就不是无感的，所以，我们不要直接调用视频录制，
- 我们可以采用其他的办法对网页内容及其变化进行录制，方法有4：
  - 1）问题里提到的html2canvas，按帧录制，不过可以做一个优化，是否发送流可提前进行对比，实际上，web的帧率是很低的，只有在一些动态效果的时候可能卡顿；
  - 2）基于MutationObserver的DOM变化录制，也就是问题提到的rrweb，其实录制过程也挺耗性能，不过好在传输的数据量小；
  - 3）基于全局状态管理器对状态变更进行录制，或者类似的状态录制方案；
  - 4）对用于渲染页面的api数据进行录制，再配合DOM事件。
- 本地录制后，就是如何将录制内容发送到远端，有2方法：
  - 1）通过服务器中转；
  - 2）通过webRTC传输。
  - 服务器中转可用websocket，可以做一些策略来优化。
- 最后是在远端播放录制内容，要么是基于stream来还原canvas，要么是不断在DOM上patch，让界面看上去是在不断的播放。其中有很多细节要处理，比如时间如何卡点，我是用requestAnimationFrame来收集每帧的变更，在每帧上进行逐一patch，如果顺利的话，基于requestAnimationFrame的是不会卡顿，但是DOM的性能堪忧，所以演变出合体方案。
- 合体方案就是收集过程是基于DOM的变化，从而可以减少数据量，更快丢到服务端，然后在云端进行渲染，将渲染后的效果通过stream给到远端，放在canvas里面甚至视频里面播放。

- 微软那个新产品clarity不就是网页回放么，就是前面几楼说的即时验算而不是录制视频。

- 服务器端server side rendering，然后记录用户所有输入，两边做状态同步，在服务器端录视频还是可以的
- 云桌面那一套呗，服务端渲染网页，扔到客户的canvas显示，再接管用户输入，延迟够低也看不出区别，就是输入框之类的地方会很恶心

- 类似需求：如何无感调用用户摄像头？怎么，想进局子？

- ## 🚀 [Ditto: Real-time sync for apps even without the internet | Hacker News_202209](https://news.ycombinator.com/item?id=32934849)
- 🗣️ CoFounder of Ditto here
  - Our entire core code base is written in Rust and I know HN goes crazy for Rust. If you’re really interested in working on very hard problems like CRDTs, partial replication, query based replication, peer to peer adhoc sync, mesh network or distributed security: please definitely take a look at our openings.

- since Ditto's replication is "delta-based" it will only sync differences. 
  - Our protocol is designed to overlay on top of custom arbitrary links, including unreliable ones. Not familiar with CCSDS, but we have explored Link16, and even built-in we replicate over BLE GATT.

- 🤔 How is it different than all the open source peer-to-peer sync tools, such as Dat/Hypercore, or PouchDB?
  - We use multihop ad hoc network connections! That’s the BIG thing that we add to the mix!
  - A) PouchDB, Couchbase, Firebase, Realm are all databases that can sync to a "master" node in the cloud.
  - B) AODV and BATMAN are really an ad-hoc mesh networking and routing protocol.
  - Ditto is both A and B. You work with Ditto as a database on your mobile, IoT, web app with common database functions (querying, updating, deleting etc...) and we will sync the changes between edge and cloud devices. 
  - Most developers cannot sensibly use AODV and BATMAN to build robust collaborative applications, it's too hard. We abstract all of the routing, network resiliency, and replication away from you; just work with the database

- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 💡 Hashes in version control systems have some great properties.
- https://twitter.com/JungleSilicon/status/1737692594459824504
- This is especially true if you persist a history, then rather than sending sequence numbers you can just send the hashes of the parent node(s). 
  - This can work for both totally ordered/flattened histories and causal graphs.
- You've probably seen @unisonweb , right? Content-addressed code?

- what if the content is very large?
  - The content? Or the number of changes? Systems like git use hashes for commits and can handle reasonably large file sizes.
  - If you’re worried about storing all of those hashes - you can push the hashes to the protocol layer and not store them internally (there are tricks necessary if you don’t want to recompute the hashes for everything).
  - Other version control systems like perforce are better at handling very large file sizes than git. I haven’t looked too deeply into why. (Specifically binary files & media content - in game dev it was the vcs of choice for a long time, not sure if it’s still the case)

- ## Because there are no pre built solutions everyone's forced to roll their own sync engine!
- https://twitter.com/LewisCTech/status/1737707633572986981
- Yeah, I find it surprising how often I talk to companies that have built their own sync with a very simple conflict model and find they don’t need much more. Last-write-wins on fine-grained document state is often good enough in practice!
- I feel multi-value registers should be the baseline since it's the simplest thing that doesn't throw data away.
  - Many apps don’t care about that.

- Conflict resolution / business logic is the real killer. (That’s part of why I like replicache’s approach; you’ve got more control over what constitutes a conflict and how conflicts etc are handled)

- https://twitter.com/steveruizok/status/1737591179682730481
- We built our own sync engine for tldraw. (I really didn’t want to, but we’re one of the few apps where we needed that last step of perf / control) 
- I’m happy to pay it, as multiplayer is a big part of the tldraw story and will continue to be. I also looove our sync system and am happy that we’ll be providing something with as close a fit as possible to our core product when we inevitably sell/license it to tldraw user-devs.

- ## It's astonishing to me how difficult it (still) is to design a syncable local-first data model.
- https://twitter.com/andy_matuschak/status/1393620663257100288?s=12
  - I keep thinking I've found a decent way, then realizing its flaws
- Take Firebase, for instance: it implements offline caching, but that's very different from sync. You have to design a whole replication strategy on top to get something like "a synced file format."

- CouchDB seems like the closest solution, if you can design a conflict-free model. But I spent the last week getting into the details of actually operating a multi-user service, and I am now quite thoroughly spooked!
- I've noticed that a lot of modern solutions to this problem assume that it's viable to read the entire data store from disk into memory on load (and, often, write the entire thing on save)—which I guess is a nice simplifying assumption… but quite limiting!
  - Microsoft sync framework (for all of its flaws) had so much of this solved 10+ years ago but because it’s such a complex problem, solving it generally like MSF did required a complex solution.
- Happy to discuss my approach with @actualbudget. Uses CRDT-based data that is stored in local sqlite that is query-able with normal sql queries. Seamlessly syncs in background. Uses hybrid local clocks & merkle tries to verify.
  - Yeah, that's roughly the approach I'm using… but jeez, so much complexity—so painful.
- There's definitely space for a this to be abstracted away. imho, the tradeoff of this complexity is a powerful model for features like undo. Worth it for me.
- Founder of @FISSIONcodes here. We designed a file system on top of IPFS
  - Thanks! I'm very excited about the distributed design direction. Unfortunately a file system doesn't quite fit my application model: I'd still need to build a database on top of this for querying/indexing.
- At Quip, we wrote data to a local leveldb bundled with native apps and synced in background using a checksumming mechanism. We had a model layer handled data loading / live updates / mutations & wrote to leveldb on native and sent api requests on web
  - Thanks! I'm using a similar model—leveldb locally, syncing in background. Wasn't clear from this article how you handle conflict-free resolution. Do the handlers all implement associative/idempotent/commutative functions?
    - Actually much simpler. Each entity has a global id and a sequence #. When updates are made, fields are marked dirty by client and changes are sent along with the current sequence. When there are no conflicts, changes are merged, sequence is bumped, new data is broadcasted.

- Abandoned the very general approach for my event sourcing-based model Flushout. Figured consistency requirements are app-specific and can be implemented on top with interceptors or even CRDTs, without incurring their impractical model size for other apps
  - This is a very graceful implementation, suggests event sourcing can be made general and compact. I'll see if I can adapt something like this to my purposes, where the data model is large and I must avoid grabbing a full snapshot except on first run
- Realized models in my side-project apps aren't large enough to really need incremental updates, but get it for free with Flushout if I start saving command history to support undo or history views...

- It’s really difficult. I’ve had success applying event sourcing to the problem, but schema evolution is a pain and it means my data model takes up a lot of my complexity budget
  - Yeah, I'm using event sourcing on a custom transport/storage system now, and it's eating up *way* too much complexity.
- At least for me, the one saving grace is that this is very amenable to TDD and testing in general; easy+fast to replay events and then verify the final state
- **I use event sourcing on @stayinsession based on that article. Helped a lot, and yeah it's really complex. But I don't believe there's other alternative than that approach**. Been researching about offline first for years too.
- In Mintter we have been working on this for more than a year... it is a challenge to ride the complexity

- do you think there's value in non-syncable, non-collaborative "local-first" ?
  - You may be able to separate the DB features from the data sync. Obsidian is just md files that it syncs, but there must be indexes around to speed things up.

- As long as the DB is fully recoverable by replaying the history of change nodes it doesn't matter what the datastore is. Indices are orthogonal side effects of the relevant history of changes / commands.
  - This is totally true, but on a practical level, I've encountered enormous and persistent complexity in the details of constructing and maintaining snapshots by replaying events.

- Tuple/triple stores sync fairly easily

- ## what solutions/libraries exist for real-time server-owned state synchronization?
- https://twitter.com/heyImMapleLeaf/status/1582180994752589824
  - ❌ not firebase or liveblocks. state is controlled and updated directly by client
  - ❌ not socket io or pusher. it's just generic messaging, no handling of state
- My @logux_io was created to sync state via web sockets. 
  - It is self-hosted and very flexible system. You can limit a state control by the server only.
  - It has types for all API. I am specially proud that you can define a one interface for Map and then re-use it between client and server as an API contract.

- ## Toying around with OS level multiplayer...
- https://twitter.com/ronithhh/status/1630733879220011008
- tbh i believe "multiplayer" should be platform level

- ## Today's coding adventure: choose a syncing storage layer for a tech demo I'm working on.
- https://twitter.com/jessmartin/status/1630658249371295758
- When you search for something like this, a bunch of things pop up, some of which I've heard of:
  - LiteFS from http://Fly.io
  - Litestream
  - dsqlite
  - sql.js
  - AbsurdSQL
  - http://vlcn.io
- there's LiteFS which is like Litestream but better. Rather than async writing your sqlite db to some replica, LiteFS actually reads each *transaction* (each change) and stores them and replays them. This allows for cool things like rollbacks since LiteFS has all of history.
  - Now what's wild is how LiteFS pulls this off: they run a separate process that reads directly from the filesystem (using FUSE) to watch the sqlite db (sqlite dbs are just one giant file, remember!) for changes, then nabs them as they happen.
- Q: If a sqlite database is normally stored in a file on the file system and browsers don't have file systems, how does sqlite-wasm store the db?
  - A: local-storage and session-storage, ofc! pretty gnarly limitations: <5mb, strings only, etc
  - 💡 OPFS runs in a worker thread, so it doesn't block the main thread, which allows the UI to be more responsive.
  - opfs只支持worker的api: createSyncAccessHandle(), FileSystemSyncAccessHandle

- One important note about sqlite-in-the-browser: the excellent sql.js has been around for years, *but* it only supports *in-memory* changes to sqlite. No persistence. Refresh 
  - While sql.js does support exporting the database as JavaScript-typed array, that's not what I want. I want streaming replication
- Dqlite is distributed sqlite that is distributing a single sqlite db across a cluster or peers. Also, importantly it runs as a library inside your app, not as a sidecar process watching the filesystem. This would be more amenable(顺从的；顺服的) to the web. Unfortunately, it only runs on C/Linux. There aren't any other client libraries for other languages / platforms. Not sure why this hasn't gotten much adoption...

- ## I find that in distributed systems, metadata size is often inversely proportional to message size.
- https://twitter.com/aboodman/status/1628166157667831808
  - Decreasing message size means increasing message rate. Each message caries less data, but increased rate means more metadata is needed to correctly run and maintain the system.

- ## [请教一下，类似 LOL，王者荣耀， Diablo3 这样的网络游戏，如何同步多机实时的数据？ - V2EX](https://www.v2ex.com/t/763822)
- microsoft Fluid 类似于 CRDT 分布式框架，CRDT 主要无中心服务器，p2p 情况下可以最终一致结果。CRDT p2p 具体应用 聊天 文字协同编辑
  - 游戏服务器是一台中心服务器，中心服务器决定客户端请求先后顺序，广播给其他客户端，没有一致性问题。

- 帧同步、状态同步
  - 帧同步，所有客户端根据服务器下发的逻辑帧（包含的信息是十台设备的操作输入），在客户端演算一遍，输入一致算法一致 所以每个人看到的结果一致，谁延迟高谁吃亏
  - 状态同步：服务器以一定的频率下发各个玩家角色的状态给各个客户端，客户端以服务器信息为绝对真理，努力往这个结果上靠
- wow 是状态同步，客户端下发操作命令，服务器运算操作结果，产生的结果推送到同屏的客户端，如果所有人都在不停的动，服务器负载是人数的平方，70 级的时候屠城只要 7 个团在一个房间内就会宕机，大概 300 人
- war3 是帧同步，客户端下发操作命令，服务器直接推送操作指令给同屏客户端，接收的客户端负责运算结果，要求所有客户端版本相同，不允许跨版本连接。录像文件可以很小，因为只需要记录操作行为，实际结果是录像+客户端共同完成的

- 实时竞技都是帧同步, 每个客户端把当前帧(例如过去 1/60 秒)的动作, 用 UDP 发出去. 而且包得很小, 为了避免做排序重发. 一般都把当前帧和之前的 2(或多)帧放到一起发出去, 还得在一个 MTU 大小内, 避免被拆包.

- ## [Couchdb有在实际生产环境中使用的例子吗？ - 知乎](https://www.zhihu.com/question/20112928/answers/updated)
- CouchDB是HTTP Restful API来操作数据库的，其它数据库系统使用TCP，在传输大量数据的情况下，HTTP协议在TCP协议之上，可能HTTP协议会比数据库自身实现的数据交互协议payload要大，造成网络性能略差

- ## [Ask HN: The state of Firebase alternatives in 2020? | Hacker News](https://news.ycombinator.com/item?id=24843664)
- There really isn’t a competitor. 
- Supabase is trying to combine OSS tooling into a somewhat similar offering but it’s not nearly as feature rich as Firebase. 
  - That having been said, most people use Firebase for real time DB and auth, and Supabase supports that now. 
  - It doesn’t, however, support offline use cases, or any of the advanced functionality of firebase.
- Pouch and couch solve the offline data scenario and live replication, but no auth story and the mapping of users to data is problematic (unless you build a proxy layer, there’s not an easy way to have some data be public, some private, and some shared).
- Realm is paid these days, I believe, and it solves the data replication, but again, no auth.

- ## [meteor: Improve offline support_202110](https://github.com/meteor/meteor/discussions/11656)
  - With Minimongo there is a touch of offline support. This could be taken further and improved. First step most likely being the ability to not loose offline only changes when the app is closed and then improved syncing once connection is restored. The final step possibly being that you could create offline-first Meteor app.
  - There is also Hoodie which uses PouchDB and CouchDB as a pair to achieve this

- ## ✨ [Nano-SQL: Offline use with Sync to Server_201801](https://github.com/only-cliches/Nano-SQL/issues/18)
- Hey gents, I'm getting close to implementing this as a core feature.
- [Here's what I'm thinking:](github.com/only-cliches/Nano-SQL/issues/18#issuecomment-392220931)
  - 1. Implement a conflict resolution feature nearly identical to CouchDB that wo  rks on the client and the server. 
  - 2. Use websockets with ajax polling fallback to allow syncing between client side databases and servers alike. 
  - 3. Include a simple JSON Web Tokens feature in the client/server model with security baked in. 
  - 4. Make three way data binding super simple using the new observer feature
- I don't think we actually include any conflict resolution code, I really like CouchDBs approach 
  - here where if a record is conflicting at all, everything gets saved as revisions of that row and a winner is selected in a deterministic way. 
  - This lets the application developers handle conflict resolution in a way that suits their use case, prevents the build from bloating into hundreds of kilobytes and prevents loss of data.

- One of the "big deal" features for me that I haven't really seen in CouchDB, Gun and many others is a flexible security model, they seem to almost exclusively be all or nothing. 
  - Let me give you a very simple example: a system with blog posts like Wordpress. Everyone should have read capability, but only specific users should have write capability
  - These are the kinds of problems I'd like to solve with nanoSQL's offline/syncing system, and honestly where I've seen many of the existing solutions fall short.
- This is definitely an issue that Gun does not resolve. 
  - CouchDB does this though. 
  - Using a revision history for a document. 
  - In projects I have worked on revisions are kept for historical purposes. And could be used for manually merging or choosing revisions. 
  - So in any storage engine that Nano-SQL uses a revisions table for all changes(or one for each table's changes) could be managed to provide a history. 
  - However conflict determination would need to take place so that we can let the User know if a conflict occurred and let them take action if they are allowed to.

- Unfortunately implementing offline db use and eventual consistency is a fairly complex beast. 
  - Multiple users can have updated the server while you are offline, so the server needs to keep track of this. 
  - The clients need a way of finding out what has changed since they were last online and if there updates are newer, push them to the server. 
  - Deletes also need to be handled. 
  - Couch uses sequence numbers for part of this.
- Some articles etc. which will help here are:
http://docs.couchdb.org/en/2.1.1/replication/protocol.html
couchbase/couchbase-lite-ios/wiki/Replication-Algorithm (maybe out of date)
http://offlinefirst.org/sync
npmjs.com/package/dexie-syncable (possibly what I'll end up using)
share/sharedb
paldepind/synceddb
kinto.readthedocs.io/en/stable
forbesmyester/SyncIt
- Browser/Server communication should be abstracted so either http or websockets can be used. In Clibu I use Websockets.

- yjs. There is a good CRDT implementation that allows 100% synchronisation. 
  - Its used in production and very easy to use.
  - I really think you should look at this, because its a leap frog technology. The way CouchDB and others work is to use the `Last Write Wins` which does not guarantee that all changes on a type ( or datbase row as it were) that are from many offline users does resolve without anyones data being overwritten.
  - 👉🏻 The interesting thing about y.js is that all the reconciliation happens clientside.
  - This means that server side you can either hold the "last know version of a type" or hold all versions known to be out there. You can do either depending on the use case.

- yjs is interesting and works well, however I have several concerns. 
  - The changes stored in IndexedDb etc. appear to grow forever. I posted on Gitter back on Mar 13 and have not had a response. This level of support which just seems to be a single developer is another concern.
- Automerge is impressive but really only suitable for in memory objects. 
  - So for example if you want to merge database doc's for offline use it isn't suitable. 
  - Also I think it's memory use keeps growing with every change. ie. No garbage collection as @gedw99 mentioned.
- hypercore which is part of DAT seems only suitable for synchronizing files, not JS Objects or Database documents.
- Orbit.js
  - I can't see any way to specify/use database indexes. I've written a Gitter post on this. 21 Feb 18
  - It looks like all data is kept in memory which can be backed up to various stores, such as IndexedDB. However I can't see that it is possible to lose the in-memory store/cache and just use IndexedDB?
  - I can't find any documentation on how synchronization works. Latest wins, CRDT ...?  Docs say it can be used to sync editor content?
- I have real trouble thinking of GunDB as a "real" database.
  - To me it is more of a distributed in-memory cache. 
  - It has no query language, no indexes and the entire "DB" is in memory. 
  - Further it is unreliable - see this long outstanding issue
- Another new entrant is TurtleDB, which has very good docs and this article however as it is unusable for my specific use case. It is also an all-in-one library vs. separate independent modules as per your comment.

- There's also an actor based model of sync and state.
  - I can't really write much more about it right now (gotta run) but hopefully I'll remember to later.
  - Here's a project that implements this system http://ceptr.org/projects/holochain#local-source-chain
  - https://github.com/holochain/holochain-proto

- If remote sync is implemented I think it could make Nano-SQL an excellent choice for progressive web apps (PWAs).
- These are some of the alternatives I have evaluated and in my opinion their pros and cons:

- https://github.com/amark/gun
  - An open source cybersecurity protocol for syncing decentralized graph data.
  - GUN is an ecosystem of tools that let you build community run and encrypted applications - like an Open Source Firebase or a Decentralized Dropbox.
  - No support for relationships, join queries nor aggregate queries
- https://github.com/dfahlander/Dexie.js
  - Limited support for relationships and no support of join nor agregate queries
- https://github.com/google/lovefield
  - No remote sync, can use either a local or a remote adapter

- `Dexie.Syncable` the Sync Server just uses Nedb as a quick way to get a sample running. You would replace that with MongoDB or whatever backend DB you wanted so you con isn't relevant here.
- Automerge is indeed impressive however last I looked (and asked) it only works with in-memory objects and isn't durable as @gedw99 mentioned.
- Like y-js I'm also concerned about lack of garbage collection with automerge which could end up consuming a lot of memory if the objects are a reasonable size and change frequently. For example a 5KB Markdown document which was edited 20 times (in a day) would use 100KB + metadata.
- Logux is another library I've been evaluating and not had time to mention before (been travelling) but shows promise. 
  - What I like about Logux, is it is completely independent of the front/backend database. Which `Dexie.Syncable` is largely.
