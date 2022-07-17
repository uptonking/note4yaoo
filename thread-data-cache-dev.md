---
title: thread-data-cache-dev
tags: [cache, data, thread]
created: 2021-08-27T07:44:27.021Z
modified: 2021-08-27T07:44:55.105Z
---

# thread-data-cache-dev

# discuss

- ## 

- ## 

- ## 

- ## Service worker didn't work for me as caching mechanism b/c of the following limitations:
- https://twitter.com/maxkoretskyi/status/1430958854754480129
  - can be destroyed at any time so can't use web sockets inside
  - cache API doesn't support POST methods while matching requests by HTTP header values
