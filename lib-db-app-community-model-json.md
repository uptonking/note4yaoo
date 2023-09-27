---
title: lib-db-app-community-model-json
tags: [community, database, json, jsonb]
created: 2023-09-26T17:18:52.637Z
modified: 2023-09-26T17:19:13.941Z
---

# lib-db-app-community-model-json

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [JSON and Virtual Columns in SQLite | Hacker News](https://news.ycombinator.com/item?id=31396578)
- 
- 
- 
- 
- 

- ## [JSON with Sqlite | Hacker News](https://news.ycombinator.com/item?id=19277809)
- At that point you can somehow normalize your schema, but only if you really have to! That is because you can get away with a NoSQL-like denormalized schema performance wise, by carefully defining index on expressions. You can somehow normalize it with views (SQLite doesn't support materialized views).

- 
- 
- 

- ## [There are over one trillion SQLite databases in active use | Hacker News](https://news.ycombinator.com/item?id=29461127)
- Disagree storing json in databases is often the best thing to do. Clickhouse for example allows you to quickly pull out relevant data and feed materialized views.
- I never said storing json in databases was wrong. I said storing json in *SQL* databases was an anti-pattern.
- It's perfectly fine. one column for a timestamp and one column to store the json. You then build materialized views pulling out whatever json fields you need.
- Just because its easier doesn't mean its better - json is just one possible materialization for your set.

- 
- 

- ## [Jsonb: Stories about performance | Hacker News_201712](https://news.ycombinator.com/item?id=15993768)
- 
- 
- 

- ## 💡 [Using PostgreSQL’s JSONB for NoSQL (2019) [video] | Hacker News_202109](https://news.ycombinator.com/item?id=28406334)
- I find this approach incredibly useful if any parts of your data don't have a uniform schema.
  - The one thing you need to look out for is developers putting stuff into JSON that belongs into proper columns. The Postgres JSON support is very powerful, but plain old relational queries are faster and often much easier to write.
  - Also for leftovers when scraping website data. Trendy SPAs usually have JSON endpoints, so I usually use some ID column, maybe timestamp column (to ease incremental syncing later on), some primary content columns, and the whole scraped JSON object is put into a data JSONB column in case some of it is needed in the future. :) Works amazingly.

- I have created an app with such a hybrid approach as the part if the model was very dynamic. The idea was that I would slowly migrate the stable bits to proper columns, but in practice that never happened. Partly also because it is not really broken, and the performance is actually quite good. You can add partial indexes etc to improve where needed.
  - But writing analytycal queries is definitely more complicated so the cost of not having a "normal" data model adds up over time. To allow business analysts to work with the data I endend up creating a a bunch of views om the data without JSONB fields as a quick fix. So though the approach worked, I am not sure I would do it again.

- I'm using the JSON mostly for parts that really have no fixed schema, e.g. fields that vary by customer. The alternative would be something like EAV, and JSON columns are far superior here.
  - Performance is perfectly reasonable with JSON, but there are many more ways to make it slow if you're not careful. Postgres has to read the entire JSON content even if you only access a small part of it, that alone can kill performance if your JSON blobs are large. The lack of true statistics can also be an issue with JSON columns. They're still easily fast enough for many purposes, they just have a few more caveats than plain columns you should be aware of.
- There's some other aspects that are not that intuitive, but also not a big deal once you know them. For example you can use a jsonb_path_ops GIN index to speed up queries for arbitrary keys and values inside your JSONB column
- What you did, in fact, was creating read models specific to use case. This is completely normal and allows one to optimize for different users: app's schema can be different than the one for analytics.

- I noticed a lot of people noting that they enjoy use some hybrid of JSON w/ their SQL. I do the same thing and I think this is an incredibly productive way to manage fast-changing things.
  - One trick I learned along the way is to **apply gzip to your JSON columns**. For us, we got over 70% reduction in column size and query performance actually increased. I presume because it is faster to read fewer IO blocks than more, esp when doing table scans (which you shouldnt but they happen).
  - The only caveat with this is if you want to query against something in the JSON, but I think this is where the balancing act comes into play regarding what is in (compressed) JSON and what is in a column.
- In Postgres you would generally use JSONB columns, those are stored as TOASTs and are automatically compressed. That compression isn't very good, but there is some work on adding other compression algorithms there.
  - PostgreSQL 14 will add lz4 compression for toast data. But if i remember correctly the first ~700 bytes are always stored inline and only the rest is compressed. But i could be wrong on this.

- The performance of JSONB is also surprisingly great. I played around with around 1M rows of data for a project using JSONB, and compared to traditional SQL, the complex queries were 500-800ms slower, which was totally reasonable for the use case.

- Been doing this for years now and it has proven itself to he a great solution. We use a hybrid approach: traditional columns in addition plus an entity/content type JSONB column.
- JSON blob + columns is the recommended approach for handling semi-structured data in ClickHouse. It's easy to add columns on the fly, since you just give the expression to haul out the data using a DEFAULT clause. ClickHouse applies it automatically on older blocks without rewriting them. For new blocks it materializes the data as rows are inserted.

- Had a great win this last week with JSONB. Basically I needed an aggregated materialized view for performance but still have access to the non-aggregated row data. Think aggregate by account ID but the query may access any given month of data for that account. It’s cheating a bit to use a non-relational structure, but the correlated subqueries I had to use before were 20x slower.

- PostgreSQL 14 is currently in beta and adds JSON subscripting
