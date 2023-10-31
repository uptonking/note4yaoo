---
title: lib-db-app-community-comparison
tags: [community, comparison, database]
created: 2023-09-17T17:45:34.428Z
modified: 2023-09-17T17:46:07.620Z
---

# lib-db-app-community-comparison

# guide

# discuss-stars
- ## 

- ## 

- ## do you use Postgres or MySQL at work?
- https://twitter.com/jarredsumner/status/1710737550292423152
  - pg vs mysql = 0.56: 0.21
  - mongodb

- ## A cheat sheet of various databases in cloud services, along with their corresponding open-source/3rd-party options.
- https://twitter.com/alexxubyte/status/1710680670568394996
  - Note: Google has limited documentation for their database use cases. Even though we did our best to look at what was available and arrived at the best option, some of the entries may be not accurate.

- ## 🛢️🔥 [Never Write Your Own Database (2017) | Hacker News_201805](https://news.ycombinator.com/item?id=16995612)
- As soon as you allow some kind of user-defined meta data, you basically end up with the entity-attribute-value pattern.
  - Every sufficiently advanced system does that, be it a CRM that allows custom fields, or a project management or ticket system, a workflow system etc. And basically all enterprise software contains elements of these systems.

- A good alternative would be to use JSON types in RDBMS in combination with classic field types. EAV is really just free form data and JSON is easier to query in MySQL or Postgres.

- ## 🔥 [Comparing Database Types | Hacker News](https://news.ycombinator.com/item?id=21060866)
- Deductive databases derive logical consequences based on facts and rules.
  - Datalog and its superset Prolog are notable instances of this idea, and they make the connection between the relational model and predicate logic particularly evident.

- The column-family databases mentioned (Cassandra, HBase) are both just fancy key-value stores that add semantics for separate tables and cell-level data so you're not rolling it yourself.
# discuss
- ## 

- ## 💡 [How to Efficiently Choose the Right Database for Your Applications | Hacker News_202102](https://news.ycombinator.com/item?id=26290252)
- I kinda disagree with separate branch for "document database" for Mongo. Mongo is a key-value storage, with a thin wrapper that converts BSON<->JSON, and indices on subfields.
  - You can achieve exactly the same thing with PostgreSQL tables with two columns (key JSONB PRIMARY KEY, value JSONB), including indices on subfields. With way more other functionality and support options.
- Not really true. MongoDB natively supports sharding, multiple indexes, high availability, arrays, sub documents, array traversal, etc - all able to be accessed in your native language with get/set functionality (or via MQL if you want). While PostgreSQL is a really powerful database, the JSON support is really painful to program against.

- 

# discuss-mongo
- ## 

- ## 🆚️ [Mongo (Atlas) vs. Planetscale for my simple SaaS?](https://www.reddit.com/r/Database/comments/wh9rd1/mongo_atlas_vs_planetscale_for_my_simple_saas/)
- Mongo:
- Pros: I have the most experience with it, super easy to get up and running, built for simple document structure like my use case, very cheap pay-as-you-go pricing on Atlas.
- Cons: Database doesn't enforce schema (ofc) so while as a dev I love it, as a business owner it feels maybe too risky. Has low connection limit (500) which could possibly bottleneck with serverless connections.

- Planetscale:
- Pros: Enforces schema and even has cool branching/merging of schema changes so feels much "safer" than Mongo to protect it from me doing something dumb. Unlimited connections so no bottleneck there.
- Cons: Free tier is probably good for a while but then immediately jumps to $29 unlike mongo where prices scales with me (though obviously thats not too bad, just more). Don't necessarily need a relational DB, but doesn't hurt I guess. A little bit more setup/work than Mongo because I have to build/migrate/merge the DB branches/schemas.

- I second the suggestion of trying CockroachDB serverless.
  - What about CockroachDB free tier serverless? You would go a very long time before paying a bill.

- Actually you can create a schema validation in Mongo. Check it out
  - [Schema Validation — MongoDB Manual](https://www.mongodb.com/docs/manual/core/schema-validation/)

- my advice would be to stick to what you know. If you know Mongo well go for it. 
  - If you're starting a business, proving the idea and marketing it is going to be a lot more important than the tech unless you're doing something bleeding-edge. 
  - Try to not overfocus on the tech. NextJS + your preferred DB seems like a good place to start.

- ## [Why You Should Never Use MongoDB | Hacker News_201311](https://news.ycombinator.com/item?id=6712703)
- We have a CMS application that supports creating custom web forms, which each have a different set of fields which hold different types of data. Email addresses, multi-select radio buttons, text areas, etc. Some forms only gets submitted once or twice, others are submitted many thousands of times. To store this in a normal relational database you either need many tables, or you need to normalize your data (probably Entity-Attribute-Value (EAV) style). We didn't want hundreds of tables, and designing a good EAV system can be tough (Magento anyone?), so we looked at other options.
  - We've settled currently on using MongoDb, with one collection to hold the (versioned) definition of each form's fields (data type, order, validation rules, etc), and another collection to hold all of the submissions (this is a laaarge collection). There _is_ a "relation" between the form definition and the submissions, but because you always query for submissions based on the form (by form_id), you don't really need to do "JOINs" (you just query out the form definition once, before the submissions). Also, because the forms are versioned, and each submission is associated with a particular version of a form, there is no need to retroactively update the de-normalized schema of past submissions (although this does limit your ability to query the submissions if a form is updated frequently - or drastically). It's not perfect, but this use case for MongoDb has been working well for us so far.

- A good simple use-case for a document database (could be MongoDB, but not necessarily) is configuration and system "schema" type data. For example, storing all of a user's settings and preferences into a document keyed by the user's Id.
- We use it for event storage in the event sourced parts of our app. For the rest of our data, we're currently migrating off of Mongo to Postgres due to an experience similar to the OP's.
