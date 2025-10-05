---
title: lib-utils-git-blog
tags: [blog, git]
created: 2023-08-29T10:24:00.429Z
modified: 2023-08-29T10:24:09.136Z
---

# lib-utils-git-blog

# guide

# blogs-vendor-github 🌰
- [MySQL High Availability at GitHub - The GitHub Blog _201806](https://github.blog/engineering/infrastructure/mysql-high-availability-at-github/?utm_source=chatgpt.com)
  - GitHub uses MySQL as its main datastore for all things non-git

- [Git at GitHub Scale - Git Merge 2022 - YouTube _202210](https://www.youtube.com/watch?v=QK6EkWqjN2s)

- [How We Made GitHub Fast - The GitHub Blog _200910](https://github.blog/news-insights/how-we-made-github-fast/?utm_source=chatgpt.com)

## ⚡️ [How GitHub Reduced Repo Storage Size by Over 90% _202411](https://newsletter.betterstack.com/p/how-github-reduced-repo-storage-size)

- GitHub supports over 200 programming languages and has over 330 million repositories. But it has a pretty big problem.
  - It stores almost 19 petabytes of data
  - And much of that data is unreachable; it's just taking up space unnecessarily.

- A developer typically installs Git on their local machine. Then, they push their code to GitHub, which has a custom implementation of Git on its servers.
- how does it track changes? 
  - Well, every piece of data Git tracks is stored as an object.
- A Git object is something Git uses to keep track of a repository's content over time.
- There are three main types of objects in Git.
  - BLOB -  Binary large object. This is what stores the contents of a file, not the filename, location, or any other metadata.
  - Tree - How Git represents directories. A tree lists blobs and other trees that exist in a directory.
  - Commit - A snapshot of the files (blobs) and directories (trees) at a point in time. It also contains a parent commit, a hash of the previous commit.
- Commit names are difficult for humans to remember, so this is where branches come in.
  - A branch is just a named reference to a commit, like a label. 
  - The default branch is called main or master, and it points to the most recent commit.

- Based on how Git keeps track of a project, it is possible to do things that will make objects unreachable.
  - Deleting a branch: Deleting doesn't immediately remove it but removes the reference to it. So the objects in the deleted branch still exist.
  - Force pushing. This replaces a remote branch's commit history with a local branch's history. This means the old commits lose their reference.
  - Removing sensitive data. Sensitive data usually exists in many commits. Removing the data from all those commits creates lots of new hashes. This makes those original commits unreachable.
  - There are many other ways to make unreachable objects, but these are the most common.

- Usually, unreachable objects aren't a big deal. They typically get removed with Git's garbage collection.
- It can be triggered manually using the git gc command. But it also happens automatically during operations like git commit, git rebase, and git merge.
- Git only removes an object if it's old enough to be considered safe for deletion. This is typically 2 weeks. In case a developer accidentally deletes objects and they need to be retrieved.
  - Objects that are too recent to be removed are kept in Git's objects folder. These are known as loose objects.
  - Garbage collection also compresses loose, reachable objects into packfiles. These have a .pack extension.
  - Like most files, packfiles have a single modification time (mtime). This means the mtime of individual objects in a packfile would not be known until it’s uncompressed.
  - Unreachable loose objects are not added to packfiles. They are left loose to expose their modification time.
- But garbage collection isn't great with large projects. This is because large projects can create a lot of loose, unreachable objects, which take up a lot of storage space.

- To solve this, the team at GitHub introduced something called Cruft Packs.

- Cruft packs, as you might have guessed, are a way to compress loose, unreachable objects.
  - The name "cruft" comes from software development. It refers to outdated and unnecessary data that accumulates over time.
- What makes cruft packs different from packfiles is how they handle modification times.
- Instead of having a single modification time, cruft packs have a separate `.mtimes` file.
  - This file contains the last modification time of all the objects in the pack. This means Git will be able to remove just the objects over 2 weeks old.
  - As well as the .pack file and the .mtimes file, a cruft pack also contains an index file with an `.idx` extension. This includes the ID of the object as well as its exact location in the packfile, known as the offset.
  - Each object, index, and mtime entry matches the order in which the object was added. So the third object in the pack file will match the third entry in the idx file and the third entry in the mtimes file.
  - The offset helps Git quickly locate an object without needing to count all the other objects.

- Cruft packs were introduced in Git version 2.37.0 and can be generated by adding the --cruft flag to git gc, so git gc --cruft.
  - By applying a cruft pack to the main GitHub repo, they were able to reduce its size from 57GB to 27GB, a reduction of 52%. And in an extreme example, they were able to reduce a 186GB repo to 2GB. That's a 92% reduction!

## [Scaling Git’s garbage collection - The GitHub Blog _202209](https://github.blog/engineering/architecture-optimization/scaling-gits-garbage-collection/?utm_source=chatgpt.com)

- At GitHub, we store a lot of Git data: more than 18.6 petabytes of it, to be precise.
- The process for permanently removing unreachable objects from a repository’s history has a history of causing problems within GitHub, especially in busy repositories or ones with lots of objects. In this post, we’ll talk about what those problems were, why we had them

- 
- 

## 📋📃 [How does Github store millions of repo and billions of files? _202104](https://www.pankajtanwar.in/blog/how-does-github-store-millions-of-repo-and-billions-of-files)

- Github is one of the world’s largest code hosting platforms for collaboration and version control
  - Repository - 200M Repo (Including 30M Public Repo)
  - Active Users - 50M

- Whenever you type a Github repo URL in the browser, a lot of things happen behind the scene to show you a beautiful repo page.
  - Suppose, you type https://github.com/github/docs in the browser.
  - After all the fancy DNS stuff, request comes to the Github load balancer
  - Load balancer forwards the requests to one of front end server ( typically 8 Core CPU, 16 GB RAM Bare Metal Server)
  - Nginx (reverse proxy server) at frontend server ships the request to Unix Domain Socket (16 Unicorn worker processes are running on it)
  - One of the workers, grabs it and sends it to backend (Running on Ruby on Rails). Backend has connection with MySQL and cache
  - If cache miss, Github uses the Grit library to retrieve the data.
  - Grit makes RPC call (Remote procedure call) to Smoke Service (It has direct access to filesystem & mapped to frontend machines)
  - Frontend machines run 4 proxy machine instance, Proxy extracts the username of repo from request
  - Then Chimney (A library which gives route to Smoke service) talks to Redis for route and gives back to Smoke
  - Smoke establishes a transparent proxy with proper file server
  - The response is sent back through smoke proxy to Ruby on rails app
  - It sends back response to client via Nginx (not through load balancer)
  - Slave file servers keeps memcache server.

- Old Github File Storage
  - Initially Github used GFS (Global File System) but as they grew, scalability took a hit. After connecting more servers to the file system, performance degraded rapidly.
  - For MySQL database replication they were using DRBD (Database Replicated Block Device) which is a distributed, flexible and versatile replicated storage solution for Linux.

- New Github Storage
  - In the new architecture, Github removed the shared file system completely and started using federated storage (a collection of autonomous storage resources which are being monitored by a common management system that provides rules, how data is stored, managed and migrated throughout the storage network).
  - In the new system, they could add as many additional machines (Linux machines running ext3/ext4) they wanted, without hitting the performance.

- Github has developed a very nice system called “Spokes” (previously known as D-Git) to store multiple distributed copies of a github repo across data centres.
  - Spokes stores multiple replicas of a repo and keeps all replicas in sync. 
  - It does replication at Git application level, replacing the older system that did replication at the file system block level.
  - GitHub makes use of the three-phase commit protocol in order to update replicas, and also a distributed lock to ensure the correct update order

- How data is stored in file storage?
- All data in a Git repo is stored in a Direct Acyclic Graph. 
  - Every commit has a link with it’s parent commit. It also has a link to a tree which keeps a snapshot of the working directory in the moment when the commit was created. 
  - This tree links to the sub-tree (folders & files) and sub-trees recursively links to other sub-trees.
  - Every object in this highly dense tree, is indexed in the database by SHA-1 hash of their content.
- Spokes system uses Git’s property and stores 3 copies of each Github repo on 3 different servers. In the worst case, even if two servers are down, one server would still be available for read, clone and pull.
- For each push to a Git repo, it goes through a proxy which is responsible for replicating the change.

### 👥 [How does Github store millions of repo and billions of files? : r/programming _202104](https://www.reddit.com/r/programming/comments/muqfmu/how_does_github_store_millions_of_repo_and/)

- Earlier GitHub used SAS drives and later shifted to SSD drives for file system but scaling the file storage for Millions of users was the biggest concern. 
  - GitHub developed a wrapper around file storage for efficient raplication and reduced latency.

### [Where does GitHub store my code and files? - Stack Overflow](https://stackoverflow.com/questions/39408791/where-does-github-store-my-code-and-files)

- Github uses Git which can be seen as an object data storage. 
  - In this storage, files and directories are stored as git trees and blobs. You may want to read about git internal to understand its architecture.

- [git with billion json files : r/git _202403](https://www.reddit.com/r/git/comments/1baognp/git_with_billion_json_files/)
  - To the best of my recollection, the standard tree algorithm in git needs to list all objects in the tree. Scale that up to 1 billion, and operations like checkout might get slow. Really slow.
  - u/mvyonline metioned scalar. This would require Git VFS support at the repo level, but I don't know if GitHub or GitLab have implemented this yet.

## [Stretching Spokes - The GitHub Blog _201710](https://github.blog/engineering/infrastructure/stretching-spokes/)

- GitHub’s Spokes system stores multiple distributed copies of Git repositories. 
- This article discusses how we got Spokes replication to span widely separated datacenters.

- 
- 
- 

## [Building resilience in Spokes - The GitHub Blog _201609](https://github.blog/engineering/building-resilience-in-spokes/)

- Spokes is the replication system for the file servers where we store over 38 million Git repositories and over 36 million gists. 
  - It keeps at least three copies of every repository and every gist so that we can provide durable, highly available access to content even when servers and networks fail. 
  - Spokes uses a combination of Git and rsync to replicate, repair, and rebalance repositories.

- 
- 
- 
- 
- 
- 
- 

## [Introducing DGit - The GitHub Blog _201604](https://github.blog/engineering/architecture-optimization/introducing-dgit/)

> DGit is now called Spokes

- GitHub hosts over 35 million repositories and over 30 million Gists on hundreds of servers. 
  - Over the past year, we’ve built DGit, a new distributed storage system that dramatically improves the availability, reliability, and performance of serving and storing Git content.
- DGit is short for “Distributed Git
- DGit performs replication at the application layer, rather than at the disk layer. Think of the replicas as three loosely-coupled Git repositories kept in sync via Git protocols, rather than identical disk images full of repositories. This design gives us great flexibility to decide where to store the replicas of a repository and which replica to use for read operations.
- If a file server needs to be taken offline, DGit automatically determines which repositories are left with fewer than three replicas and creates new replicas of those repositories on other file servers. This “healing” process uses all remaining servers as both sources and destinations. Since healing throughput is N-by-N, it is quite fast. And all this happens without any downtime.

- 🏠 DGit uses plain Git
  - Most end users store their Git repositories as objects, pack files, and references in a single .git directory. They access the repository using the Git command-line client or using graphical clients like GitHub Desktop or the built-in support for Git in IDEs like Visual Studio. 
  - Perhaps it’s surprising that GitHub’s repository-storage tier, DGit, is built using the same technologies. 
  - Why not a SAN? A distributed file system? Some other magical cloud technology that abstracts away the problem of storing bits durably?
  - The answer is simple: it’s fast and it’s robust.
- Git is very sensitive to latency. A simple git log or git blame might require thousands of Git objects to be loaded and traversed sequentially. If there’s any latency in these low-level disk accesses, performance suffers dramatically. Thus, storing the repository in a distributed file system is not viable. Git is optimized to be fast when accessing fast disks, so the DGit file servers store repositories on fast, local SSDs.

- 
- 
- 
- 

## [Git's database internals I: packed object store - The GitHub Blog _202208](https://github.blog/open-source/git/gits-database-internals-i-packed-object-store/?utm_source=chatgpt.com)

- In this five-part blog post series, we will illuminate Git’s internals to help you collaborate via Git, especially at scale.
- The core idea I want to convey is this: Git is the distributed database at the core of your engineering system.

- 
- 
- 

# blogs-vendors

## [xet - Show HN: We scaled Git to support 1 TB repos | Hacker News _202212](https://news.ycombinator.com/item?id=33969908)

- I’ve been in the MLOps space for ~10 years, and data is still the hardest unsolved open problem. 
  - Code is versioned using Git, data is stored somewhere else, and context often lives in a 3rd location like Slack or GDocs. 
  - This is why we built XetHub, a platform that enables teams to treat data like code, using Git.
- Unlike Git LFS, we don’t just store the files. We use content-defined chunking and Merkle Trees to dedupe against everything in history. This allows small changes in large files to be stored compactly
- Today, XetHub works for 1 TB repositories, and we plan to scale to 100 TB in the next year. 
  - Our implementation is in Rust (client & cache + storage) and our web application is written in Go. 
  - XetHub includes a GitHub-like web interface that provides automatic CSV summaries and allows custom visualizations using Vega. 
  - Even at 1 TB, we know downloading an entire repository is painful, so we built git-xet mount - which, in seconds, provides a user-mode filesystem view over the repo.

- The tl; dr is that "xet" is like GitLFS (it stores pointers in Git, with the data in a remote server and uses smudge filters to make this transparent) with some additional features:
  - Automatically includes all files >256KB in size
  - By default data is de-duplicated 16KB chunks instead of whole files (with the ability to customize this per file type).
  - Has a "mount" command to allow read-only browse without downloading

- git-xet follows the patterns established by other git extensions like git-annex and git-lfs, but with some UX improvements. 
  - In all of these cases, the large/binary file contents are actually stored outside of git, but available with git commands. 
  - The goal here is to make working with and versioning code and data together seamless, not to blindly use the git internals to store data. 

- How's this differ from using git LFS?
  - We are significantly faster?  Also, block-level dedupe, scalability, perf, visualization, mounting, etc.

- Versioning data is great, but storing as diffs is inefficient when 99% of the file changes each version.
  - We don't store as diffs, we store as snapshots -- and it's efficient thanks to the way we do dedupe

- There are a couple of other contenders in this space. DVC (https://dvc.org/) seems most similar.
- If you're interested in something you can self-host... I work on Pachyderm (https://github.com/pachyderm/pachyderm), which doesn't have a Git-like interface, but also implements data versioning. Our approach de-duplicates between files (even very small files), and our storage algorithm doesn't create objects proportional to O(n) directory nesting depth as Xet appears to. (Xet is very much like Git in that respect.)
  - Xet's system for mounting a remote repo as a filesystem is a good idea. We do that too

- I also have a lot of issues with versioning data. But look at git annex - it's free, self hosted and has a very easy underlying data structure 
  - Sounds like `git annex` is file-level deduplication, whereas this tool is block-level, but with some intelligent, context-specific way of defining how to split up the data (i.e. Content-Defined Chunking). For data management/versioning, that's usually a big difference.
- XetHub Co-founder here. Yes, one illustrative example of the difference is: Imagine you have a 500MB file (lastmonth.csv) where every day 1MB is changed. With file-based deduplication every day 500MB will be uploaded, and all clones of the repo will need to download 500MB. With block-based deduplication, only around the 1MB that changed is uploaded and downloaded.

- depending on your needs, you can just use a tool like bup or borg directly. Bup actually uses the git pack file format and git metadata.

- If git annex stores large files uncompressed you could use filesystem bl9ck level deduplication in combination with it.
  - There are filesystems that support inline or post-process deduplication. btrfs and zfs come to mind as free ones, but there are also commercial ones like WAFL etc.
  - It's always a tradeoff. Deduplication is a CPU-heavy process, and if it's done inline, it is also memory-heavy, so you're basically trading CPU and memory for storage space. It heavily depends on the use-case (and the particular FS / deduplication implementation) whether it's worth it or not

- Founder of DoltHub here. Dolt hasn't come up here yet, probably because we're focused on OLTP use cases, not MLOps, but we do have some customers using Dolt as the backing store for their training data.
  - Dolt also scales to the 1TB range and offers you full SQL query capabilities on your data and diffs.

- What does a Merkle Tree bring here? (honest question) I mean: for content-based addressing of chunks (and hence deduplication of these chunks), a regular tree works too if I'm not mistaken (I may be wrong but I literally wrote a "deduper" splitting files into chunks and using content-based addressing to dedupe the chunks: but I just used a dumb tree). Is the Merkle true used because it brings something else than deduplication, like chunks integrity verification or something like that?

- git-annex is one of the most powerful tools I have ever used. You can use git for tracking changes in text, but use a different system for tracking binaries.

- Why do you need 1Tb for repos? What do you store inside, besides code and some images?
  - Repositories for games are often larger than 1TB, and with things like UE5's Nanite becoming more viable, they're only going to get bigger.

- 🤔 Does this fix the problem that Git becomes unreasonably slow when you have large binary files in the repo? Also, why can't Git show me an accurate progress-bar while fetching?
  - Mostly! (At the moment, it doesn't fully fix the slowdown associated with storing large binary files, but reduces it by 90-99%. We're working on improving to closer to 100% that by moving even the Merkle Tree storage outside the git repo contents.)
  - As for why git can't show you an accurate progress bar while fetching (specifically when using an extension like git-lfs or git-xet), this has to do with the way git extensions work -- each file gets "cleaned" by the extension through a Unix pipe, and the protocol for that is too simple to reflect progress information back to the user. 
  - In git-xet, we do write a percent-complete to stdout so you get some more info (but a real progress bar would be nice).

- How data is split in chunks ?
  - Content defined chunking. Specifically a variation of FastCDC. We have a paper coming out soon with a lot more technical details.
- They mention 'content-defined chunking', but it as far as understand it requires different chunking algorithms for different content types. Does it support plugins for chunking different file formats?
  - Today we just have a variation of FastCDC in production, but we have alternate experimental chunkers for some file formats (ex: a heuristic chunker for CSV files that will enable almost free subsampling). Hope to have them enter production in the next 6 months.
- That's interesting. Can a CSV chunker make adding a column not affect all of the chunks?
  - The simplest really is to chunk row-wise so adding columns will unfortunately rewrite all the chunks. If you have a parquet file, adding columns will be cheap.

## [XetHub | NFS > FUSE: Why We Built our own NFS Server in Rust _202309](https://xethub.com/blog/nfs-fuse-why-we-built-nfs-server-rust)

- Every program knows how to read files and write files. Its a truly universal API. 
- As such, I love the idea of FUSE. FUSE, or “Filesystem in Userspace” is a set of Linux interfaces that allow user-mode programs to define a filesystem.
  - This allows filesystem drivers to be built very easily without needing a kernel module. 
  - Fuse is the basis for a large number of filesystem clients, including NTFS and even remote “filesystems” like SFTP or Amazon S3
  - It can also be used to make strange filesystems which are not actually filesystems like WikipediaFS which allows one to edit wikipedia articles using their own text editor.

- https://sourceforge.net/projects/wikipediafs/ /GPLv2/201507/python/inactive
  - https://wikipediafs.sourceforge.net/
  - WikipediaFS is a mountable Linux virtual file system that allows to read and edit articles from Wikipedia (or any Mediawiki-based site) as if they were real files.
  - Warning! WikipediaFS is currently unmaintained.

- at XetHub, we wanted to build an easy way to access any version of any dataset from your laptop using the tools you have. 
  - The obvious solution to enabling this superpower was FUSE.

- FUSE however, is an frustrating API to build against:
  - there are 2 API classes to choose from — a low-level API and a high-level API
  - there are 2 incompatible API versions (libfuse2 and libfuse3)
  - and lots of other smaller API changes over time (See FUSE_USE_VERSION).
  - FUSE is unavailable natively on Mac and Windows and requires the user to install a 3rd party driver (MacFuse, WinFuse). Each of these drivers may have subtle API incompatibilities.

- Is it possible to build a userspace filesystem interface that is truly cross-platform?

- NFSv3 is 20 years old and is a network filesystem protocol that was so simple and so ubiquitous that nearly every operating system has a built-in implementation of it.
  - The server is completely stateless: This simplifies the implementation immensely.
  - Simple Cache Consistency Rules: Server does not define cache policy. The client can be as smart as it wants. Instead, the protocol defines a mechanism for the server to notify the client when something changes.
  - NFS Client and protocol has builtin timeout, retry and failure semantics we can immediately take advantage of. 

- XetHub has the world’s first natively cross-platform, user-mode filesystem implementation, allowing you to mount arbitrarily large datasets on your machine without needing any kernel driver.
  - This enables you to, in just a few seconds, locally mount ~660 GB of Llama 2 models or write DuckDB queries to analyze large parquet files and scan just the data you need.
  - All of this is currently supported on Linux, Mac and Windows Pro

- We are open sourcing nfsserve, our Rust implementation for the NFS server https://github.com/xetdata/nfsserve

## [XetHub | XetHub joins Hugging Face to replace Git LFS and accelerate AI collaboration _202408](https://xethub.com/blog/xethub-joins-hugging-face-to-replace-git-lfs-and-improve-collaboration)

- 
- 
- 

- [XetHub | Benchmarking Performance: XetHub vs DVC, Git LFS, and LakeFS _202310](https://xethub.com/blog/benchmarking-xethub-vs-dvc-lfs-lakefs)

- [XetHub | From Files to Chunks: Improving HF Storage Efficiency _202411](https://xethub.com/blog/from-files-to-chunks-improving-hf-storage-efficiency)

- [XetHub | Improving Parquet Dedupe on Hugging Face Hub _202410](https://xethub.com/blog/improving-parquet-dedupe-on-hugging-face-hub)

- [XetHub | Shutting down XetHub: Learnings and Takeaways _202410](https://xethub.com/blog/shutting-down-xethub-learnings-and-takeaways)
# blogs-git-database
- [make a blog post about git like databases](https://github.com/multun/blog/issues/4)

## [Git Internals Part 2: How does Git store your data? _202207](https://www.developernation.net/blog/git-internals-how-does-git-store-your-data/)

- 
- 
- 
- 

## [Using Git as a key-value database](https://secure-git.guide/015_How-to-use-Git-as-a-database/)

- With Git you can store data in two different ways: Git objects, References
- Git internally uses a key-value database with only 4 types of objects: blobs, trees, commits and annotated-tags
- Each object is stored in the database and the way to reference the object is by using its sha1 (a checksum of the content).
- This database is immutable. You can only add new content.

- You can store your data inside blob objects. When you want to update the version of your object you can store a new object
- When you update a blob object you could create a commit.
  - This model uses an orphan branch for each object. An "orphan" branch is a branch that is not connected to any other branch. That means the first commit does not have any ancestors.

- We normally have two options to fix that problem with normal databases, you can either lock the record when you want to modify it (pessimistic locking) or try to modify it always and make the update fail if the record has changed (optimistic locking).
- Git only allows us to use the optimistic approach. When you try to “push” your object version by updating the reference in the origin repo you will get an error if the reference (branch) was already changed.
# blogs-git-usage
- [Git从入门到应付日常工作](https://jumpshare.com/s/P42MV2FmKfnzSLXjaFUk)

- [示意图多 Git Branching and Merging: A Step-By-Step Guide](https://www.varonis.com/blog/git-branching)
# blogs-fossil
- [Fossil Versus Git](https://fossil-scm.org/home/doc/trunk/www/fossil-v-git.wiki)
# blog-git-version-history

## [ipld-version-control _201706](https://gist.github.com/flyingzumwalt/a6821e843366d606aeb1ba53525b8669)

- hypercore-protocol.org is built on version control, if anyone's interested 
# blogs-diff 🆚

## 🧑‍🏫 [Git Diff | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/saving-changes/git-diff)

```diff
# the input sources of the diff
diff --git a/diff_test.txt b/diff_test.txt
# internal Git metadata. correspond to Git object version hash identifiers
index 6b0c6cf..b37e70a 100644
# a legend that assigns symbols to each diff input source
--- a/diff_test.txt
+++ b/diff_test.txt
# a list of diff 'chunks'
# A diff only displays the sections of the file that have changes
# The first line is the chunk header. Each chunk is prepended by a header enclosed within @@ symbols. The content of the header is a summary of changes made to the file.
# -1 +1 meaning line one had changes. 
# @@ -34,6 +34,8 @@ meaning 6 lines have been extracted starting from line number 34. Additionally, 8 lines have been added starting at line number 34.
@@ -1 +1 @@
# The remaining content of the diff chunk displays the recent changes
-this is a git diff test example
+this is a diff example
```

```shell
# When a file path is passed, the diff operation will be scoped to the specified file.
# By default git diff will execute the comparison against HEAD
# 👉 compare the specific changes in the working directory, against the index, showing the changes that are not staged yet
git diff HEAD ./path/to/file
# with the --cached option the diff will compare the staged changes with the local repository
# --cached option is synonymous with --staged.
git diff --cached ./path/to/file

# Comparing files between two different commits
git diff commitId1 commitId2

# Comparing files from two branches
git diff main new_branch ./diff_test.txt

# Branches are compared like all other ref inputs to git diff
# two dots indicate the diff input is the tips of both branches. 
# The same effect happens if the dots are omitted and a space is used between the branches.
git diff branch1..other-feature-branch

# three dot operator initiates the diff by changing the first input parameter branch1. It changes branch1 into a ref of the shared common ancestor commit between the two diff inputs, the shared ancestor of branch1 and other-feature-branch. The last parameter input parameter remains unchanged as the tip of other-feature-branch.
git diff branch1...other-feature-branch

```

- git diff --color-words
  - 可以展示行内diff, 删除的字符是红色，新增的字符为普通黑色而不是绿色

- `git diff` can be run on binary files. Unfortunately, the default output is not very helpful.
  - Git does have a feature that allows you to specify a shell command to transform the content of your binary files into text prior to performing the diff.
# more-blogs
- [Git's database internals I: packed object store - The GitHub Blog](https://github.blog/2022-08-29-gits-database-internals-i-packed-object-store/)

- [Git as a NoSql database](https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/)
