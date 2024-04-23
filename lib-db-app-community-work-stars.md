---
title: lib-db-app-community-work-stars
tags: [community, database]
created: 2021-08-30T15:51:01.157Z
modified: 2023-10-27T06:54:20.487Z
---

# lib-db-app-community-work-stars

# guide

# discuss-stars
- ## 

- ## 💡👣 Most databases were built when data was static and queries were dynamic. 
- https://twitter.com/tantaman/status/1699826662408409383
  - For applications, most queries are static and the data is dynamic
- What you really want is a database where a query is the same things as an index, is the same thing as a subscription... These are all the same underlying mechanic.

- ## 🆔️ GUID做主键的弊病：
- https://twitter.com/geniusvczh/status/1772367461091795070
  - 1、guid生成是随机的离散的，主键通常会生成主键索引，为了优化搜索、插入、删除操作的效率，显然主键有序更好，这是其一；
  - 2、Oracle、SQL Server和MySQL的常规索引都是B树或B+树，是一种平衡树。在插入和删除的时候，因为guid的离散性，会导致平衡树失衡，导致数据重排
- btree在写入数据到叶子层的page的时候，需要不断排序。数值型的主键id直接排序即可，因为写入的id肯定比之前的大，而uuid需要根据一定规则进行排序，因为是不规则类型，因此对应的record需要不断的进行重排，这样当前page中在进行着不断的排序，不断的对象和地址的copy。

- 我原来也用自增数字，后来由于删除过数据，在库间copy表时，两个表的数字键会不一样，这给我带来很大的麻烦，而搜索性能方面的弊端在我这里并不突出或用别的方法解决，我就以后都用guid了。省心。
- 碰到数据拆分合并，guid还是最好的选择
- 我都10年没用过自增了，如果重逻辑重重构的话，GUID显然是无二选择

- 如果用UUIDv7有序的呢
  - Sequential GUID吗？那和snowflake id没啥区别了吧。我觉得Sequential GUID不能叫"GUID"了
  - 微软特例叫guid，我们java boy都是叫uuid，用ulid和雪花的估计也少了

- 取决于 传统的db还是 distributed kv 比如dynamo。对于k, v来说，uuid反而是受到鼓励的, 因为会均匀的分布在不同的node上
  - 但dynamo不是有自己的hash func么？可以让数据分散在不同的node上。这样一来，感觉guid都有些redundant了。
- 你说的是对的。 例外在于，dynamo可以用partition key + sort key 作为pk 如果不必要的使用了两个field作为pk, 而第一个field有重复的值，就会出现data skew的问题，可能影响性能。 再者，如果同时动态创建多个新的数据，用uuid是最简单的方法。（分布式保持一个一直递增的id不简单）

- 🐛 使用自增主键，有删除数据的话，oracle没有问题因为它使用的是自增sequence 。但mysql 会重复使用被删除的主键，有时候会带来业务查询上的问题。

- 果然是mysql受害者。别人的数据库用不用guid总的来说差别不是很大，就是mysql的效果特别明显

- 
- 
- 

- ## 🆔️🐬 The problem with using a UUID primary key in MySQL
- https://twitter.com/PlanetScale/status/1770120605905612861
- I'm pretty certain the same issues exist for UUIDs regardless of the DB.
  - I use a CUID which may suffer from some issues itself, but in practice I've not had problems.
- Most DB engines including SQLite use b-trees. As the database grows, you might notice inserts get slower. It's often overlooked as users are forgiving of slow writes and even more so of bulk writes. 
  - CUID (not CUID2) is good as it is increasing over time
- CUID is deprecated due to security issues though: https://github.com/paralleldrive/cuid. You can change the size of your ID with CUID2. Does this change anything for you, or would you still go with CUID?

- Bad for performance, but very good for minimizing bugs. By using IDs that are globally unique like UUIDs, you'll never mistakenly mix up a reference.

- not mentioning k-sorted uuid like ksuid that specifically fixes the sort issue for b-tree indexes

- ### 📝 [The problem with using a UUID primary key in MySQL _202403](https://planetscale.com/blog/the-problem-with-using-a-uuid-primary-key-in-mysql)

- The many versions of UUIDs

- Be aware that there are several tradeoffs to doing so when compared to an auto-incrementing integer.
- Insert performance
  - Whenever a new record is inserted into a table in MySQL, the index associated with the primary key needs to be updated so querying the table is performant. 
  - Indexes in MySQL take the form of a B+ Tree, which is a multi-layered data structure that allows queries to quickly find the data they need.
  - the goal of page splitting is to keep the B+ Tree structure balanced so that MySQL can quickly find the data it's looking for. 
  - With sequential values, this process is relatively straightforward; however, when randomness is introduced into the algorithm, it can take significantly longer for MySQL to rebalance the tree. 
