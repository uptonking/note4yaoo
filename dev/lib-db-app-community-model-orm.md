---
title: lib-db-app-community-model-orm
tags: [community, database, orm]
created: 2023-09-24T19:05:18.256Z
modified: 2023-09-24T19:05:33.866Z
---

# lib-db-app-community-model-orm

# guide

# discuss-stars
- ## 

- ## 

- ## SQL may have all those problems, but the main use case for ORMs is the mapping of relational data to objects. 
- https://x.com/penberg/status/1906236557125677356
  - SQL is increasingly just the the universal database protocol enabling ORMs.
- SQL was designed as a user facing language, not as a programming interface.
  - Yes, 100%! However, it also functions as a decent intermediate representation for ORMs to access b-trees, which is why i think of it as imperfect, universal data access protocol

- ## 🏘️ I’m seeing more and more devs writing db queries directly inside their API route handlers and I find it quite bizarre. Where do you write your db queries?
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
# discuss-orm-usage-tips
- ## 

- ## 

- ## 还是得用 ORM，一个小项目觉得简单直接上 SQL，现在想加功能都提心吊胆的，生怕手写的 SQL 出问题。
- https://x.com/noobnooc/status/1913445803420717218
- ORM能做到的上限很低的，只有手写SQL的20%。报表类查询就需要很多手写SQL。另外高级的约束和衍生数据(derived data)都需要写触发器，这也是ORM做不到的
  - 日常应用层的业务大部分都能满足了，有些查询用 ORM 解决不了还可以换回 SQL 。完全不用 ORM 的话，业务层一堆 SQL 我都不太敢改

- ## prisma 真是被炒作过头了。。。准备迁移到 drizzle
- https://x.com/rxliuli/status/1893181573769408894
- drizzle 好用，全都在 ts 内解决，没有 dsl，深度体验写了两个项目，一个接 aws rds 标准 CI/CD 升级，另一个接 supabase 快速开发都很方便。
- 原生 SQL 永远都是一个选择，迁移起来也挺痛苦的，prisma 把默认值、updatedAt 之类的都放到程序抽象层去实现了
- 虽然查询上prisma方便一些，但它的问题是好像没办法通过代码来控制迁移，只能用cli来控制迁移
  - 用docker做web应用时，还可以勉强用http://entrypoint.sh来执行prisma migrate deploy。但用electron做桌面应用时，我已经完全想不到办法了
  - drizzle就没这个问题，而且打包后docker镜像也会小不少

# discuss-against/cons
- ## 

- ## 

- ## I will never use an ORM again, in any project. Use the repository pattern. Avoid SQL injection by never passing raw text through to the repo abstraction.
- https://x.com/thrawn01/status/1925911513304289748
- most repositories are basically ORMs in practice, they’re one pattern, but they typically bind underlying SQL to native classes/structs, definitely an ORM. 

# discuss
- ## 

- ## 

- ## 🦀 目前见过最变态的设计之一，sqlx postgres 的 Transaction RAII rollback 的实现会在 connection buffer 里面写一个 ROLLBACK 语句，然后在归还连接池的时候跟着这个 ping 一起发送。
- https://x.com/leiysky/status/1934181807727198610  
  - 也就是说不用 sqlx 的连接池而自己管理连接的情况下 rollback 只能等有缘人发送了

- ## ORMs exist because SQL is inexpressive and has a bad type system. They don’t fix the underlying problems but do mask them somewhat. 
- https://x.com/jamesacowling/status/1906054483186212893
  - Raw SQL is too dangerous to use in large production app code though.
  - With ORMs there’s no real type bijection and they operate on the schema they know, not what may have drifted in the DB. I’m no Prisma/Drizzle hater though and a modern ORM is safer than raw SQL, responding to OP. 

- I would argue that SQL has an incredibly expressive and beautiful type system, which is very well suited for operating a cash register or computing regional sales numbers, but too constrained for modern OLTP apps
  - Storage types aside, the text-based SQL query language has very loose typing/guardrails. There aren’t many languages where it’s easier than SQL to make a minor typo and destroy your entire company.

- ## 各种流行的orm都有一些先天性的不足，比如很难描述partition, merge into和CTE等高级请求，甚至是复杂一点的transaction。
- https://twitter.com/geniusvczh/status/1762750265089007886
  - 这些硬伤会导致你哪一天真的用上的时候，会发现手写sql难以跟用了orm的部分保持状态的一致性，最后只能全部代码删掉重来。这才是我认为orm 不好的的地方
