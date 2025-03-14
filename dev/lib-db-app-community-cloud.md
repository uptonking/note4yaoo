---
title: lib-db-app-community-cloud
tags: [cloud, community, database]
created: 2023-10-27T19:03:36.913Z
modified: 2023-10-27T19:03:54.530Z
---

# lib-db-app-community-cloud

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-db-saas
- ## 

- ## 

- ## 

- ## What's up with managed Postgres providers starting to offer Auth?
- https://x.com/ImSh4yy/status/1899244975780479263
- Front end frameworks are missing loads of backend features and the DB providers think they can lock customers in with them faster than the front end frameworks can.

- Easier to setup row level security based api, if auth is built in.
# discuss
- ## 

- ## 

- ## 

- ## 云计算厂商的机器，是怎么挂载云硬盘的呢？用的什么技术呢？难不成是 SMB？
- https://twitter.com/sci_kobayashi/status/1730097196983570748
- 公有云不了解，之前做的通信私有云 IaaS 是挂到物理机用专门的网卡，走 iscsi、ceph 或者存储厂商的等价的协议成 block device，再 virtio 给 vm。
- 私有协议，virtio驱动
- ceph群集，fiber san等
- 虚拟存储方案，如ceph
- 云硬盘我理解为DAS, 单机独占，虚拟机通常是暴露为virtio块设备，底层是黑盒，自建非虚拟机使用的可以使用iscsi作为底层。smb通常用在NAS上，不是块设备，区别为可以多机共享。
- 一般是专门的存储网络，高性能的很多是走fc协议，san网络。还有更高性能的，用的是infiniband网络，带宽达到数百G。
- 如果说开源出来的协议的话可能有用nfs或者iscsi的，前者基于文件目录的层级，后者是底层的块设备层级。

- ## 我觉得学术界和工业界还是有点脱钩, 还在研究一些在 数据库在 modern hardware 上的优化, 
- https://twitter.com/baotiao/status/1727058804905509126
  - 我理解以后的数据库大部分应该是针对云上的硬件进行优化了, 包括 VM, essd 等
- 现在云厂商的 Paas 团队都针对底下 Iaas 做研发, 而不直接对接硬件了
- 不一定，云太贵了，而且很难发挥硬件极限，不符合系统研究的方向

- ## 🦀🔥 [Building a Cloud Database from Scratch: Why We Moved from C++ to Rust (2022) | Hacker News_202302](https://news.ycombinator.com/item?id=34737626)
- 
- 
- 

- ## 🦀🔥 [Building a Cloud Database from Scratch: Why We Moved from C++ to Rust | Hacker News_202205](https://news.ycombinator.com/item?id=31535158)
- 
- 
- 
