---
title: pattern-local-first-community
tags: [community, local-first, pattern]
created: 2022-03-03T18:19:36.049Z
modified: 2023-09-13T20:24:41.516Z
---

# pattern-local-first-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔 Is it wrong to build all blog content into a SQLite database that you ship alongside your blog and access serverside via RSC
- https://twitter.com/steveruizok/status/1711466753711128633
  - So my situation is: I have a bunch of markdown files with frontmatter (section, category, order) and some authors and sections and categories. I’m currently parsing them all and putting them in a big json blob that I can pull from on the server
  - It’s more than good enough, but it’s quite big (>5mb) and likely to grow as more content gets added. And it seems like a good excuse to learn some sqlite
  - update: its fine and it rules actually
  - I could probably do the same for search / chat bot with a vector database right?

- it's a really good pattern, particularly if you then serve the blog from an edge platform. @simonw coined the term the "baked data architecture" for this.
  - [The Baked Data architectural pattern](https://simonwillison.net/2021/Jul/28/baked-data/)
- The more I use this pattern the more I like it! My https://til.simonwillison.net site is a blog served directly out of a SQLite database on Vercel - code here: https://github.com/simonw/til
  - I'm not using edge functions, it's on regular Vercel functions - I don't know if edge functions differ in a way that would cause it not to work 
  - **The DB file is treated as if it was a code file and uploaded as part of the deployment**

- Why building the content? :) **You could have SQLite as the source of truth for content**. We've used that approach for http://postowl.com.
  - Aside from that, I think SQLite can also serve as a cache instead of SSG

- Only downside is lack of diffs/binary format. Not sure it’s better than MDX + frontmatter.

- I don’t know about RSC. But Kent C Dots uses SQLite for his site
- Just did this for my personal blog! The ergonomics are amazing and no longer have to fumble with all of this unstructured data

- it’s good imo. you don’t need a managed database for something a file can do
- Sounds similar to how we serve mdx. Except we use files instead of Sqlite.
- For me it works to redeploy my static blog on every change

- A couple markdown files, totally fine. 1000s of markdown files, no please, data is really expensive in some parts of the world.

- Sounds like you just want query engine  on top of your blob. Maybe some json based query is fast enough or maybe you want to put only some parts of the data into the database. I generally like jsons, so not sure you got reason to pump it all into sqlite

- ## what's the Component-level big idea for local first apps? 
- https://twitter.com/threepointone/status/1691454722518208513
- Lots of cross over between local first and server side components, ie writing sync code that talks to your db rather than doing fetches by hand. 
  - See @geoffreylitt ‘s awesome talk on **riffle** here
- yeah, i think there's a big idea lurking which is basically like: at its best, local-first makes writing your app feel like php in a good simple way, but with a great modern UX
- I think this direction is actually a _red herring(熏青鱼；转移注意力的话题；与事实不相干的论点)_. 
  - After heading down that path, I realized that local-first is just a normal app with a fast network.
  - Inevitably, you want to separate the render and main processes so you’ll be caching data in the render process after all…
- I think this is what limited riffle as well, that every query blocked the main thread. Gotta go fast!
  - Yeah (riffle)we’ve kept everything in render process for now. Has gotten us surprisingly far. Solves many problems, creates lots of new problems :) Probably will need a more split architecture eventually, but I still believe in keeping things synchronous as much as possible
- I did something something similar using Electron with `nodeIntegration: true` . Then you can use SQLite directly in the renderer process.
  - I really liked how it simplified your performance analysis. Everything has to fit in a single frame and can happen in a single call stack.
  - It reminds me of game development. Because in a game, everything HAS to happen in a single frame. And you have to work with that performance constraint so you don’t have very complex queries.
  - But I’m a productivity tool with dynamic queries, that’s going to be an issue…
- The _final straw(终于导致失败(或垮台)的因素)_ for me was the security model. 
  - If your app is using the internet, the lack of process isolation is really scary from a security perspective.

- Most apps we use nowadays are cloud-first apps which mostly become useless when:
  - there is no stable internet connection
  - the service is offline or discontinued (h/t Google)
# discuss-big-data
- ## 

- ## 

- ## 

- ## 🔁 One of the local-first killer features is automatic data syncing.
- https://twitter.com/schickling/status/1766011500018237879
  - Similarly how React freed developers from manual view rendering/maintenance, local-first sync engines free developers from manually fetching and pushing data.
  - This unlocks global reactive data.

- 🤔 How does it handle a large amount of data? For example, for all of the issues of one company in GitHub or something similar, there will be a bottleneck with the first initial sync, right?
- We (as in the local-first community) are still trying to figure out the best practices for this, but there are a few different approaches to handle this.
  - You could for example break up your entire application data into "semantic buckets" (e.g. for GitHub per repo) and then prioritize syncing what you'll need for a given UX use case. 
  - Sometimes this is referred to as partial syncing but you could also model this in a hybrid cloud/local-first way.
  - Definitely a key challenge that needs to be explored further. That being said, there are many, many apps where this is a non-issue.
- I'd argue that those "extreme cases" might not be ideal fits for local-first software as of today

- A nicer example would be a Wiki scenario where local-first would still be a vast improvement. Greedy sync top n nodes incl. edges, lazy sync beyond that. Always persist when nodes were written to by the current user. Purge read-only by LRU.

- The thing that made local-first really click with me was when I realised that solving the data syncing problem is 95% of the work needed for real-time multiplayer.
  - Only difference between offline eventually consistent sync and realtime multiplayer is latency.
- Also 90% of crud backends. You end up with a permissionslist and db-triggered side effects
  - Yep, the permissions side is one of the key parts of what we're building with @ElectricSQL , with CRUD being a big part of our target market. I've built a few demos using event-sourcing from PG triggers, it works really well, and has great DX.
# discuss-pm
- ## 

- ## 

- ## Why can’t the killer category for local-first be e-commerce?
- https://x.com/bidah/status/1801960144089026714
  - Why all revolves on SSR as the fastest experience when it’s not?
- The only piece that is consistently local-first in e-commerce is the shopping cart experience. For the rest of the experience, i.e. browsing content, you wouldn't get that much benefit from client-side storage tbh (coming from a local-first evangelist)
- e-commerce tends to be short sessions where most users never come back. less benefit of upfront cost of syncing - even with partial progressive sync it’s just different user behavior
  - Right. Maybe native mobile that tends to get already  that initial load cost be a good candidate for local first ecom instead of the web.
- Just because local first solutions never solved the two biggest problems: automatic partial sync, and small bundle size. Most today sacrifice both, or at least one. But ecomm and most sites need both.

- ## 不要用导出微信读书笔记之类的浏览器插件, 可能会被判定为爬虫违规抓取内容，会封号的。最近看到几个封号的分享了。
- https://twitter.com/plusyip/status/1751450228656582752

# discuss-local-vs-server 🆚🏘️
- ## 

- ## 

- ## 

- ## 下半年的 LobeChat 2.0 ，我就准备来一个巨大的跃迁，删掉 2023 年 0.x 时期的探索性产物和废弃代码，全面转向 服务端 db 为核心的架构 _202508
- https://x.com/arvin17x/status/1953657427070443828
- 建议做成一个可选项，当时在做快速demo的时候只有lobe的前端db符合需求，其他的都是成本太高。如果这个feature放弃，这部分人就要转向其他方案了。
  - 前端 db 还会有的，只是不是默认方案了，要通过环境变量开启，docker 也会提供
  - Desktop有本地db ，也可以连接云端

- 还支持本地使用吗。
  - 当然支持
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Got an idea for naming offline sync modes:
- https://x.com/oleg008/status/1927701855808999455
  1. Offline-first – Your app needs to sync all data to work; full offline guarantee.
  2. Offline-second – Your app syncs only the initially necessary data. It will sync on a "need-to-have" basis. There's no guarantee all data is available offline, but the app generally works offline.
  3. Offline-third – Your app can temporarily lose internet access, and what you’ve been working on remains available. It will attempt to sync once you're back online. Only partial offline functionality.

- ## 🤼🏻 Eventually, I'd like to write a talk titled something like "Critical problems with local-first " _202410
- https://x.com/jlongster/status/1851261217580466491
  - I'll just go ahead and say it: I don't think it's the future anymore. 
  - It's cool for some very specific apps (obsidian for example) but most things shouldn't build around it.
