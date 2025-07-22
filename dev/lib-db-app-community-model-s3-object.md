---
title: lib-db-app-community-model-s3-object
tags: [aws-s3, comunity, database, object-storage]
created: 2024-03-13T14:25:51.906Z
modified: 2024-03-13T14:26:26.220Z
---

# lib-db-app-community-model-s3-object

# guide

# minio-dev
- brew install minio/stable/minio
  - minio server /mnt/data{1...64}
  - The MinIO deployment starts using default root credentials `minioadmin:minioadmin`; 
  - http://127.0.0.1:9000 and log in with the root credentials

- Enabling bucket versioning on a bucket with existing data immediately creates a `NULL` value version ID for each unversioned object.
# discuss-stars
- ## 

- ## 

- ## 💡🆚️ Can anyone recommend something on the 'why' of object stores like S3? 
- https://twitter.com/LewisCTech/status/1767676201961922762
- The invariants imposed by a filesystem structure (graph) are very hard to maintain in a massively parallel/distributed system, compared to an ordered key space pointing to blobs.
  - OK I kind of get 'why not a file system'. But I don't understand 'why not a key value store'.
- I'm not sure I understand what distinction you're drawing between a key value store and an object store.
  - Implementations are going to be pretty different here for those. K/V is small objects with a spectrum of different R/W access patterns and possibly multi-key atomicity/transactions. Also probably geared toward low latency. 
  - Object storage is mostly create and read. Large objects
- 🆚️ I would say they are both key-value stores w/ diff performance tuning for the values. 
  - The assumption w/ object storage is the values may be v large, and shouldn't have any structure imposed on them (i.e., they are blobs). 
  - DB-like KV has structure, size limits, and low latency
  - DB-like KV has low latency and additional access patterns (like indexes) gained by imposing structure and size limits
- how does that translate to disk storage? the key data structures for KV stores are LSM Trees and B+ Trees. What are they for object stores?
  - Why does that matter for users of these services?

# discuss-slatedb-news
- ## 

- ## 

- ## 

- ## SlateDB now has clones _202502
- https://x.com/criccomini/status/1886490144049651867
  - Clone an existing DB's data to a new location. Clones reference the data from the old bucket rather than copying. Writes to the clone update the new location. Compaction merges old data into new directory.

# discuss-s3-tools
- ## 

- ## 

- ## Let's say I have a 1GB+ JSON file on AWS S3 for a day's worth of data.
- https://x.com/arvidkahl/status/1910713079123366065
  - I want to combine these files into per-week, per-month, and per-year files, but I don't want to download, combine, and upload the merged file(s). That feels wasteful.
  - How would you do this economically?

- How’s the data structure of the per day week year file differ from the days worth of data? Is it an aggregate with summary statistics? Or just an append?
  - It's all just JSON arrays, so it would be a big append (but unfortunately not just a file append because of JSON syntax)
- quick tip: use JSONL! You still get the structure of json but you can append!
- Jsonl should be your choice of format because of lower memory usage during processing. Most of the time, you don't need to load the files into the memory.
- you absolutely should use jsonl in the future. But if this is a json array, you can technically still stream parse it, just a bit trickier.
- Actually jor jsonl files it is a file append. Each line is one row.

- compress each file, use jsonl, and use a streaming reader/writer

- 
- 

# discuss-seaweedfs
- ## 

- ## 

- ## 

- ## [Looking for SeaweedFS experiences : r/selfhosted _202212](https://www.reddit.com/r/selfhosted/comments/zks8xn/looking_for_seaweedfs_experiences/)
- The major issue I have is with the Weed Mount (FUSE), which has a number of bugs that can result in corruption, particularly around SQLite database. This basically makes Plex, Sonarr, Radarr unusable. At the moment I suffer from sporadic `weed mount` process crashes, which just fowl the reliability of the service
  - Thanks for sharing your experience. Having to run JuiceFS and Minio instead of just one piece of software makes more management overhead, so I would like to avoid that if possible.

