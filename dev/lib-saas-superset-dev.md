---
title: lib-saas-superset-dev
tags: [apache-superset, bi, viz]
created: 2020-09-25T08:01:55.941Z
modified: 2023-12-15T17:04:12.218Z
---

# lib-saas-superset-dev

# xp

- 优点
  - 可视化功能丰富
- 缺点
  - 渲染慢、查询慢

- xp
  - 首页的卡片和可视化预览图可切换显示模式

- who is using #superset
  - preset.io作为主力研发公司
  - 第三方厂商直接开卖云服务了 [Apache Superset as a Service](https://pushmetrics.io/apache-superset)
    - superset cloud/online demo
# docs

## faq

### Can I join/query multiple tables at one time?

- Not in the Explore or Visualization UI. 
  - A Superset SQLAlchemy datasource can only be a single table or a view.
  - When working with tables, the solution would be to materialize a table that contains all the fields needed for your analysis, most likely through some scheduled batch process.

### What database engine can I use as a backend for Superset?

- By default, Superset creates and uses an SQLite database at `~/.superset/superset.db`. 
  - SQLite is known to not work well if used on NFS due to broken file locking implementation on NFS.

- To clarify, the database backend is an OLTP database used by Superset to store its internal information like your list of users, slices and dashboard definitions.
- Superset is tested using Mysql, Postgresql and Sqlite for its backend. 
  - It’s recommended you install Superset on one of these database server for production.
- Using a column-store, non-OLTP databases like Vertica, Redshift or Presto as a database backend simply won’t work as these databases are not designed for this type of workload. 
- Installation on Oracle, Microsoft SQL Server, or other OLTP databases may work but isn’t tested.
- Please note that pretty much any databases that have a SqlAlchemy integration should work perfectly fine as a datasource for Superset, just not as the OLTP backend.
# ref


- [SuperSet安装配置及导入示例数据](https://iminto.github.io/post/superset%E5%AE%89%E8%A3%85/)

- [2022 Recap of the Apache Superset Project | Preset](https://preset.io/blog/2022-visual-recap-of-the-apache-superset-project/)

- [Understanding the Superset Semantic Layer](https://preset.io/blog/understanding-superset-semantic-layer/)
  - A semantic layer is an abstraction over your base data, which usually inhabits some type of SQL-speaking data base or data engine, that maps the underlying data to human-friendly metaphors.
  - The goal of a thin semantic layer then is to primarily enable last mile data transformation for the explicit purpose of visualization.
  - Looker built an entire product essentially around a semantic layer (LookML). 
    - While this established Looker as a source of truth in an organization for business metrics, it also created an immense amount of lock in. 
    - You couldn’t take your LookML models with you and use them with another tool, if you decided to switch BI tools.
  - The semantic layer in Superset consists of three main metaphors:
  - 👉🏻️ Virtual Datasets
    - A physical dataset in Superset represents a table or view in your database. 
    - Superset is able to automatically pull in relevant information from the database (like schema and column types). This information is saved in Superset’s metadata database. 
    - If a change to the underlying database table occurs, you can click Sync Columns from Source to force Superset to update its internal data model.
    - Virtual datasets enable you to elevate a freeform SQL query against your database into a dataset entity in Superset. 
  - 👉🏻️ Metrics
    - a metric in Superset is any valid, aggregating SQL snippet that can be included in a SELECT clause. 
    - Each line within the SELECT clause below are valid metrics in Superset
    - like count(*), max('price'), sum('iphone_orders')
  - 👉🏻️ Calculated Columns
    - Calculated columns let you define simple transformations (as SELECT statements) for quick, last-mile data preparation.
    - You can define any valid, non-aggregate SQL snippets that can be included in a SELECT clause. Note that this means you can reference multiple columns in your calculated column queries.
  - it’s helpful to remember that all of these features exist to help you craft better and more complex SQL queries. 
  - BI tools provide convenient UI interfaces and affordances so you can avoid having to manually write very long SQL queries from scratch.
  - Ultimately, the end-user facing features of Superset  help you generate more complex SQL queries.
    - Virtual datasets, metrics, and calculated columns provide useful abstractions and superpowers to augment your queries.
    - Explore provides a no-code, drag & drop UI for quickly generating queries that power visualizations.
    - Because the final artifact of the workflows in Superset is SQL, you can use SQL Lab to debug any of the queries that are written. 
    - When in Explore, select the hamburger menu in the top right corner and then select View Query to observe the query SQL Superset generated.

