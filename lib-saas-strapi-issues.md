---
title: lib-saas-strapi-issues
tags: [issues, strapi]
created: 2024-02-15T05:46:16.207Z
modified: 2024-02-15T05:46:32.456Z
---

# lib-saas-strapi-issues

# guide

# issues-done
- ## [Deleting/Updating content-type doesn't drop/migrate the database _201805](https://github.com/strapi/strapi/issues/1114)
- we don't delete your tables we just create new ones, therefore the behavior you described is the correct one.

- Fixed in v4, marking as closed
  - There is no configuration for this as we will just delete the column/table on reboot when it's deleted. We did discuss a warning or a safer method but opted not to do it in v4. 
  - When you use v4 we will simply clean up the database for you.

- Yes this is currently intended (as you deleted the schema effectively), the best method to hold onto the data is take a database backup.
  - If you are simply renaming a content-type or field then you will have to (for now) write a custom migration

- [Data Loss in Content-Type Table After Schema Modification _202401](https://github.com/strapi/strapi/issues/19141)
  - In Strapi v5 D&P and i18n won't be able to be disabled (though they don't have to be used) so technically in v5 the D&P delete issue won't be a problem anymore since it'll be forced on for all content-types (though you'll have the option to auto-publish by default or if new content should be a draft state).

- ## [Can't install strapi - Questions and Answers - Strapi Community Forum](https://forum.strapi.io/t/cant-install-strapi/33500)
- TypeError: Cannot read properties of undefined (reading 'addBreadcrumb')

```shell
# cd to your project and
npm install --legacy-peer-deps
npm run develop
```

# issues-not-yet
- ## 

- ## 

- ## 💾 [Can I save and upload media file with google drive?](https://forum.strapi.io/t/can-i-save-and-upload-media-file-with-google-drive/24817)
- I guess you could but you would have to make your own plugin for it.

- ## [Issue installing sharp glib-object.h: No such file or directory · lovell/sharp](https://github.com/lovell/sharp/issues/4003)
- [Update sharp package to version v0.33.2 · strapi/strapi](https://github.com/strapi/strapi/pull/19311)

- 
- 
- 

- ## [Concurrency issue with two nodes Postgres cluster _202309](https://github.com/strapi/strapi/issues/17929)
- Knex don't natively support clusters

- I've not used PG-Pool before (as I'm more of a MariaDB user) but I have used ProxySQL (which is a MySQL/MariaDB tool that is very similar).
  - Generally the "sync" in a DB cluster is typically non-blocking but it will depend on the cluster setup. You have a primary PG node and a read-replica yeah?
- Read-replicas should never be syncing back to master, it should be a one-way sync from master -> slave and that should be async.

- TBH for multi-node speed and fault tolerance I would generally recommend MariaDB. PG is best for single-node performance but their clusters are less than great (personal bias here).
  - MariaDB's Galera cluster (with multi-master support) is far superior especially if your application is write heavy.

- ## [Strapi won't start on a pooled database  _202103](https://github.com/strapi/strapi/issues/9546)
- There is a difference between connection pooling and database pooling
  - Connection pooling is a group of connections to a database that can be reused (instead of opening a connection, requesting data, and closing it will keep the connection alive to request more data on another request.) Connection pooling is about reducing connection latency
  - Database pooling AKA Database clustering is entirely different and typically means you have a primary database node and multiple read-replicas. Knex.js doesn't support Database pooling.

- How about separating the read and write database connections at the application level? When there are more collection types, the initial startup time for strapi becomes very slow or unable to start even with connection pooling. Separating the read connections to a scalable read replica set could solve this issue. (I'm using Postgres in my case)
  - EG: ProxySQL or MariaDB Maxscale which allow for read/write splitting, monitoring, logging, and even caching which far exceed anything we can (or will do) at the application level

- ## [Why doesn't Strapi have a built-in refresh token feature? - Questions and Answers - Strapi Community Forum _202304](https://forum.strapi.io/t/why-doesnt-strapi-have-a-built-in-refresh-token-feature/27543)
- JWTs usually have an expiration time (e.g., 15 minutes, 1 hour) to limit their validity. 
  - When a token expires, the client needs to obtain a new one. 
  - This is often done using a refresh token, which is a separate, longer-lived token that the client can exchange for a new JWT. 
  - This is a standard procedure that pretty much every api uses. 
  - So, why is no such feature implemented in Strapi?

- ## [Sharp - Media Upload Memory Leak](https://github.com/strapi/strapi/issues/14417)

- ## [Dissatisfaction with Strapi: Stability, Scalability, and Support - General - Strapi Community Forum _202301](https://forum.strapi.io/t/dissatisfaction-with-strapi-stability-scalability-and-support/24854)
- After spending 3 weeks on the customization of a large-scale e-commerce application, I ultimately decided to move away from Strapi permanently.
  - the lack of basic transaction rollback capabilities was a significant limitation for my use case.
  - the exception handling in the lifecycle hooks was not an effective solution and often resulted in a “400” error.
- For most large-scale projects, we have our users going for the enterprise edition that provides access to solution engineers. 

- I was also very surprised by the very heavy changes made from V3 to V4. Is ok to introduce breaking changes, but V4 broke everything. If you do the same for V5 I’m not switching.

- ## 🐛 [Inconsistency between responses gotten from the REST API and the Entity service API_202401](https://forum.strapi.io/t/inconsistency-between-responses-gotten-from-the-rest-api-and-the-entity-service-api/34975)
- strapi-plugin-transformer plugin was what I was going to recommend. Another approach you can use, is to write a transformer function to flatten the response.

- Yes, the transform plugin is the way to go. 
  - But I’ve recently learned that it’s all a joke. 
  - You see, core controllers invoke the transformResponse function which iterates over the service response and produces this highly impractical data/meta/attributes structure. This takes time. Then, the middleware offered by the transform plugin iterates again over that transformed response and flattens it. Which takes time again. 
  - A performant way would be to disable that transformResponse function alltogether, or at least the part that wraps all non-id field within attributes. Maybe patch-package could be used for that.
