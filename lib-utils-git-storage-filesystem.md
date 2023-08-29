---
title: lib-utils-git-storage-filesystem
tags: [database, filesystem, git, storage]
created: 2021-06-01T16:54:44.333Z
modified: 2023-08-29T10:23:33.198Z
---

# lib-utils-git-storage-filesystem

# guide

# [Git数据存储的原理浅析](https://segmentfault.com/a/1190000016320008)
- 我的疑问：
  - git怎么存储数据的，如何能根据存储的数据可以很精确的回退到制定的版本？
  - git存储和docker的存储机制类似吗？是不是都是分层的存储？
  - git如果不是分层，每次提交都存储起来，那么数据量大了会怎么办

- 解惑路线是，从新建一个本地git仓库开始，一步一步增加数据和提交，观察内容的具体变化。
- git init
  - index是索引文件; 
  - HEAD表示当前提交的指针位置; 
  - refs文件夹中的文件是不同分支指向的commitID; 
  - logs文件夹中记录的是每次refs的历史记录; 
  - **objects文件夹中的内容就是用来存放git本地仓库对象**
- git数据结构是什么样的呢？
  - git是以键值的方式存储的，也就是说任何类型的数据都可以存储。因此也可以在任何时候通过键取出对应的值; 
- git中底层生成了4中数据的对象：
  - tree对象：可以看作一个目录，管理一些“tree”对象或是“blob”对象。它有一串指向“blob”对象或是其它“tree”对象的指针，一般用来表示内容之间的目录层次关系(就像文件和子目录)。
  - blob对象: 一个“blob”通常用来存储文件的内容。一个“blob”对象就是一块二进制数据，blob对象的键是根据SHA1算法生成的，所以若两个文件在一个目录树或是一个版本仓库中有同样的数据内容，那么它们将会共享同一个“blob”对象，和其所对应的文件所在路径、文件名是否改被更改都完全没有关系。
  - commit对象：“commit”对象指向一个“tree对象”，并且带有相关的描述信息，标记项目某一个特定时间点的状态。它包括一些关于时间点的元数据，如时间戳、最近一次提交的作者、指向上次提交的指针等等。
  - tag对象： 一个“tag”对象包括一个对象名(SHA1签名)、对象类型、标签名、标签创建人的名字(“tagger”), 还有一条可能包含有签名(signature)的消息。
- 当新增一些内容的时候，进行git commit命令会出现什么变化？
  - 当进行一次提交的时候，objects、logs和refs文件夹都会发生变化，我们主要关注objects文件夹。
  - **每次commit都会对数据进行一次保存，会生成commit对象、tree对象和blob对象**; 
  - objects文件夹里面的数据存放的具体规则，对于这三种对象，都会用SHA-1对内容和头信息生成Hash值，去hash值的前两位为objects目录下面的文件夹的名字，取剩余38个字符为文件名
- 总结问题的答案
  - git的数据存储数据结构是键值类型，分为4个对象，并且每次提交都是整个文件的存储，而不是分层的增加存储，所以这样会导致存储的数据量很大，
  - 那git用的方法是使用zlib对数据进行压缩，所以我们打开存储的文件是这样的数据，那我们都是用cat-file命令来查看的，怎么才能这些内容是经过zlib压缩过的呢？
  - 我用GO语言写了一个简单的程序，来验证这些数据是经过zlib压缩之后的，运行这个程序的时候带上你要查看git对象的文件路径，就可以看到被还原的内容了; 

