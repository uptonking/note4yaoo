---
title: lib-collab-community-sync
tags: [collaboration, community, synchronization]
created: 2022-11-29T20:41:00.894Z
modified: 2022-11-29T20:41:25.566Z
---

# lib-collab-community-sync

# guide
- sync-xp
  - 基于缓存实现sync有点类似于react-query
  - 参考vlcn

- 协作方案参考
  - Liveblocks, synced-store, FluidFramework, gun, pouchdb
  - automerge (2017), yjs (2015), sharedb (2013)

- 成熟的解决方案一般都会设计和公开自己的同步协议
  - database: couchdb, rxdb, 
  - framework: meteor-ddp, feathers-sync, gnu, realm/Atlas-Device-Sync
  - editing: yjs-protocols, automerge-sync

- [Building an offline realtime sync engine](https://gist.github.com/pesterhazy/3e039677f2e314cb77ffe3497ebca07b)
  - figma, linear
  - pouchdb, fluid, watermelonDB, Liveblocks

- 考虑到客户端升级的问题
  - 同步前一定要检查一个version，参考indexeddb upgrade

- 支持offline的架构
  - 还可以考虑使用多级缓存，不一定全量数据库，类似react-query + indexeddb
# linear-realtime-sync

## [linear sync 分享_202002](https://www.youtube.com/watch?v=WxK11RsLqp4&t=2169s)

- object graph
  - 使用mobx进行state management, 自动更新view
  - object graph支持object reference itself

- object pool
  - just normalize all your data structures into one pool
  - there's one big array of all the objects that represent your entire dataset in your application
- from this object pool, we are able to create this object graph, then pass this object graph to the views
- there are 3 objects in the object pool, but there are 5 objects in the object graph
- in the beginning , the object pool is empty
  - somewhere stream data into the pool
  - find team id in object pool, update user will update team, 在model层实现
  - object pool里面的对象大多是扁平的
  - object pool里面对象删除后，也会删除object graph对应的对象
  - object pool里面的crud都会自动更新object graph，然后自动更新view

- transaction queue
  - view触发的changes先在前端执行，然后才发送到后端
  - 如果后端accept change，因为前端已执行，就不返回数据信息
  - 如果后端reject change，因为冲突、权限等原因，transaction持有旧数据，可以用来回滚，此时界面可能有闪烁
- realtime sync更适合后端不拒绝的场景，这样回滚闪烁会较少
  - 前端先乐观更新
  - figma team实践出的结论也是这样的

- backend to frontend
  - backend has a queue of all the changes made to the database
  - backend broadcast changes to clients
  - 客户端的change会发送到后端，后端会发送给其他客户端

- optimization： object store
  - 在前端持久化数据
  - every change from backend gets stored locally in the indexeddb
  - clients reload/刷新时，不会从后端请求数据，而是在启动时先从本地idb构建object pool, 然后再连接到后端，后端再发来数据
  - 如果离线时间过长，后端发来的数据就较多，此时前端已经展示数据了
  - transactions也是这样，本地也持久化了所有transaction，刷新客户端时，会更新objects和transations
- 支持offline mode，恢复在线后，本地持久化的transactions会被发送到后端

- entire workflow(01:07:45)
  - 启动时从local db创建object pool
  - 根据decorator从object pool创建object graph, render view
  - 更新issue时，通知object pool属性更新了, create transaction 发送到后端，后端发送给其他客户端进行同步更新object pool

- 客户端更新数据很简单，类似setState(newData)，sync engine会处理同步、持久化、冲突等问题

- discussions

- 离线冲突的问题
  - 默认last-write-win
  - 更多是业务逻辑问题，而不是技术问题
  - 在linear llw可以work，但在groupon的交易冲突时会提示用户选区版本

- ## When we started work on @linear , we felt real-time sync was a core functionality we had to invest in from the get-go. 
- https://twitter.com/artman/status/1558081796914483201
  - It turns out sync was important, but not for the reasons we thought.
- Our gut feeling was that real-time updates were required from a modern tool like Linear. Who wants to refresh to see the latest data? But how often do you find yourself in a situation where multiple people update data simultaneously in a project management tool?
  - Not that often, it turned out. Aside from special cases where your team gets together to operate on data - like planning your next cycle - edits are made across the entire dataset, with the same data being touched at the same time relatively infrequently.
  - 👉🏻 Don’t get me wrong, we still believe that real-time sync is essential, 
  - but there are two more valuable things we got out of real-time sync that we did not appropriately anticipate: **App speed** and **Ship speed**.
- Amen! Noticed the same while working on http://syncedstore.org and yjs; being forced to really separate the data layer for sync comes with many additional benefits (local first, pluggable storage, dev speed etc)

- 👉🏻 The most straightforward way to implement real-time sync is to load the entire app state and then keep it up-to-date with real-time changes. 
  - While we’ve had to add complexity to this simple initial implementation to support larger workspaces, the core tenant/tenet still holds.
  - Clients have the vast majority of their workspace data stored locally. Hence page loads are all but eliminated. As a result, startup times are fast, filters work instantly, and there are no page loads.
- So how well do you handle large workspaces now?  When I first talked about to you about the impl I always wondered what the design would end up being for large corps.
  - We do handle them pretty well, at least from the realtime sync aspect. A few more major changes and then we can pretty well scale to any kind of company size while keeping sync active for the data you are usually interested in.
- I’m curious to know if you are planning to modify the engine to improve the experience for large workspace, the current architecture of loading all data doesn’t seem to scale. Would loading only a subset of the data break the nice abstraction that the sync engine seems to give?
  - 🤷🏻 no answer yet
- How do startup times stay fast when loading the entire state to the client?
  - We first load data that you’ll immediately need, and then selectively stream in data that your likely to access next. And results are stored, so only the first load will be a bit slower.
- Noted, thank you. Do you store on localstorage, so the next full load will be faster? Or by first load do you just mean first request in the browser lifecycle?
  - We store the users dataset in IndexDB, which is really the only viable option, yet is not very good for relational data.
- 🤔 But what if the size of the data gets really large? Like the data from many years… Is still everything loaded into the local storage?
  - No. When the dataset gets larger we selectively preload only the data your likely to access into the local database, and the dynamically load data that you access outside of this dataset.

- But arguably even more essential and surprising was that real-time sync helped us ship new functionality much faster than regular architectures. How? By eliminating a vast swathe of complex and error-prone code.
- 👉🏻 Sync automatically takes care of generating API calls, creating transactions, applying them on the backend, handling conflicts and errors, reverting erroneous changes, rebasing in-fight changes, and offline capabilities.
  - To create a new feature as an engineer, you essentially render and modify local in-memory data structures to build new functionality. 
  - All the complexity that comes with requests, conflicts, network errors and retries are handled by sync for free.
- All UI code automatically re-renders when the data that they accessed updates. Whether the data changes come from the user or the network doesn't matter. So you get multi-player for free, too.
- As you can imagine, reducing the number of layers engineers have to work on dramatically improves the speed at which we can ship new functionality. After experiencing this architecture at scale, I'm spoiled for life.
- For a pretty old - but still relevant - talk on our sync engine, check out

- Linear is great! What did you use specifically for sync and did you roll out all the reconciliation code yourself or did you leverage other tools?
  - ws for sockets, and idb to make working with IndexDB a bit more pleasant, but other than that it’s a custom solution.

- 🤔 How do you see this scaling down the road? You mentioned some modifications for larger workspaces. I suppose there are a lot of assumptions built on top of the current sync engine. If you need to radically update it in the future, wouldn't that force a huge client re-write?
  - Data access in most places is already async and the sync client has three tiers of data: in memory, local database and network. Client code is agnostic to where the data is coming from. Was a a lot of work, but that’s really the scaling story.
- Do you think it could work for an app with much more content, for example something like Notion or Confluence? Could be difficult to maintain a full copy of everything on every device, especially on smartphones. Same problem as hit monorepos  too big to be cloned.

- It turns out that a sync engine is actually a much more general solution because of functional purity and managed effects. Essentially you move all the effects (async calls) into the sync engine service layer.

- when will linear open source the react-query for sync?
  - Haha there are also a lot of other options: replicache, http://convex.dev, http://clientdb.dev, a new one called aphrodite
# discuss
- ## 

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
  - A: 😱 local-storage and session-storage, ofc! pretty gnarly limitations: <5mb, strings only, etc
  - 💡 OPFS runs in a worker thread, so it doesn't block the main thread, which allows the UI to be more responsive.

    - opfs只支持worker的api: createSyncAccessHandle(),FileSystemSyncAccessHandle

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

- ## [Nano-SQL: Offline use with Sync to Server_201801](https://github.com/only-cliches/Nano-SQL/issues/18)
- Hey gents, I'm getting close to implementing this as a core feature.
- [Here's what I'm thinking:](github.com/only-cliches/Nano-SQL/issues/18#issuecomment-392220931)
  - 1. Implement a conflict resolution feature nearly identical to CouchDB that works on the client and the server. 
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
