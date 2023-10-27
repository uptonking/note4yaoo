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

- ## 🚀🔥 [EventReduce: An algorithm to optimize database queries that run multiple times | Hacker News_202004](https://news.ycombinator.com/item?id=22888239)
- Materialize exists to efficiently solve the view maintenance problem: https://materialize.io/
- Any database which offers what are called "continuous queries" also solves this problem. 

- 🤔 Sooo...is this Materialized/Indexed Views?
- Materialized views solve a similar problem but in a different way with different trade-offs. 
  - When you have many users, all subscribing to different queries, you cannot create that many views because they are all recalculated on each write access to the database. EventReduce however has a better scalability because I does not affect write performance and the calculation is done when the fresh query results are requested not beforehand.
  - Others have pointed this out already: This is wholly dependent on the RDBMS used, and Oracle offers incremental refresh on demand. I have to admit though that I mistakenly thought that MSSQL would as well...
- Correct me if I'm wrong, but Materialized Views have the limitation that you need to refresh the entire view! Often you know which rows will change based on the data you receive.
  - This depends on the RDBMS. Oracle for example has incremental materialized view updates.

- ## [A Data Pipeline Is a Materialized View | Hacker News_202102](https://news.ycombinator.com/item?id=26217911)
- although built-in materialized views don't allow partial updates in Postgres, you can get a similar thing with normal tables and triggers.
- Of the traditional RDBMSs, I believe Oracle has the most comprehensive support for materialized views, including for incremental refreshes.
- SQL Server has indexed views, which is "real time" refresh since it's a separate clustered index that's written to at the same time as the base tables.
- Well, indexed views aren't materialized views per se, they are a tradeoff between maintenance and deterministic performance.
  - A materialized view is nothing more than a snapshot cache, a one time ETL job. So it can abide by any constraints and is completely untethered from the data that created it. So you have to create your own maintenance cycle, including schema validation and any dynamic / non-deterministic aspects of the MV.
  - An indexed view is modified just like the clustered index of any tablr object upon which it depends, as an affected "partition" of the DML. That's what the SCHEMABINDING keyword is for, binding the view to any DML statements of its underlying base table(s). So no need to maintain it at all, at the expense of conforming to a fairly rigid(刻板的；严格的) set of constraints to ensure that maintenance is ..umm ..maintainable.
  - In practice most views' logic are perfectly simpatico with the constraints of an indexed view - the tradeoff is write performance vs the "cache hit" of your view.
  - I do way more OLAP/HTAP engineering in my day job so indexed views are less common vs. Columnstores, but indexed views are a highly underutilized feature of SQL Server.

- Data engineering really is just a maintenance of incrementally updated materialized views, but no tool out there yet recognizes it. They at best help you orchestrate and parallelize your ETLs across multiple threads and machines. They become glorified makefiles at the cost of introducing several layers of infrastructure into the picture (eg. Airflow) for what should have been solved by simple bash scripting.

- DBT is interesting, but is far from what I'm describing.
  1. It is only for structured SQL, not for arbitrary data. I can't use it to unpack raw zipped data for example
  2. It couples logic for data transformation and view state management. Actually it makes you do it yourself, so it doesn't really help at all. You'll get burned by storing view state together with your data, eg. when a batch increment contains no data.
  3. It is not built with "incremental materialized views" in mind. It still thinks in a batch refill mode and incremental mode according to this [0].
  - It is certainly an improvement over managing sql scripts by hand, but far from the ultimate goal of maintaining materialized views in a declarative way.
- dbt doesn't do much automation/ETL outside of the database you're working in, as other tools might be able to.

- 
- 