- JuiceFS with Redis (with append-only + real-time save) is extremely reliable for me. It stores the data on any S3-compatible storage backend (e.g. Amazon S3, GCP Cloud Storage, or your local Minio cluster). The config allows you to set how often the metadata is backed up to the S3. While file data is stored on S3-compatible storage, the metadata can be stored on Redis, etcd, TiKV, etc. Plenty of setup options. Easy to install too. One thing about these mounted file systems. They use FUSE and the file names must be <= 255 characters.
- JuiceFS is not a storage backend; it's a distributed mounting system, allowing you to make the same storage available all across your network. It will need a block storage like Minio which does erasure coding and storage. 
# discuss-minio-like
- ## 

- ## 

- ## 

- ## 🆚 [S3 implementation comparison — Vitastor _202405](https://vitastor.io/en/blog/2024-05-09-s3-comparison.html)
  - The main interest during comparison is comparing the S3 frontend, the external part of the server, because the storage layer will anyway be replaced with our own one (Vitastor).
- Summary 
  - Ceph > Zenko CloudServer > Minio > SeaweedFS
  - According to ceph s3-tests: 576 > 382 > 321 > 56.

- ## [MinIO Alternative (Petabytes) : r/kubernetes _202403](https://www.reddit.com/r/kubernetes/comments/1bdq4yl/minio_alternative_petabytes/)
- We use rook-ceph in our product. If you have enough osds configured, it's pretty reliable. From what I've seen, it is quite sensitive to host ungraceful reboots or shutdown. Other than that, it seems fine.
- Rook Ceph is fine if you use lots of virtual disks to reduce pg size. Usually have to force reboots and I find the object storage a pain to set up, especially with certificates, but it does the job. I sometimes have issues with volumes mounting to specific nodes too but could also be the old environment I'm on. Easy as fuck to scale at least. Just mount new empty volumes and it just eats them up.

- ## 💡 [Garage - S3 object storage alternative to Minio : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kw1q9j/garage_s3_object_storage_alternative_to_minio/)
- Are there options to present files as both POSIX compatible directory tree and as flat objects a la S3?
  - No, garage store files as chunks on disk, although they are just zstd-compressed blob, so you can simply put them back together, no additional wrapping of any kind.

- there is seaweedfs (more complicated) which does not store files on the disk, but you can mount it with fuse which exposes a posix dir tree

- juicefs 你搜搜索这个满足你需要吗

- Ceph is really good, but also « harder » to maintain and different to Garage from what I read. Garage is really meant to be even on old PC’s. Ceph has nearly all S3 features but not all, and to me it’s better in a real clustered internal network with high bandwidth.

- the best thing in minio was that it had an all-in-one binary. you just copy one file anywhere, run it, and you have a full S3 server with GUI and everything without any install or root user requirement.

- I am using Garage as well, two additional remarks though: setting CORS is not that intuitive, needs a separate s3 compatible client to change defaults (as far as i know)

- I considered garage at some point and stuck to minio, I think it was because of lack of integration with notifications (I run a faas when things change in a bucket). Anybody has a feature comparison ?

- SSE-C encryption seems supported as per

- Does this guard against data corruption? MinIO has some built-in protection that will repair corrupted files.
  - Yes it does, see https://garagehq.deuxfleurs.fr/documentation/operations/durability-repairs/ for more details.

- The one downside I’ve found with garage is it doesn’t support unathenticated access to files. So I always have to code my app to generate authenticated URLs, which isn’t always important to me (as the files are not sensitive).
  - It actually does, through the per-bucket “web access” feature.

- ## [Can someone with experience with Ceph and MinIO or SeaweedFS _202208](https://news.ycombinator.com/item?id=32498332)
  - I currently run a single-node SnapRAID setup, but would like to expand to a distributed one, and would ideally prefer something simple (which is why I chose SnapRAID over ZFS). 
  - Ceph feels to enterprisey and complex for my needs, but at the same time, I wouldn't want to entrust my data to a simpler project that can have major issues I only discover years down the road.

- Seaweedfs has problems with large "pools" it's based on an old facebook paper (haystack) and supposed for block storage to distribute large image caches. I found it mediocre(平庸的；不够好的) at best as it's documentation was lacking, performance was lacking (in my tests) and the multitude of components were hard to get working. The idea behind it is that every daemon uses one large file as data store to skip slow metadata access. There are different ways to access the storage over gateways.
- MinIO is changing so much in the last years thatI can't give a competent answer but compared to seaweedfs it uses many small local databases. Right now it's deprecating many features like the gateway and it is split into 2 main components (cli and server) compared the seaweedfs deployment is dead simple, but I don't know which direction the project is going. Went from a normal open source project to a more business like deal (in what I saw) like I said I didn't quite follow the process.
- Ceph is based on blocmlk storage. Offers an object gateway (s3/swift), fs (cephfs) and block storage (rbd). You can access everything through librados directly as well. For a minimal setup you need a "larger" vluster but it is the most flexible solution (imho). Uses the most resources as well, but you can do nearly everything you want without limit with it.

