---
title: lib-viz-superset-dev
tags: [apache-superset, lib]
created: '2020-09-25T08:01:55.941Z'
modified: '2020-12-08T13:35:12.509Z'
---

# lib-viz-superset-dev

# xp

- 优点
  - 可视化功能丰富
- 缺点
  - 渲染慢、查询慢

- xp
  - 首页的卡片和可视化预览图可切换显示模式

- who is using
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
