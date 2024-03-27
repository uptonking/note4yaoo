---
title: lib-db-app-community-query-join
tags: [community, db, query]
created: 2023-10-31T11:17:38.308Z
modified: 2023-10-31T11:17:48.697Z
---

# lib-db-app-community-query-join

# guide

# blogs-join
- [Using Functional Dependency Analysis to improve Join performance | DoltHub Blog_202312](https://www.dolthub.com/blog/2023-12-13-functional-dependency-analysis/)
# discuss-stars
- ## 

- ## If you find yourself writing a lot of JOINs and dealing with query speed, it is time to redesign your database.
- https://twitter.com/RaulJuncoV/status/1765008031509631014
- 3 ways you can solve these problems:
  - 1. If two tables are often joined, you can combine them into a single table. But make sure the merged table maintains all necessary information.
  - 2. If the data doesn't change often. You can duplicate the information in many tables to avoid joins.
  - 3. Store the result of a complex query in materialized views (or indexed views). This form of logical Denormalization doesn't need to change the underlying table structures.
  - We call this Denormalization.
  - Denormalization is a strategic decision that should balance performance improvements and data integrity.

- ## 👨🏻‍🏫 How do SQL Joins Work? The diagram below shows how 4 types of SQL joins work
- https://twitter.com/alexxubyte/status/1734245951009910881
  - INNER JOIN
  - LEFT JOIN
  - RIGHT JOIN
  - FULL OUTER JOIN

- https://twitter.com/alexxubyte/status/1734410242774167619
  - I make stupid errors, many people notice them and point them out, enabling me to fix them quickly
  - This is the updated version.

- https://twitter.com/milan_milanovic/status/1736371310614270131
  - What is the difference between inner, left, right, and full join?
# discuss
- ## 

- ## 

- ## 

- ## Lots of queries that remove duplicates using DISTINCT or GROUP BY after an INNER JOIN (or LEFT JOIN) could perform significantly better if using a SEMI JOIN
- https://twitter.com/lukaseder/status/1772971845785927825
  - [If you remove duplicates after INNER JOIN, consider using SEMI JOIN](https://blog.jooq.org/sql-join-or-exists-chances-are-youre-doing-it-wrong/)
- An JOIN is nothing but a filtered cartesian product
  - In SQL, a cartesian product can be written as either a CROSS JOIN, or a table list in the FROM clause.
- By using a SEMI-JOIN. It is called semi join (i.e. “half” join) in relational algebra, because we only care about one side of the JOIN operation in the results, not the other side.
  - Unfortunately, SQL doesn’t have SEMI JOIN keywords
  - The SQL way to express a SEMI JOIN is by using EXISTS () or IN (). 

- ## 7 SQL Joins You Must Know
- https://twitter.com/AmigosCode/status/1766073736640303292
➡️ Inner Join: Retrieves records with matching values in both tables.
➡️ Left Join: Retrieves all records from the left table and matching records from the right table.
➡️ Left Join with Null Check: Filters only the records where there is no match in the right table (NULL values).
➡️ Right Join: Retrieves all records from the right table and matching records from the left table.
➡️ Right Join with Null Check: Filters only the records where there is no match in the left table (NULL values).
➡️ Full Join: Retrieves all records when there is a match in either the left or right table.
➡️ Full Join with Null Check: Filters only the records where there is no match in either the left or right table (NULL values).

- ## Colocated and interleaved tables are one of the performance optimization techniques available in some distributed SQL databases.
- https://twitter.com/denismagda/status/1733187029997932891
  - The tables can improve performance for JOINs by storing child and parent table records together on the same database node.
  - [Colocated and Interleaved Tables in Distributed SQL Databases: Tradeoffs_202312](https://medium.com/@magda7817/colocated-and-interleaved-tables-in-distributed-sql-databases-tradeoffs-f2e7b1b9d68e)
  - But as with any optimization technique, there are some tradeoffs:
  1. Data and Load Skew - some nodes may start storing and processing more data than others.
  2. The Best Parent Tradeoff - some tables are in many-to-many relationships with others, making it challenging to choose the best colocation strategy for them.

- ## Prisma doesn’t JOIN (related records are fetched as separate requests from the DB) so I think it’d be slow at the edge anyways_202310
- https://twitter.com/jitl/status/1719347464359026862
- Hey Jake! While you are correct, we don't use Joins in every instance. We are currently doing a lot of work to fix this. We pushed out the initial change in 5.4. More to come! Thanks for using Prisma!

- ## [For Want of a JOIN | Hacker News_202212](https://news.ycombinator.com/item?id=34092645)

- With that said, the JOIN is a very powerful concept which, unfortunately, has been given a terrible reputation by the NoSQL community. Moving such logic out of the database and into to DB's client is just a waste of IO and computing bandwidth.
  - SQL has been the ONLY technology/language that has stuck with me for > 25 years. The fact that it is (apparently) not being taught by institutions of higher learning is just a shame.
- I agree. It took me 3 years or so to actually land in a project and learn SQL for the first time. Before it was all with ORMs. I didn't know what a join was for the first couple of years of my career. Understanding SQL and being able to work with data interactively has made me a better software engineer. This tech is important enough that it should be taught in university/coding camps.

- I often wonder how often this exact problem happens, but where A and B are [micro]services owned by two different teams, one is required by company policy to use their APIs not their raw databases, and escalation of each of these issues e.g. query size/rate limiting runs the risk of burning political capital on top of everything else.

- ## 🆚️🍃🐘 [Comparison of Joins: MongoDB vs. PostgreSQL | Hacker News_202004](https://news.ycombinator.com/item?id=22834036)
- why one would choose mongo over postgres?
- There's really only one reason to choose mongo over a competent RDBMS, and that's schemalessness at the database level--which most users of mongo then toss away by adding a schema package at the code layer.
  - If your data is relatively freeform with good indices on stable fields, mongo is hugely convenient, and can be easily structured to scale horizontally. For non-join based aggregation (i.e, aggregation within a collection), mongo is very performant, and works fine for a lot of use cases. I'm using it storing large amounts of simple timeseries data and it's great, largely because my use case doesn't require more complex data structures.
  - As soon as you want to deal with more complex structured data, mongo is worse than any RDBMS. The only viable noSQL solution to complex structures is denormalization, which is sometimes a legit choice. But unless you know your primary use is just retrieving a set of documents based on indexed fields (and many are), get an RDBMS.

- MongoDB has built-in auto-failover with replica sets. It is possible to set this up for PGSQL with third-party tools but it's hard to get right.
  - MongoDB has built-in multi-instance sharding support. Again this is possible for PostgreSQL with table partitioning and FDW but it is hard to maintain.

- I can’t address MongoDB, but nosql vs relational generally, there are two reasons:
  - (1) what’s faster than a fast join? No join. With nosql you have more flexibility to store the data organized in the same way it is accessed. You don’t need to join to another table if the data your app needs is already directly part of the main data the app requests. You do need to understand your access patterns well, and develop migration plans when they change.
  - (2) scalability. nosql databases generally let you scale horizontally more easily/gracefully than relational databases, though there are trade offs.
  - Put it together and you get performance at scale, though you generally need to understand your data access patterns and usually need to be more resilient to inconsistencies.
- I've found that being able to change quickly is more valuable that the marginal performance boost that mongo would give. Denormalization is possible in postgres.
- > what’s faster than a fast join? No join. With nosql you have more flexibility to store the data organized in the same way it is accessed.
  - You can definitely do this in PostgreSQL via materialized views. They're directly supported in recent releases, and they don't require you to denormalize the underlying datamodel unlike NoSQL.
- Well, a materialized view is denormalized data. You distinguish it from the “underlying data model”, but you can do that in nosql as well. Also, materialized views still tend to be oriented to rectangular data, which isn’t always how you want to access data.
  - I agree with the general point that Postgres and other relational databases can do nosql things (and nosql databases can do relational things).

- You can do that by using a JSONB column in postgres (including indexes), and that way you can upgrade to typed columns at yout leisure (and on a per-column basis).
- PostgreSQL has the JSONB data type which is essentially the same as the BSON type except slightly better optimized for reading partial documents. And PostgreSQL also provides good indexing support for them, and did so before MongoDB.

- Can someone who is using MongoDB and a RDBMS at the same time tell me the exact use cases where MongoDB is fitter? Structured logs? Caching? Sessions? And why MongoDB does it better?
- Cluster is very easy in MongoDB and for unstructured data. I've looked into clustering postgresql a few time and it seems like a pain in the butt. TBH, storing data without thinking about relation is just kicking the can down the road.
- Relational DBs for everything that needs joins. MongoDB is horrible with that and should not be used. One would not put an off-road vehicle on a race track and expect it to win.
- The biggest one is searching jsons. You essentially have a database that stores jsons and you can search it. Just dump a json and search it goes a long way. My problems are more the atomicity guarantees which are not very consistent.

- A basis for the apples to oranges argument is that you don't use MongoDB when you need JOINs.
  - You almost always need JOINs
  - The only way I see it being useful is for scaling purposes. But there are way better, more stable, more resistant to failure kv stores out there.

- If you picked mongodb and you are using joins, you've picked a wrong tool for a job.

- 🤔 Is there any real reason why a document store can't have good joins between collections?
  - I don't think most document stores enforce foreign key relationships (and hence consistency) like RDBMS do, so in practice that would make joins difficult.

- ## 🔥 [Joining CSV and JSON data with an in-memory SQLite database | Hacker News_202106](https://news.ycombinator.com/item?id=27565482)
- 
- 
- 

- ## 🔥 [Doing a database join with CSV files | Hacker News_201912](https://news.ycombinator.com/item?id=21923911)
- 
- 
- 

- ## 🔥 [Show HN: OctoSQL – Query and join multiple databases and files, written in Go | Hacker News_201907](https://news.ycombinator.com/item?id=20449610)
- 
- 
- 
