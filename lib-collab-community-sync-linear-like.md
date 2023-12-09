---
title: lib-collab-community-sync-linear-like
tags: [collaboration, community, data-sync]
created: 2023-12-08T16:02:05.696Z
modified: 2023-12-08T16:02:26.515Z
---

# lib-collab-community-sync-linear-like

# guide

# linear-sync-engine

## 📝 [Scaling the Linear Sync Engine - Linear Blog__202306](https://linear.app/blog/scaling-the-linear-sync-engine)

## 🎞️ [cs-repeat: linear sync engine__202306](https://www.youtube.com/watch?v=Wo2m3jaJixU)

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

## 🎞️ [cs-repeat: linear sync__202002](https://www.youtube.com/watch?v=WxK11RsLqp4&t=2169s)

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
# discuss
- ## 

- ## The last part of @linear that wasn’t already fully real-time - our document editor - is now real-time and collaborative._202312
- https://twitter.com/artman/status/1733419868827828319
- Initially, collaborative editing did not top our list of priorities. The reason was straightforward: issues within Linear seldom necessitated simultaneous collaborative writing.
- However, as we started refining our project management capabilities, the need for collaborative editing became apparent. 👉🏻 Writing extensive product specifications is a collaborative endeavor, requiring multiple stakeholders to engage in editing documents in real-time.
- This emerging need spurred us to implement collaborative editing across all views where editing of larger documents occurs, including issue descriptions.
- This posed unique challenges and demanded specific engineering solutions. A notable feature of Linear is the absence of a distinct 'edit' mode in documents. When you access an issue, the document description is immediately editable.
- This means we needed a system where live updates from other users are visible instantaneously when you navigate to an issue. However, establishing a collaborative editing session demands significant backend resources.
- A backend service must maintain the document's state to synchronize changes across users. To optimize resource utilization, we developed a system that only initiates a full editing session when at least one user is actively editing the document, and another is viewing it.
- 👉🏻 We piggy-back on top of our existing WebSocket connection that we use for regular sync and let the backend know whenever the client is looking or stopped looking at a document and whenever the document receives input focus.
- This approach has resulted in a reduction of about 96% in the number of live editing sessions, compared to a scenario where a session would be initiated for every document view.
- 👉🏻 The core of our real-time editing functionality is powered by Yjs, a CRDT framework. It enables the transmission of updates from clients to the backend via our existing WebSocket connections.
- Given our distributed backend infrastructure, we had to ensure that updates from clients connected to different sync servers would also be synchronized across backend servers using PubSub.
- All updates are also stored in Redis to enable new servers getting up to speed when joining an editing session. Additionally, the backend periodically saves changes to our database, ensuring that users outside the editing session receive updates through our sync protocol.
- Live editing is an enhancement and there should be no data loss even in the hypothetical scenario of our live editing systems are experiencing a total outage.
- Each client, regardless of whether they’re part of an editing session or not, operates as if they were the sole editor, periodically syncing changes to the server using our standard sync mechanism.
- Instead sending the content of the entire document as we did before, we now only send changes in CRDT format to the sync backend. The backend can thus can receive updates from multiple clients and merge them into the existing document conflict-free.
- This approach also allows clients to work offline and later merge their changes seamlessly into the server, preserving the integrity of concurrent live editing sessions that happened in the past.
- Finally, we needed to address API users. Unlike client applications that send CRDT updates, API send the entire document content, which would effectively overwrite any changes made by lived editing users.
- To circumvent this, we diff the document received via the API to the current version and compute the minimal necessary updates to achieve that state. For instance, adding a paragraph via the API results in appending a line rather than replacing the entire document.
- These update will then seamlessly integrate with ongoing live editing sessions.

- ## When we started work on @linear , we felt real-time sync was a core functionality we had to invest in from the get-go. _202208
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
  - 👉🏻 Data access in most places is already async and the sync client has three tiers of data: in memory, local database and network. Client code is agnostic to where the data is coming from. Was a a lot of work, but that’s really the scaling story.
- Do you think it could work for an app with much more content, for example something like Notion or Confluence? Could be difficult to maintain a full copy of everything on every device, especially on smartphones. Same problem as hit monorepos  too big to be cloned.

- It turns out that a sync engine is actually a much more general solution because of functional purity and managed effects. Essentially you move all the effects (async calls) into the sync engine service layer.

- 🤔 when will linear open source the react-query for sync?
  - Haha there are also a lot of other options: replicache, http://convex.dev, http://clientdb.dev, a new one called aphrodite
- No wonder! Sync is hard, but having it simplifies a lot!
