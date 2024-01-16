---
title: thread-domain-multi-tenant
tags: [database-design, forum, tenant]
created: 2024-01-16T06:14:02.085Z
modified: 2024-01-16T06:14:59.465Z
---

# thread-domain-multi-tenant

# guide

# blogs
- [Meta/Facebook - How a graph model can scale your relational DBs - Tantamanlands_202210](https://tantaman.com/2022-10-19-meta-scales-mysql.html)

- [How Slack Built Shared Channels - Slack Engineering_2020](https://slack.engineering/how-slack-built-shared-channels/)
# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## @turbopuffer is built with multi-tenancy in mind from day 1. 
- https://twitter.com/Sirupsen/status/1746971216995373301
  - every namespace is just a prefix on object storage. 
  - some customers have 100, 000s, some have 1.
- More than storage, multitenancy on compute and network is much harder. Avoiding noisy neighbor is much harder.

- ## 译评了一下DHH的新篇，这个想法挺有意思：不搞多租户卖服务，从而规避大量无谓的开发/运维复杂度
- https://twitter.com/GobeUncleWang/status/1747123437703954616
  - [多租户是Web服务的复杂之源](https://mp.weixin.qq.com/s/jKv9l_ro6rWei4QnXck-zw)
  - 我们正试图通过 ONCE 项目来探索这个问题 —— 这是我们即将推出的一系列基于Web网页的系统 —— 你可以将其作为产品购买，而非作为服务租用。我们的想法是，您将自己部署并运行这个产品，无论是在云上的虚拟机还是你自己的硬件上 —— 而且只为您自己服务：没有多租户机制，数据不会相互混杂，扩容伸缩起来也简单得多。

- ## I have heard that Slack started out single-tenant, and it was a massive pain that took years to rearchitect to multitenancy as soon as they needed features that spanned tenants.
- https://twitter.com/tantaman/status/1747118687641817115
- IIRC Facebook started single-tenant which meant scaling a new college just meant adding a new server. But eventually they managed to glue together the entire world into a single graph. 
- Turning that multi tenant just meant presenting all those dbs as one at the api level but sharded by school (much later by social hash) internally.
  - Is there much of a distinction between single and multi tenant when organized this way?
  - migrating object ids so they would encode the db they lived on and creating a solid abstraction to allow querying over those shards transparently.

- I don't think Slack started as single-tenant. Here's some background:
  - [How Slack Built Shared Channels - Slack Engineering_2020](https://slack.engineering/how-slack-built-shared-channels/)