- https://x.com/jlongster/status/1851993194583527902
  - I truly do support people building new libraries and databases
  - but let's be honest: it's going to be really really hard. You're crazy if you start a new company and bet the whole thing on a brand new library/db build buy one or two people
  - a smart strategy is to be as compatible as you can with the mainstream stacks, i.e. SQL should be your interface. imagine a user transitioning away from your product and onto a normal stack and make that as easy as possible. that's the best way to build trust

- That's (almost) what I say all the time. Local-first isn't for everyone. Offline first, maybe, but not local-first—not now, maybe never. That's why I focused @evoluhq on strictly limited use cases where privacy and independence are essential.
  - By the way, I'm close to completing the redesign of the Evolu sync. MerkleTree was nice, but it does not scale and is not very efficient. But it did its work and was honest work. Thank you for that. It helped me to start with something.
- What are you re-designing too? I was always worried about the MerkleTree approach and avoided it but that was probably a premature optimization. Nice to see it has gotten you so far.

- Local-first is not against authoritarian rules but rather to provide an alternative to them if someone wants to.

- How about own your data first. I am amazed how the world is feeding AI with data petrol just because:) I use Obsidian with my NAS. No problem sharing and collaborating.

- ## 🤔 [A Local-First Case Study | Hacker News _202410](https://news.ycombinator.com/item?id=41712593)
- I had thought that the advantage of CRDTs was you do not need a centralized server and that if you do have a central server Operational Transforms are easier. Am I missing why CRDTs are used here?
- A few thoughts on this:
  - First and (maybe most importantly), WebRTC in browsers requires a central server for signaling. So unless web browsers loosen that constraint, a "true" P2P web app without a central server is unfortunately infeasible(办不到的；不能实行的).
  - My understanding is that with Operational Transforms, the server is "special" — it's responsible for re-ordering the clients' operations to prevent conflicts. I mention a little later in the article that Y-Sweet is just running plain Yjs under the hood. So it is a central server, but it's easily replaceable with any other instance of Y-Sweet
  - Peers will only sync their changes if they're online at the same time. That means that the longer peers go without being online simultaneously, the more their local documents will diverge. From a user experience point of view, that means people will tend to do a lot of work in a silo and then receive a big batch of others' changes all at once — not ideal! Having a "cloud peer" that's always online mitigates that (this is true for any algorithm).
- The ability to run your own server--or even not requiring a bespoke set of operations--isn't a special property of a CRDT; the same thing should be doable with something like ShareJS and it's generic tree/JSON structures.
- You’re right, that is one of the advantages of CRDTs, but it turns out to be hard to realize on the web — aside from RTC (which has its own dragons), you still need a server in the mix.
  - The other thing an authoritative server solves is persisting the data. Because one server is the authority for a document at a time, you can use S3 or R2 for persistence without worrying about different servers with different versions of the document colliding and erasing each other’s changes.

- OT would work fine to make this collaboratively editable. It’s just not local first. (If that matters to you.)
  - With an OT based system like sharejs or google docs, the server is the hub, and clients are spokes connecting to that hub. Or to put it another way, the server acts as the central source of truth. If the server goes down, you’ve not only lost the ability to collaboratively edit. You've also usually lost your data too. (You can store a local copy, but sharejs not designed to be able to restore the server’s data from whatever is cached on the clients).
  - With Yjs (and similar libraries), the entire data set is usually stored on each peer, the server is just one node you happen to connect to & use to relay messages. Because they’re using Yjs, the author of this travel app could easily set up a parallel webrtc channel with his wife’s computer (in the same house). Any edits made would be broadcast through all available pipes. Then even when they’re on the road and the internet goes down, their devices could still stay in sync. And if the server was somehow wiped, you could spin up another one. The first client that connects would automatically populate the server with all of the data.
  - But whether these local first characteristics matter to you is another question. They might be a hindrance(阻碍物, 妨碍) - for commercial data, centralisation is often desirable. I can think of plenty of use cases where replicating your entire database to your customers’ computers (and replicating any changes they make back!) would be a disaster. It depends on your use case.

- A lot of the newer local first systems, like Triplit (biased because I work on it), support partial replication so only the requested/queried data is sent and subscribed to on the client.
  - The other issue of relying on a just the server to build these highly collaborative apps is you can't wait for a roundtrip to the server for each interaction if you want it to feel fast.
  - The best approach IMO (again biased to what Triplit does) is to have the same query engine on both client and server so the exact query you use to get data from your central server can also be used to resolve from the clients cache.

- ## 怎样将保存一个完整的网站到本地？
- https://x.com/vikingmute/status/1839845550650536012
  - 直接使用页面另存为会有非常多的问题，主要是静态资源的问题，比如图片不显示等等。
  - 方案一：找到一个开源库 SingleFile
  - 方案二：原帖中的一段 Gist 代码，https://gist.github.com/markflorkowski/4269bc529324dceb2858c77b7609704c
我看了一下处理：使用FileReader 读取，external css 转换成 inline，并且修改地址到 absolute，图片转换成 base64 images。

- ## [Local First, Forever | Hacker News _202406](https://news.ycombinator.com/item?id=40786425)
- I think an important requirement for making the "forever" aspect of local-first possible is to make the backend sync server available for local self-hosting.
  - If there's an app-specific backend sync server it's not going to be "forever." Why can't syncing data be commodified via a dumb cloud that just syncs blobs? If you want privacy locally encrypt everything.

- https://remotestorage.io/ was a protocol intended for this. IIRC the visison was that all applications could implement this and you could provide that application with your remotestorage URL, which you could self host.
  - I used remoteStorage.js for a while for an app, but the JS SDK was too limited

- The thing about local first syncing options like this is that they mostly do not work on mobile. For example iPhones cannot handle dropbox syncing random text files in the background as a regular filesystem for an app to deal with.

- Matthew Weidner's blog post has been enlightening. When a centralised server is involved, CRDTs and OT are merely optimisations over server reconciliation so yes CRDTs aren't always the best approach. It is a compelling approach for text editing though.

- ## The more I play with local-first tech, the more I question everything for web apps.
- https://x.com/BHolmesDev/status/1827482864176206231
  - “Why not SSR?” - So you can boot up state from Indexeddb instantly without waiting
  - “Why not RPC actions?” - So you can write to Indexeddb instantly without waiting

- I already use CSR with react for everything behind a login and SSG with Astro for everything static/SEO. Adding SSR would only save some requests at the cost of increasing complexity.

- ## Tech stack doesn't matter but the user experience does matter. 
- https://x.com/karrisaarinen/status/1796992391834206518
  - "...but local-first is slow to open": Opening up our 5yo @linear workspace with 50k issues
- Linear team is just goated.

- ## "Distributed versus coordinated collaborative editing" has the same distinction as local-first and offline-first architectures.
- https://twitter.com/evoluhq/status/1787513314269934014
  - Local-first isn't (yet) for everyone, and it will not be in the next few years, at least. A lot of ephemeral data doesn't have to be stored forever. Storing data forever is expensive, as is E2E encryption. Having no central server is even more expensive.
  - Long story short, local-first is expensive and should be used only for precious data.

- ## 我很怀疑 local-first 软件在文件数量大了之后的易用性，如果不限制空间大小的话，对用户和服务商来说都是很大的负担，你能想象一个永远全量下载的云盘么
- https://twitter.com/kk_shinkai/status/1768454538259001723
- Git 大多数文件都是纯文本吧
- 感觉这和 local-first 也不太一样，local-first app 都是会在每次启动的时候自动把所有数据同步到本地的，Git 得用户手动控制，和云盘的逻辑更像一点