- SeaweedFS author here. Thanks for your candid answer. You do not need to use multiple SeaweedFS components. Just download the binary and run "weed server -s3".
  - There are many other components, but you do not really need to use them. This default mode should be good enough for most cases. I saw many times people try to optimize too early, but often unnecessary, and sometimes in the wrong way.
  - Depending on your case, you may need to add more filers. UCSD has a setup that uses about 10 filers to achieve 1.5 billion iops. 
  - There are many AI/ML users switching from MinIO or CEPH to SeaweedFS, especially with lots of images/text/audio files to process.
- I found MinIO benchmark results is really, well, "marketing". MinIO is basically just an S3 API layer on top of the local disks. Any object is mapped to at least 2 files on disk, one for metadata and one is the object itself.

- 
- 

- ## [Ask HN: Is there any good open-source alternative to MinIO? | Hacker News _202309](https://news.ycombinator.com/item?id=37587356)
  - MinIO has got some heavy licensing costs for commercial use. I was wondering if there is any object storage with an S3 API - ideally with a UI and something that could be run easily in a container.

- If you're looking for an open-source alternative to MinIO for object storage, you might want to consider projects like Ceph and OpenIO. 
  - Ceph offers scalable and high-performance storage, while OpenIO focuses on an object storage solution with a decentralized approach. Both have active communities and can be suitable options depending on your specific requirements.

- There is also Apache Ozone https://ozone.apache.org/

- SeaweedFS and Garage.
- I am using Seaweedfs with 40+ TB data and ~100M files. Serve 100-200k+ users daily with servers that just have HDD.

- We migrate from minio to seaweed around 2020/2021. At that time our minio server have problem handling hundreds of thousands small files.
- We used it for around 2yrs with the s3 gateway and it was very stable for around 50 TB of data mostly very small files (50-200kb).

- We were trying Garage out for quite some time and it worked well apart from two things: anonymous access and the bigger blocker for us was AGPL. 
  - Minio and Garage having the same license means I would always prefer Minio.

- ## [Alternatives to Minio? (self-hosted S3-compatible object storage) : r/selfhosted _202210](https://www.reddit.com/r/selfhosted/comments/y4tvgw/alternatives_to_minio_selfhosted_s3compatible/)
- I've been using https://github.com/seaweedfs/seaweedfs. There are many pieces in that architecture but the single binary with arguments `server -dir=/data -s3 -idleTimeout=30` will do the trick to serve S3