- ref
  - [Git内部存储原理](https://zhaohuabing.com/post/2019-01-21-git/)
# [What filesystem does GitHub use for its repositories and why?](https://www.quora.com/What-filesystem-does-GitHub-use-for-its-repositories-and-why)

# discuss

- ## 

- ## 

- ## [github是如何存储海量的代码的，用到了什么技术，使用了什么数据库？](https://www.zhihu.com/question/56516064)
- 看看他们的技术博客，libgit2、glb-director
- 常见的分布式文件系统 GFS、HDFS、Lustre 、Ceph 、GridFS 、mogileFS、TFS、FastDFS等。
  - 各自适用于不同的领域，它们都不是系统级的分布式文件系统，而是应用级的分布式文件存储服务。

- ## [github的大量小文件存取是如何实现的?](https://www.zhihu.com/question/20056542)
- 按常理来看，写的部分应该是正常文件系统，但读的部分肯定是要用数据库的，不可能文件系统之间直接网络请求
  - 写的时候比如说SSH推送commit，或者是网页上的merge等命令, 这些最终都会转移到文件服务器来做具体的git操作，然后把变化映射到数据库里面。这些写的请求绝对数量虽然大，但比起网络请求的数量就不值一提了。
  - 然后数据库加缓存应付大访问量就很成熟了，没有什么特殊的。

- ## [How does Github store millions of repo and billions of files?_202104](https://blog.pankajtanwar.in/how-does-github-store-millions-of-repo-and-billions-of-files)
- Github Architecture
- Whenever you type a Github repo URL in the browser
  - After all the fancy DNS stuff, request comes to the Github load balancer
  - Load balancer forwards the requests to one of front end server ( typically 8 Core CPU, 16 GB RAM Bare Metal Server)
  - Nginx (reverse proxy server) at frontend server ships the request to Unix Domain Socket (16 Unicorn worker processes are running on it)
  - One of the workers, grabs it and sends it to backend (Running on Ruby on Rails) Backend has connection with MySQL and cache
  - If cache miss, Github uses the Grit library to retrieve the data.
  - Grit makes RPC call (Remote procedure call) to Smoke Service (It has direct access to filesystem & mapped to frontend machines)
  - Frontend machines run 4 proxy machine instance
  - Proxy extracts the username of repo from request
  - Then Chimney (A library which gives route to Smoke service) talks to Redis for route and gives back to Smoke
  - Smoke establishes a transparent proxy with proper file server
  - The response is sent back through smoke proxy to Ruby on rails app
  - It sends back response to client via Nginx (not through load balancer)

> Slave file servers keeps memcache server.

- Grit gives you object oriented read/write access to Git repositories via Ruby.
- Grit is no longer maintained. Check out libgit2/rugged.
  - Rugged is a library for accessing libgit2 in Ruby.
- libgit2 is a pure C implementation of the Git core methods. 
  - It's designed to be fast and portable.

- Github uses Rackspace instead of Amazon EC2 as Amazon Elastic Block Store was not nearly as fast as bare metal when they ran benchmarks for handling high disk IO operations.

- Old Github File Storage
  - Initially Github used GFS (Global File System) but as they grew, scalability took a hit. 
  - After connecting more servers to the file system, performance degraded rapidly.
  - For MySQL database replication they were using DRBD (Database Replicated Block Device) which is a distributed, flexible and versatile replicated storage solution for Linux.

- ✨ New Github Storage
  - In the new architecture, Github removed the shared file system completely and started using federated storage (a collection of autonomous storage resources which are being monitored by a common management system that provides rules, how data is stored, managed and migrated throughout the storage network).
  - In the new system, they could add as many additional machines (Linux machines running ext3/ext4) they wanted, without hitting the performance.

- Spokes
  - Github has developed a very nice system called “Spokes” (previously known as D-Git) to store multiple distributed copies of a github repo across data centres.
  - Spokes stores multiple replicas of a repo and keeps all replicas in sync. It does replication at Git application level, replacing the older system that did replication at the file system block level.
  - GitHub makes use of the three-phase commit protocol in order to update replicas, and also a distributed lock to ensure the correct update order

- How data is stored in file storage?
  - **All data in a Git repo is stored in a Direct Acyclic Graph**. 
  - Every commit has a link with it’s parent commit. 
  - It also has a link to a tree which keeps a snapshot of the working directory in the moment when the commit was created. 
  - This tree links to the sub-tree (folders & files) and sub-trees recursively links to other sub-trees.
  - Every object in this highly dense tree, is indexed in the database by SHA-1 hash of their content.
- Spokes system uses Git’s property and stores 3 copies of each Github repo on 3 different servers. 

- ## [Projects that power GitHub](https://github.com/collections/projects-that-power-github)
  - libgit2
  - mysql-server, elasticsearch, redis
  - jekyll
  - ruby
  - leaflet, primer-css, d3
  - puppet

- For git hosting, **it doesn't make sense to use a network filesystem**. 
  - Git backend doesn't require shared network access or a large global name space. 
  - Each repository is tiny compared to any individual disk. 
  - Simply using individual disks (JBOD+RAID1 or Amazon EBS or smaller SAN LUNs or virtualized disk images) with XFS or Ext4 like disk file systems will allow you to scale to very large number of repositories. 
  - Eliminating RAID controllers will allow you to eliminate disk contentions (due to random seeks). 
  - Any failure will be contained and not bring down the whole site. 
- We originally used GFS, but as we connected more servers to the file system, the performance degraded rapidly.
  - Instead of continuing to use a shared file system, we re-architected the site to use federated storage that allows us to add boxes without incurring any performance penalties. 
  - The boxes themselves are just standard linux machines running ext3.

- ## [How We Made GitHub Fast_200910](https://github.blog/2009-10-20-how-we-made-github-fast/)
  - We use Redis as a persistent key/value store for the routing information and a variety of other data.
  - Once the Smoke proxy has determined the user’s route, it establishes a transparent proxy to the proper file server. 
  - We have four pairs of fileservers. Their names are fs1a, fs1b, …, fs4a, fs4b. 
  - These are 8 core, 16GB RAM bare metal servers, each with six 300GB 15K RPM SAS drives arranged in RAID 10. 
  - At any given time one server in each pair is active and the other is waiting to take over should there be a fatal failure in the master. 
  - All repository data is constantly replicated from the master to the slave via DRBD.
  - Every file server runs two Ernie RPC servers behind HAProxy. 
  - Each Ernie spawns 15 Ruby workers. 
  - These workers take the RPC call and reconstitute and perform the Grit call. 
  - The response is sent back through the Smoke proxy to the Rails app where the Grit stub returns the expected Grit response.
  - When Unicorn is finished with the Rails action, the response is sent back through Nginx and directly to the client (outgoing responses do not go back through the load balancer).
  - The above flow is what happens when there are no cache hits
