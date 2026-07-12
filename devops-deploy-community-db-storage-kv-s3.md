---
title: devops-deploy-community-db-storage-kv-s3
tags: [aws-s3, storage]
created: 2026-06-25T08:45:56.076Z
modified: 2026-07-12T14:42:35.687Z
---

# devops-deploy-community-db-storage-kv-s3

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-free/awesome
- ## 

- ## 

- ## 

- ## 

- ## 突然发现现在 CF 和 PlanetScale 合作了？可以直接在 CF 的 dashboard 中创建 PlanetScale 的数据库了
- https://x.com/vikingmute/status/2069970665663508736
  - Supabase 太坑，看着免费，几天不用的就给你挂起，还要写个 worker 触发一下，不如PlanetScale 直接每月 5 刀的方案好。
  - D1 好是好，大部分都可以满足需求，就是免费的是按 rows read 付费要注意点，还是要最好整个 5 刀入门套餐。

- 自己托管的PostgresSQL也可以用HyperDrive。这是为了解决每一个Worker都需要频繁的请求数据库，防止连接池枯竭。所以在Cloudflare边缘侧维护一个共享的连接池，给所有的Worker可以共用，提高连接的效率。
  - HyperDrive, 维护一个线上的连接池，用来连到外部的数据库。

- ava 后端用 PlanetScale 比 Supabase 舒服多了，MySQL 兼容 Spring Boot 直接接，连方言都不用改
  - Supabase 免费版那个挂起机制确实坑，做出海产品用户体验很差
  - CF + PlanetScale 一体化结算这个很香，少一个平台少一个坑
# discuss-paid
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
