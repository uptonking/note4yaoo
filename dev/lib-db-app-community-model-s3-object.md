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

- standalone MinIO does support bucket versioning, but the “warning” in the docs is really about durability and production‑readiness, not about the absence of the feature.
  - Versioning is available in Single‑Node Single‑Drive (SNSD) deployments. As of the May 4,  2023 server release, MinIO standalone (SNSD) will happily accept mc version enable … and keep multiple object versions in your bucket
  - That notice is cautioning that, on a single drive, all your versions live on the same disk without erasure coding. If that disk fails, all versions go with it.

- 
- 
- 

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

- ## 🤔 [SeaweedFS fast distributed storage system for blobs, objects, files and datalake | Hacker News _202402](https://news.ycombinator.com/item?id=39235593)
- SeaweedFS is built on top of a blob storage based on Facebook's Haystack paper. The features are not fully developed yet, but what makes it different is a new way of programming for the cloud era.
  - When needing some storage, just fallocate some space to write to, and a file_id is returned. Use the file_id similar to a pointer to a memory block. There will be more features built on top of it. File system and Object store are just a couple of them.
  - The allocated storage is append only. For updates, just allocate another blob. The deleted blobs would be garbage collected later. So it is not really mmap.
- The blob storage is what SeaweedFS built on. All blob access has O(1) network and disk operation.
  - Files and S3 are higher layers above the blob storage. They require metadata to manage to the blobs, and other metadata for directories, S3 access, etc.
  - These metadata usually sit together with the disks containing the files. But in highly scalable systems, the metadata has dedicated stores, e.g., Google's Colossus, Facebook's Techtonics, etc. SeaweedFS file system layer is built as a web application of managing the metadata of blobs.
  - Actually SeaweedFS file system implementation is just one way to manage the metadata. There are other possible variations, depending on requirements.
- what makes it different is a new way of programming for the cloud era?
  - Previously fallocate just allocate disk space for a local server. Now SeaweeedFS can allocate a blob on a remote storage.

- SeaweedFS does the thing: I've used it to store billions of medium-sized XML documents, image thumbnails, PDF files, etc. It fills the gap between "databases" (broadly defined; maybe you can do few-tens-KByte docs but stretching things) and "filesystems" (hard/inefficient in reality to push beyond tens/hundreds of millions of objects; yes I know it is possible with tuning, etc, but SeaweedFS is better-suited).
  - The docs and operational tooling feel a bit janky at first, but they get the job done, and the whole project is surprisingly feature-rich. I've dealt with basic power-outages, hardware-caused data corruption (cheap old SSDs), etc, and it was possible to recover.
- In some ways I feel like the surprising thing is that there is such a gap in open source S3 API blob stores. 
  - Minio is very simple and great, but is one-file-per-object on disk (great for maybe 90% of use-cases, but not billions of thumbnails). This has not been true since 2021. https://blog.min.io/minio-optimizes-small-objects/
  - Ceph et al are quite complex. There are a bunch of almost-sort-kinda solutions like base64-encoded bytes in HBase/postgresql/etc, or chunking (like MongoDB), but really you just want to concatenate the bytes like a .tar file, and index in with range requests.
- The Wayback Machine's WARC files plus CDX (index files with offset/range) is pretty close.

- GarageS3 is a nice middle ground, it is not file on disk per object but it's simpler than SeaweedFS as well. https://garagehq.deuxfleurs.fr/ /AGPL
  - Yes, garage sourcecode is very easy to read and understand. Didn’t read seaweed yet.
- Garage has no intention to support erasure coding though.

- 🤔 What are the pros/cons of storing one file per object?
  - For many small objects a generic filesystem can be less efficient than a more specialised store. Things are being managed that aren't needed for your blob store, block alignment can waste a lot of space, there are often inefficiencies in directories with many files leading to a hierarchical splitting that adds more inefficiency through indirection, etc. 
  - The space waste is mitigated somewhat by some filesystems by supporting partial blocks, or including small files directly in the directory entry or other structure (the MFT in NTFS) but this adds an extra complexity.
  - The significance of these inefficiencies will vary depending on your base filesystem. The advantage of using your own storage format rather than naively using a filesystem is you can design around these issues taking different choices around the trade-offs than a general filesystem might, to produce something that is both more space efficient and more efficient to query and update for typical blob access patterns.
  - The middle ground is using a database rather than a filesystem is usually a compromise: still less efficient than a specially designed storage structure, but perhaps more so than a filesystem. They tend to have issues (it just inefficiencies) with large objects though, so your blob storage mechanism needs to work around those or just put up with them. A file-per-object store may have a database also anyway, for indexing purposes.
