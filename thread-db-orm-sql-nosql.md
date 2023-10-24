---
title: thread-db-orm-sql-nosql
tags: [database, nosql, orm, sql, thread]
created: 2020-11-22T12:10:09.397Z
modified: 2021-05-23T10:17:05.993Z
---

# thread-db-orm-sql-nosql

# discuss-stars

- ## 

- ## 

- ## 真的不能理解喜欢用mybatisplus的QueryWapper的人，手写一个SQL三十秒写完了，QueryWapper 写了我5分钟。而且直接写SQL还能用IDE的代码检查，批量重构，真不理解。
- https://twitter.com/jihuayu123/status/1716749205010837877
- 这玩意只适合单边操作 写复杂sql用wapper就是找罪受
  - 即使是简单操作，Wapper也没见的比sql好写，也没见的比sql可读性高啊
- 我觉得querybuilder最大的优势是能带来编译时检查，但是mybatis plus 的querybuilder做不到这一点，写起来还很不方便
  - 而且mybatis plus写简单sql方面还不如jpa好用
  - 特别是在java template string出来以后

- ## "Hosting SQLite databases on Github Pages" is absolutely brilliant: it adds a virtual filesystem to SQLite-compiled-to-WebAssembly in order to fetch pages from the database using HTTP range requests 
- https://twitter.com/simonw/status/1388933092216164352
  - [Hosting SQLite databases on Github Pages](https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/)
  - Check out this demo: I run the SQL query `select country_code, long_name from wdi_country order by rowid desc limit 100` and it fetches just 54.2KB of new data (across 49 small HTTP requests) to return 100 results - from a statically hosted database file that's 668.8MB!
  - Looks like the core magic here is only around 300 lines of (devastatingly clever) code
  - https://github.com/phiresky/sql.js-httpvfs
- But it does not support updates, right?
  - Of course it can’t write to this file, but a read-only database is still very useful
- I love SQLite but it has it's limitations and if handled improperly it can be a nightmare and even degrade performance & security issues.
  - e.g. not using block SQL transactions will quickly result in read-writes that take millennial(一千年的).
- It used to take me 15 hrs plus to write 10, 000 records to a sqlite file and block commits using transactions reduced that to a few minutes.
  - I used to do a big transaction in sqlite for this, copy the DB file, # pragma synchronized off, write everything, done.
