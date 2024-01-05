---
title: lib-db-app-community-model-json-document
tags: [community, database, json, jsonb]
created: 2023-09-26T17:18:52.637Z
modified: 2023-10-26T15:01:36.462Z
---

# lib-db-app-community-model-json-document

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Show HN: CursusDB – A new scalable distributed document oriented database in go | Hacker News_202401](https://news.ycombinator.com/item?id=38869393)
- For new products I always recommend the same thing: name your competitors and use cases. Compare them in a table; don't make the user think. Who should and should not use your product? Being in-memory and distributed, I imagine your competitors include Ignite and Hazelcast?
- Also write a blog post titled "YourProduct vs alt1 vs alt2 vs alt3 etc" 'cause "alt1 vs alt2 vs alt3" is what I'm searching
- You have competitors whether you like it or not -- unless you don't care for users, either. A sibling commenter asked "Why not just use Couchbase?" If your answer is "figure it out yourself; I already wrote documentation" you are shooting yourself in the foot. Documentation is not marketing. Marketing means helping potential users understand why they should use your product rather than something similar.
- Hazelcast seems like Redis. CursusDB is more like MongoDB I'd say in comparison.

- Interesting product. I'm reading through the source and... Woah... it is all in one single file with zero unit tests.
  - this seems like a very odd choice for organizing a database codebase. Some of the methods like cluster. HandleClientConnection() are crazy long for loop + if/else + switch + goto
  - I know that you've said this is just kind of in your best interests codebase, but if I was planning on making any sort of dependencies on this project, I'd probably shy away from it because it seems like unmanageable spaghetti.
- It's not even 3, 000 lines. That's not a lot of spaghetti.
  - The lack of tests though...

- Just want to add this bit so I've recently finished node's transaction persistence. Mind you I've actually tested power outages at my own house. Don't wanna get into too much details about that lol!!

- CouchDB is distributed by nature as well. So why use this over CouchDB.
  - CouchDB's design to me personally is not that great. 
    - I don't like the replicated design or the query language. 
    - To boot(再者, 此外) I don't like complexities. I try to avoid them when designing something complex. CursusDB core code is under 6k lines because of that reason. 
    - I also wanted to create something I want to use. Simple. Setting up a secure, reliable and powerful database shouldn't be complex and I made certain of that when designing CursusDB. 
    - CursusDB's query language as well is very simplified yet powerful because of my complexities ideology.

- why wouldn't I just use Couchbase? It is proven and has a community around it.
  - I don't like MongoDB or Couchbase. I dislike their query languages and designs in general. I built the DB for my own liking and use cases. 
  - If others like it that's great, if not it doesn't hurt me. 
  - I made it open source to follow the process and I'm not looking for any profit or gain for doing any of it. I'd like honest opinions obviously but that's all. Eventually if people really like the DB and it requires ALL my time then I'll try to expand on the cloud offering because I am mighty passionate about the project and want to see it being used as much as possible and easily as possible!

- Seems like you could do the same with rqlite, since SQLite supports JSON.
  - I just didn't want to go the route of SQLite + a layer. SQLite as well is not encrypted by default. 
- rqlite: Their github mentions encryption but it's only node to node using TLS not much else. https://rqlite.io/docs/guides/security/
  - With rqlite all traffic between the nodes can be encrypted, as can be the HTTP API. Yes, the data at rest is not, but there are many ways to protect that. One way would be to use an encrypted file system, perhaps.
  - Encrypted data-at-rest is a valid request, but what use cases would it address?
- I never liked the idea of having any database storing my data in a way which can be seen in plain sight regardless of permissions and so forth. Servers get broken into very often and protecting the data within the files is important to me.

- ## 🔥 [Writing a document database from scratch in Go: Lucene-like filters and indexes | Hacker News_202203](https://news.ycombinator.com/item?id=30835444)
- 
- 
- 

- ## [JSON and Virtual Columns in SQLite | Hacker News](https://news.ycombinator.com/item?id=31396578)
- 
- 

- ## [JSON with Sqlite | Hacker News](https://news.ycombinator.com/item?id=19277809)
- At that point you can somehow normalize your schema, but only if you really have to! That is because you can get away with a NoSQL-like denormalized schema performance wise, by carefully defining index on expressions. You can somehow normalize it with views (SQLite doesn't support materialized views).

- 
- 

- ## [There are over one trillion SQLite databases in active use | Hacker News](https://news.ycombinator.com/item?id=29461127)
- Disagree storing json in databases is often the best thing to do. Clickhouse for example allows you to quickly pull out relevant data and feed materialized views.
- I never said storing json in databases was wrong. I said storing json in *SQL* databases was an anti-pattern.
- It's perfectly fine. one column for a timestamp and one column to store the json. You then build materialized views pulling out whatever json fields you need.
- Just because its easier doesn't mean its better - json is just one possible materialization for your set.

- ## 🔥 [Cloud Firestore: A New Document Database for Apps | Hacker News_201710](https://news.ycombinator.com/item?id=15393396)
- 
- 
- 