- GitHub 其实已经意识到这个问题，而且已经做了一些改进。目前的 GitHub Actions/CI 应该都用上了。 
  - 不过这也使得 Git 变得更像 SVN，感觉 Linux 内核那边不会接受。毕竟违反了 Git 分布式/没有 center control 的设计目标。
  - [Get up to speed with partial clone and shallow clone - The GitHub Blog _202012](https://github.blog/2020-12-21-get-up-to-speed-with-partial-clone-and-shallow-clone/)

- 这种 local-first 感觉更好的例子是比特币，每个矿工都要下载完整的区块链/账本，以抵御 51% 攻击。

- ## if your app implements optimistic-ui, fully functioning for reasonable periods of network loss, with automatic retry and exponential backoff, how would you handle request failures?
- https://twitter.com/WarrenInTheBuff/status/1753204757013946581
- server single source of truth. next request is reconciliation

- It depends on the use-case
  - revert the item to a draft state 
  - show an error as a notification
  - pop up a modal if it needs to resolve now
  - sometimes you can just mark it as failed and allow them to browse failed jobs + retry manually 
  - success is default case, no extra work

- ## 几个月后，我觉得我没有开发local-first的笔记App的必要。天下没有免费的午餐。
- https://twitter.com/himself_65/status/1745342123421978982
  - 理想情况下，CRDT可以放入任何情况，比如数据库，甚至是渲染DOM
  - 更具体地看，CRDT的开发体验远比其他技术差。其他技术，比如如SSR或React中的RSC。至少你可以给用户看之前看到报错；
  - 对于这样的local-first CRDT App，App发布到客户端之后，一切都将是未知的。无法想象出客户端的某个边缘情况会导致整个应用程序崩溃。我觉得可能是因为传统的本地优先应用程序（如PWA）在客户端运行代码，但数据仍在服务器上；开发者仍然会知道数据上发生了什么（如果你觉得UI=f(data)对的）。但对于CRDT来说，数据的源头和结果都在客户端，即使UI = f(data)是正确的，你有f，但你不知道输入，你得到一个错误的UI。我们应该如何枚举错误呢？
  - 当然有解决方法：加更多日志，做更多备份，做更多监控...... 然后就遇到了性能问题，所以这就是我觉得的的没有免费的午餐。
  - 我仍然相信CRDT在许多情况下是非常有想法的，更有意义（如绘图，笔记）。但这并不涉及更一般的情况，也不意味着用户会关心它。

- 主要问题是用了CRDT比较好融资

- ## The state of the offline-first ecosystem is incredibly depressing._202312
- https://twitter.com/oofdere/status/1735090979647160471
  - Closed source tools: Replicache, Ditto, etc.
- "Open source" tools: There *are* open-source client-side databases with sync support, but they're locked into a closed/shared source sync ecosystem. Examples are MongoDB Realm, which doesn't sync without Atlas, and Couchbase Lite, which doesn't sync without Sync Gateway.
- CouchDB and co.: So much wasted potential here. There used to be so many ways to sync with CouchDB on the client: Couchbase Lite used to support it, IBM had an open source sync layer for it, PouchDB still supports it but good luck even importing it in a modern Vite+TS app.
- RxDB: This shit deserves its own category. Like, come on, charging for SQLite and IndexedDB? Really? 

- ## Provide a better user experience by making your app offline-first:
- https://twitter.com/dannymoerkerke/status/1719285753677512849
  1. cache all assets
  2. make sure network calls are deferred when offline until back online (background sync)
  3. make sure downloads are continued in the background when the app is closed and deferred when offline (background fetch)
  - Start by adding a service worker.
  - [How To Make Your Website Work Offline | by Danny Moerkerke | ITNEXT_202003](https://itnext.io/how-to-make-your-website-work-offline-b5be47b92adc)
  - [How To Make Your Website Work Offline part 2 | by Danny Moerkerke | ITNEXT](https://itnext.io/how-to-make-your-website-work-offline-part-2-6923b9038dd6)
- This is the direction frameworks should be taking, not further reliance on a server for UI like RSC. Vercel is trying to convince everyone server rendering is the right direction, because Vercel sells time on those servers.
  - Exactly, the future of web apps is installability, not workarounds for problems those frameworks created.

- How do you work with cache when the content changes? Take static JSON as an example... Would you change name at every update? Append a version number as a query parameter?
  - You can use different strategies like networkFirst or staleWhileRevalidate

- "Deferring" network calls until online sounds easy on paper but requires basically a complete rearchitecture of most applications. It's not realistic and it counterproductive to make such sweeping statements. Most apps are fine with just showing a "you're offline" message.
  - Let me then add that network calls should be deferred when offline where it makes sense, for example when sending a message. When offline you can store the message in IndexedDB for example and send it when the network is back. This doesn't have to be hard with background sync.
- This is what I mean, once you start putting things in IndexedDB now you have to add a synchronization protocol, add UX to show users if something failed or the server rejected the message for whatever reason. What happens if user logs out and in again? Etc. It's a huge task.
- With the Background Sync API, the mechanism is already there
- You still have to handle UX for many error states this can end up in and you still have to handle login/logout in a privacy friendly way. And it doesnt' work on ~half of mobile devices. I'm building a local-first app right now! Sometimes it makes sense, but mostly not.
- dev.to is just one of the better documented cases of failed ServiceWorker adoption. People mostly broadcast their successes, rarely their failures. I've come across a lot of SW moaning over the past five years. I attribute that to lack of familiarity.

- ## The three main approaches people are taking with local-first are:
- https://twitter.com/kylemathews/status/1701663361145135126
  - crdt datatypes: replicated data structures like yjs and Jazz w/ js data types that sync
  - crdt+table: Replicated Database Tables that sync Postgres to SQLite in client
  - The unique "Replication as a Protocol" approach Replicache is taking
- The tools really shine for real-time, multiplayer, and offline use cases.

- Also replicated DB like CouchDB and Couchbase has had for years

- 
- 
- 

- ## ✨ [Show HN: ElectricSQL, Postgres to SQLite active-active sync for local-first apps | Hacker News _202309](https://news.ycombinator.com/item?id=37584049)
- Conceptually sounds like this is what Firebase, Couchbase Lite, and Mongo Reach do in the NoSQL world.

- 🤔 I want to be able to have a Postgres database as the central source of truth for all data and user accounts, but then have each users private content to be siloed and synced to their own SQLite database which they alone have access to. Is this possible with electricSQL?
  - This is the exact pattern we target. Drop Electric onto an existing Postgres data model and use the Shape-based sync to manage dynamic partial replication of subsets of data between central Postgres and local SQLites: https://electric-sql.com/docs/usage/data-access/shapes
- This is also the pattern targeted by PowerSync (disclosure: co-founder) — selectively syncing scoped data for the user from Postgres to their own client SQLite database. Sync Rules are used to define which data is synced to which users: https://docs.powersync.co/usage/sync-rules

- 
- 
- 
- 

- I'm looking forward to trying this out. Currently I get this functionality by using PouchDB on the client with a CouchDB sever. Then on my API server I have some janky code in a cron job to sync changes from CouchDB to PostgreSQL.
  - Hey, I work at Electric, The CouchDB/PouchDB pattern is how I originally got interested in local first, they are such a good tool, but having the full power of Postgres and then SQLite on the client, I believe, is a real game change.

- ## 如果不使用 React 这类框架的话，如何优雅地实现 offline web app 呢？
- https://twitter.com/beihuo/status/1720168712421204477
  - 我理解 Service Worker 可以实现这点，但是如果使用后端生成 HTML 的框架，比如 Hotwire 或者 LiveView，好像很难实现 offline？

- ## [Local-first software: You own your data, in spite of the cloud (2019) | Hacker News_202310](https://news.ycombinator.com/item?id=37743517)
- Couchdb/pouchdb remains one of the best: it's super easy to setup and is production-ready, but it's gonna be json docs with no transactions, so it can be limiting.
  - Y.js and automerge emerged as solutions combining CRDTs and content transfer, they look really promising. There is a Y.rs version if that's better for you.
  - I feel like you're not really interested in full p2p but want some centralization point to manage some auth stuff, so I'd investigate couchdb/pouchdb first.

- I've used tRPC and GraphQL before and I've really been thinking of something where we'd have the same DX as the client-server model such as with tRPC and GraphQL but in a way where there is no difference between client and server state, there is only "state." This makes sense because for local-first, the entire state of the app must be replicated locally anyway. Recently there have been CRDT solutions that try to solve this problem, however, such as Triplit, or ElectricSQL
  - Meteor wrapped the MongoDB API for this purpose. You are working with collections and can run the same queries over them, regardless of whether you are connected to a DB instance or the browser's local storage.
  - For CouchDB an equivalent exists in the form of PouchDB

- 🤔 How do CRDTs work with blobs/files?
  - I don't know. I guess they simply don't.
  - My approach would be to categorize user content into
    - CRDT-enabled content considered as the norm, and
    - content trapped in legacy containers that do not support CRDT.
  - With an implied warning for the user: legacy content offers a limited user experience.
  - Migration from "legacy" to "normal" should be fully supported, and as transparent as possible (but needs dedicated support for each file format). 
  - Converting "normal" (CRDT-enabled) content into files/blobs should be treated as a "take an snapshot" export operation.

- ## [Offline First – A Better HTML5 User Experience | Hacker News_201612](https://news.ycombinator.com/item?id=13245647)
- Offline is not a mere feature you can bolt on to existing architectures because you are really building a distributed system. 
  - Architectures that work well for distributed systems and especially p2p architectures thrive in this environment. 
  - 👉🏻 Instead, you can take this idea further and implement a kappa architecture (sometimes also called "event sourcing") where you **maintain a log locally on every client which is the source of truth, not a server**. 
  - When a network connection is available, you can replicate the log to a server or directly to other clients. 
  - You can build indexes (materialized views) that sit on top of this log to answer queries more quickly than reading the entire log out every time. 
  - You can also blow away these indexes and rebuild them from the log whenever your requirements change (migrations).
- Unfortunately the web is missing a few pieces that would make it a very good platform for fully p2p, distributed apps. 
  - Service workers are a good start, but they have a 24-hour upper cap on max-age of the service worker itself, so users can't trust on first use (TOFU) and then be more secure against kinds of active targeting. 
  - The suborigin specification and iframe sandboxes for distributing apps offline and p2p would be much more useful for offline sandboxes if they didn't require that a server send an http header. 
  - These will become much more important as the web bluetooth API matures, which can allow distributing user data and application updates in a totally offline environment.

- ## [Offline-First Apps: Why Should Apps Be Made to Work in an Offline State? | Hacker News_202208](https://news.ycombinator.com/item?id=32544837)
- My startup built an SDK framework that’s allows companies to build offline apps that can even sync over a multihop mesh network. It’s powered by a CRDT to handle the conflict resolution.
  - From my experience most of our customers are not mobile developers (they’re JavaScript developers asked by their bosses to build mobile apps) and don’t even want to spend time learning coredata or room for iOS or Android. So most of the time they just stick to what they know, HTTP requests.
  - Luckily we made our SDK easy to use so that these JavaScript developers can get both the network communication and the offline first caching in one product. They absolutely love it.
  - Most apps aren’t offline first because it’s so hard to build the infrastructure to pull it off without a lot of bugs. Most apps focus entirely on the UI code layer. If infrastructure and frameworks made this a lot easier to use, I bet offline first would be a lot more popular
- Ditto is the real deal and the best CRDT database out there atm. 
  - There are expressive CRDT libraries like Yjs and Automerge but these don’t give you persistence. 
  - There are mature databases out there that include CRDTs, like Redis and Postgres EDB, but these have very limited semantics. 
  - Ditto is a proper database with a rich set of CRDTs. It’s well engineered, the team are great and it has a compelling DX / realtime APIs.
- Ditto is both an embedded + cloud database + a mesh network, it's really 2 startups in 1.
  - A) If you're looking for just offline-first and data sync, there are some company's that have done this: Realm (MongoDB), Firebase, Firebase
  - B) If you're looking for just mesh networks: Build it yourself using Bluetooth Low Energy, Local Area Network, P2P Wi-Fi Direct, Apple Wireless Direct
- Ditto is a combination of both families of problems, it's basically creating 2 startups at the same time (mesh + distributed database)
- ditto: It’s powered by a CRDT to handle the conflict resolution.
  - Ditto is a distributed database, each peer has it's own database. The database is organized into collections and each collection is a Ditto Document (this does not work like most NoSQL document databases). 
  - Each property of the document is it's own CRDT, you as the user can pick which CRDT you'd like to use, our current catalog includes:register/counter/binary/RGA
- A CRDT is a way to solve multi-leader replication without having the application code resolve conflicts.
  - To implement this, every application node keeps a vector clock per register (an atomic piece of shared state). 

- I’ve tried PouchDB before but only on “toy” projects not deployed production. What challenges have there been with PouchDB or other offline-first techniques?
  - I like offline first app design, and have built several. However, I don't do it anymore unless there is a very clear use case and direct customer benefit. Some apps just don't work offline at all.
  - One of the decision trees is you often have some API needs and can't just live within the pouch db database. Particularly account creation and such. It may need to plug into other services and initiate them, you could use a database as a message queue, but it's awkward compared to an API.
  - The couch/pouch models gets somewhat more complex when you leave the one db per user model. If there are shared data buckets, the database access patterns require a good deal of thought and experience with the couch db auth model. Particularly it's limitations.
  - Offline access also requires thought around sensitive data. If a user has had their access revoked, an offline first app may preserve it which can rub against security requirements.
  - Initial sync can be very slow if you're dealing with a lot of data. This can be a poor experience if you make a new user wait minutes to get started. Or you can also build a backend so they can start immediately and then switch to the local copy after replication. I've build this kind of system before.
  - There are advantages to the route. Minimal data transfer from the server can represent lower load for your services. You can also do an offline only model for data, potentially lowering cloud costs for the number of users you serve - a definite boon for free tiers.

- 
- 

- ## 缓存与身份问题: Local-first state machine puzzlers:
- https://twitter.com/jamespearce/status/1715419614530994471
  - 1) You're anon, create content cached locally, then authenticate. Is it joined to the account?
  - 2) Log out. Is the content still cached and visible?
  - 3) Create more content, authenticate as different user. What is joined to the new account?
