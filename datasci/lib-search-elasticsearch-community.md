---
title: lib-search-elasticsearch-community
tags: [community, elasticsearch]
created: 2023-01-02T08:49:27.078Z
modified: 2023-01-02T08:49:39.114Z
---

# lib-search-elasticsearch-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Elasticsearch, the server_201608](https://www.elastic.co/blog/elasticsearch-the-server#_embedded_elasticsearch_not_supported)
- Some users run Elasticsearch as embedded. We are not going to stop them from doing so, but we cannot support it. 
  - Embedding Elasticsearch bypasses the security manager, the Jar Hell checks, the bootstrap checks, and plugin loading. 
  - It is inherently unsafe and not recommended for production. 
  - For the sanity of our developers and support team, we cannot support users who disable all of the safety mechanisms which we have added for good reasons. 

- ## [ElasticSearch in-memory for testing - Stack Overflow](https://stackoverflow.com/questions/31400491)
- As of 2016 embedded elasticsearch is no-longer supported
