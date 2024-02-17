---
title: lib-fwk-orm-knex-docs
tags: [docs, knex]
created: 2023-01-22T19:52:24.639Z
modified: 2023-01-22T19:52:35.031Z
---

# lib-fwk-orm-knex-docs

# guide
- resources
# overview
- The heart of the library, the knex query builder is the interface used for building and executing standard SQL queries, such as `select, insert, update, delete`.

- Knex can be used as an SQL query builder in both NodeJS and the browser, limited to WebSQL's constraints (like the inability to drop tables or read schemas). 
  - 🚨 Composing SQL queries in the browser for execution on the server is highly discouraged, as this can be the cause of serious security vulnerabilities.
  - The primary target environment for Knex is Node.js
  - The browser builds outside of WebSQL are primarily for learning purposes

- 
- 
- 

# docs
- The client created by the configuration initializes a connection pool, using the `tarn.js` library
  - This connection pool has a default setting of a `min: 2, max: 10` for the MySQL and PG libraries, and a single connection for sqlite3 (due to issues with utilizing multiple connections on a single file).
  - Note that the default value of `min` is 2 only for historical reasons. It can result in problems with stale connections
  - It is recommended to set `min: 0` so all idle connections can be terminated.

- TypeScript support is currently best-effort. Knex has a very flexible API and not all usage patterns can be type-checked and in most such cases we err on the side of flexibility. 
# Interfaces
- Promises are the preferred way of dealing with queries in knex
  - The main benefit of promises are the ability to catch thrown errors without crashing the node app, making your code behave like a `.try / .catch / .finally` in synchronous code.

- Streams are a powerful way of piping data through as it comes in, rather than all at once.
  - If you wish to use streams with PostgreSQL, you must also install the `pg-query-stream` module. 
  - If you wish to use streams with the `pgnative` dialect, please be aware that the results will not be streamed as they are received, but rather streamed after the entire result set has returned.

- A `query` event is fired just before a query takes place, providing data about the query, including the connection's `__knexUid / __knexTxId` properties and any other information about the query as described in toSQL. 
  - Useful for logging all queries throughout your application.
- A `query-error` event is fired when an error occurs when running a query, providing the error object and data about the query, including the connection's `__knexUid / __knexTxId` properties and any other information about the query as described in toSQL. 
  - Useful for logging all query errors throughout your application.
- A `query-response` event is fired when a successful query has been run, providing the response of the query and data about the query, including the connection's `__knexUid / __knexTxId` properties and any other information about the query as described in toSQL, and finally the query builder used for the query.

- A `start` event is fired right before a query-builder is compiled.
  - While this event can be used to alter a builders state prior to compilation it is not to be recommended. 
  - Future goals include ways of doing this in a different manner such as hooks.
# config
- A knexfile.js generally contains all of the configuration for your database
  - db connection
  - env
  - migrations
  - Knex uses Liftoff to support knexfile written in other compile-to-js languages.

- ECMAScript Module support for knex CLI's configuration, migration and seeds enabled by the `--esm` flag
  - `node --experimental-modules ./node_modules/.bin/knex $@`
# Query Builder
- Most of the knex APIs mutate current object and return it. 
  - This pattern does not work well with type-inference.
  - If you don't want to manually specify the result type, it is recommended to always use the type of last value of the chain and assign result of any future chain continuation to a separate variable (which will have a different type).

- "With" clauses are supported by PostgreSQL, Oracle, SQLite3 and MSSQL. 
  - With" materialized clauses are supported by PostgreSQL and SQLite3. 

- onConflict
  - Implemented for the PostgreSQL, MySQL, and SQLite databases. 
  - A modifier for insert queries that specifies alternative behaviour in the case of a conflict. 
  - A conflict occurs when a table has a PRIMARY KEY or a UNIQUE index on a column (or a composite index on a set of columns) and a row being inserted has the same value as a row which already exists in the table in those column(s). 
  - The default behaviour in case of conflict is to raise an error and abort the query. 
  - Using this method you can change this behaviour to either silently ignore the error by using .onConflict().ignore() or to update the existing row with new data (perform an "UPSERT") by using .onConflict().merge().
# Schema Builder
- The `knex.schema` is a getter function, which returns a stateful object containing the query. 
  - Therefore be sure to obtain a new instance of the `knex.schema` for every query.
# Transactions
- All queries within a transaction are executed on the same database connection, and run the entire set of queries as a single unit of work. 
  - Any failure will mean the database will rollback any queries executed on that connection to the pre-transaction state.

- Throwing an error directly from the transaction handler function automatically rolls back the transaction, same as returning a rejected promise.

- Notice that if a promise is not returned within the handler, it is up to you to ensure `trx.commit, or trx.rollback` are called, otherwise the transaction connection will hang
  - Calling trx.rollback will return a rejected Promise

- Note that Amazon Redshift does not support savepoints in transactions.
# Raw
- Raw query object may be injected pretty much anywhere you want, and using proper bindings can ensure your values are escaped properly, preventing SQL-injection attacks.
- Positional bindings `?` are interpreted as values and `??` are interpreted as identifiers.
  - To prevent replacement of ? one can use the escape sequence \\?.

- The `knex.raw` may also be used to build a full query and execute it, as a standard query builder query would be executed. 
  - The benefit of this is that it uses the connection pool and provides a standard interface for the different client libraries.
# Ref
- Can be used to create references in a query, such as column- or tablenames. 
- This is a good and shorter alternative to using `knex.raw('??', 'tableName.columName')` which essentially does the same thing.
# migration
- `knex.migrate` is the class utilized by the knex migrations cli.

- By default, each migration is run inside a transaction. 
  - Whenever needed, one can disable transactions for all migrations or per-migration

- A lock system is there to prevent multiple processes from running the same migration batch in the same time. 
  - When a batch of migrations is about to be run, the migration system first tries to get a lock using a `SELECT ... FOR UPDATE` statement (preventing race conditions from happening). 
  - If it can get a lock, the migration batch will run. 
  - If it can't, it will wait until the lock is released.
- The locks are saved in a table called "tableName_lock"; it has a column called `is_locked`
# more