- The other commenter already outlined the main trade-offs, which boils down to increased latency and storage overhead for the file-per-object model. As for papers, I like the design of Haystack. https://www.usenix.org/legacy/event/osdi10/tech/full_papers/...

- We (https://hivegames.io/) use this for storing 50+ TB of multiplayer match recordings ("replays"), heavily using the built-in expiry feature. It's incredibly easy to use and to built on top off; never had an issue updating, migrating or utilizing new features.

- This sounds like what Microsoft has tried but failed to do in numerous iterations for two decades: OFS (Cairo, unreleased predecessor to Windows 95), Storage+ (SQL Server 7.0), RFS (SQL Server 2000), Exchange Webstore, Outlook LIS, WinFS, and finally Microsoft Semantic Engine.

- We tested both SeaweedFS and Min.io for cheaply (HDD) storing > 100TB of audio data. Seaweed had much better performance for our use case.
  - with MinIO and erasure coding a single PUT results in more IOPS and we saw lower performance.
  - Also, expanding MinIO must be done in increments of your original buildout which is annoying. So if you start with 4 servers and 500TB, they recommend you expand by adding another 4 servers with 500TB at least.

- Advantages over Ceph?
  - Ceph should have 10x+ metadata overhead for chunk storage. When using erasure-coding writes are faster because it's using replication and then erasure-coding is done async for whole volumes (30GB).

- Forgive my ignorance but why is this preferable to a big ZFS pool?
  - I could be wrong here, but I believe this (ceph, et al) is the answer to the question: > """But what if I don't have a JBOD of 6x18TB hard drives with good amount of ECC RAM for ZFS? What if I have 3 raspberry pi 4's, at different houses with 3x 12TB externals on them, and 2 other computers with 2x 4TB externals on them, and I want to use that all together with some redundancy/error checking?" That would give (3x3x12)+(2x2x4)=124 TB of storage, vs 108TB in the ZFS single box case (of raw storage).
- Ceph is nice, but performance is lackluster on anything but a proper cluster (pun intended).

- Things to make sure of when choosing your distributed storage:
  1) are you _really_ sure you need it distributed, or can you shard it your self? (hint, distributed anything sucks at least one if not two innovation tokens, if you're using other innovation tokens as well. you're going to have a very bad time)
  2) do you need to modify blobs, or can you get away with read/modify/replace? (s3 doesn't support partial writes, one bit change requires the whole file to be re-written)
  3) whats your ratio of reads to writes (do you need local caches or local pools in gpfs parlance)
  4) How much are you going to change the metadata (if theres posix somewhere, it'll be a lot)
  5) Are you going to try and write to the same object at the same time in two different locations (how do you manage locking and concurrency?)
  6) do you care about availability, consistency or speed? (pick one, maybe one and a half)
  7) how are you going to recover from the distributed storage shitting it's self all at the same time
  8) how are you going to control access?

- Have used SeaweedFS to store billions of thumbnails. The tooling is a bit clunky, but it mostly works. The performance is very good for small-ish objects (memory usage + latency), and latency remains consistently good into 99.9 percentiles. We had some issues with data loss and downtime, but that was mostly our own fault.

- 
- 
- 

- ## [Looking for SeaweedFS experiences : r/selfhosted _202212](https://www.reddit.com/r/selfhosted/comments/zks8xn/looking_for_seaweedfs_experiences/)
- The major issue I have is with the Weed Mount (FUSE), which has a number of bugs that can result in corruption, particularly around SQLite database. This basically makes Plex, Sonarr, Radarr unusable. At the moment I suffer from sporadic `weed mount` process crashes, which just fowl the reliability of the service
  - Thanks for sharing your experience. Having to run JuiceFS and Minio instead of just one piece of software makes more management overhead, so I would like to avoid that if possible.

- JuiceFS with Redis (with append-only + real-time save) is extremely reliable for me. It stores the data on any S3-compatible storage backend (e.g. Amazon S3, GCP Cloud Storage, or your local Minio cluster). The config allows you to set how often the metadata is backed up to the S3. While file data is stored on S3-compatible storage, the metadata can be stored on Redis, etcd, TiKV, etc. Plenty of setup options. Easy to install too. One thing about these mounted file systems. They use FUSE and the file names must be <= 255 characters.
- JuiceFS is not a storage backend; it's a distributed mounting system, allowing you to make the same storage available all across your network. It will need a block storage like Minio which does erasure coding and storage. 
# discuss-vercel-blob
- ## 

- ## 

- ## 

- ## 

- ## 📃 [Supabase Storage now supports the S3 protocol | Hacker News _202404](https://news.ycombinator.com/item?id=40083807)
  - we have a storage product for large files (like photos, videos, etc). 
  - The storage paths are mapped into your Postgres database so that you can create per-user access rules (using Postgres RLS)
  - We can do neat things like dump postgres tables in to Storage (parquet) and you can connect DuckDB/Clickhouse directly to them.

- is the data really stored in a Postgres database? Do you support transactional updates like atomically updating two files at once?
  - We do not store the files in Postgres, the files are stored in a managed S3 bucket.
  - We store the metadata of the objects and buckets in Postgres so that you can easily query it with SQL. You can also implement access control with RLS to allow access to certain resources.
  - It is not currently possible to guarantee atomicity on 2 different file uploads since each file is uploaded on a single request, this seems a more high-level functionality that could be implemented at the application level
- So this is like, S3 on top of S3? That's interesting.
  - Yes indeed! I would call it S3 on steroids!
  - Currently, it happens to be S3 to S3, but you could write an adapter, let's say GoogleCloudStorage and it will become S3 -> GoogleCloudStorage, or any other type of underline Storage.
  - Additionally, we provide a special way of authenticating to Supabase S3 using the SessionToken, which allows you to scope S3 operations to your users specific access control

- I like to Lob my BLOBs into PG's storage. You need that 1-2TB of RDS storage for the IOPS anyway; might as well fill it up. Large object crew, who's with me?!
- I don't. S3-compatible storages usually are significantly cheaper, allow to offload HTTP requests. Also huge databases make backups and recoveries slow.
  - The only upside of storing blobs in the database is transactional semantics. Buf if you're fine with some theoretical trash in S3, that's trivially implemented with proper ordering.
- that's not how this works. files are stored in s3, metadata in postgres
  - A trigger could add a "job" to delete the blob into another table when the file record is deleted though..
- Lol. The most PG blob storage I've used in prod was a couple hundred GB. It was a hack and the performance wasn't ideal, but the alternatives were more complicated. Simple is good.
  - Yeah, it's a great place to start. I took the time to implement streaming reads/write via npgsql's client support for it (it can stream records, and of course the Lob storage is broken into page sized rows) and performance is pretty darn good.

- in my experience Supabase was definitely challenging to selfhost. Pocketbase being literally single-binary doesn't make Supabase look good either, although funtionalities differ.
  - Yes, we have a vastly different architecture from Pocketbase. We choose individual tools based on their scaling characteristics and give you the flexibility to add/remove tools as you see fit.

- The S3 API reference is closest to a formal spec there is. The request, response and the error codes are pretty well documented.

- do you support pre-signed URLs?
  - we do not support signed URLs just yet, but it will be added in the next iteration
- Presigned URLs are useful because client app can upload/download directly from S3, saving the app server from this traffic. Does Row-Level Security achieve the same benefit?

- ## 💡 [The open-source alternative to Vercel Storage _202305](https://javascript.plainenglish.io/dodging-the-vercel-storage-tax-there-are-better-open-source-alternatives-ef04e537b598)
- Vercel Postgres — A PostgreSQL database powered by Neon, that’s easy to set up, easy to integrate with any Postgres client
- Vercel KV — a Redis compatible Key-Value store, powered by Upstash, available at Vercel Edge locations, and usable with any Redis client.
- Vercel Blob — An accessible, streamlined Amazon S3-compatible solution to upload, store, and serve binary files, powered by Cloudflare R2

- ## 📝 [Vercel Blob docs](https://vercel.com/docs/vercel-blob)
- Each Vercel Blob store can be accessed by multiple Vercel projects. Vercel Blob URLs are publicly accessible
- Each Blob is served with a `content-disposition` header. Based on the MIME type of the uploaded blob, it is either set to `attachment` (force file download) or `inline` (can render in a browser tab).
  - This is done to prevent hosting specific files on @vercel/blob like HTML web pages. 

- When you request a blob URL using a browser, the content is cached in two places: Your browser's cache, Vercel's cache
  - Both caches store blobs for up to 1 month by default to ensure optimal performance when serving content.

- 🐛 When you delete or update (overwrite) a blob, the changes may take up to 60 seconds to propagate through our cache. 

- For optimal performance and to avoid caching issues, consider treating blobs as immutable objects:
  - Instead of updating existing blobs, create new ones with different pathnames 

- There are still valid use cases for mutable blobs with shorter cache durations, such as a single JSON file that's updated every 5 minutes with a top list of sales or other regularly refreshed data. 
  - For these scenarios, set an appropriate cacheControlMaxAge value and be mindful of caching behaviors.

- By default, Vercel Blob prevents you from accidentally overwriting existing blobs by using the same pathname twice. When you attempt to upload a blob with a pathname that already exists, the operation will throw an error.
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