- On http://typecell.org I chose to only copy content on sign up. Tried other scenarios as well but imo was getting quite difficult to follow what was happening (without investing more in ux patterns to, for example, give the user the option to choose)
- Log out, cache cleared. The risk of adding content to a previous account instead of the one you just logged into could have big implications.
- My best solution so far has been to default all non-logged-in content to an “anon” user, and then provide an api that allow devs to associate some or all current “anon” content to an actual user.
  - They can write an auto association algorithm that works for them, or provide pop-ups asking the user what they want to do with the data.

- ## Are products changing from "one giant DB with all user data mixed" to "Isolated data. E.g., 1 DB per user"?
- https://twitter.com/tantaman/status/1696165303464468489
- collaboration in a "db per user" model is a disaster.
  - I have strong opinions that people should stick with a model that mixes user data and enforce separation via  row level security.

- A totally different approach that seems to work well for some classes of applications is "db per file"

- Go one step further: decouple data from app entirely and colocate data with the user.
  - Not just 1 db per user per app, but 1 db per user, period

- ## upwelling: version control for writing
- https://twitter.com/geoffreylitt/status/1633956142996127744
  - Perhaps the most important idea in the piece: creative privacy is valuable! We shouldn't just accept always editing in a public doc. Our tools should actively let us decide when we're ready to share.
  - Another key idea, often lost in discussions around CRDTs: in creative work, many conflicts cannot be automatically resolved.
  - All you can do is have data structures, UI, and workflows that make it easy for humans to review and decide
  - I'm now strongly convinced that a critical primitive for the future of creative tools is: git-style branching version control, adapted for non-programmers, with smarter conflict detection heuristics, blended with realtime collaboration

- I'd say this is a requirement for any interactive software, and that the programming platform should support that. We shouldn't expect each tool to reinvent this

- ## I am watching the talks from the Berlin Local-First meetup and liked the talk by @schickling “why you need Local First”.
- https://twitter.com/sitnikcode/status/1673740334872797186
  - Short answer: for DX
- 1. We constantly try to think that the frontend is something simple, not a distributed system. As a result, we design the architecture on simple request-response communications.
- 2. But in reality there are a bunch of distributed systems problems (latency, performance). To solve them, we create caches and make them too complex. In the end, the cache becomes like a small database (like Apollo client).
- 3. But since our architecture was created a long time ago without taking into account the distributed system (and we thought that we would have a simple cache, not a real database), the DX and speed of development drops a lot
- 4. The idea of Local First is that we don't lie to ourselves, but think of the frontend and backend as nodes of a distributed system. As a result, we have a database on the client, not a cache. Maybe even source of truth. The server becomes much simpler, the DX improves.

