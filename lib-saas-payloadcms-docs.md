---
title: lib-saas-payloadcms-docs
tags: [docs, payloadcms]
created: 2023-02-05T18:40:02.963Z
modified: 2023-12-15T17:04:30.575Z
---

# lib-saas-payloadcms-docs

# guide

# overview

# docs-v3

> Payload is the Next.js fullstack framework.

- Payload is designed to interact with your database through a Database Adapter, which is a thin layer that translates Payload's internal data structures into your database's native data structures.
- Payload officially supports the following Database Adapters:
  - MongoDB with Mongoose
  - Postgres with Drizzle
  - SQLite with Drizzle
- The Database Adapter is an external dependency and must be installed in your project separately from Payload. 

- If your project has a lot of dynamic fields, and you are comfortable with allowing Payload to enforce data integrity across your documents, MongoDB is a great choice.
- You should prefer a relational DB like Postgres or SQLite if You have a lot of relationships between collections and require relationships to be enforced

- It's important to note that nearly every Payload feature is available in all of our officially supported Database Adapters, including Localization, Arrays, Blocks, etc. 
- The only thing that is not supported in SQLite yet is the Point Field, but that should be added soon.

- Database transactions allow your application to make a series of database changes in an all-or-nothing commit. 
  - By default, Payload will use transactions for all data changing operations, as long as it is supported by the configured database. 
  - Database changes are contained within all Payload operations and any errors thrown will result in all changes being rolled back without being committed. 
  - When transactions are not supported by the database, Payload will continue to operate as expected without them.
- Transactions in SQLite are disabled by default. You need to pass `transactionOptions: {}` to enable them.
- MongoDB requires a connection to a replicaset in order to make use of transactions.

- 
- 
- 
- 
- 

## db

- 
- 
- 
- 
- 
- 
- 
- 

# more
- `PAYLOAD_SECRET` is a required environment variable for Payload. 
  - It is a long, random, unguessable string that Payload uses for encryption workflows — signing and verifying auth tokens, password hashing, and other server-side crypto. 
  - It is not an API key you paste into the admin UI; your app reads it from the environment at startup.
