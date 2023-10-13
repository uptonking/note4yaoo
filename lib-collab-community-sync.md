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

- sync实现要点
  - client发送内容op/patch/changes, 发送时机，接收内容
  - server接收，发送内容

- **partial/selective-sync**
  - sync by table/collection/doc，可参考 pouchdb
  - sync by versionNumber/timestamp
  - 👉🏻 **query-based sync**: 取数基于query，query时可使用各种filter，可参考mongo-realm

- 协作方案参考
  - Liveblocks, synced-store, FluidFramework, gun, pouchdb
  - automerge(2017), yjs(2015), sharedb(2013)

- 成熟的解决方案一般都会设计和公开自己的同步协议
  - database: couchdb, rxdb, 
  - framework: meteor-ddp, feathers-sync, gnu, realm/Atlas-Device-Sync
  - editing: yjs-protocols, automerge-sync

- [Building an offline realtime sync engine references](https://gist.github.com/pesterhazy/3e039677f2e314cb77ffe3497ebca07b)
  - figma, linear
  - pouchdb, fluid, watermelonDB, Liveblocks

- 考虑到客户端升级的问题
  - 同步前一定要检查一个version，参考indexeddb upgrade
  - logux支持客户端不同version

- 支持offline的架构
  - 还可以考虑使用多级缓存，不一定全量数据库，类似react-query + indexeddb
# linear-realtime-sync

## [cs-repeat: linear sync engine__202306](https://www.youtube.com/watch?v=Wo2m3jaJixU)

- 小结
  - 先回顾linear sync engine的架构
  - delta sync的实现细节: partial bootstrap
  - 架构优化
    - bootstrap is slow: lazy load model
    - 分离 sync-server 和 graphql-api
    - graphql-api oom: streaming rest api
    - db bootstrap is slow: add mongodb as cache
    - batch loader

- benefits of sync
  - performance
  - realtime
  - offline
  - less notworking/persistence
  - collab: undo/rebase
  - less backend servers, local-first

- architecture
  - object pool
  - sync-engine builds object graph from object pool
  - object graph reflects business models
  - devs use object graph, not pool
  - use mobx to tie ui to model object, ui auto rerender on model update
- sync-engine not care where changes come from, processing local-change/network-change is the same

- local models are in memory
- when changes happen
  - changes are packed into transaction
  - tr is added to the tr queue
  - tr is persisted on local disk, so works for offline page refreshing/replaying
  - tr will be sent to backend

- view is a representation of object graph
  - if object graph changes, views auto update

- sync-engine goals
  - faster dev/perf
  - sync

- usecase: a new user comes in
  - user has no local data
  - load data from backend
  - clients receives and unpacks json blob
  - client constructs model objects, and build object graph, flush to indexeddb
  - clients load almost everything from server and save it locally
- sync
  - clients connect to sync server using websocket
- transaction
  - a client makes a change
  - not store it local db immediately, for change has not been verified
  - changes are optimistic ui, but not local db
  - make change in memory, create a tr, send tr to server
  - tr is persisted in local db
  - if client goes from offline to online, all tr will be sent
  - if server rejects tr, client will roll back changes
  - tr queue 
  - api will use sync actions to write to backend db table
  - sync server will constantly fetch new sync actions table, and send to valid clients
  - client receives realtime actions from sync server through websockets

- if updated are sent multiple times, it works
  - the second delete wont exec

- linear reads from local db
  - user may have more than local indexeddb, for multiple workspaces or multiple users
  - local db has a hash version, for breaking changes
  - local db contains tables for all model objects
  - id is always key-path, always query by id of model-object
  - value is json blob, contains data of model object, in `json0` format
- there is metadata in tr table
  - the last syncId
  - sync action id is increasing
  - client only cares id greater than itself
- a dev changes a model property
  - the model object is valid
- for schema change, simply delete all the data that is part of the change
  - if it's a big change, the user may wait longer
  - the perf is good, but may be optimized

- delta-sync(27:51)
  - if we do a full bootstrap, we load all the data from server and then connects to websocket
  - changes may happen between load and websocket
  - **client will take the last syncId(like 3000) from local db, send it to the sync server**
  - the sync server will send all server's changes like(3000-5000) to client, query server db, send big blob of data to client
  - client receives sync updates, and do the rest

- 🤔 delta sync may be heavy, if client comes back month later
  - thousands of changes to each model object will be serialized as json and sent when client connects
  - the server wants to be realtime
  - whenever a new client connets, it will pause everybody else's updates and service
  - if the clients has synced, server will continue reading sync actions to others
  - the sync server is not involved in sending delta packets
  - client requests delta sync to graphql api 
- when a client connects, 
  - client will load all data from backend as a full bootstrap, then connects to sync server using websocket
  - client receives sync actions, but **queue them in memory before applying**, just keep adding to local queue
  - while that happening, client makes another requests to graphql api with last syncId, 
  - client receive from graphql api, apply to local db, then flush queue to local db, now client is realtime sync
- this diagram is for the first year, but linear is growing

- 🤔 bootstrap is taking a long time on the client
  - if your org is big, the data is big
- **partial bootstrap**
  - comments are not shown until u navigate to screen
  - client dynamically load model objects
  - lazy collection
    - 类似generator、从缓存读
- if u know the collection is lazy, u can kick off hydration beforehand, or wait for the hydration to happen
  - hydration means going to the local-db/network, u get a promise back, when promise fullfilled, u know everything is hydrated
  - we get suspend boundaries, while hydrating, we render no fallback, just render nothing
  - when hydration finishes, suspense will render the comments very quickly

- optimize serialing mobx on those model object
  - previously we observe all the model objects
  - now we only observe model object when we access them, like finding model object by id, accessing collection

- 🤔 the graph api is slow
  - load most important model objects
  - other model objects are delayed loading
  - if lazy collection is not in local db, wait for promise

- the graphql api is not slow, but crashing with oom
  - we are running out of memory
  - graphql is good for small op, but bad for huge op
  - graphql needs to construct entire response in memory, it cannot stream anything, the response is a big blob having all data present
  - linear workspace uncompressed might be something like 150mb, server has to keep it in memory
- 👉🏻 introducing streaming rest api
  - we add a new endpoint interally
  - client will request to streaming api 
  - streaming endpoint will make a streaming database connection to the database with the big query that contains everything for that user
  - then it streams the response row by row from db to api, and sent to client, so memory consumption is low
  - when client accepts, read data will be removed from memory

- 🤔 full bootstrap is often, db suffers
  - read from the replica, not main database
  - the replica may be late/lag
  - clients requests with last syncId
- we add a new database as cache
  - we tried google gcp bigtable, it turned out mongodb is faster
  - we periodically save all the data in serialized format to mongo
  - we take org by org(if enough changes), we take all the model objects for all the users, we serialize them and put them next to each other so that reads are fast
  - instead of streaming from postgres, we stream from mongodb
  - mongodb's data may be a bit older, but we have all the mechanisms for client to catch up with that data
  - the data we write to mongodb contains the last syncId
  - the streaming endpoints decides to go from mongo or postgres
  - if no dump or too old, it will do it from postgres, and generate the dump at the same time

- we move delta sync to streaming rest endpoint, that goes to postgres
  - delta sync needs to be in realtime

- streaming rest endpoint is a bit slow
  - we add a batch loader
  - we do a partial bootstrap when we load client's data, only the necessary data
  - everything else is pushed to batch loader
  - batch loader is a way to stream data in on demand from network
  - instead of fetching from indexeddb, fetch from batch loader, it will load from indexeddb or streaming rest api
  - batch loader will dedup requests

- lazy-loaded Issue
  - parent: `CachedPromise<Issue>`, if fullfilled, it will has value prop
  - hydrate(): `Promise<Hydrated<Issue>>`, value is set after hydrated

## [cs-repeat: linear sync__202002](https://www.youtube.com/watch?v=WxK11RsLqp4&t=2169s)

- object graph
  - 使用mobx进行state management, 自动更新view
  - object graph支持object reference itself

- object pool
  - just normalize all your data structures into one pool
  - there's one big array of all the objects that represent your entire dataset in your application
- from this object pool, we are able to create this object graph, then pass this object graph to the views
- there are 3 objects in the object pool, but there are 5 objects in the object graph
- in the beginning, the object pool is empty
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
# discuss-partial-sync
- ## 

- ## 

- ## [IndexedDB chunkstore · attic-labs/noms](https://github.com/attic-labs/noms/issues/2602)
- At the moment people use pouchdb and other things to enable offline first apps, but sync back to the server is less than stellar(杰出的) in terms of options, and couchbase is pretty tough to work with IMHO.
  - And lastly i can use gopherjs and bind to the JS NOM OR to the golang noms.
  - I guess you need to abstract a file system into a indexeddb, which is not a huge feat.

- ## [how to to do partial (descending)l sync? F.e. chat messages](https://github.com/pouchdb/pouchdb/issues/8221)
  - Imagine I have chat app, and chat may have potentially million of messages in a room. What is a best practice to sync such a database to web browser? Is it possible to sync f.e. last 1000 messages, then if user scrolls, resync last 2000 messages?
  - As I understand I can achieve this passing query_selector to replicate method, but the question is, will it resync items with sequence_number lower then last sync? I mean will it sync oldest messages after newer message was synced?

- You can use filtered replication

- ## 🤔 [I created PouchDB. After a year... | Hacker News](https://news.ycombinator.com/item?id=24355263)
- I created PouchDB. After a year or so I handed that project off to some great maintainers that made it much better as I had grown a little skeptical of the replication model and wanted to pursue some alternatives.
- It’s been about 10 years, much longer than I thought it would take, but I have a young project that finally realizes the ideas I had back then.
- Sometime after PouchDB was created I realized that it just **wasn’t going to work to replicate a whole database to every client**. 
  - In fact, even a view of the database wasn’t going to work, because the developer isn’t in a position to really understand the replication profile of every user on all of their devices, you need a model that has partial, or more accurately “selective” replication based on what the application accesses in real time.
- I became convinced that the right primitives were already present in git: merkle trees. Unfortunately, git did a very poor job of surfacing those primitives for general use and I wasn’t having much luck finding the right approach myself.
- Shortly after joining Protocol Labs I realized they had already figured this out in a project called IPLD. Not long after that, I started leading the IPLD project/team and then putting together my ideal database whenever I found a free moment.
- It’s very young, lots of missing features, still working on some better data-structures for indexing, but it is very much a database that replicates the way git does and approaches indexing over a primary store the way CouchDB does, but there’s a lot more too.
- With these primitives we can easily **nest databases inside of other databases** (and create unified indexes over them) and we can easily extend the data types in the database to user provided types. Using some of these features it already supports streams of binary data, databases in databases, and linking between pieces of data.

- dagdb /133Star/MIT/202010/js/leveldb/git/inactive
  - https://github.com/mikeal/dagdb
  - DagDB is a portable and syncable database for the Web.
  - It can run as a distributed database in Node.js, including using AWS services as a backend.

- ## [CouchDB 2.1.0 | Hacker News](https://news.ycombinator.com/item?id=14950060)
- If you are looking for something like CouchDB but only syncs partial subsets of the data you request (rather than the whole thing), try checking out gundb

- ## [PouchDB, the JavaScript Database That Syncs | Hacker News_201612](https://news.ycombinator.com/item?id=13101870)
- PouchDB's replication capability is interesting, but is there a way to make it lazy load to the local DB instead of doing everything up front? I hesitate to use it for a web project with 10+ MB of docs where it would otherwise be ideal.
  - You can provide a **server-side filter function** to replication and progressively filter partial replications until eventually everything gets replicated. At that point it becomes a question of architecture of your documents: how much is needed to replicate before a user may be productive?
  - You can also explore **pouchdb-replication-stream** to build bundles that PouchDB can bootstrap from a little bit faster than a chatty replication.
  - That said, I've found initial replications of large databases (one I've worked with this week is a 25+ MB CouchDB database full of photos) is quick enough (and mostly bandwidth constrained) that I haven't had much in the way of concern over it.

