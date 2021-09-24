---
title: job-algs-faq
tags: [algorithms, faq, job]
created: '2021-09-21T19:41:58.469Z'
modified: '2021-09-23T08:26:55.811Z'
---

# job-algs-faq  

# guide

# base-data-structure

## hashmap/dict

- 哈希冲突
- 当哈希表的索引范围是 [0,M-1] 时，最常见的哈希函数是除留余数法，但是很多时候不同关键码值 key 会计算得到相同的哈希值，发生表内冲突，此时需要进行处理
- 闭域法/开放地址法
  - 所有记录存在一张表内，为每个记录求得一个探查序列，如果产生冲突则增加偏移重新取模
- 开域法/链地址法
  - 将 hash 地址相同的记录链接在同一链表中
# base-sort

# base-search
