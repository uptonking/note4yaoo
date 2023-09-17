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

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Mongo (Atlas) vs. Planetscale for my simple SaaS?](https://www.reddit.com/r/Database/comments/wh9rd1/mongo_atlas_vs_planetscale_for_my_simple_saas/)
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