- ## [Limit records synchronized in PouchDB/CouchDB - Stack Overflow](https://stackoverflow.com/questions/38834877/limit-records-synchronized-in-pouchdb-couchdb)
- Yes you can, use filtered replication 

- ## [Partial syncing in pouchdb/couchdb with a particular scenario - Stack Overflow](https://stackoverflow.com/questions/39536131/partial-syncing-in-pouchdb-couchdb-with-a-particular-scenario)
- If you take a look at the PouchDB documentation, you should see the options.doc_ids. 
  - This parameter let you setup a replication on certain document ids. 

- ## [Syncable: possible collaboration · dexie/Dexie.js](https://github.com/dexie/Dexie.js/issues/397)
- What my library does is synchronize with the server every couple of minutes but the server is offline most of the time. 
  - I use a timestamp to know what to synchronize and the data update is done automatically, the user does not have to define how to do the update.
- Your use case seems similar to that of Dexie. Syncable - background sync that just happens when online without the user having to think about it. 
  - With Dexie. Syncable, the user is just using Dexie in the same way as if the addons weren't present but Dexie. Syncable will continuously keep the database in sync with the server bidirectionally.

- I want to implement partial data sending but I'm not sure I understood the concept correctly.
  - clientIdentity is essential for the server to be able to buffer uncommitted changes

