---
title: lib-db-dolt-docs
tags: [docs, dolt]
created: 2023-08-25T21:17:33.752Z
modified: 2023-08-25T21:17:44.884Z
---

# lib-db-dolt-docs

# guide

# overview
- initial release: 201908

- 
- 
- 
- 
- 

- DoltHub is a modern web interface to a modern SQL database, Dolt.

- Dolt now supports cherry-pick.
  - With cherry-pick support, it's easy to re-apply changes from any existing commit in your database to any branch. 

- One of the benefits of being MySQL compatible is fair and honest performance assessments. Just dump your Dolt database, import to MySQL, and run the query. We can't hide!

- If you want soft deletes in your SQL database, Dolt is the best choice. 
  - You get all the benefits of soft deletes like data loss prevention, disaster recovery, and audit with none of the downsides of the traditional soft delete solutions.

- Dolt is a database that is built from the ground up to support version control. 
  - To be fully ACID-compliant, we built a new persistence layer for Dolt that supports durable transactions at high throughput. 

- Historically, database version control needed to be simulated using slowly changing dimension. 
  - Dolt is a database with slowly changing dimension built in. It's true database version control, no simulation required.

- Dolt has two options for replicating your primary Dolt database to another Dolt database: Standby Replication and Remote-based replication. 
  - Dolt can also be used as a replica of an existing MySQL instance.
# docs
