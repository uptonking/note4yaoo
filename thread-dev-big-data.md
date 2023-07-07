---
title: thread-dev-big-data
tags: [big-data, thread]
created: 2023-04-19T07:30:03.445Z
modified: 2023-04-19T07:30:34.872Z
---

# thread-dev-big-data

# guide

# discuss
- ## 

- ## nice talk about Umbra: A Disk-Based System with In-Memory Performance,
- https://twitter.com/mim_djo/status/1657614372439744512
  - a perfect example for pure in-memory DB is #PowerBI vertipaq, very fast but very expensive too,
- Was just thinking about this today while watching the LTT video about a 21 ssd (pcie g4 x2) carrier board. It gets competitive throughput with DRAM sticks...at about a $20k price tag, so way more than dram... The problem is that throughput matters a lot less than latency.


- ## 一段时间不见，clickhouse竟然有这么多重大特性
- https://twitter.com/li_taiyang/status/1648174437299265541
  - 理清了ast/query tree/plan/pipeline等阶段，支持连续join
- 初步集成三大数据湖：iceberg/delta-lake/hudi