- ## [Implementing Dexie. Syncable ISyncProtocol · dexie/Dexie.js](https://github.com/dexie/Dexie.js/issues/901)
- As what I recall partial changes are put in an intermediate table named "uncommittedChanges".
  - as I recall, the Dexie. Syncable framework should directly start another sync in case it was part partial so it continues to recieve data until partial is false. Then the framework should commit the uncommitted changes into the db.
- I did implement partial also for server -> client
  - Client sends the latest revision it got from the server. When using partial for server -> client, the server returns only a part of the array and the latest revision is the newest element in the partial array. Next time the client requests data with that revision, the changes are newly calculated. The server also tells the client that it was a partial data set so that the client can immediately request more data.

- ## [🤔 mongodb: Query Based sync support?](https://www.mongodb.com/community/forums/t/query-based-sync-support/5329/2)
- MongoDB Realm currently(202006) only supports full sync.
  - The team is considering how to architect more flexible sync options in future, but there isn’t a specific timeline for this yet

- We are still(202103) a long way away from launching query-based sync 2.0 with a more flexible syncing API. 
  - My suggestion would be to **use partition-based sync** and not wait as we will not have QBS production ready before the legacy realm cloud shuts down.

- [The timing for supporting partial synchronization](https://www.mongodb.com/community/forums/t/the-timing-for-supporting-partial-synchronization/4116)
  - Since it is uncertain when partial sync will be supported, we will move data from the partial sync realm to the full sync realm.

- ## [Partially synced patterns · WordPress/gutenberg](https://github.com/WordPress/gutenberg/discussions/50456)
- [The `wp:pattern` block](https://github.com/WordPress/gutenberg/issues/48458)

- Partially synced mode is different. When a pattern that's partially synced is inserted, it retains a reference to the source pattern. The blocks within the pattern are locked so that they cannot be removed or reordered and new blocks cannot be inserted (this is called contentOnly locking). Only specific parts of the pattern considered 'content' can be edited (denoted by adding __experimentalRole: 'content' to a block's definition).

- The concept of partial syncing could be considered as similar to the way a handlebars, mustache, or other templating system works.
  - For partially synced patterns, I think it's also important that the data (the values of 'content' attributes) is kept separate from the template (the source pattern). This way, the data can be interpolated or injected into the pattern to produce the resulting HTML.

- ## [[Sync] Allow for partial push · Nozbe/WatermelonDB](https://github.com/Nozbe/WatermelonDB/issues/206)
- Three ideas come to mind, from simplest to hardest:
- Just Sync Everything — like I suggested before. 
  - I think in most cases there's just no harm in this, and only benefits.
- Per-collection sync enable — currently ALL tables (except for magic localStorage table) are synced. 
  - I think a lot of apps might have a need for tables for local stuff (needing more complex stuff than LocalStorage provides), so it's reasonable to add a parameter to synchronize() to point to which tables to sync / skip syncing. 
  - This complicates your code, since you'd need to have two classes — one for synced orders, one for draft orders. 
  - But I think you could easily manage it with subclassing (AbstractOrder extends Model; Order extends AbstractOrder; DraftOrder extends AbstractOrder — the first would have most of the common logic, and the other two would just have stuff like publish() etc.)
- New sync status — currently there's created, updated, deleted (local changes waiting to be pushed) and synced (no local changes since pulled). 
  - There could also be draft. 
  - Your app would be responsible for managing such status — as this is much simpler on Watermelon's end and more versatile for apps with different needs. 
  - Needless to say, records would be recognized by client as changed if draft, but would not be pushed until changed to created. 
  - This seems doable, but further analysis is needed. And lots of tests if one was to implement it

- ## [Initial Sync Download · Nozbe/WatermelonDB](https://github.com/Nozbe/WatermelonDB/issues/650)
- My first idea was to limit the sync size to a number of versions (or timestamps as per the default implementation) so it chunked the data. 
  - Once i tried this i quickly realised that i cannot guarantee how much data is between the 2 timestamps/versions as the data may or may not have been added to certain tables, therefore impossible to gauge.
  - So the core of the problem is that there is a risk of passing too much data between a server and a device, so i decided it would be better to calculate the size of the data between 2 versions and store this in a table. version_from	version_to	size

- ## [vlcn: Partial CRR Sync](https://vlcn.io/docs/networking/partial-crr-sync)
- While it is possible to implement partial sync with the primitives available to you today, it is not advised and not supported. 
  - In Q3/Q4 2023 we will be releasing primitives specifically intended to support partial sync, row level security, and large scale multi-tenant databases.

# discuss-solutions
- ## 

- ## 🚀 [Ditto: Real-time sync for apps even without the internet | Hacker News_202209](https://news.ycombinator.com/item?id=32934849)
- since Ditto's replication is "delta-based" it will only sync differences. 
  - Our protocol is designed to overlay on top of custom arbitrary links, including unreliable ones. Not familiar with CCSDS, but we have explored Link16, and even built-in we replicate over BLE GATT.

- 🤔 How is it different than all the open source peer-to-peer sync tools, such as Dat/Hypercore, or PouchDB?
  - We use multihop ad hoc network connections! That’s the BIG thing that we add to the mix!
  - A) PouchDB, Couchbase, Firebase, Realm are all databases that can sync to a "master" node in the cloud.
  - B) AODV and BATMAN are really an ad-hoc mesh networking and routing protocol.
  - Ditto is both A and B. You work with Ditto as a database on your mobile, IoT, web app with common database functions (querying, updating, deleting etc...) and we will sync the changes between edge and cloud devices. Most developers cannot sensibly use AODV and BATMAN to build robust collaborative applications, it's too hard. We abstract all of the routing, network resiliency, and replication away from you; just work with the database