- Are service workers good enough that we can write full stack apps (possibly with @vercel 's NextJs) with SQL + RestAPI + SPA and deploy the whole thing to a CDN?
- We have some fun experiments going with this and actions
  - the hard part is dealing with concurrent actions (and teaching git to diff/merge sqlite) 
  - but the kludgy(不成熟的，蹩脚的) solution of "if push rejected, reset pull and retry" is surprisingly effective
  - Have you got a prototype of git diffing SQLite? That could be fantastic for a whole bunch of my projects. I have a sqlite-diffable thing I've been playing with
  - https://github.com/simonw/sqlite-diffable
  - it works by dumping the DB to plain text (ndjson)
  - ultimately my use-case was append-only, so I went with the retry-upon-failure strategy (which only really matters in case of concurrent action execution). Not elegant but did the trick!

- ## 💡 On the debate between raw SQL & ORMs, I find myself flip-flopping over the years.
- https://twitter.com/tantaman/status/1662123332051914758
- ORMs should be used till you need to tune queries, then you should write your own. If your app starts with raw sql, you’ll eventually roll your own orm for the basics, which is worse.
- What reasons do people usually end up rolling their own in your opinion? I’d like to understand the deficiencies of SQL better so I can improve upon it with some extensions. E.g., composability is a big issue in sql.
  - Extensions to sql? I don’t think that is the right focus. 
  - People roll their own orm because they end up writing the same select, insert, update queries for every table. 
  - An orm is sql composability.
- I think composability & pulling hierarchical (rather than tabular) data is solvable with some minor tweaks to the language --
  - Interesting. What’s your goal? Using sql to query non-relational databases? Or writing more complex queries for current dbs? If it’s the latter, it may be useful on things like client-side SQLite, but I would think it would get hard to nail down performance on large databases.
- Most custom orms are written by teams that didn’t pick an out of the box orm in the first place.
  - And this is a natural journey. Most teams shouldn’t jump to the end. Start with an out of the box orm until you run into performance issues. Then dig a layer deeper to tune your queries. Finally consider denormalizing to nosql if you need it.
  - The journey is orm -> tuned custom queries -> denormalized nosql.

- The final answer is sql if you absolutely need to normalise your data. However that’s rarely the case and you probably should be using document storage, else you need to rebuild your domain model.
  - I find the opposite to be true. Best to normalize asap, always problematic to use a document store.
- The reason I usually avoid relational storage is neatly explained here
  - [DDD & Data Modelling: How Do I Persist Aggregates? - James Hickey](https://www.jamesmichaelhickey.com/how-do-i-persist-ddd-aggregates/)
  - however if you’re not working with aggregates then sql imho is the way to go. 
  - ORM often adds more complexity than it takes away.
- People often use document storage as a way to avoid dealing with sql. This will give issues sooner or later as you still need to model your data [in a DDD way]. Sql just forces you to model [in a normalised way], so it might give the impression to be a better solution.

- Thinking of entities as maps; everytime we update a map, do we generate a string of "update map set key1=value1 where id="? Or every map read, create a string of "select key1 ..." and ask the map to parse it? That's why I don't like raw SQL for 80% of app code that is CRUD 

- I think the strongest argument for ORM’s is enforcing good practices w.r.t SQL injections. That being said I use an ORM mostly because I hate writing SQL and just want to avoid it where I can - but sometimes you can’t avoid it for performance
- There are some good frameworks that leverage typed format strings to eliminate SQL injection. E.g., in the JavaScript world, this one that creates a `sql` template tag which escapes  variables provided to the template string
  - yeah this is a great alternative to ORM's!
- I would love a DB abstraction that lets my app do relational reasoning and lenses over projections in a much simpler way than Apache Calcite
  - Odds that someone somewhere has a `SQL -> Calcite -> ORM'ed Objects -> SQL` flow?
- I dont like building my own migration frameworks and always want someone to figure out the best possible moves there for my DB. I built Notion’s SQLite one after a bunch of research and its fine
  - there was nothing out there that fit our use-case of "talk to SQLite from a browser app over IPC to a native app"
- ah ok. I (eventually) need a migration thing for my kv store, and i cant find much out there about kv database migration…
  - If you don’t have transactions, IDK. Generally people run a job to iterate the key space and copy v1 records to v2, and then a cleanup job that re-enques anything written to v1 keys to get migrated again. Finally at some point you decide you’ll read and write only v2 records.
- For KV things I try to draft off of what people do with DynamoDB. Maybe this can serve as inspiration
- https://github.com/sensedeep/onetable-migrate /js
  - This library provides migrations support for DynamoDB OneTable.
- this is cool, thanks! The up/down idea is similar to what I had in mind. Also looking at stripe’s versioning thing
  - Seems the idea is basically a pipeline of versioned codecs.

- I'm a fan of just using SQL. SQL is already a wonderful abstraction over data storage. Treating a relational database like nested documents just leads to confusion. (Nothing wrong with nested documents, but then... why use an RDBMS?)

- There's a nice sweet spot with query builders, especially if they're very thin & map 1:1*. 
  - Writing raw SQL only, more often than not, you end up maintaining your own query builder logic. 
  - You should'nt do it in-house, especially when Knex & @kysely_ exist, proven, battle-hardened

- IMHO: ORMs are just another thing to learn and debug. Never have I worked on a project that uses an ORM where I didn’t have to also write & read SQL.

- It depends, but just use SQL (with a query builder if needed). Kill ORMs
- Query builders can be a nice middle ground in my experience

- ## There is one place where having an ORM was unequivocally(表达明确的；毫不含糊的) the right decision and much of my career was built on extending it to get developers to "do the right thing.". That place was Meta.
- https://twitter.com/tantaman/status/1662502624963223560
  - The Ent framework at Meta:
1. Let us colocate privacy rules with data. Each entity definition was required to have read and write privacy policies.
2. Data validation & migrations.
3. Integrations. The SDL, being code, could be extended by devs to support use cases outside of data storage.
4. Arbitrary backends.
5. Arbitrary indexing services.
6. Deletion.

- If your ORM only talks SQL, can't link multiple datastores, doesn't support extending it's codegen with custom plugins, doesn't support row level security, can't do dual reads and writes to support live migrations -- then you might as well stick with raw SQL.
# discuss
- ## 

- ## 

- ## 

- ## AFAIK the technique used in SQL WHERE queries with index support relies on building a bitmap which represents keys that satisfy the query. 
- https://twitter.com/Horusiath/status/1634447500525404163
  - Can anyone point me to a source code where such bitmap is being build by the query executor?
- [Bitmap Indexes - PostgreSQL wiki](https://wiki.postgresql.org/wiki/Bitmap_Indexes)

- ## how & why #ScyllaDB engineers moved to B-tree & B+-tree data structures for linear search in their #NoSQL distributed database.
- [The Taming of the B-Trees](https://www.scylladb.com/2021/11/23/the-taming-of-the-b-trees/)

- ## Very common mistake in ActiveRecord: checking for the existence of a `belongs_to` associated record with `present?` or `blank?` . 
- https://twitter.com/nateberkopec/status/1441406828424822792
  - This is an almost-guaranteed N+1. 
  - You have the foreign key on the record you're looking at - just check if the foreign key is `nil?` .
- If you have a situation where the foreign key might be set but the record doesn't exist: fix that problem before it begins, don't defensively code around it here and shoot yourself in the kneecap.
- ActiveRecord does such a strong job auf abstracting the _id away, so it would awesome if it could do that too in these situations…

- ## I honestly just feel kinda embarrassed for people still arguing about ActiveRecord.
- https://twitter.com/taylorotwell/status/1420402348216786950
  - Friendly reminder that no matter how you feel about this Tweet, all of the code you push to GitHub today will be handled by a platform that uses ActiveRecord.
- Writing code vs arguing on Twitter about the best way to write code. I'll take the former
- When there are multiple ways to solve the same problem, arguments and turf wars always keep happening! 
  - Examples: Vim vs Emacs, Linux vs Windows, Ubuntu vs Fedora, PHP vs Python, etc. etc. ActiveRecord vs DataMapper is just another item on the Yin/Yang pattern

- ## Show HN: FaunaDB, a strongly consistent, globally distributed cloud database__201703
- https://news.ycombinator.com/item?id=13879475
- > It’s relational, but not SQL.
  - Why not? If you already support relational algebra, it seems like a non-brainer to just add SQL. Even if it's only SQL-92 you would be able to support some existing tools/ORMs almost for free.
- This is explained a bit in a blog post[1]. Basically, this is because FaunaDB uses Calvin to do distributed transactions, which makes it hard to support OLAP-style SQL sessions. (If I understand the Calvin paper[2] correctly, this has to do with a combination of how it doesn't support "dependent" transactions, and how it does concurrency control.)

- ## Do not generate database tables on the fly
- https://twitter.com/sseraphini/status/1397888359910055940
- it has some use cases tho, when you don't know which entities and columns you gonna store, and you don't want to use JSON/JSONB for all data
  - Just use nosql
  - in the case of where I'm working we probably use sql because we want to store structured/relational data, we just don't know the tables/columns beforehand.they are user defined (mapped from something else)
  - @MongoDB shine on this. you can use a wildcard to even make optimize queries on user defined data

- ## MikroORM: One ORM to rule them all
- https://www.reddit.com/r/node/comments/nia2i5/one_orm_to_rule_them_all/
- Mikro absolutely thrashes TypeORM with its hands tied behind its back. 
  - It even gives Prisma a run for its money as well (I’ve used all three of these in high load applications at scale). 
  - Unit of work is wonderful and “just works” once you properly connect it to your request context.
  - The only thing that was killing me was **lack of type safety when calling `toJSON()` **, but that’s already staged for the next release!
- My question is are you able to do everything using an ORM efficiently? Or do you still write complex SQL’s? For my job, we don’t use an ORM, and have basically a long list of a couple hundred stored procedures in Oracle DB to do every task. What are your views on this?
  - Any ORM will give you a “perfect” query for simple stuff, and I’ve found it’s a perfect fit for 95% of queries. 
  - You absolutely have to drop down to pure sql for the more complex queries.
  - Analytics, multi-joined counts, and extremely large where clauses are usually good candidates.
  - Prepared statements are an awesome choice! I’d say that the only downside is that it generally aces your front end devs out of making tweaks to those endpoints, which really depends on how your company operates.
  - One more thing: make sure you’re always checking the cost of your most used queries (something that’s less intuitive on an orm). I’ve been burned on queries that “felt” fast and then got extremely slow once the table had a few million rows.
- TypeORM died when MikroORM came out. The documentation sucks, it's buggy as hell and the type-safety doesn't even come close to what MikroORM offers, let alone all the issues with getting the CLI to work.
  - I wrote a pretty detailed comment on how MikroORM compares to Prisma, using their own selection of features that Prisma advertises against TypeORM, and think MikroORM absolutely holds its own against Prisma.
  - Prisma's main advantages at this point are type-safety, at the cost of flexibility. Since Prisma returns objects, it can use generics in a completely different way, but that also makes it less of a traditional ORM, meaning you can't leverage after-the-fact loading of relations, computed fields, or any sort of business logic in models.
  - MikroORM on the other hand offers nearly the same level of type-safety with helpers like isInitialized(), load(), while still giving you full access to the underlying query builder (KnexJS), entity manager for hydration, and properly leverages DB transactions the way an ORM should.

- ## One of the biggest limitations of a static site is the inability to host a queryable db with it w/o loading the entire db
- https://twitter.com/privatenumbr/status/1389041601494855685
  - Turns out this is actually possible by segmenting a sqlite db into smaller chunks. Very inspiring!

- ## Made my database access about 20x faster (and smaller!) by removing some tables and storing json in sqlite instead. 
- https://twitter.com/steipete/status/1378633040289792009
  - The JSON1 extensions are compiled into iOS and make queries super easy. 
- Worked with a German car manufacturer during my bachelor‘s thesis. We tried many different things to optimize database performance: schema normalization, in-memory search in the app, etc. What helped most with least effort? Installing a freaking indexing plugin for text fields 
- How did you identify those tables and json -> sqlite to make db faster? Analysing db queries processing time?
  - One table had on average 100x more rows than the others 😬
  - And yeah track time in queries
- For most apps we use json files instead of a database. Not possible for all apps but it is waaay faster when it is possible.
  - We have done it even with large data sets. The large bulk could be referenced by an id (= filename) so not generally applicable, but still.
  - We have another app with read/write data sync’ed with backend, everything in json files. Works great. Again, no generally applicable.
- It's not possible to query on JSON values - or is it?
  - SQLite supports partial indexes and indexes on expressions, as ‘big’ DBMSs do. You can build indexes on generated columns and even turn SQLite into a document database.

- ## Declarative data modelling has been the heart of @KeystoneJS from the start, but mapping it to SQL database structure is proper hard. 
- https://twitter.com/JedWatson/status/1369644213067935745
- The balance @prisma have struck with Migrate - auto gen’d sync, with the escape hatch of real SQL when you need it - is a game changer

- ## This is probably why planetscale.com is using MySQL instead of Postgres 
- https://twitter.com/flybayer/status/1368749877044318214
  - [Why Uber Engineering Switched from Postgres to MySQL_201607](https://eng.uber.com/postgres-to-mysql-migration/)
- It would be interesting to know if Postgres architecture is still the same after 5 years since the article. We are thinking of switching from mysql to postgres for better json management
- They're using MySQL because of Vitess planetscale.com/vitessI
  - The article is very old. Postgresql was and is far superior to MySQL in almost every way. 
  - Quite an amateurish article from uber. Or, if I may , done in the Stackoverflow way, written by a person with not much of an academic background. Hey, everyone can be an engineer after all!

- ## Guilty pleasure: I sort of like writing SQL.
- https://twitter.com/BenLesh/status/1364681180021329922
- I enjoy doing a thing akin to SQL Golfing... 
  - where I try to have any report/export being done 100% in SQL 
  - my code is just making the query and sending the result as json
- Yeah, we definitely can't be friends anymore.
- I like how there's not a lot of ambiguity in SQL, 
  - unlike typeof undefined === "undefined" (true) or typeof undefined === undefined (false)
- SQL is beautiful maths with quirky syntax.
- It's algebraic set theory in concrete terms.

- ## [Geode 和 redis 两个分布式内存数据库的对比，优缺点？](https://www.zhihu.com/question/31699176/answers/updated)
  - Geode是分布式内存数据库，提供了可配置的一致性保证，能够保证数据不丢失，更符合数据库的定位。
  - 而Redis的定位本身就是缓存，采用的最终一致性和周期性持久化策略，在单服务进程模型下，提供了高性能缓存服务
  - Geode是java生态圈，有多种运行模式，可以lib方式运行在client端，其支持的客户端语言有限。
  - Redis引擎是C编写，运行更高效，性能损耗低，由于交互协议简单，支持的客户端语言众多，基本上常用的语言都能够支持。
  - 其实这两者的比较不在一个维度上，

    - 一个是应用场景定位，前者更看重数据安全性、后者作为缓存更看重性能；
    - 一个是上手难度，前者上手比较困难，运维起来也会复杂很多，后者上手简单，集群化方案也比前者简单；
    - 从社区活跃度方面来看，前者社区不怎么活跃，DB-ENGINES在kv存储中排名23， 后者社区活跃，应用广泛，在kv存储中排名第1。

  - 准确的说，Geode不是内存数据库(In-Memory DataBase, IMDB)，而是有数据库功能的内存数据网格（In-Memory Data Grid, IMDG）。

    - 在CAP原理下，Geode可以保证集群内数据的强一致性，注意是真正的强一致性而不是最终一致性，再加上分区可用性，因此是一个CP型的产品，可以提供统一的数据视图，支持高并发下的acid事务。
    - 而Redis是不保证一致性的，因此即使Redis集群，也只能是AP型产品。
    - 另外Geode还有内置的pub/sub，逻辑分组和管理监控等一系列企业级产品功能，因为Geode项目本身就是Pivotal公司把十几年历史的及其成熟的GemFire开源贡献给Apache的顶级项目。

- ## [ObjectiveSQL: 让Java更像SQL](https://www.v2ex.com/t/727939)
- 到底是让Java像SQL一样编程，还是让SQL像Java一样编程，纠结了很久，还是让Java更像SQL，
  - Java的语法表现力不够，只能扩展Javac，实现了算法运算，比较运算，逻辑运算符重载，并封装了常用数据的的函数，抽象了Expression，使Java非常接近SQL，
  - 同时也实现了简单SQL编程的代码生成，基本不需要写代码，也不需要配置就能实现简单SQL的编程
- 我对比过mybatis的 `DynamicSQLBuilder` ，它做的太土了，大都数都是以字符串的形式体现，我的改进有三块：
  1. 动态代码生成：模型中的所有字段都会被动态生成一个Order的内部类Table中的字段。
  2. 算术运算、比较运算符和逻辑运算重载，也就是说Java中的 +, -, * / , >, <, &&, || 都会转换成SQL语句中的表达式，
  3. 我封装了常用数据库的常用函数，例如：count, sum等有上千个的，这样就不会出现字符
  - 上述做法的好处是，最大程度的避免的SQL的语法错误，动态代码提示和单元测试。

- ## Is there an IndexedDB equivalent for Node.js?
- https://www.reddit.com/r/javascript/comments/4ohy5t/is_there_an_indexeddb_equivalent_for_nodejs/
  - IndexedDB is a good thing inside browsers, but I wonder why isn't such a thing not available for Node. JS? 
- https://github.com/bigeasy/indexeddb
  - A pure Node.js implementation of the async W3C Index DB API.
- The reason something like that doesn't exist on the BE is that for size that small you can load it fully into memory, as such it is easier to just use a JSON file for persistence.
  - For larger dataset without a server there are BerkeleyDB, LevelDB, and KyotoCabinet. 
  - However, those are generally designed to be database backends rather than used directly by applications. 
  - For larger data sets, you really should use a database of sort, as they would manage what is kept in memory and what is left on the disk.

# ref
- [OceanBase的一致性协议为什么选择paxos而不是raft?](https://www.zhihu.com/question/52337912/answers/updated)
