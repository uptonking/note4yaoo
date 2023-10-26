---
title: toc-db-postgresql
tags: [postgresql, toc]
created: 2023-10-26T15:28:28.832Z
modified: 2023-10-26T15:28:53.748Z
---

# toc-db-postgresql

# guide

# popular
- https://github.com/centerofci/mathesar /GPLv3/python/svelte
  - https://mathesar.org/
  - open source tool that provides a spreadsheet-like interface to a PostgreSQL database.
  - You can use Mathesar to build data models, enter data, and even build reports.
  - [Show HN: Mathesar – open-source collaborative UI for Postgres databases | Hacker News_202303](https://news.ycombinator.com/item?id=34999774)
# pg-viewer

# powered-by-pg

# pg-rewrite
- pg-mem /1.6kStar/MIT/202310/ts
  - https://github.com/oguimbal/pg-mem
  - https://oguimbal.github.io/pg-mem-playground/
  - An in memory postgres DB instance for your unit tests
  - It works both in Node or in the browser.
  - 依赖immutable.v4、functional-red-black-tree、json-stable-stringify、lru-cache、moment、pgsql-ast-parser、@mikro-orm/core~pg
  - The sql syntax parser is home-made. Which means that some features are not implemented, and will be considered as invalid syntaxes.
  - limitations
    - Materialized views are implemented as views (meaning that they are always up-to-date, without needing them to refresh)
    - Indices implementations are basic
    - All number-like types are all handled as javascript numbers, meaning that types like `numeric(x,y)` could not behave as expected.
    - No support for timezones
  - https://github.com/oguimbal/pgsql-ast-parser
    - a Postgres SQL syntax parser. 基于nearley、moo实现
    - This parser does not support (yet) PL/pgSQL.

## pg-like

# more