- ## [Materialize Raises a $32M Series B | Hacker News](https://news.ycombinator.com/item?id=25277511)
- Materialize is an "RDBMS" (though it's not, really) engineered from the ground up to make these sorts of dataflow graphs of matviews-on-matviews-on-matviews practical, by doing its caching completely differently.
  - Materialize looks like a SQL RDBMS from the outside, but Materialize is not a database — not really. (Materialize has no tables. You can't "put" data in it!) 
  - Instead, Materialize is a data streaming platform, that caches any intermediate materialized data it's forced to construct during the streaming process, so that other consumers can work off those same intermediate representations, without recomputing the data.
- If you've ever worked with Akka's Streams, or Elixir's Flows, or for that matter with Apache Beam (nee Google Dataflow), Materalize is that same kind of pipeline. 
  - But where all the plumbing work of creating intermediate representations — normally a procedural map/reduce/partition kind of thing — is done by defining SQL matviews; and where the final output isn't a fixed output of the pipeline, but rather comes from running an arbitrary SQL query against any arbitrary matview defined in the system.

- RDBMSes enable you to create materialized views only for data in the database. 
  - Materialize enables you to do this for any streaming data source in your organization, with the ease of writing SQL. This enables you to simply write a SQL statement joining data from Salesforce + SAP + Siebel as soon as the data changes, and store the results as a near real-time up to date database table. 
  - It does depend on a lot of underlying plumbing: streaming platform (e.g. kafka), and streaming data sources (e.g., kafka connect + debezium).

- What exactly are "materialized views"?
  - It's a query of which you save the results in a cache database table, so next time when it is queried, you can provide the results from the cache.
  - Typically, in a traditional RDBMS, the query is defined as a sql view, which you either have to manually refresh, or can be refreshed periodically.
  - Using streaming systems like kafka, it's possible to continously update the cached results based in the incoming data, so the result is a near realtime up to date query result.
  - Writing the stream processing to update the materialized view can be complex, using SQL like materialize enables you to do, makes it a lot more productive.
- a materialized view is a view with a cached result-set
  - But like any cache, it needs to be maintained, and can become out-of-sync with its source.
- Although materialized views are part of the SQL standard, not all SQL RDBMSes implement them. 
  - MySQL/MariaDB does not, which is why you'll find that much of the software world just pretends matviews don't exist when designing their DB architectures.
- The naive approach that some other RDBMSes (e.g. Postgres) take to materialized views, is to only offer manual, full-pass recalculation of the cached result-set, via some explicit command (REFRESH MATERIALIZED VIEW foo). 
  - This works with "small data"; but at scale, this approach can be so time-consuming for large and complex backing queries, that by the time cache is rebuilt, it's already out-of-date again!
- Because there are RDBMSes that either don't have matviews, or don't have scalable matviews, many application developers just avoid the RDBMS's built in matview abstraction, and build their own.
  - Thus, another large swathe(长而宽的一条) of the world's database architecture either will use cron-jobs to regular run+materialize a query, and then dump its results back into a table in the same DB; 
  - or it will define on-INSERT/UPDATE/DELETE triggers on "primary" tables, that transform and upsert data into "secondary" denormalized tables. 
  - These are both approaches to "simulating" matviews, portably, on an RDBMS substrate that isn't guaranteed to have them.
- Other RDBMSes (e.g. Oracle, SQL Server, etc.) do have scalable materialized views, a.k.a. "incrementally materialized" views. 
  - These work less like a view with a cache, and more like a secondary table with write-triggers on primary tables to populate it — but all handled under-the-covers by the RDBMS itself. 
  - You just define the matview, and the RDBMS sees the data-dependencies and sets up the write-through data flow.
- Incrementally-materialized views are great for what they're designed for (reporting, mostly); but they aren't intended to be the bedrock for an entire architecture. Building matviews on top of matviews on top of matviews gets expensive fast. These RDBMS's matviews were never intended to support complex "dataflow graphs" of updates like this, and so there's too much overhead (e.g. read-write contention on index locks) to actually make these setups practical. And it's very hard for these DBMSes to change this, as their matviews' caches are fundamentally reliant on database table storage engines, which just aren't the right ADT to hold data with this sort of lifecycle.

- How were previous implementations of materialized views deficient?
  - Not really mentioned here, but in standard postgres it might be quite expensive to update the view so you can only do it periodically. Materialize keeps that up-to-date continuously.
  - Joins were unavailable or subject to extreme limitations. Or just plain wrong!

- Isn't this pretty similar to what Dremio does?
  - Dremio is a batch processor, not a stream processor. The fundamental difference is that a batch processor will need to recompute a query from scratch whenever the input data changes, while a stream processor can incrementally update the existing query result based on the change to the input.
  - This can make a huge difference when making small changes to large datasets. 

- The headline refers to "incrementally updated materialize views". How does a company get funding for a feature that has already existed in other DBs for at least a decade?
  - Incrementally-maintained views in existing database systems typically come with huge caveats. In Materialize, they largely don't.
  - Most other systems place severe restrictions on the kind of queries that can be incrementally maintained, limiting the queries to certain functions only, or aggregations only, or only queries without joins—or if they do support maintaining joins, often the joins must occur only on the involved tables' keys. In Materialize, by contrast, there are approximately no such restrictions. Want to incrementally-maintain a five-way join where some of the join keys are expressions, not key columns? No problem.
  - That's not to say there aren't some caveats. We don't yet have a good story for incrementally-maintaining queries that observe the current wall-clock time. And our query optimizer is still young

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

- ## 🔥 [Show HN: Query your database using plain English, fully on-premises | Hacker News_202308](https://news.ycombinator.com/item?id=37315667)
- 
- 
- 

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