- I simply had too much data for Garage to handle it properly, at least 2 years ago. It's not just that it was many TBs (it was about 3TB back then, it's closer to 7 now), but most of all the problem was that I had lots of small files (at the moment, it's almost 400k files)
- No problem with garage itself particularly. The issue is that I wanted to give another app access to the same data (specifically, httpd2 running inside Docker) and that didn’t support S3 natively. I found ways to mount the S3 volume inside a Docker container as volume, but i got to the conclusion that it wasn’t worth it. I also can’t remember for sure, but I believe Garage doesn’t store data on the file system as-is, but rather chunks it, so giving my container direct access to the file system wasn’t an option. Backups were harder too. My backup strategy for the other data is to use restic to sync to 2 other places, and restic didn’t work perfectly with data in garage. Eventually I wanted to standardize on either using garage for everything, or direct access for everything. Having S3-compatible endpoints is great in theory but in practice it wasn’t worth it
- 💡 even min.io store the data in "chunks", as would CEPH, the idea/method is to spread the chunks with their redundancy data (or duplicated/etc.) much like RAID. the fact the files are named the same, doesn't mean the data "usable" on anything other than a single node.

- There's apache ozone, but it's buggy as hell

- ## [Nutanix Objects violates MinIO’s open source license | Hacker News _202207](https://news.ycombinator.com/item?id=32148007)
- Any recommendations on MinIO forks or open-source alternatives with more welcoming licenses?
  - There are quite a few Storage projects out there with a S3-compatible API storage, that can be used in place of Minio such as Ceph, Openstack Swift, SeaweedFS, etc..
- No one in their right mind would attempt to use Ceph in place of MinIO. Yes, Ceph can provide S3 compliant object storage via the RadosGW, but the effort and footprint is not worth it for MinIO use cases. 
  - On the other hand, OpenStack Swift's all-in-one (typically used by developers) could easily be a replacement of MinIO.
- The CNCF maintains a list of closed and opensource container-friendly storage backends

- our organization was using Minio as an external S3 replacement and had contacted their sales once. When a decision was made to not go for the paid plan, we were legally threatened saying that we cannot even make remote calls to a AGPL software.

- Around 2019, a lot of kubernetes distributions started popping up. They often bundle various open source solutions into one platform/PaaS and sell it to the end users. I wonder, - Do they share revenue with the open source projects?

- libvirt uses LGPL and the KVM/linux kernel uses GPL. Both are fine to keep to yourself if you run it on your own machine and only expose it over the network.
  - MinIO uses AGPL which explicitly includes network usage so Nutanix is forced to provide all patches and associated code.
# discuss
- ## 

- ## 

- ## 

- ## Last year, it was S3 Express One Zone. This year, it’s S3 Tables. These features indicate three key trends:
- https://x.com/YingjunWu/status/1864411659336552753
  - Lakehouses are the new norm. The days of traditional data warehouses are numbered!
  - Apache Iceberg’s leadership in the open table format space has been reaffirmed by a major cloud provider.
  - Every data infrastructure vendor must now seriously consider their Apache Iceberg strategy.

- ## Justin, CTO of Docker, share my post on implementing "Delta Lake" from scratch in a talk at kubecon. "Object Storage Is All You Need"
- https://x.com/eatonphil/status/1857807099851395336
  - [Build a serverless ACID database with this one neat trick (atomic PutIfAbsent) | notes.eatonphil.com _202409](https://notes.eatonphil.com/2024-09-29-build-a-serverless-acid-database-with-this-one-neat-trick.html)

- ## Why are Object Databases not mainstream and we still waste gigawatts of electricity to convert to tables and relations back and forth?
- https://x.com/bercut2000/status/1809141678013387080
- Because modern SQL adopted NOSQL features, we can store and index JSONs in SQLite.

- Normalisation is a core capability of the relational model. The good parts of object databases were integrated in SQL's ORDBMS extensions, just like the good parts of XML and JSON dbs were integrated in SQL/XML and SQL/JSON.

- ## Are there any databases which use S3 / S3 Express One Zone as primary storage?
- https://x.com/iavins/status/1801799034455396669
- TiDB Serverless uses S3 as its primary storage.
  - Are there any details available on you store the pages, indexed and kept it all cost efficient?
- It has a custom LSM implementation., unlike TiKV which uses RocksDB. The SST files are stored on S3.
  - It has a custom LSM implementation., unlike TiKV which uses RocksDB. The SST files are stored on S3.

- @DatabendLabs relies solely on S3 for its primary storage, which means there's no need for tiered storage or intermediate disk caching. 
  - With a stateless query engine that’s production-ready, DatabendLabs is well-equipped to handle both batch processing and streaming data tasks seamlessly.

- EBS is a replicated and scalable system. What is the practical benefit of processing data on/from S3(like why not use directly use EBS)?
  - S3 is cheap for storage, expensive for individual requests. 
  - EBS is expensive to store but cheap for individual requests. 
  - If we did all reads directly from S3 it would be very expensive.
- Makes sense. I am guessing the database runs totally from EBS. Is there a situation where a warmed up database node needs to pull data from S3? I guess compacted files, etc?
  - Starting up a new compute node will initially read from S3, cold start just like any other database. This architecture makes it very easy to startup new compute nodes against S3 and scale compute or other background services. Since it’s a cache and more expensive than S3, we want to keep the minimum amount of data in the EBS cache. Also, the architecture has a distributed file system abstraction at the storage layer. This allows adding any type of caching between S3 and the compute node. Eg., we could write some type of distributed shared memory layer as another cache type to reduce latency further and  reduce the cost by sharing this cache, we don’t do this but it’s possible.

- here it is RisingWave Streaming Database with Yingjun Wu
