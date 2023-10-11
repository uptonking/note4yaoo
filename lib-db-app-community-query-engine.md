---
title: lib-db-app-community-query-engine
tags: [community, database, query-engine]
created: 2023-09-17T17:41:27.117Z
modified: 2023-09-17T17:41:51.689Z
---

# lib-db-app-community-query-engine

# guide

# discuss-stars
- ## 

- ## 

- ## 🌰 ai based search for tldraw's docs
- https://twitter.com/tldraw/status/1712099716966547787
  - uses @OpenAI to create vector embeddings from our docs files
  - stores the embeddings into a local vector database (vectra by @stevenic)
  - creates an embedding from each query
  - searches the vector database using that embedding
  - results and ranks the results
- I think the hard part here is setting priorities, like articles should be more important than headings inside of the articles, etc. So we've still got some work to do!

- 🤔 is it wrong to ship a local vector database with your app
- nah, don't even have to call it a db, just a scan through a bunch of arrays is fine
- No it’s good. do it but for layers on the canvas
- What is the service behind? Algolia?
  - Nope, literally a vector db and a call to openAI's embeddings endpoint
- Nope, literally a vector db and a call to openAI's embeddings endpoint

- ## I’m seeing more and more devs writing db queries directly inside their API route handlers and I find it quite bizarre. Where do you write your db queries?
- https://twitter.com/ImSh4yy/status/1711092090103267784
- In NestJS: Controller => service => DB query using Prisma
- In the repository: Repository -> Service -> Controller
- For a POC, the router. 
  - For an serious app, i follow the adaptor pattern (glorified way of saying domain based functions called by the routers/controllers)
- Why is this bizarre? With a good ORM like Prisma, this is becoming the norm tbh
  - It's a matter of "separation of concerns, " which is then translated into several important "abilities" in the code: readability, maintainability, scalability, reusability, etc.
  - Accessing the database from all over the place is a code smell, in fact a big one, imo, and could cause many issues as things start to grow. 
  - As a basic example, imagine you want to start caching certain queries. If your db is being accessed from all over the place, you'd most likely run into many issues trying to ensure every query is properly cached and invalidated at the right time.
- I break all the queries into their own Query controllers and only expose them to the rest of the code as an abstracted layer.
  - Router -> Controller -> Query

- I abstract all DB queries inside “services” or “controller” classes. Not just DB queries but all IO related operations.

- "Early stage, " "iteration speed, " "MVP, " etc., are all excuses for writing shitty code.
  - **it's bad practice to write db queries inside your router** alongside all its other responsibilities.
  - Spending a few seconds abstracting away some database queries is negligible compared to the time it takes to debug issues that arise from the few seconds you thought you were saving.
  - Premature optimization and overengineering are indeed a waste of time during the MVP and early stages of a product. However, writing clean, well-structured code isn't either of these.
# discuss-view
- ## 

- ## 

- ## [Practical advice for creating (and updating) materialized views? : PostgreSQL](https://www.reddit.com/r/PostgreSQL/comments/hvysvi/practical_advice_for_creating_and_updating/)
- Dimtri Fontaine recommends using the publish / subscribe messaging queue feature, ON UPDATE and have a listener that consumes the message and triggers the refresh

- ## [Materialized Views vs Views](https://www.reddit.com/r/SQL/comments/158498q/materialized_views_vs_views/)
- I could be wrong, but the way I view (ha) this is:
  - A View is a dynamic query. It is a table that is not stored, but rather it is a select query that is executed every time you query that view.
  - A materialized view seems to be the result of a query that is stored on disk, meaning it is not dynamic and does not change unless you refresh it or overwrite it somehow.
  - So if your original table is updated somehow, the view will also bring that new information while the materialized view won't change.
- If your view is joining a lot of tables or is doing something complicated/not optimized very well and is slow to load. It may be better to create a materialized view so that the result is stored to disk

- to the end-user, a View is basically just a table. It has a query which produces the view, but when you work with a view, you treat it like a table.
  - A Materialized View simply caches the result (on disk) such that the underlying query doesn't need to be run each time. You might use something like this to set up some historical sales data for an analyst. 

- There’s a difference between materialized views in Oracle and SQL Server though.
  - In Oracle it’s as you describe: a view stored on disk that is refreshed periodically to increase performance of slow running views.
  - In SQL Server, a materialized view is created when you add an index to the view. SQL Server will keep the MV current without having to schedule periodic refreshes.
# discuss
- ## 

- ## 

- ## ✨ This brilliant technique for handling database queries literally saved Discord.
- https://twitter.com/ProgressiveCod2/status/1708007839170482666
  - It helped them store trillions of messages and fetch them without bringing their DB cluster to its knees.
  - The technique is called Request Coalescing(联合；合并).
- Here’s what happens under the hood:
  - The first user that makes a request causes a worker task to spin up in the data service
  - Subsequent requests for the same data will check for the existence of that task and subscribe to it
  - Once the initial worker task queries the database and gets the result, it will return the row to all subscribers at the same time.
- There are several pros to using Request Coalescing:
  - Efficient utilization of database resources
  - Ability to handle more concurrent requests without creating hot partitions
  - Reduce latency
- But there are some cons as well:
  - Implementation can be complex with regards to getting a fair distributed reader-write lock. Basically, multiple readers need to access the data simultaneously while preventing conflicting writes
  - Overall latency may go down, but certain requests will take more time
- this technique is NOT needed normally. But at a certain scale, it can actually save your business

- 🤔 Caching results achieves the same effect (querying the DB once) without added complexity. Why choose Request Coalescing instead?
  - their logic was probably like - If 10 clients ask for the same data at the same time, that's 10 db fetches if they all see a **cold cache**. With request coalescing that's 1 fetch that fulfills all 10 clients.
  - So I guess the main reason for choosing this was unbounded concurrency.
- The problem with hitting a cold cache you’re describing is known as cache stampede(惊逃，乱窜). It’s a real issue for highly loaded systems. However, there are mitigation(缓和; 减轻) strategies, such as locking or cache refresh ahead of expiration
- Caching could be done separate from this. This layer optimizes when caching expires and you end up with N requests trying to repopulate cache.

- How is this diff from cache layer ton top of database?
  - This technique is not a replacement for cache. The idea is to handle concurrent requests waiting for the same task (DB fetch) to complete. Also, in Discord's case, message data might change frequently where cache invalidation becomes a costly solution.

- why not to use redis? As we know, same record is being requested multiple times. That will reduce IO operations.
  - This technique is not a replacement for cache. The idea is to handle concurrent requests waiting for the same task to complete and that is fetching the record from a data source (DB or cache). The scale at which this might be needed is simply not there for most apps.
- When you cache for Discord, the data might change, or something might be updating the DB ( messages ); also, to cache, you have to write and delete again costly thing. It is better to take a pool read once and relay it to the pool.
  - Good points

- 
- 
