---
title: lib-db-postgresql-community-showcase
tags: [community, examples, postgresql, showcase]
created: 2023-10-26T16:45:28.359Z
modified: 2023-10-26T16:45:47.318Z
---

# lib-db-postgresql-community-showcase

# guide

# discuss-stars
- ## 

- ## 
# discuss
- ## 

- ## 

- ## 🔥 [PolarDB, yet another open source database system based on PostgreSQL | Hacker News_202105](https://news.ycombinator.com/item?id=27330342)
- 
- 
- 

- ## [digitalOcean: Fully managed PostgreSQL databases | Hacker News_201902](https://news.ycombinator.com/item?id=19162729)
- 
- 
- 

- ## 🔥 [PostgREST – Serve a RESTful API from any Postgres database | Hacker News_202212](https://news.ycombinator.com/item?id=34172205)
- 
- 
- 

- ## 🔥 [PostgREST: REST API for any Postgres database | Hacker News_202011](https://news.ycombinator.com/item?id=25159097)
- 
- 
- 

- ## 🔥 [PostgREST – A fully RESTful API from any existing PostgreSQL database | Hacker News_201703](https://news.ycombinator.com/item?id=13959156)
- 
- 
- 

- ## 🔥 [PostgREST – REST API from any PostgreSQL database | Hacker News_201507](https://news.ycombinator.com/item?id=9927771)
- 
- 
- 

- ## ☁️🔥 [fly.io: Free Postgres databases for small projects | Hacker News_202201](https://news.ycombinator.com/item?id=30018197)

- Free tier of CloudFlare Pages/functions runs the app at the edge by default. For Fly.io, this scaling has to be manually configured for both the app and the DB. Are there any plans to offer it by default for the free tier? It is hard to evaluate the benefits of having the data center near the end user when it is not offered out of the box, especially since all the Fly.io blog posts talk about how great their service is for HTML-over-the-wire UIs like Phoenix live view and Rails Hotwire.
  - You can squeeze a hell of a lot more perf out of general purpose compute that is maybe an extra 15 ms away than one-shot workers lacking any in-RAM persistence, or ability to do much more than limited local k/v lookups. The equation is totally different. Many workers I've seen (or written) start by reaching out over the Internet to another backend. There goes most of your edge benefit almost immediately.

- For comparison, note also that ElephantSQL offers 20MB databases on their free tier with 5 concurrent connections. https://www.elephantsql.com/plans.html
- https://supabase.com/pricing - 500MB, 2GB download/month (can be used as plain PostgreSQL)
- https://www.cockroachlabs.com/pricing - 5GB, 250M "request units"/month distributed, PostgreSQL-ish

- ## 🔥 [PgOSQuery: Expose the operating system as a Postgres database | Hacker News_201410](https://news.ycombinator.com/item?id=8532835)
- 
- 
- 