- ## Offline is not just online with extreme latency. This is one of those "mathematically true, but not true for humans" things.
- https://twitter.com/aboodman/status/1648777443262488576
  - You can't automatically merge conflicts when are disconnected for long periods, because their *intents* can diverge such that they become incompatible.
- When *online* you can use any kind of merge strategy so long as it preserves useful invariants *to the developer*. If users see that collaboration did something they don't like, they can just undo it. Not too much work is lost.
  - These tools don't work while offline because what users care about is amount of work lost. When offline the potential work lost scales from "milliseconds" to "days" and this isn't acceptable.
  - Different strategies are required for applications where users can be disconnected for significant amounts of time.

- Have you tried using llm for suggesting merge strategies yet? Seems like a fun use case to experiment with. Probably never a good idea to automatically merge, but draft one maybe.
  - No but I think it’s a great idea particularly for text.

- Is git the best example of a collaborative offline application?
  - It's the one that jumps to mind, yeah. Ink & Switch did an amazing article about the general problem recently
  - [Upwelling: Combining real-time collaboration with version control for writers.](https://www.inkandswitch.com/upwelling/)

- orders of magnitude(巨大，量值) matter, and jitter(紧张不安的动作) matters. 
  - A system that is designed to deal with 100ms latency will not deal well with minute-long latencies. 
  - And as a corollary(必然的结果或结论), nothing can work well if your latency could be 1s, 100s, or 1000s.

- ## I've learnt more about software engineering from building local-first software than any other space.
- https://twitter.com/JungleSilicon/status/1635146316165828609
- data substrate(底层；基层)
  - storage, cache, queries, events, api, auth
- crdt
  - types, Snapshots, transactions, versions
- network
  - ser/deser, encoding, handshake
- malleable-software(延展性的, 易适应的)
  - rich-text, search, markdown, plugins

- ## This was the original problem that got me interested in local-first software. I wanted messaging apps to work like phone providers.
- https://twitter.com/JungleSilicon/status/1630331881207246848
  - My initial thoughts were to separate the data layer from the application itself, that way each application could read from that data layer. 
  - The data layer could be similar to an Apple cloud account or Dropbox. 
  - The problem is - this introduces friction(分歧；不和) for the user.
  - If you instead store the data in your local device and have that sync with a cloud backup / relay, it makes it a more seamless process as you only need to set up the account once and then all your data will sync to it.
- Makes me wonder why we don’t have a messaging protocol like email for instant messaging…
  - There is RCS, which is an international  3GPP standard, but Apple refuse to implement it, and other providers pretend it's a Google thing (it's not)
  - And XMPP, solving instant messaging and presence as a w3c spec

- ## So much CRDT literature seems to focus on collaborative text, but it feels like a pretty niche(针对特定小群体的) problem to me._202210
- https://twitter.com/gaforres/status/1584909330859671553
  - Block editors like Notion are good enough for most cases. 
  - Editing the same sentence or even paragraph as someone else doesn't really seem like a common user need.
  - But I guess if you're aiming to build perfectly general abstractions you're forced to target the hardest niche case. In my experience making systems, trying to universalize to that extent can become the enemy of progress and usability.
- Collab text feels like a product black hole. If you did it perfectly, the UX would still be bad. It has no tactility(有触觉的；能触知的). People don't co-work that closely in real life. It would be rude. IMO the value of collaboration is a sense of togetherness, but with personal space.
- After having worked on manuscripts with 4+ participants for 6 years or so, I have come to think exactly this. I don't know how we've managed to come to this point; it's like a dance where we all have to step on each others' toes to participate.
  - On the other hand, it does relieve the team of the burden of appointing a merge gatekeeper of changes. In which case, simultaneous editing helps.
- I would assume that when writing async, the merging and keeping the history is more important to not cause any unexpected overwrites when you have been writing offline for some time and sync your changes back
  - I suspected there might be a blind spot in my reasoning while writing those tweets, and this very well may be it! Offline-first text could totally be difficult at block level.
  - Still feels like it would be very difficult to solve with a generalized system, though. Like the final paragraph would diverge inline as changes come in with no respect for meaning. Manual mege at the block level might still be a better UX.
- Is there a tool/library that can handle ordered trees out of the box that you know of? Thx
  - Depends on how you want to query it... The framework I'm building uses schema based data which doesn't handle recursive nesting, but could represent a graph by ID references and query each level iteratively. Not ideal. Classics like YJS probably better. Check GUN too.
- collaborative text is good because its a list type that people are already familiar with! turns out we can build arbitrary JSON out of lists (like what Automerge and Yjs have done) which allow you to synchronize state of entire applications

- ## Lots of upsides to local-first apps, but one downside is if you break prod, you can't just revert. 
- https://twitter.com/gaforres/status/1626642640518148096
  - Users will probably have written bad data to their local device already.
- Just wondering, in theory, if everything is event based, then writing bad data should be fine, once you know how to rewind them right?
  - Y'know I hadn't even really thought that far. lo-fi encodes the schema version in each event, so a revert could ignore all future schema version events. However, it also uses IndexedDB, and there's no way to downgrade the database version too...
- A failure recovery could maybe be a new version with a directive to drop any events from the bad version and continue on from there. I could see that working as a last resort.

- yeah this has bitten us, we had some flaky early persistence code writing bad data onto user's machines, and one deploy i wish we could have simply reverted. @SomeHats made a herculean effort to clean  up the bad data and add checks to prevent further bugs slipping into prod.
  - Still, we're thinking of maybe switching to event sourcing as a source of truth to alleviate the rollback problem. That would be much tricker for local-first apps though.
- I’m doing event-sourcing in my local-first app. It works really well so far. No migrations are the best migrations.
- Mostly what removes the need for something like a migration. My lib lo-fi models data as event series but still needs some special logic for schema changes. Would be interested in simplifying!
- For my app there are two kinds of schemas: 1) App db schema 2) event type schema
  - When ever (1) changes, I just rehydrate a fresh db from scratch with the new app schema - no migrations needed. For (2) I so far only do additive changes (e.g. via event versioning)

- ## I think many people agree that building a modern web app forces app devs to think too much about distributed systems and grapple with a stack that has tons of layers.
- https://twitter.com/geoffreylitt/status/1622632087932248065
  - Tangentially(不直接相干的，略为触及〔主题〕的) related thread, more about the importance of actually investing in a good architecture. see linear
- Most web apps don't need to be distributed, but for those that do, companies like @flydotio are striving to make distributed just as easy.

