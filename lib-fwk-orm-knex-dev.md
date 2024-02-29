---
title: lib-fwk-orm-knex-dev
tags: [knex]
created: 2023-01-22T19:52:12.643Z
modified: 2023-01-22T19:52:21.676Z
---

# lib-fwk-orm-knex-dev

# guide

- pros
  - transaction support (with savepoints)
  - connection pooling
  - streaming queries

- cons
  - ?

- features
  - both a promise and callback API

- who is using #knex
  - cms: strapi, directus, ghost
  - app: nocodb, locokit, budibase, automatisch
  - fwk: feathers.v5: 基于schema+resolver，通过knex+mongoose支持rdbms和nosql
  - libs: bookshelf, mikro-orm, adonisjs-lucid
  - more: undb, lightdash
# dev
- knex is for relational data. Using it with Mongo doesn't make much sense. I wholeheartedly recommend Mongoose.
# [changelog](https://github.com/knex/knex/blob/master/CHANGELOG.md)
- resources
  - [Changelog | Knex.js](https://knexjs.org/changelog.html)
  - [Upgrading to new knex.js versions](https://github.com/knex/knex/blob/master/UPGRADING.md)

## v

## v3.1.0_20231208

- Add transactor.parentTransaction
- MySQL: Added implementation for upsert

## v3.0.0_20231006 🎯

- Drop compatibility for Node < 16

- Fix migrate:unlock when used with custom identifier wrapping

## v2.0.0_20220421 🎯

- Restore sqlite3 package
  - Since `sqlite3` is maintained again, we switched back to it. 
  - If you are using `@vscode/sqlite3` driver dependency, please replace it with `sqlite3` in your package.json; 
- Migrate Jake to 10.8.5

## v1.0.0_20220116 🎯

- Node.js older than 12 is no longer supported

- Replaced unsupported sqlite3 driver with @vscode/sqlite3
  - If you are using `sqlite3` driver dependency, please replace it with `@vscode/sqlite3`.
- Changed data structure from RETURNING operation to be consistent with SELECT
  - RETURNING operations now always return an object with column names; 
- Changed Migrator to return list of migrations as objects consistently
  - Migrator now returns list of migrations as objects.

- Support fromRaw
- Support whereLike and whereILike
- Support creating a new table in the database based on another table
- Implement support for custom seed sources
- Advanced JSON support
- SQLite: New dialect, using `better-sqlite3` driver 
- SQLite: Switch to `@vscode/sqlite3`.
- SQLite: Switch to @vscode/sqlite3
- PostgreSQL: Support JOIN and USING syntax for Delete Statement

## v0.95.0_20210303 🚨

- TypeScript 4.1+ is now required

- Various internal refactorings
  - There was a major internal restructuring and renaming effort. Most dialect-specific compilers/builder have dialect name as a prefix now.

- [Refactor to classes_20210101](https://github.com/knex/knex/pull/4190)
  - Clients are now classes instead of new-able functions. Please migrate your custom clients to classes.

- TypeScript type exports changed significantly. 
- Add transaction isolation support
- Add analytic functions
- Change default to not trigger a promise rejection for transactions with a specified handler
- Allow 'match' operator
- Support optimizer hints
- Make "first" and "pluck" mutually exclusive 
  - "first" and "pluck" can no longer be both chained on the same operation. 
  - Previously only the last one chained was used, now this would throw an error.
- Added merge strategy to allow selecting columns to upsert
- Global static `Knex.raw` support dropped, use instance `knex.raw` instead. 
- CLI: Use UTC timestamp for new migrations
- SQLite: Fallback to json for sqlite3 when using jsonb
- SQLite: Recreate indices when altering a table
- SQLite: Add support for altering columns

## v0.21.19_20210302

- SQLite: Made the constraint detection case-insensitive
- SQLite: Add primary/foreign support on alterTable

- Node.js older than 10 is no longer supported

## v0.20.0_20191025

- orderBy accepts QueryBuilder
- Add validation in .offset()

## v0.10.0_20160215

- insert and update now ignore undefined values. 
  - Back compatibility is provided through the option useNullAsDefault
- Add schema.jsonb. Deprecated schema.json(column, true)

## v0.1.0_20130513

- Initial Knex release
# more
