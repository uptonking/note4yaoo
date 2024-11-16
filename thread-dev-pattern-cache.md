---
title: thread-dev-pattern-cache
tags: [cache, pattern, thread]
created: 2021-08-27T07:44:27.021Z
modified: 2023-12-10T14:20:42.600Z
---

# thread-dev-pattern-cache

# guide

# discuss-stars
- ## 

- ## 

- ## idb-cache: An IndexedDB-based caching library with encryption and chunked storage, optimized for performance and security.
- https://x.com/aaronshaf/status/1856751512778645785
  - Implements AsyncStorage interface. Hence, pluggable into TanStack Query.

- Random question, part from AsyncStorage standard, why all cache libraries are not designing cache key as plain object just like tanstack query queryKey dose?
  - TanStack Query serializes queryKey to a string.
- Yes, I know that. It just order the perperties by key and just JSON.stringify it. It's just much easier to use an object. Idk it just me or I frequently forget to include some properties into the cache key
  - That was something I really liked about rails' built in caching. They have a convention where anything that responds_to "cache_key" would be used 

- what is the use case to use this library? or storing encrypted data to local storage?
  - Avoiding unencrypted storage of PII.
# discuss
- ## 

- ## 

- ## 

- ## Data is cached at many stages, from the client-facing side to backend systems. 
- https://twitter.com/sahnlam/status/1761638991131259173
- Let's look at the many caching layers:
1. Client Apps: Browsers cache HTTP responses. Server responses include caching directives in headers. Upon subsequent requests, browsers may serve cached data if still fresh.
2. Content Delivery Networks: CDNs cache static content like images, stylesheets, and JavaScript files. They serve cached content from locations closer to users, reducing latency and load times.
3. Load Balancers: Some load balancers cache frequently requested data. This allows serving responses without engaging backend servers, reducing load and response times.
4. Message Brokers: Systems like Kafka can cache messages on disk per a retention policy. Consumers then pull messages according to their own schedule.
5. Services: Individual services often employ caching to improve data retrieval speeds, first checking in-memory caches before querying databases. Services may also utilize disk caching for larger datasets.
6. Distributed Caches: Systems like Redis cache key-value pairs across services, providing faster read/write capabilities compared to traditional databases.
7. Full-text Search Engines: Platforms like Elasticsearch index data for efficient text search. This index is effectively a form of cache, optimized for quick text search retrieval.
8. Databases: There are specialized mechanisms to enhance performance, some of which include caching concepts:
   - Bufferpool: This is a cache within the database that holds copies of data pages. It allows for quick reads and writes to temporary storage in memory, reducing the need to access data from disk.
   - Materialized Views: They are similar to caches in that they store the results of computationally expensive queries. The database can return these precomputed results quickly, rather than recalculating them.

- ## Caching is one of the fastest ways to boost performance.
- https://twitter.com/ProgressiveCod2/status/1755496174768070824
- But when you scale to thousands of servers in multiple clusters across regions, caching becomes extremely challenging.
- There are 3 major challenges that one has to solve:
  - Managing latency, load, and failures within a cluster
  - Managing replication of data within a region
  - Managing consistency of data across regions
- I talk in detail about how Facebook solved all of these issues with Memcached in my latest article.
  - [Facebook's Memcache Breakdown _202402](https://newsletter.systemdesigncodex.com/p/facebook-memcache-breakdown)

- ## 7 concepts you need to master Cache.
- https://twitter.com/RaulJuncoV/status/1733531023005110576
- Cache Hit Ratios
  - This is the answer to how effective your cache strategy is. 
  - A high hit ratio indicates that the Cache frequently contains the requested data. A high hit ratio minimizes fetching it from slower layers.
- Eviction Policies
  - They determine which data stays in the Cache and which gets removed; it's about efficiency.
  - Common policies include:
  - Least Recently Used (LRU)
  - Most Recently Used (MRU)
  - Least Frequently Used (LFU)
- Cache Coherence
  - Of course, it gets more complex In distributed systems.
  - Maintaining data consistency across these caches is critical.
  - Cache coherence ensures that all copies of a data item reflect the most recent version.
- Cache Granularity
  - This is about the size of the data units stored in the Cache. Granularity decisions impact the Cache's efficiency and hit ratio. 
  - How much data do you need to store in each operation?
- Cache Warm-up
  - Preloading the Cache with data expected to be in high demand will improve performance.
  - Especially in systems where cache hits are critical for speed.
- Cache Partitioning
  - In a well-organized toolbox, you'd have separate compartments or trays for different tools.
  - Cache partitioning is the same. It's about dividing the Cache into different sections, each tailored for a specific data type or request.
  - This organization improves the Cache since retrieving the data is easier and faster.
- Cache Compression
  - When space is at a premium, compressing cached data allows you to store more information.
  - But, this comes with the trade-off of processing overhead during compression and decompression.
- Caching isn't just dumping data somewhere and forgetting about it.
  - It's about being smart with what, how, and when you store data to make everything run smoother and quicker.

- ## Service worker didn't work for me as caching mechanism b/c of the following limitations:
- https://twitter.com/maxkoretskyi/status/1430958854754480129
  - can be destroyed at any time so can't use web sockets inside
  - cache API doesn't support POST methods while matching requests by HTTP header values