- 
- 
- 

# discuss
- ## 

- ## 

- ## It's astonishing to me how difficult it (still) is to design a syncable local-first data model.
- https://twitter.com/andy_matuschak/status/1393620663257100288?s=12
  - I keep thinking I've found a decent way, then realizing its flaws
- Take Firebase, for instance: it implements offline caching, but that's very different from sync. You have to design a whole replication strategy on top to get something like "a synced file format."

- CouchDB seems like the closest solution, if you can design a conflict-free model. But I spent the last week getting into the details of actually operating a multi-user service, and I am now quite thoroughly spooked!
- I've noticed that a lot of modern solutions to this problem assume that it's viable to read the entire data store from disk into memory on load (and, often, write the entire thing on save)—which I guess is a nice simplifying assumption… but quite limiting!
  - Microsoft sync framework (for all of its flaws) had so much of this solved 10+ years ago but because it’s such a complex problem, solving it generally like MSF did required a complex solution.
- Happy to discuss my approach with @actualbudget :) Uses CRDT-based data that is stored in local sqlite that is query-able with normal sql queries. Seamlessly syncs in background. Uses hybrid local clocks & merkle tries to verify.
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
  - A: 😱 local-storage and session-storage, ofc! pretty gnarly limitations: <5mb, strings only, etc
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