- Higher storage utilization
  - All primary keys in MySQL are indexed. By default, an auto-incrementing integer will consume 32 bits of storage per value. Compare this with UUIDs. If stored in a compact binary form, a single UUID would consume 128bits on disk. 
  - secondary indexes will also consume more space. This is because secondary indexes use the primary key as a pointer to the actual row, meaning they need to be stored with the index.
  - This can lead to a significant increase in storage requirements for your database depending on how many indexes are created on tables using UUIDs as the primary key.

- Best ways to use a UUID primary key with MySQL
- Use the binary data type
  - While UUIDs are often sometimes as 36-character strings, they can also be represented in their native binary format as well.
- Use an ordered UUID variant
  - Using a UUID version that supports ordering can mitigate some of the performance
- Use the built-in MySQL UUID functions
  - MySQL supports generating UUIDs directly within SQL; however, it only supports UUIDv1 values. 
  - there is a helper function in MySQL called `uuid_to_bin`. Not only does this function convert the string value to binary, but you can use the option 'swap flag', which will reorder the timestamp portion to make the resulting binary more sequential.
- Use an alternate ID type
  - different formats such as Snowflake IDs, ULIDs, or even NanoIDs

- ## 🆔️ Myth(神话，想像或虚构的人物): Using UUID as the primary key will slow down inserts. 
- https://twitter.com/gwenshap/status/1686148804821811200
  - Fact: Not in Postgres.
  - I often recommend using UUIDs instead of integer sequences as primary keys. I was surprised to discover that many developers are uncomfortable with them and believe they will slow down inserts. 
  - [UUIDs are Bad for Performance in MySQL - Is Postgres better? Let us Discuss - YouTube](https://www.youtube.com/watch?v=Y5mWz4vK10A)
- It makes the code easier as well because you can generate IDs on the client.
  - Exactly! this also makes the system as a whole more scalable. This is not something you need early on, but changing PKs later is super hard and starting with UUIDs is not.

- 🆔️ [GUIDS case sensitive? - C# / C Sharp](https://bytes.com/topic/c-sharp/answers/233494-guids-case-sensitive)
  - Is the uniqueness of a guid case-sensitive?
  - No. A guid is really just 128 bits of data. The string representation is just one way of making it a little easier to read and work with
  - The "letters" you refer to are actually hex digits A-F, so no, case doesn't matter.
  - A GUID is a 128 bit structure. The normal string representation uses 32 hex digits to represent the 32 nibbles in the structure, and is not case-sensative.

- ## 🆔️ [Universally Unique Lexicographically Sortable Identifier in Go | Hacker News _201612](https://news.ycombinator.com/item?id=13116308)
  - [Understanding How UUIDs Are Generated | Hacker News _202009](https://news.ycombinator.com/item?id=24636204)

- I wonder why you would ever want it to be case-insensitive? Surely that increases the possibility of clashes, and violates the very good principle of least surprise (pretty much every other ID in the world is case-sensitive).
  - The hex representation of GUIDs/UUIDs is case insensitive in most interpretations, I'd say that counts enough.
- I'd be surprised if many developers these days actually compared UUIDs case-insensitively, though, even if they're intended to be. Microsoft, which have relied on GUIDs for years going back to their version of DCE/RPC, probably does it right.

- 🆚️ compare ULID with UUID
  - An ulid is "sortable". 
    - But the whole point of an UUID is a random unique ID. Non guessable. Sortable is not a feature you normally want from an uuid. And still UUIDs are still sortable. But it doesnt have any meaning. 
  - An ulid also encodes Time, an uuid doesn't. 
  - An uuid has less change of clashing: Its 128 bit vs 80 bit for ulid.
  - An uuid is also url safe.
  - An ulid is case insensitive. I don't see how this is an advantage.

- ULIDs are meant to be compared with Time UUIDs in particular

- ## 🆚️🆔️ [Question: how this compares with ulid ? · paralleldrive/cuid _201804](https://github.com/paralleldrive/cuid/issues/103)
- ulid lacks the client fingerprint. It may get away with that because by default, it will only use a CSRNG rather than pseudo-random source.
- cuid has been battle tested in production in apps with hundreds of millions of users since 2012. We have never had a verified report of collision issues. We continuously run collision tests across multiple generating hosts. I have never seen them fail in a production release of cuid (Beware: I have seen slug collisions).
  - As of this writing, cuid is used in 488 packages and over 21, 000 repos, including the native id generator for some dbms systems. ulid is used in 34 packages and 153 repos. This doesn't mean it's better, but it does provide evidence that it's a lot more battle tested.
- Because cuid doesn't rely on CSRNG, it is likely to be faster, and synchronous.
- ulid is more configurable -- it allows you to supply your own time and random number generators via the factory -- this could also be considered a downside, because you trade off consistency and the assurance that your id generating methods are battle-tested and collision resistant.

- ### [feat: add support to cuid · cockroachdb/cockroach _202211](https://github.com/cockroachdb/cockroach/issues/91006)
- Thanks for the feature request! Until we add this support, you might be able to get what you want by using a `bytes` column, and in 22.2, you can add a user-defined function that converts it to CUID format.
# discuss
- ## 

- ## 

- ## 🤔 客户端直连数据库的做法，是二十年前 MIS 系统的落后做法了，首先负载上不去，只适合小单位内部用用；
- https://twitter.com/skywind3000/status/1782191554750468555
  - 其次靠数据库本身的权限控制会导致客户端权限过大，客户端是在别人手里的，被破解或者出问题容易乱搞；
  - 再，存储过程的问题是同具体数据库绑定太死，切换麻烦，发布更新不方便；关于价1/N
- 虽然有ANSI SQL，但是各个数据库还是有自己独特的方言、函数。为了以后迁移数据库方便，不用存储过程，用SQL，后续工作量并没有少很多
- 人家做审计本来也没什么scale需求。每个用户对应sql server的一个user，省去了自己写登录系统，登录系统强度也有保障，还能整合Windows账号实现SSO，登录Windows就自动登陆了SQL Server。权限配好是没有漏洞的。不是所有人都是做Amazon Google这个规模的应用的，得根据实际需求来选择tech stack。
  - 权限管理的要点就在于隔离，你登陆操作系统等于登陆数据库这种事情，你敢做我还不敢用呢；什么叫数据库权限配置好就没漏洞？行级权限加列级权限你配置一下看看？不要说的好像到不了谷歌亚马逊的规模就该好好用sqlserver一样，事实上客户端直链数据库的做法，就是普通互联网创业公司的负载也支撑不到。

- ## 🆚️ How does ULID compare to UUIDv7?
- https://twitter.com/hnasr/status/1729062666621055366
  - They're both timestamp+random, but is there any functional difference?
- I don’t think there is much difference, both are time based (which is the key here). ULID came before UUID7 that is why Shopify went with it. 
  - there are more bits dedicated for time in UUID7 than ULID (60 vs 48) but honestly I can’t think of a use case needing more than 48 bits
- I thought UUIDv7 provides 48 bits for UNIX timestamp in milliseconds precision.
  - you are right, I confused it with UUIDv6 when I looked it up. 

- FWIW Shopify doesn't use ulid/uuid as primary keys, so @bdewater is likely referencing either (a) one index, (b) a specific table—not across the platform Far more about capacity planning, tenant isolation primitives, horizontal everything, and bottleneck whack-a-mole

- ## 🕛🔥 [Big problems at the timezone database | Hacker News_202109](https://news.ycombinator.com/item?id=28650019)
- 
- 
- 

- ## 🛢️🔥 [The Next 50 Years of Databases (2015) | Hacker News_201911](https://news.ycombinator.com/item?id=21508210)
- 
- 
- 

- ## this isn’t to say that every application should have its own totally bespoke(定制的) database. most of them probably shouldn’t. 
- https://twitter.com/aboodman/status/1708208649984950515
  - but these things are not magical and we should remember that they’re just code, too. code we can understand and debug and modify as needed.
- That’s not to say you shouldn’t write your own database, or web server, or compiler. Just don’t do it because your app is somehow magical and unique. Your app is variables and for loops inside, too
- There is no magic. It’s just variables, if statements, and loops, arranged cleverly. Every time - every single time - I’ve looked inside a web server, database, browser, or whatever my reaction has been the same.
- I remember very clearly the first time I got to look at gws -- google web server. Just given the name and aurora of the company, I was expecting something grand, inscrutable, insanely complex. Instead, I got an event loop and some very nicely structured event registration code.
  - Also usually a bunch of FIXME comments, comments explaining weird code choices, and sometimes even comments expressing frustration. I.e. just the same as in any codebase that you’d work on yourself.
- This is actually a nice corollary(必然结果): making things simple and easy to understand is the real art of software engineering.
- Also often the simplest code is the easiest for the computer to run. a compiler from the 2000s will happy unroll normal for loops. Code that stacks abstractions 10 layers deep - probably not
  - unfortunately I’m addicted to complicated abstractions like incremental programming
- 
- 
- 

- ## 🤔 [Skip the API, ship your database | Hacker News](https://news.ycombinator.com/item?id=37497345)
- If you give access to your DB directly, your API effectively becomes your API with all the contract obligations of the API. Suddenly you don't completely control your schema: you can't freely change it, you need to add things there for your clients only. 👉🏻 I've seen it done multiple times and it always end up poorly. You save some time now by removing the need to build API, but later you end up spending much more time trying to decouple your internal representation from schema you made public.
- The system that I'm currently responsible for made this exact decision. The database is the API, and all the consuming services dip(浸；泡) directly into each other's data. This is all within one system with one organisation in charge, and it's an unmanageable mess. The pattern suggested here is exactly the same, but with each of the consuming services owned by different organisations, so it will only be worse.
- Versioned views, materialized views or procedures are the solution to this. It is frequent that even internally, companies don't give access to their raw data but rather to a restricted schema containing a formated subset of it.
  - Views will severely restrict the kinds of changes you might want to do in the future.
  - Stored procedures technically can do anything, I guess, but at that point you would be better with traditional services which will give you more flexibility.
- Of course it’s possible, but now you need more people with DB and SQL knowledge. Also, using views and stored procedures with source control is a pain. Deploying these into prod is also much more cumbersome than just normal backend code. Accessing a view will also be slower than accessing an “original” table since the view needs to be aggregated.

- A downside I didn't see mentioned (it was gestured at with contracts and the mention of backwards compatible schema changes, but not addressed directly) was **tight coupling**. 
  - When you link services with APIs, the downstream changes of a schema migration end at the API boundary. 
  - If you are connecting services directly at the database level, the changes will propagate into different services.

- A very interesting idea to be sure, but IME the biggest downside (which tbf is mentioned in the article) is the contract. If you have clients with knowledge of and dependency on the schema, you can't change it in a breaking way unless you update all the client's code.
  - I've tried various patterns in the past like one that just exposes database columns as an API, and this pain point always comes calling and it hurts. 
- I've freelanced with several teams, primarily comprised of front-end devs, who decided to use Firebase for their product. When they first told me they query the database directly from both their website and their mobile app, I immediately was like "so...what happens if you need to change the structure of the database"?

- The solution to this is the same as with APIs: versioning. Instead of naming your table "my_foo", you name it "my_foo_v1". Then, when you want to make a breaking change to the schema, you: 
  1. Create a new table "my_foo_v2" with your desired schema
  2. Modify write queries for "my_foo_v1" so that they also write to "my_foo_v2"
  3. Copy over existing data in "my_foo_v1" to "my_foo_v2" with a migration script
  4. Modify read queries for "my_foo_v1" so that they read from "my_foo_v2" instead
  5. Remove all write queries to "my_foo_v1"
  6. Drop the "my_foo_v1" table

- 
- 

- ## [Best practices on primary key, auto-increment, and UUID in RDBMs and SQL databases](https://stackoverflow.com/questions/52414414)

- What I always do, even if it's redundant, is I create primary key on auto increment column (I call it `technical key`) to keep it consistent within the database, 
  - allow for "primary key" to change in case something went wrong at design phase 
  - and also allow for less space to be consumed in case that key is being pointed to by foreign key constraint in any other table 
  - and also I make the candidate key unique and not null.
- Technical key is something you don't normally show to end users, unless you decide to. 
  - This can be the same for other technical columns that you're keeping only at database level for any purpose you may need like modify date, create date, version, user who changed the record and more.

```SQL
CREATE TABLE users(
  pk INT NOT NULL AUTO_INCREMENT,
  id UUID NOT NULL,
  PRIMARY KEY(pk),
  UNIQUE(id)
);
```

- This question is quite opinion-based so here's mine.
- My take is use the second one, a separate UUID from the PK. The thing is:
  - The PK is unique and not exposed to the public.
  - The UUID is unique and may get exposed to the public.
- If, for any reason, the UUID gets compromised, you'll need to change it. Changing a PK may be expensive and has a lot of side effects. If the UUID is separate from the PK, then its change (though not trivial) has far less consequences.

- if you make it an increasing number, your competitors will know how many users you have and how fast you are adding new ones.

- I came across a nice article that explains both pros and cons of using UUID as a primary key. 
  - In the end, it suggests using both but **Incremental integer for PK and UUIDs for the outside world**. 
  - Never expose your PK to the outside.