- ## When we started work on @linear , we felt real-time sync was a core functionality we had to invest in from the get-go. 
- https://twitter.com/artman/status/1558081796914483201
  - [linear sync 分享_202002](https://www.youtube.com/watch?v=WxK11RsLqp4&t=2169s)
  - 默认last-write-win, 出现冲突时，提示用户选择版本
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

- ## What are some interesting research groups in tech along the lines of these:
- https://twitter.com/JungleSilicon/status/1622755131921154048
  - Dynamicland
  - Braid
  - Ink & Switch
- [The Overedge Catalog: The Future of Research Organizations](https://arbesman.net/overedge/)
- Along socio-technical research lines:
  - @funDAOmental
  - @humsys
  - @metagov_project
  - @block_science

- ## glad to see more talented devs embracing local first tools. But I'll warn you: data migrations! If you want your app to live long term, best to have a plan for change.
- https://twitter.com/gaforres/status/1619354329798029312
  - [Local-first data migrations](https://blog.gfor.rest/blog/lofi-migrations)
- The freedom you get from having data live on-device is the best feeling. 
- But the data is stuck on their phone, and the tab is closed. You want to convert all foos into bars for v2. How do you do it?
  - 👉🏻 A common approach is to drop a version number on the data and try to rewrite the data on load if it's out of date. But your client may not have loaded the latest JS (service worker cache, offline) before it starts writing changes.
- It's possible to receive changes to data that target the old shape from peers after you've already upgraded your local copy, even ones that are timestamped after your migration. This can corrupt your local data, and there's no canonical server copy to fall back on.
- This problem can quickly expand to require checks and guards all over the codebase, ruining the free feeling of local first development. And at least for me, it would keep me up at night to wonder if a user will lose their data because I didn't think it through.

- ## 💡 [rxdb: Offline First_202109](https://news.ycombinator.com/item?id=28690427)
- what's a good solution for syncing with the main database after the device goes back online?
- 👉🏻 CouchDB/PouchDB(the JS compatible cousin) make use of a global sequence counter to track which documents have changed between sync.
- Each database uses an arbitrary byte string to mark a position in a sequence of updates to the database. 
  - Each document has the sequence counter of when it was created/updated/deleted. 
  - This sequence counter only matters to that particular database (it does not need to be mirrored, it's just a local ref. of WHEN the doc was modified in that particular database).
- **Syncing is then a process of looking up the last read sequence counter from a checkpoint document** (i.e. what was the last modification) and passing that sequence counter to the `changes` endpoint to get a list of all documents with a sequence counter AFTER that, and then pulling/pushing those documents to the local/remote database, and saving the new latest sequence counter.
- The official docs give some more info. One key point is if I modify a document several times between syncs, it will only show once in the changes feed with the latest sequence counter for that document. Couch's conflict resolution strategy is a topic for another time, but an interesting one.

- It’s an open question and ultimately depends on your app. 
  - For our mobile app we try to merge simple changes automatically and for trickier ones we allow the user to merge or select changes with a UI, a bit like git. 
  - We try to keep our objects small and granular enough that this very rarely occurs. 
  - **For a lot of apps last write wins (e.g compare and always take the lastest timestamp) is enough** and probably the most common solution you’ll see but you have to be OK with a certain amount of data loss. 
  - Newer, fancier CRDT based merging solutions are on the horizon, like Automerge for example but I feel they’re a little way off mainstream adoption.

- Get all entities whose `updated_at` is larger than the max `updated_at` in your local database.
  - Then what if the schema changed? Columns renamed, dropped or new columns added that is non-nullable, or new foreign keys with non-null constraints?
- I am considering to add a version field to my documents so that I can **migrate the document to the most recent version before persisting in to the server's database**. When sending documents to the client you may have to force it to update to the latest application version though.
  - True. For simple apps with not much logic, you can get away with different front-ends/offline-syncs adding their own rows, and then only respecting the latest row in the main db, usually based on timestamp. But if you have something more complex where multiple workflows get triggered as side effects, then you may run into trouble when the latest row is in fact not the truth of the reality that we wanted, so there is still some risk ending up with states or workflows based on a false reality. This can become a nightmare if you a have few scheduled events/tasks/crons that does things periodically, thus the only way to mitigate that is to fully embrace eventual consistency and idempotency, and the "easiest" way to get there is to embrace the actor model paradigm
  - Point being, comparing two versions of applications against each other is not enough - you may need to version your data too and use timestamps to make a final decision on which version is truth. You may also need to set or build a tolerance system to say it will only sync "old" data if within x amount of days, lets say less than 7 days old. And so on.
- Earlier this year I experimented with combining CRDTs using the incredible yjs with PouchDB. It worked really well, completely magic syncing with full automatic handling of sync conflicts! 
  - [(Alpha) PouchDB integration for Yjs](https://gist.github.com/samwillis/1465da23194d1ad480a5548458864077)
- I think my main problem with PouchDB and by extension CouchDB was that it seemed **hard to add validation in the backend** (including authentication/authorization). I remember having to build some kind of proxy that hooks into the CouchDB protocol to deny certain requests. I am pretty sure that's solved by now 
  - That was a problem I always had with replicating directly to CouchDB. They have added more authentication methods now, like proxy auth and JWT, so authorizing on a per-database basis isn't too bad.
  - However, I gave up on CouchDB after my server kept getting hacked by crypto miners. I'm sure whatever exploit they were using has been patched, but I'm hesitant now to use a DB that's open to the world.
- I think the most common CRDT libraries try hard to reduce the overhead of CRDTs. I am not expert but I could imagine that you could also remove some of the historical data if you know that all clients are reasonably up to date and if they aren't they have to discard their changes that are too old.

- I still haven't found the "holy grail architecture" for offline-first with backend sync where the backend isn't just a simple data store but also has business logic and interacts with external systems.
  - Doing offline-first well implies that the app has a (sqlite or similar) local database, does work on that database and periodically syncs the changes to the backend. 
  - This means you have N+1 databases to keep in sync (with N=number of clients).
  - When the backend isn't very smart it's not too hard, you can just encapsulate any state-changing action into an event, when offline process the events locally + cache the chain of events, when online send the chain to the backend and have the backend apply the events one by one. Periodically sync new events from the backend and apply them locally to stay in sync. This is what classic Todo apps like OmniFocus do.
  - The problems start when the backend is smarter and also applies business logic that generates new events (for example enriching new entities with data from external systems, or adding new tasks to a timeline etc). 
  - When trying to make the offline experience as feature-rich as possible, I always end up duplicating almost all of the backend logic into the clients as well. And in that case, what is even the point of having a smart backend.
- 👉🏻 Seems like you're describing event sourcing. I'm building an offline-first app and doing pretty much what you're describing.
  - Yes it looks like event sourcing. But most of the classic event sourcing implementations I've seen are mostly backend only.
  - The project I'm currently hacking on has an MQTT broker that is used by both clients and backend and the events can come from anywhere.
  - Enabling all this in an offline-first paradigm is hard and requires a lot of duplication, I am very close to just saying screw this and requiring network connectivity for most of the features.

- Check out WatermelonDB 
- pouchdb is mostly unmaintained and issues are just closed by the state bot instead of being fixed.
  - So in the last major RxDB release, I abstracted the underlaying pouchdb in a way that it can be swapped out for a different storage engine. 
  - This means you could in theory use RxDB directly on SQLite or indexeddb. 
  - In practice of course someone has to first create a working implementation of the RxStorage interface.

- Offline first is a dream to me, I build a big note-taking app (midinote.me) which is 100% offline, 
  - 👉🏻 but now the biggest pain point is the full text search, yes, we can use DB like this and PouchDB to store data, 
  - but currently, there isn't a good solution for full text search in javascript, 
  - I tried lunr.js the performance is poor, and researched FTS by sqlite, it don't support Chinese, 
  - I ever considered pack the lucene (on JVM) with Electron.js( the desktop wrap on JS) on desktop, I'm not sure it is a good idea, 
  - now I am going to re-think all these things, and considering give up offline and switch to server side full text search, it will save huge effort comparing to client-side search!
- pouchdb-quick-search didn't work for you?
  - Yes, I used it, generally, on JS platform, the performance is not so good to do FTS, especially when document is long and the data getting huge.

- Meteor uses `minimongo` on the client which sync's with the server; effectively doing the same thing. It's actually amazing how much better the UX is when you have spotty coverage.
- I think Oracle APEX works on the same premise? Store locally in indexedDB and sync up when the connection is back on-line. No need for difficult programming, APEX does this out of the box .
  - Anyhow, a way to force this behaviour in APEX is to make every user interaction a write action on the DB. This way you either save locally or to the backend (but you don't have to worry about the sync between the two).

- 🤔🛢️ Has anyone used ObjectBox in anger and can share their experience?
  - I experimented with ObjectBox a bit, but I decided against using it because it isn't open source. The language wrappers are apache2 but the core library is only provided as a binary blob. I think this is bad because you can't inspect how it works, fix bugs, port it to new archs, integrate it fully into your build system, etc. Also, every cursor operation must call into their function entry points (as opposed to being inlined in your code for example).

- ## How many records can you sort/filter/paginate in a web browser?
- https://twitter.com/jamespearce/status/1605273072851886090
- tinybase: Without breaking a sweat: 10, 000 word corpus for client-side autocomplete
  - https://tinybase.org/demos/word-frequencies/
  - tmdb: 1, 000 paged relational records
  - https://tinybase.org/demos/movie-database/

- A browser doesn't struggle wrangling many mb of data it memory.
  - It struggles keeping track of and updating thousands of elements in the Dom. I've only ever done 20k records but would feel comfortable easily doing hundreds of thousands using react-virtualized.
- Yep, agree with all that. The good news is there's no need to display it all, just want to hold it in memory and sort/filter.

- ## My goal is to build a database that makes it easier to build local-first software.
- https://twitter.com/ccorcos/status/1532185301438738433
  - Embedded, reactive, schemaless, and transactional read/write directly to indexes (inspired by FoundationDb)
- SQLite is great, but it leaves much to be desired. It's mostly just a problem with SQL. 
  - Queries aren't reactive, no multi-valued columns, no indexes across tables for relational queries... All of these currently require bespoke(定制的) solutions.
- Segment trees/ interval trees are cool, I implemented one once for keeping track of register liveness in a compiler code generator
- Interesting idea to have cross-table indexes; is any RDBMS supporting that?
  - I think many databases avoid it because of arbitrarily expensive write time complexity. 
  - For example, one tweet = one row per follower. 
  - In a large multi-tenant(租户) system, companies end up with event-sourced architecture like Twitter with eventual consistency.
  - But for personal tools and fully distributed local-first p2p apps, that shouldn’t be as much of an issue. Worst case scenario, your computer is slow, but you aren’t going to break the app for everyone else.
- Write amplification can be a problem in these scenarios as well.
  - True. But if someone tweets and it needs to end up in 100M feeds, then thats just the nature of the problem… Not allowing indexes for this scenario doesn’t solve the problem.
- https://github.com/ccorcos/tuple-database
  - The local-first, "end-user database" database.
- https://github.com/ccorcos/game-counter
  - TupleDatabase as a UI state management system.
  - External effects interface through services defined on the Environment.

- ## The idea of persisting UI state to a database has me thinking of tons of possibilities. 
- https://twitter.com/devongovett/status/1526227167952117761
  - Not only a super nice user feature, also great for development. You could reload and be right where you left off with no Fast Refresh needed. Or debug state using database tools. So cool!
  - According to the article, sqlite is fast enough to store the scroll position and re-query data in a virtualized table in real time
- Yes, that is how our app works for 7 years now ; -) we syns whole sate (localStorage then and idb now) and react to changes. All UI is built in browser. No hot reloads  needed.
- I remember reading an article quite a while ago about how FB built their iOS app where everything was driven from SQLite tables - everything. It’s a pattern I’ve been interested in applying for a while. We already do it with business logic loaded + cached in client driving ui
- There's a ClojureScript project that explores similar ideas: https://github.com/fulcrologic/fulcro. It changed my perspective on UI development

- ## In Riffle we avoid manual network by optimistically loading all data onto the client and doing queries locally. 
- https://twitter.com/geoffreylitt/status/1505932761453977606
  - HF / DIEL take a diff approach: keep some computation server-side, but help schedule across the boundary
  - Interesting tradeoffs there. Having all data local seems simpler when it's possible. eg: 0 net latency enables new patterns like storing UI state in the DB.
  - OTOH, def some benefits to putting data/compute off-device. Access control, avoid huge data / queries on device...

- ## Wrote an essay about Riffle, a new project I've been working on. Guiding question: could we simplify app dev w/ a new kind of reactive local-first database?
- https://twitter.com/geoffreylitt/status/1499083601387864069
- I imagined: what if you could customize any web app in a spreadsheet view?
  - Apps today aren't _actually_ built on spreadsheets.
  - OK then, so what would it look like to build apps w/ spreadsheets?
  - There've been some great answers to this in prior work, but they often have a low complexity ceiling--good for building TodoMVC, but hard to scale up.
- w/ Riffle we're trying something ambitious: simplify app dev for both experts building "real apps", and novices.
  - Focused on providing an awesome foundation for state management, inspired by good ideas from databases research, spreadsheets, incremental computation, and more.

- ## I'm having trouble reconciling an offline-first app with online SaaS sync. 
- https://twitter.com/_paulshen/status/1431745519873781765
  - How do you handle auth while offline? 
  - What happens to your offline documents/changes when you reconnect logged out or as a different user?
- files backed by git provide some inspiration. you own the files on your disk. but the manual push/pull and resolution steps don't translate directly to "apps"
- Maybe figma can help you with some ideas of how to handle it
  - [Can I work offline with Figma?](https://help.figma.com/hc/en-us/articles/360040328553-Can-I-work-offline-with-Figma-)
  - Figma is probably the gold standard here. this doc is very thorough. thanks!
  - I tried making some Figma changes offline and deleted my session cookie. It silently lost the changes but Figma doesn't claim to be an offline tool. The save to `.fig` file is nice.
- Understood. The feature to save the document to .fig file is neat, as that's the only guaranteed way to avoid losing data.
- Brainstorm: it could be split into different layers:
  - give the user a way to export the docs to a file (avoid user losing offline data if they want to, ex, uninstall the browser)
  - when reconnecting, if session is ok + user still has same access to the docs, sync the changes*
- I think it’s ok to disallow switching accounts when you’re offline.
- agreed but things can change on the server side while you're offline. maybe you lose permissions to the file or you triggered an action to log out of all your clients.
  - What should happen in those cases isn’t technically hard, but more of a problem of designing a UI that informs and sets expectations effectively. I do understand designing such a UI isn’t trivial.
- Offline data sync is complicated with web browsers. User might have a few tabs opened, so you need to sync between them.
  - You probably don't want to sync the same changes from all tabs. 
  - Only Chrome has a way to sync data in background I think. 
  - Other browser quirks like IndexedDB not working in FF private tabs and Safari had some problems. So it gets complicated quickly

- ## It’s quite rare for software to offer both a real local file format and also substantial(大量的，重大的) cloud/SaaS behavior (ie other than syncing). 
- https://twitter.com/andy_matuschak/status/1428777459235782660
  - Usually it’s one or the other
  - if the cloud has active behavior, apps are thin clients which don’t expose an accessible on-disk format (eg Notion).
  - I recently finished re-architecting @withorbit to expose an on-disk format, thought I’d write a bit about what I learned.
- Orbit的解决方案小结
  - 存储层基于SQLite
  - 协作/同步层基于比CRDT更简单的events log
- It’s hard to pull this off, as I&S describe. 
  - You need to design a file format which syncs efficiently and reliably, which is already tough. 
  - Gets tougher when your SaaS is an active replica with its own public API, and when you layer on indexing/querying, migration, sparsity.
- There are enterprise solutions which solve these problems (Realm, CouchDB), 
  - but one consistent limitation is that they “own” the file format, and often the server component as well. 
  - I don’t feel good exposing my on-disk format to local clients if it’s tied to a specific backend.
- CRDTs are a useful piece of the puzzle, but they don’t solve the problem as fully as people often imagine. 
  - The I&S folks are working diligently on many of these. 
  - But **one problem I don’t know how to solve** is the complexity of the resulting opaque file formats.
- In an ideal world, everything’s just plaintext, so you can modify it with whatever tool you like. No libraries needed. 
  - Problems with this include semantic sync, indexing, structured data, etc. 
  - SQLite is almost as good, if the schema is well-defined
  - [SQLite As An Application File Format](https://www.sqlite.org/appfileformat.html)
- Maybe someday automerge’s serialization format will be as durable and universal as SQLite’s, but in the meantime, it’s certainly not amenable(易处理的) to casual concurrent local access in some user script.
- Of course, **SQLite leaves you to solve syncing**. 
  - The typical approach is a write-only log of events (CRDT mutations or otherwise) which can be replayed across replicas. 
  - Snapshots of entity states are computed from queries across these events.
- That’s **the approach Orbit takes**: simple event structures (simpler than CRDTs, sacrificing some of their key guarantees to reduce complexity), with well-defined merge operations, in a SQLite db. 
  - Users can write scripts to insert their own events if they like.
- I’m still not satisfied with this. 
  - Reading/writing data yourself requires using Orbit’s libraries or a SQLite library and an understanding of the schema. 
  - I’d like to just expose the data as plaintext, but I’m not yet sure how to achieve that practically.
- One approach is to define Git-style “plumbing” CLI primitives which offer plaintext-like I/O to your data structures. 
- Another is to define a FuseFS layer, @rsnous style.
- Orbit’s cloud server has its own (third, ugh) backend implementation, which it uses to offer APIs, aggregate analytics (for my research), and services like study reminder notifications.
  - I see now why people don’t generally do this. It was a huge amount of work. 
  - As it happens, Orbit’s implementations are quite general (i.e. they have almost no specific knowledge of Orbit’s structures), so perhaps they’ll be of use to others.
- https://github.com/andymatuschak/orbit
  - Orbit is an experimental platform for publishing and engaging with small tasks repeatedly over time.

- another hard thing about implementing this type of data format is that web browsers demand their own implementation. 
  - @kirkbyo_ kindly implemented an IDB-based Orbit backend. Excited about absurd-sql

- I like what @craftdocsapp does here: for each note, you can choose to persist either to on-disk file or to their realtime cloud. A sensible compromise given there's not a great way (yet!) to get the best of both worlds
  - In your Metamuse interview I really liked when you (or maybe it was @_adamwiggins_ or @mmcgrana ) talked about how code IDEs provide all these features on top of basic data, like “jump to definition”, syntax highlighting etc. Wonder how this can be applied to other data…
  - Another example is Photoshop (or any bitmap image editor); Instead of an array of bytes representing plain text, it operates on an array of bytes representing pixels. Adds computed information like histogram, color replacement, etc.
  - Yeah layering complex interpretations over a simple serialized format seems to work well in those domains. 
  - Note taking seems trickier… eg, Markdown isn’t powerful enough to express Notion documents
  - Maybe Notion documents is not a good benchmark and maybe markdown is not the ideal “elemental material” or perhaps it is. Figma is interesting as its file format is a list of key-value maps. The app then gives special meaning to certain keys and values.
  - Aside: interestingly this is the data format underlying almost everything in Spotify; an ordered dictionary. 
  - Keys and values are just byte strings. Hierarchy and meaning applied computationally. (3-way diff-merge was less hard to implement this way. Etc etc.)
- Ingredients for a future:
  • Elemental material that is absent of meaning (but has some structure)
  • Domain-specific agreements about meaning of data (eg rich text editor, game scene, etc)
  • Synchronization tools that act on the elemental material (w/ optional domain knowledge)
- Elemental material: maybe XML is the closest we've ever gotten? HTML, RSS, SVG are three distinct domains.
  - I had always hoped a file sync service like Dropbox or iCloud could add a developer API and become the last point, but that didn't happen.
- Maybe JSON can be the elemental material? Definitely my default choice moving simple structured data between programs.
  - This is why I find automerge interesting--it provides that sync tool on the structured layer without any domain-specific knowledge
- I think JSON is popular because it is the weakest link. 
  - No integers or pointers, sparse representation (like XML.) 
  - But ultimately I think that story of how PostScript came out of the JaM project as a solution the problem of an evolving data structure is a good lesson.
  - Hmm yeah... maybe this gets at a fundamental tension: weaker, stripped-down formats are easier to make generic across domains + tools? Eg: a huge drawback of plaintext code is the lack of pointers, and yet smart editors can "rename function" just fine by interpreting the text
  - Similarly, newline-delimited text in classic UNIX tools is a very underconstrained/weak format, but simultaneously super versatile and quite useful... maybe two sides of the same coin? idk
- I wonder a lot about relational database as "elemental material"... eg, what if my emails, calendar, photos, contacts, projects, tasks were all just in sqlite? I could routinely use a nice Airtable-style UI to manually edit, and also write scripts against my DB quite easily
  - Very interesting idea. SQLite is very portable and truly open, so that's a good start. 
  - I struggle with one thing with SQLite though and I wonder how you deal with this: How to... look at it, copy paste, massage the structure, etc. (e.g. bitmap = image editor, text = text editor)
  - There are plenty of GUI apps for SQLite of course but they are all MUCH less flexible than say editing a text file in a good text editor with things like Ctrl+A to select all
  - Maybe what we need is a really good editor for whatever a good "elemental material" is for data. I'm thinking something that can make use of the speed of a keyboard but have more dimensions than sequential bytes (i.e. plain text.) Maybe a DOM structure?
- Yeah, agree: the elemental material can only be as good as the best editor for the format. 
  - Fun to imagine the ideal keyboard-driven SQLite viewer/editor for daily usage. Inspirations could be classic iTunes, Airtable, + more powerful visual query UIs
  - It's funny how many apps eventually build a table UI... each one has unique quirks, and usually not extraordinary UI since the team is busy w/ other stuff
  - Like, instead of Github building a table UI for Issues, could I just use familiar Airtable or magic generic table editor ?
- I wonder if better to focus on SQL as the communication protocol, rather than SQLite as an implementation?
  - For example: maybe I would like to use my table editor with a web service exposing a virtual SQL database as just an API; I don't care what lives behind the SQL protocol
- If you use a Mac, there's a decent chance your email, photos, calendar and tasks are already in SQLite
- I tend not to run it directly against the SQLite files in-use by apps though, 
  - since they're not designed with concurrency in mind (they often don't enable WAL mode so you get a lot of locking errors) - my tools tend to create a separate database copy which I update intermittently(间歇的，断断续续的)
- I've not tried applying a write to a file used by some application yet - my worry is that they'd have some weird denormalizations that I wouldn't fulfill and I'd break things
  - Yeah that makes sense. Seems like a general challenge w/ sharing a database across apps... I guess only hope would be to try to encode as many constraints as possible directly in the DB layer
- The other problem with encouraging other apps to access your DB file directly is that it turns your schema into a supported API, which makes schema changes massively harder if you don't want to break things outside your app's control
- I like the idea of defining named SQL views that are the "supported" way to access data - that way you can change the rest of the schema and then modify those views to continue serving the same shape of data against the modified schema
  - Yeah that makes total sense for reads! Writes seem to require more machinery though... I guess you can (1) get fancy and figure out how to send writes backwards through the view query, or (2) treat SQL as just a read interface and have some separate constrained write API
  - I guess writes could be handled by predefined stored procedures in databases that support those, but sadly SQLite doesn't (yet)
- @simonw ‘s blog post about querying photo metadata gives me hope that sqlite are at the heart of other consumer apps even though it’s not advertised widely.
- Another random inspiration is how Automerge assigns unique IDs to every little piece of a JSON blob… hard to make it efficient, but incredibly convenient foundation for having pointers that stably reference anything
  - Re: types, I am enamored by super rich types, things like “phone number”, “email address”, “US State”, etc. Maybe naive to imagine these types can be agreed upon by everyone (I know world is complicated!) but still feel so convenient…

- This was the world people imagined with RDF
  - It's supported today by Google (search engines, Gmail) and other large small companies. JSON-LD, RDFa, microformats.  Works directly with many triple stores with a standard graph query language. Whatever it's flaws nothing is nearly as widely supported.

- Have you looked at Firebird? It's a db that supports ANSI SQL and claims to seamlessly flip between on-disk, in-memory and client/server. I've never tried it beyond v simple local things.

- Didn't consider scuttlebutt but looked at many distributed logs like it. 
  - Two key issues are the need for indexing/querying and an on-disk file format I can expose to local clients, ideally one which is not tied to protocol implementation.

- This is very top of mind for me with http://natto.dev. I've tried representing canvases as text files and using isomorphic git in the browser. The current live version uses yjs, a CRDT, though not syncing. hoping to share the next (final?) iteration soon.

- TabFS is an example of another (perhaps heavier) way to go about it, basically keeping client/server by using a virtual filesystem
  - https://omar.website/tabfs/
  - Technically no cloud, but you are integrating with a foreign and otherwise opaque system
  - TabFS is a browser extension that mounts your browser tabs as a filesystem on your computer. Each of your open tabs is mapped to a folder.

- One observation that @pvh makes is that web browsers aren't a good fit for local-first. They're fundamentally thin clients with throwaway local caches. Maybe that's part of the mismatch for Orbit?
  - Thick clients with a sync-style model like Dropbox, Git, Craft, and Obsidian are easier to fit with this, although often still don't have a user-facing flat file format outside of explicit export.
  - **On CRDTs and merging: I think this is less about realtime collaboration** (although that's important) and more about the fact that once you have multiple sources of truth, there has to be a reliable way to reconcile them.
  - If my phone and my laptop are peers rather than subservient to a central server, it doesn't matter if I'm never "live" editing on both devices. 
  - There will be situations where the changes need to be merged, and Git-style conflict resolution is too heavyweight for many/most apps.

- Currently I’m staying far away from automatic merging of text edits precisely because of the “opaque file format” problem. 
  - But automatic merging of edits made to “conceptually different text chunks” is straightforward in a replicated key/value store & the format is still simple.
- Stopped thinking about storage implementations earlier because I knew that would require another project entirely. Glad someone took a stab at it!

- An in-between solution is to keep source of truth on the server but 
  - (a) guarantee all data can import/export to a simple format like csv, 
  - and (b) periodically export it to user owned place (eg s3, gdrive), so the user doesnt worry that “a” is a fake claim.
