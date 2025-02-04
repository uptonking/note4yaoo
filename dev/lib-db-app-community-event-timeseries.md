---
title: lib-db-app-community-event-timeseries
tags: [community, database, events, timeseries]
created: 2023-10-26T18:56:20.572Z
modified: 2023-10-27T07:03:12.118Z
---

# lib-db-app-community-event-timeseries

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🤔 Is anyone building a serverless time-series database? (for geotiff)
- https://twitter.com/medriscoll/status/1761463338440200299
  - The architecture would be a one-dimensional version of what cloud optimized GeoTIFFs use:  tiles across time, with different aggregation levels (minutely, hourly, daily, etc), all backed by an object store.
  - You wouldn't need an always-on database, just a lightweight client to pull and process tiles, that could be spun-up on demand.
  - And you could probably connect it directly to @warpstream_labs , for a fully serverless ingestion and database time-series service.

- I’m building Data Taps with Boiling and DuckDB. Very simple and scalable data ingestion. Then analytics on Boiling serverless and on browser (duckdb wasm). But what does ”building a db” mean these days?
- protomaps is a good inspiration for this
- I think DuckDB will handle this really well in a release or 2. The plan is to propagate the notions of partitions & orderings through the execution plan. Then joins, window functions, etc can use that to do less work! It may require manual columns at different time granularities.
- I've seen a system like this, columnar format based. NAS based rather than object store, but it worked great at scale

- ## 🤔🔥 [Why Not to Build a Time-Series Database | Hacker News_201811](https://news.ycombinator.com/item?id=18402890)
- 
- 
- 

- ## ⏳🔥 [How Time Series Databases Work, and Where They Don’t | Hacker News_202110](https://news.ycombinator.com/item?id=28901063)
- 
- 
- 

- ## 🌰⏳🔥 [Write a time-series database engine from scratch | Hacker News_202107](https://news.ycombinator.com/item?id=27730854)
- 
- 
- 

- ## 🔥 [Writing a Time Series Database from Scratch | Hacker News_201704](https://news.ycombinator.com/item?id=14177411)
- 
- 
- 

- ## 🔥 [A Comparison of Time Series Databases and Netsil’s Use of Druid | Hacker News_201610](https://news.ycombinator.com/item?id=12686445)
- 
- 
- 

# discuss-influxdb
- ## 

- ## 

- ## [Influxdb made the switch from Go to Rust | Hacker News_202310](https://news.ycombinator.com/item?id=37725778)
- The issue is that InfluxDB is an infrastructure product. Changing the core impacts the way users interact with the product. If Figma decided to change their backend, it could be transparent to users.
  - Opinions could be different if first they implemented a complete compatibility layer, Flux included, prior to making the migration.

- I love InfluxDB 1.x and the TICK stack. They abandoned a beautiful piece of software to chase shiny things with 2.x... sad to see them do it again.

- Can someone explain what's the InfluxData's market? Or how they make/plan to make money? If we speak about metrics, Prometheus just win.
  - Metrics is certainly one use case that people pay us for. With v3, we expect that real-time analytics and some more data warehousing types of use cases will become interesting. We always envisioned InfluxDB as a store for observational data of all kinds, not just metrics.
  - InfluxDB v3 is built to handle this kind of data. It's a columnar database, using object storage and Parquet files for persistence.
- Prometheus is not just the db itself, it’s the ecosystem around it. You’ve got service-discovery, alertmanager and basically every application in existence having a /metrics endpoint and some pre-made Grafana dashboard.
# discuss
- ## 

- ## 

- ## 

- ## What does the twitterverse recommend for a managed time series database? _202312
- https://twitter.com/apurva1618/status/1730353635027304614
- I'm running Influx on a Raspberry Pi for collecting my solar system's data. Works very well
  - just regular solar panels (10 kWp) and battery storage. The inverter exposes all kind of data which I query every 30 sec and put into Influx. Then I have a Grafana dashboard, so I e.g. know when it's good time to turn on heavy consumers, without having to buy energy from
- What is your query patterns?  Don’t pick a database on hype and dreams.  Query patterns decide for you.
- Grafana - why not just go to the industry default?

- ## 🔥 [Timescale Announces New Database Cloud | Hacker News_202110](https://news.ycombinator.com/item?id=28761453)
- 
- 
- 

- ## 🔥 [Apache Druid vs. Time-Series Databases | Hacker News_202004](https://news.ycombinator.com/item?id=22868286)
- 
- 
- 

- ## 🔥 [CERN swaps out databases to feed its petabyte-a-day habit | Hacker News_202309](https://news.ycombinator.com/item?id=37581145)
- 
- 
- 

- ## ⏳🔥 [Launch HN: QuestDB (YC S20) – Fast open source time series database | Hacker News_202007](https://news.ycombinator.com/item?id=23975807)
- 
- 
- 

- ## ⏳🔥 [M3DB, a distributed timeseries database | Hacker News_202002](https://news.ycombinator.com/item?id=22391270)
- 
- 
- 

- ## ⏳🔥 [Timescale, an open-source time-series SQL database for PostgreSQL | Hacker News_201708](https://news.ycombinator.com/item?id=14984464)
- 
- 
- 

- ### 🔥 [Timescale: Building a scalable time-series database on PostgreSQL | Hacker News_201704](https://news.ycombinator.com/item?id=14035416)
- 
- 

- ## 🔥 [Time Series Databases to Watch | Hacker News_201905](https://news.ycombinator.com/item?id=19825566)
- 
- 
- 

- ## ⏳🔥 [It’s About Time for Time Series Databases | Hacker News_201801](https://news.ycombinator.com/item?id=16230464)
- 
- 
- 

- ## ⏳🔥 [A Review of Time Series Databases | Hacker News_201609](https://news.ycombinator.com/item?id=12486866)
- 
- 
- 

- ## ⏳🔥 [Prometheus: An open-source service monitoring system and time series database | Hacker News_201502](https://news.ycombinator.com/item?id=8995696)
- 
- 
- 
