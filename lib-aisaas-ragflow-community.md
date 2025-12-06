---
title: lib-aisaas-ragflow-community
tags: [community, rag, ragflow]
created: 2025-12-06T13:25:36.923Z
modified: 2025-12-06T13:25:53.871Z
---

# lib-aisaas-ragflow-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## [S3 Support apart from local upload _202509](https://github.com/orgs/infiniflow/discussions/10328)
- 20251031: We're working on it. Expected to be released in our next version.

- ## [[RAGFlow] Use OSS componets instead of source avaliable counter parts _202405](https://github.com/orgs/infiniflow/discussions/1258)
  - I wonder will the community willing to swap some of the components with source available license to FOSS alternatives to fully embrace the philosophy and spirit of open source.
  - Currently I spot two: ElasticSearch to OpenSearch, and Redis to Valkey. I believe two are drop in replacements (except ElasticSearch as the SDK refuse to work with OpenSearch but I believe the code change will be minimal).

- One question about Elasticsearch is that its license prohibits providing the software to third parties as a hosted or managed Service, so it seems like using Elasticsearch in RAGflow does not have problems?
  - In addition, using Elasticsearch for RAGflow is only a temporary solution for now, after our own database infinity is mature and stable(during this summer), it will be the main choice for RAGflow, because it provides much more powerful features than Elasticsearch with multiple recall, much better performance, and lower resource consumption.

- Regarding to Elasticsearch, it will be removed in future, as long as Infinity is totally stable. However, if the community users insist on keeping Elasticsearch as a choice, it would be replaced with OpenSearch at that time.
# discuss-issues
- ## 

- ## 

- ## 

- ## [[Bug]: Layout analysis in document parsing is way too slow _202511](https://github.com/infiniflow/ragflow/issues/11529)
- The slow layout analysis you’re seeing is a known issue on ARM-based Macs like the M3 Ultra. RAGFlow’s document parsing (especially layout analysis) is heavily optimized for x86 CPUs and NVIDIA GPUs, but lacks ARM-specific optimizations—so even with powerful hardware, performance can be much worse on Mac ARM systems

- ## [[Question]: Issue running docker compose from the quickstart (Mac) _202412](https://github.com/infiniflow/ragflow/issues/3804)
- We officially support x86 CPU and nvidia GPU. While we also test RAGFlow on ARM64 platforms, we do not plan to maintain RAGFlow Docker images for ARM.
  - You can either use a x86 CPU machine to deploy RAGFlow or follow the guide build the RAGFlow docker image on ARM platform by yourself.

# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
