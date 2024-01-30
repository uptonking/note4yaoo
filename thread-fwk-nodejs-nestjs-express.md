---
title: thread-fwk-nodejs-nestjs-express
tags: [express, framework, nestjs, thread]
created: 2021-04-23T18:10:04.807Z
modified: 2022-12-19T01:51:23.851Z
---

# thread-fwk-nodejs-nestjs-express

# guide

# discuss-stars
- ## 

- ## Is there a way to bridge the gap between fetch-like server APIs of `Request => Promise<Response>` with Node.js APIs of `(IncomingMessage, ServerResponse) => void` .
- https://twitter.com/tomus_sherman/status/1752268167777243209
  - have a look at how hono does it
- After a brief glance it looks like this is bridging `Node -> fetch`

# discuss
- ## 

- ## 

- ## this was a question about implementing multi-tenancy in a single database
- https://twitter.com/thdxr/status/1689028039684857856
  - basically even though you have many customers, you want to pretend like each customer has their own database
- one way to implement this is to specify a column in every single table - in this case `workspace_id` .
  - every single query you do on behalf of a customer will be filtered `where workspace_id = xxx` .
  - from their point of view it's like only their own data exists in the db

- Any thoughts on the following when using 1 db for all your customers?
  - "data privacy": customer is concerned data could leak bc it's in the same db instance as other customers
  - queries get slow for everyone bc one large customer is hogging all the resources of that db

- Another useful tip, user input should rarely, if ever contain a workspace_id, it should be inferred from the session/ token

- Worked in many large B2B SaaS platforms, most use DB/Customer for several reasons: 
  1. Cost/Risk in compliance industries of a developer missing the "where clause" and leaking sensitive data
  2. Getting "all" a customer's data is much, much easier (think 'subpeona')
  3. Scaling/Grouping customers for performance is super easy
  4. Don't need 'extra' columns in all your main tables
  5. The "management" of multiple DBs vs. Compound key is non-existant. You're just switching at a different point in the code (cxn vs. query).
  6. Giving customers their own copy is far easier (particularly if you're in the cloud)
  - But, it is more slightly more challenging to aggregate data unless you're using multi-server results

- I would recommend uuid as primary key for these tables, a simple thing early on that helps a lot later when these multi Tennant databases grow.

- For multi-tenancy in a single database, you should consider using RLS (row level security)

- ## Looking forward to run @nestframework in @stackblitz‘s microOS directly in @googlechrome !!! And it boots up lightning fast
- https://twitter.com/Mike_BeastCode/status/1385350399377379328
  - 在云端编辑器中直接运行后端服务代码，注意需要消耗云服务商的资源
  - npm包可以被缓存，所以对于云服务商的成本没有预期的高
