---
title: lib-collab-utils-clock-time
tags: [collaboration, crdt, hybrid-logical-clock]
created: 2023-01-18T17:00:07.960Z
modified: 2023-01-18T17:00:50.055Z
---

# lib-collab-utils-clock-time

# guide

# hybrid logical clock
- who is using #hybrid-logical-clock
  - tinybase
  - crsqlite
  - CockroachDB
  - YugaByte DB

- notes
  - TiDB: Centralized clock

- hybrid-logical-clock roadmap 待改进的地方
  - 需要保存所有op，新客户端需要获取所有op从头开始计算
  - 每个单元格都有一个clock，其实可以每行保存一个clock+每列保存到该clock的偏移量
  - ref
    - [crsqlite](https://github.com/vlcn-io/cr-sqlite#3-crdts-for-mortals)

## blogs

- [Hybrid Logical Clocks | Jared Forsyth.com](https://jaredforsyth.com/posts/hybrid-logical-clocks/)
  - https://github.com/jaredly/hybrid-logical-clocks-example

## implementations

- https://github.com/consento-org/hlc
  - a Hybrid Logical Clock implementation in JavaScript. 
  - You can use this in a decentralized system to sort statements created by tow separate devices.
  - It is comparable to CockroachDB's implementation. 
    - It creates Timestamps with a nanosecond WallClock (using bigint-time) that supports de-/encoding to fixed size 96bit Uint8Arrays (compatible with codecs) or JSON object.
