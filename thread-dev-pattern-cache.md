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

- ## 📌 Top 5 Caching Strategies Explained:
- https://x.com/ashishps_1/status/1886633417921425440

1. 𝐑𝐞𝐚𝐝 𝐓𝐡𝐫𝐨𝐮𝐠𝐡: The application always queries the cache first. If the data is not in the cache (cache miss), the cache itself fetches it from the database and stores it for future requests.

Pros: Simplifies application logic, ensures cache always has fresh data.
Cons: Higher cache complexity, might not suit write-heavy systems.

👉 Best for: Read-heavy apps like CDNs, social media feeds, and user profiles.

2. 𝐂𝐚𝐜𝐡𝐞 𝐀𝐬𝐢𝐝𝐞 (𝐋𝐚𝐳𝐲 𝐋𝐨𝐚𝐝𝐢𝐧𝐠): The application first checks the cache. If the data isn't found (cache miss), it fetches it from the database and stores it in the cache for subsequent requests.

Pros: Keeps cache small, avoids unnecessary data in memory.
Cons: Cache misses can be expensive, risk of stale data if updates are frequent.

👉 Best for: Systems with a high read-to-write ratio, like e-commerce sites.

3. 𝐖𝐫𝐢𝐭𝐞 𝐓𝐡𝐫𝐨𝐮𝐠𝐡: Every write operation is first stored in the cache, then immediately written to the database.

Pros: Ensures cache and database are always in sync.
Cons: Higher write latency, unnecessary caching of rarely accessed data.

👉 Best for: Consistency-critical systems, such as financial apps.

4. 𝐖𝐫𝐢𝐭𝐞 𝐀𝐫𝐨𝐮𝐧𝐝: The application directly writes to the database, bypassing the cache. The cache gets updated only when a read request occurs.

Pros: Avoids caching rarely accessed data.
Cons: Higher cache miss rate, causing frequent database reads.

👉 Best for: Write-heavy systems where data isn’t immediately needed, like logging systems.

5. 𝐖𝐫𝐢𝐭𝐞 𝐁𝐚𝐜𝐤: Data is first written to the cache, and the cache asynchronously updates the database in the background.

Pros: Super-fast writes, reduces database load.
Cons: Risk of data loss if the cache crashes before syncing with the database.

👉 Best for: High-write throughput systems, such as social media feeds.

- Which Caching Strategy Should You Use?
  - If reads are more frequent      → Read-Through / Cache-Aside
  - If writes need to be consistent → Write-Through
  - If you want to minimize unnecessary caching → Write-Around
  - If you need ultra-fast writes   → Write-Back

- ## 📌 7 Cache Eviction(驱逐; 逐出) Strategies You Should Know:
- https://x.com/ashishps_1/status/1886271044933079354
1. 𝐋𝐞𝐚𝐬𝐭 𝐑𝐞𝐜𝐞𝐧𝐭𝐥𝐲 𝐔𝐬𝐞𝐝 (𝐋𝐑𝐔)
- Removes the least recently accessed item first.
- Works well when older data is less likely to be used again.
- Example: Browser cache, in-memory caches like Redis.

1. 𝐋𝐞𝐚𝐬𝐭 𝐅𝐫𝐞𝐪𝐮𝐞𝐧𝐭𝐥𝐲 𝐔𝐬𝐞𝐝 (𝐋𝐅𝐔) 
- Evicts the least accessed items over time.
- Prioritizes keeping frequently used items in cache.
- Example: Machine learning inference caches, recommendation systems.

1. 𝐅𝐢𝐫𝐬𝐭 𝐈𝐧, 𝐅𝐢𝐫𝐬𝐭 𝐎𝐮𝐭 (𝐅𝐈𝐅𝐎)
- Evicts the oldest stored item first, regardless of usage.
- Simple to implement but may remove still-relevant data.
- Example: Simple queue-based caching systems.

1. 𝐑𝐚𝐧𝐝𝐨𝐦 𝐑𝐞𝐩𝐥𝐚𝐜𝐞𝐦𝐞𝐧𝐭 (𝐑𝐑)
- Randomly evicts an item when the cache is full.
- Low overhead, but less predictable performance.
- Example: Used in some network routers.

1. 𝐌𝐨𝐬𝐭 𝐑𝐞𝐜𝐞𝐧𝐭𝐥𝐲 𝐔𝐬𝐞𝐝 (𝐌𝐑𝐔)
- Opposite of LRU – evicts the most recently accessed item first.
- Useful when recent data becomes obsolete quickly.
- Example: Video streaming buffers, certain financial applications.

1. 𝐓𝐢𝐦𝐞 𝐭𝐨 𝐋𝐢𝐯𝐞 (𝐓𝐓𝐋)
- Items are evicted after a set time limit (expiry time).
- Prevents stale data, useful in distributed systems.
- Example: DNS caching, API response caching.

1. 𝐓𝐰𝐨-𝐓𝐢𝐞𝐫𝐞𝐝 𝐂𝐚𝐜𝐡𝐢𝐧𝐠
- Uses a fast in-memory cache (e.g., Redis) & a slower persistent cache (e.g., disk-based).
- Optimizes speed & storage by balancing hot and cold data.
- Example: CDN caching, hybrid cloud storage solutions.

- No single strategy is perfect—the right choice depends on:
  - Data access patterns (frequent reads? high writes?)
  - System constraints (memory, CPU, disk space)
  - Performance trade-offs (latency vs accuracy)

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