- 最麻烦的一点是，代码里用了ORM的模型，就得处处使用，还不如自建模型，底层用原生SQL和DB Helper函数hybrid编写。
- 所以我觉得说不定可以把数据访问层搞成接口，前期用EF实现，后期有必要的话用裸SQL/SP慢慢重写就行了。

- ## 💡 what would the functional equivalent of an ORM look like?
- https://twitter.com/Aron_Adler/status/1751208146498957430
- DDL isn't declarative and should be. At least, should be more declarative.
- Let me give a concrete example. Suppose columns had both a name and an ID, a bit like protobuf. 
  - Then when you supply a new table definition, the IDs would determine the column identities, and many schema evolutions would be unambiguous.
  - Columns could be added, removed, renamed, and reordered with no ambiguity, given only the desired target state.
  - This needs more thought to pin down all the corner cases, but the point is, a small change to the way tables work could make schema evolutions a lot less imperative.
  - and that doesn't work with SQL tables in their current form because those evolutions are inherently ill-defined.

- My answer is Squeal(haskell). I applied category theory for a strongly typed embedding of SQL including DDL and DML in Haskell. For instance DDL statements form morphisms of a category whose objects are schemas. 

- Elixir's Ecto does a good job of being a really thin ORM-like.

- There’s a clojure library called korma you could check out.
- Slick is a Scala library that calls itself a Functional Relational Mapper.

- Maybe look at LINQ. One idea is that querying in-memory and DB data is similar.

- ## I agree  with @ThePrimeagen that SQL ORMs are a leaky abstraction 
- https://twitter.com/matthew_linkous/status/1721930302321295426
  - but the real takeaway is that SQL is not a good fit for building apps - that's why there's so many people reaching for ORMs in the first place

- ## 🔥 [Prisma – Database tools for modern application development | Hacker News_201904](https://news.ycombinator.com/item?id=19598287)
- 
- 
- 

- ## [Is ORM still an anti-pattern? | Hacker News_202306](https://news.ycombinator.com/item?id=36497613&p=2)
- In any sufficiently complex application, something like a query builder that allows different parts of the application to work together to lazily compose queries (vs combining/filtering/sorting the data in memory) will be created at some point.
  - ORM is a tool that can make this easier, it's also a tool that can make it easier to shoot yourself in the foot (ie by making it easy to create N+1 queries without knowing). Like all tools, there are tradeoffs that need to be accounted for together with the actual use case to make a decision. Operating on SQL statement strings is not something I'd recommend in any case.
- LINQ isn’t exactly an ORM. You create strongly typed LINQ statements that are turned into expression trees that are then turned into a query by a query provider.
- Good points! As someone who uses both ORM and raw SQL (I actually really like SQL as language) I sympathize with both sides of this debate. 
  - I prefer the readability of ORM in my models when developing, but closely monitor and optimize for N+1 and other inefficiencies, when needed. "When needed" is never cut-and-dry, but I try not to optimize too early. 
  - I actually tend to start new projects from the database and will scaffold with factories, seeders, and raw SQL queries to get a sense of the data model prior to coding.
  - ORM's such as Eloquent in Laravel also have some nice methods to resolve N+1 and perform lazy loading, but it's always tradeoff.

- the line between an ORM and a query builder is a very blurry one
  - your query builder isn't just string based to avoid a lot of potential bugs which are easy to introduce and miss in tests? It also has a simple way to (de)serialize row from/to POD structs? Now you already have a thin ORM.

- A point I'm missing is: without using an ORM (or however else you're calling your database interface) you will eventually end up writing and maintaining one yourself, at least for CRUD stuff, and it will be filled with weird bugs, edge cases and security holes.

- ## [What ORMs have taught me: just learn SQL (2014) | Hacker News_201909](https://news.ycombinator.com/item?id=21031187&p=2)
- Will tend to agree with the author.
  - Initially ORMs can save time when developing as you get an easy mapping between objects and the database.
  - However in practise ORM tends to give you quite horrible JOINs that quite frankly are hard to understand for humans.
  - Further more I think that **ORM can lead to a bad practice in the sense that you do not need to think about your data layout first**. 
  - But for database performance data layout is of utter most importance. One need to have data in lay out in a form that makes the application run fast. ORMs does not necessarily provide that. One need to normalize the database.

- This topic pops up frequently here on HN and every time I’m shocked at how many people have issues with ORMs! I’ve been using Hibernate/Spring Data for several years now and never ran into any issues. If I need to write a complex query, I can easily write a @Query annotation in HQL and it neatly fits right in to the repository class.

- 
- 
- 
- 
- 
