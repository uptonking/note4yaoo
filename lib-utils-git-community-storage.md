---
title: lib-utils-git-community-storage
tags: [community, git, storage, vfs]
created: 2025-01-01T16:02:49.007Z
modified: 2025-01-01T16:03:02.565Z
---

# lib-utils-git-community-storage

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-git-s3
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Crab builds on Hugging Face’s open-source Xet libraries to bring chunk-level deduplication to Git, with large files stored in your own S3, GCS or Azure bucket.
- https://x.com/haipingfu/status/2095682433924595878
  - Unfortunately technology alone isn’t worth billions. Ecosystems are. Hugging Face has built one of the strongest ecosystems in AI and it’s already worth more than GitHub ($7.5 billion) was when Microsoft acquired it.
- Content-defined chunking is the part that pays off daily: change a byte in a 2 GB checkpoint and only the touched chunks upload.

- ## 🚀 Today I’m open-sourcing Crab: serverless Git for large files at any scale, released under Apache 2.0.
- https://x.com/haipingfu/status/2094863027682386215
  - Git remains one of the best interfaces for collaborative work: add, commit, branch, merge, push, clone. The problem isn’t the workflow—it’s the weight behind it.
  - Modern repositories often mix source code with model checkpoints, datasets, videos, game assets, scientific outputs, and build artifacts. Store everything as ordinary Git blobs and repositories become slow and expensive. Move large files elsewhere and you lose Git’s biggest advantage: one exact, branchable history.
  - Crab keeps that history intact. Git stores compact pointers, while Crab splits large files into content-defined chunks, deduplicates and packs them, and writes them directly to the same object-storage bucket as the repository. Your bucket is the single storage layer. There is no Crab data server or separate database, an object store bucket is all you need.
  - You can clone lazily, hydrate only what a person or job needs, dehydrate clean files to reclaim space, and keep using normal Git commands.
  - Crab is written in Rust. The open-source repository includes the complete CLI, Git remote helper, storage crates, architecture notes, documentation, and tests.
- crab + bucket is a great fit for code agent. Crab uses git packfile for incremental push, and it also provides operational commands like ‘crab repack’ to optimize packfile storage and clone/fetch latency. I’d hope crab would be the truly distributed way for agentic development.

- Content-defined chunking pays off hardest on model checkpoints, where a fine-tune touches a slice of the tensors and the rest dedupes away.
  - Yes it’s like versioned objects, and crab is a good fit in this area thanks to `xet` protocol by huggingface.

- Git LFS had the same pitch and bolted a metered server in front of the bucket. GitHub's bandwidth quota was the product. Pointers straight into your own storage is the version that should have shipped in 2015.
  - Exactly. That’s basically the idea behind Crab: Git pointers, your own object storage, no LFS server or bandwidth tax in the middle/tram will pay S3 bandwidth though

- How are you handling authentication?  How about impersonation?
  - Team or developer would use their bucket credentials when publish commits to their bucket, I have managed auth coming soon.
- This will need to be in pre-receive hook for validation and you’ll need to compare the git commits signature to the users e-mail for the push.  When I was at GH this was one of the first slow downs we saw

- Crab and Archil feel like different products focused on different layers.

Crab is more of a Git extension: it lets Git use object storage as the remote backend.

Archil, from what I understand, is focused more on the storage layer, though their product scope is obviously much broader than storage alone. If it speaks S3, Crab should be able to store Git repos on Archil too.

- ## Introducing Crab: a serverless Git remote storage solution for teams working with large files. _202606
- https://x.com/haipingfu/status/2068501689267830894
  - Git is still the best collaboration model we have for software: branches, commits, review, rollback, CI, and history.
  - But modern repositories no longer contain only code.
  - They contain model weights, datasets, media assets, simulation outputs, build artifacts, checkpoints, design files, and other large binary payloads that can easily reach gigabytes or terabytes.
  - That creates a painful tradeoff. Plain Git bloats history. Git LFS adds another server, endpoint, quota model, and operational surface. Manual object-storage buckets keep bytes somewhere durable, but they separate the data from Git history and make collaboration harder to reason about.
  - Crab is built around a simpler idea: Keep Git as the interface. Use your cloud object storage as the backend. Remove the server layer in between.
  - The repository stays lightweight because Git carries metadata and tiny pointer files, while the real payloads live durably in your bucket.
  - Under the hood, Crab uses Git remote-helper and filter-process concepts to make large-file handling feel native. The developer works in Git, while Crab manages chunking, deduplication, upload, checkout, hydration, and storage layout.
  - The technical model is designed for large binary data.
  - Large files are split into content-defined chunks, so small edits do not necessarily rewrite the entire file. Crab can identify which chunks are already known and which chunks are new. Known chunks skip upload. New chunks upload once. Chunks are packed into xorbs to reduce duplicate storage, bandwidth, and object request volume.
  - Clone and checkout are also designed for large repos. Instead of forcing every user or CI job to materialize terabytes immediately, Crab can clone metadata first. Teams can inspect branches, review code, and start work quickly with lightweight pointer checkout, then hydrate real bytes only when needed.
  - Crab does not require a central LFS server or a new database service. Storage stays in your cloud account. Your buckets, IAM, lifecycle rules, encryption posture, and identity model remain the control plane.
  - The goal is not to replace Git. The goal is to let Git keep doing what it is excellent at: collaboration, review, history, and coordination.
  - Crab turns object storage into an enterprise Git remote for large files. Git-native large files. Your cloud. No server layer.

- Is everything persisted in object storage? Do you employ some kind of a local caching layer to improve read/write latency?
  - Yes, all stored in a bucket, including the metadata and chunks, shards etc. we used different layers of caching mechanism to improve reading/writing latency, repo level cache, localhost cache, dedicate cache server and lastly the object store.

- https://x.com/haipingfu/status/2095223602757214362
  - Crab isn’t just for large files. It works well for normal code/text repos too.
  - It stores Git packfiles directly in your bucket and supports incremental push/fetch/pull.
  - For coding agents, that’s a pretty good model: your local repo ↔ your object store. No Git hosting server in the middle, no extra service to operate, and no dependency on GitHub request limits.

- is crab only suitable for large files?
  - Small files should be working, large file pointers are small files and indexed by git ODB. I used k8s repo and replayed 1000 commits to object store, didn’t get any issues, I can show you how to setup the credentials if you need.

- https://x.com/haipingfu/status/2094948857205727360
  - When Crab compares with Git LFS, DVC and Huggingface Hub/Bucket:
  - Crab uses your own object-store bucket as the Git remote, with Xet-style chunking and dedup built in.
  - No LFS server. No storage platform. Just Git and a bucket.
# discuss-git-fs/web
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Show HN: Hubfs – File System for GitHub | Hacker News _202203](https://news.ycombinator.com/item?id=30653916)
  - HUBFS is a file system for GitHub and Git. Git repositories and their contents are represented as regular directories and files and are accessible by any application, without the application having any knowledge that it is really accessing a remote Git repository. 
  - The repositories are writable and allow editing files and running build operations.

- If you build your software to operate on a POSIX-y file system, you can support anything that shows up as a file system. For example: A local working tree of files, an NFS share, or now a remote git repository.

- I've often thought of using git/github as a document store to replace google drive. I might experiment with this and rsync to see if that makes it possible.

- Any plans to add support for gists to Hubfs?
  - Gists are just repos under the hood, it should work natively.

- I don't think the filtering they mention for security actually works? Anybody who clones a repo on GitHub can make their own commits appear under the original org url when accessed by ref.
# discuss-git-db
- ## 

- ## 

- ## 🔥 [Git as a NoSql Database (2016) | Hacker News_202104](https://news.ycombinator.com/item?id=26703808)
- In almost every database-backed application I've ever built someone, at some point, inevitable asks for the ability to see what changes were made when and by whom. My current preferred strategy for dealing with this (at least for any table smaller than a few GBs) is to dump the entire table contents to a git repository on a schedule.

- I store all my dates in sql as text in iso format so I can easily sort them
  - Strong SQLite vibes... (SQLite doesn't have a date format, it has builtin functions that accept ISO format text or unix timestamps)
- Why is this bad?
  - Sql databases usually come with their own date types that are implemented with integers behind the curtains. They take up less space and are easier to sort than text fields.

- Why not have a history table and use SQL triggers to insert the new data as JSON everytime someone changes something?
  - Indeed. I have on multiple occasions written scripts to automatically generate the triggers and audit tables

- Git annex is pretty flexible, more of a framework for storing large files in git than a basic sync utility. ("Large" meaning larger than you'd want to directly commit to git.) If you're running Git Annex Assistant, it does pretty much work as basic file sync of a directory. But you can also use it with normal git commits, like you would Git LFS. Or as a file repository as chubot suggested. The flexibility makes it a little difficult to get started.

- Isn't the problem attempting to be solved here solved by event sourcing? Which lets you 're-create' your changes and is - ultimately- suppose to allow you effectively log each change in such a way its re-playable backwards and forwards
  - Kind of, but there’s more to it. “Event sourcing” is the pattern being implemented by git’s immutable object database, but there’s also all the hashing and reference management.

- 
- 
- 
- 
- 
- 

- ## 🌵🔥 [GitDB, a distributed embeddable database on top of Git | Hacker News_202207](https://news.ycombinator.com/item?id=31987240)
- version control in general turns out to be highly applicable in many areas far beyond source code. I think it's still under-utilized.
  - Yes, it's extremely common to see applications which need a datastore to end up needing lots of version control type features later on, which end up implemented ad-hoc over a general database.
- Git is an abstraction over file trees (or even more generally just chunks of data), and it turns out a ton of problems in software are easily modeled and dealt with as files in a tree.
  - Lots of problems in software are easily modeled as ordered lists, but that doesn't mean linked lists are the right tool for accomplishing that.

- GitDB doesn't handle merge conflicts, so I'm not convinced it would handle multiple clients well. The It's again marked as something they might do in the future someday. I suspect this is pretty fragile. (Note: I was _not_ claiming litestream would do such a thing. Just replication.)

- You can already store and sync issues in git repo metadata, check out git-bug: https://github.com/MichaelMure/git-bug

- How does merging work? Would it even be acceptable to allow automatic merging in all types of application?
  - To be honest, I would be completely fine with a use case that offloads conflict prevention to the application.

- ## [How to implement git-like "branching" on a MongoDB database in Node.js - Stack Overflow](https://stackoverflow.com/questions/64635567/how-to-implement-git-like-branching-on-a-mongodb-database-in-node-js)
- I think you are diving into the world of temporal data so it would probably help a lot to start drawing timelines.

- ## [Does git use databases? - Quora](https://www.quora.com/Does-git-use-databases)
- Git stores everything inside objects found inside .git directory.
- All the references (40 characters hash) pointing to those references are stored inside refs directory.
- git treats files and directories in 3 stages: your normal files/directories, staging area, committed area(repo). 

- ## [Is there a better database than Git (with serializable, immutable, versioned trees)? - Stack Overflow](https://stackoverflow.com/questions/7152276/is-there-a-better-database-than-git-with-serializable-immutable-versioned-tre)
- Datomic provides a persistent data storage and a built-in time notion.

- Although the index/working copy parts of git can be separated out easily enough, git is not designed for merges or commits at the rate of thousands per second on a single machine. The core code is not even threadsafe, for the most part. You will likely need to create some new system for your data (you can still use git for the code, of course, and can also look into generating git commits to represent your data when necessary, etc).
- So libgit2 isn't thread-safe? It would seem that Git would be inherently thread-safe considering it's data structure
  - Nope! It has cache structures, etc, that are not thread-safe. The core git code was only designed to run in a single-threaded manner as command line tools, after all.

- [Git: the NoSQL Database - Speaker Deck](https://speakerdeck.com/bkeepers/git-the-nosql-database)
# discuss
- ## 

- ## 

- ## 

- ## [Gitfs: Version Controlled File System | Hacker News _202108](https://news.ycombinator.com/item?id=28263356)
- To be clear on what this is, it allows you to mount a git repo and use writes to the filesystem to autocommit and push to the remote, effectively using git and a server to synchronize directories between remote hosts.
  - That is not the same thing I would think of as a version-controlled filesystem. That would be something more like the ClearCase MultiVersion Filesystem, which allows you to define versioned views of an entire filesystem. 

- I expected it to be closer to Microsoft's GVFS
  - There, they used a filesystem interface to speed up checkouts for large repositories.
- VFS for Git was superceded by https://github.com/microsoft/scalar and then many of the features were merged into mainline git, so what is left now is a thin shell around git features in the form of MS's forked git binary
- VFS for Git solves the issue of having gigantic bloated monorepos used by thousands of devs, making sure user efficiently downloads only what is needed for him.

- NixOS can also move between system generations seamlessly. The approach is entirely different though, the system is fully defined by its config files and will be recreated from scratch each time it is changed (except /home and /var, mostly).

- It's different from git-annex in that it's using git itself (git-annex just uses git to track metadata/hash to facilitate large files), but there's a similarity to git-annex's 'Git-annex Assistant' in how it "any subsequent changes made to the files will be automatically committed to the remote".

- ## [Microsoft and GitHub team up to take Git virtual file system to macOS, Linux | Hacker News _201711](https://news.ycombinator.com/item?id=15723926)
- git blame is not the issue that we're most concerned about. The basic, highest priority functionality in Git - things like git add - are the the issues we're most concerned about.
  - git add is O(n) on the number of files in the repository. When you run `add` , git reads the index, modifies the entry (or entries) that you're changing, and writes the index back out.
  - The Windows repository has about 3.5 million files. Running `git add` - when we started thinking about moving Windows into Git - took minutes.
  - Git does have some functionality to support very large repositories - using shallow clones, sparse checkouts and the like. We've added narrow clones, to only download portions of the tree, and automation to handle this automatically without user intervention.
  - That's the scaling work that we're doing with GVFS. And these changes bring the P80 time for git add down to 2.5 seconds. We've been contributing these changes back to git itself

- Did I misunderstood the idea, or is GVFS essentially making git a non-distributed VCS?
  - I think once you're checked out, you're still distributed as far as being able to make and push commits which modify the files you have. But obviously someone can't clone files from you which you don't yourself have.

- ## [More on GVFS | Hacker News _201702](https://news.ycombinator.com/item?id=13594721)
- It sounds like GVFS solves the problems of big repos by only fetching and diffing files you actually need. It might handle a 300GB repo, but its does this by only working with the 1GB of the repo you actually use, and "virtualizing" the rest. If you pulled down the full 300GB repo then it would suffer from the same issues as a vanilla git repo.
  - GFVS isn't really a file system like NTFS or ext3. It's a way to work with a subset of a git repo in a flexible manner (not submodules).
- Exactly. GVFS is not a filesystem based on Git.

- I wonder how hard it would be to port the same client code to also run under FUSE on Linux/Mac. For this to take off outside of Microsoft, it needs universal client support.
  - Someone at Google created an unofficial project that does something similar to GVFS. It's a bit more limited as it was focused around Android's use case, but it seems like it could be a good base?
  - https://github.com/google/slothfs

- ## [Git Virtual File System from Microsoft : r/programming _201702](https://www.reddit.com/r/programming/comments/5rtlk0/git_virtual_file_system_from_microsoft/)
- disclaimer: MS employee, not on GVFS though
  - Git LFS addresses one (and the most common) reason for extremely large repos. But there exists a class of repositories that are large not because people have checked large binaries into them, but because they have 20+ years of history of multi-million LoC projects (e.g. Windows). For these guys, LFS doesn't help. GitFS does.
- a different question maybe, if you are migrating to Git, why keep all of the history? Is the ability to view history from 1997 still relevant for every day work?

- We did try Git LFS. Actually, TFS / Team Services was one of the first Git servers to support LFS and we announced support - with GitHub - at the Git Merge conference last year. The issue with LFS is it doesn't solve all the scale problems we need to solve for Windows.
- 📌 There are 3 main scale problems with moving Windows to Git:
  - Large files / content - LFS addresses this.
  - Lots of files - LFS does not solve this. 1, 000, 000 small files in Git produces extremely slow status scans (10min to run git status). Breaking up a legacy code base can take years of engineering effort, so reducing to a smaller file count is not possible or practical.
  - Lots of branches - LFS doesn't solve this, but GVFS doesn't either so we came up with a different solution. 
- That said, listing all 3 scale issues will give everyone the full context of the problem we're solving. 
  - Thousands of engineers work on Windows and each of them will have 10+ branches. We're estimating 100k branches for the repo. 
  - To quickly perform the haves / wants negotiation that happens with a fetch / push, we needed a solution. We call it "limited refs" and I'll give more details if people are interested.
- When moving to a monorepo, Twitter had status scan troubles and solved it by forking the official Git client and using Watchman to avoid rescanning on every invocation. Obviously this is a very different approach than that of GVFS, which alters official client behavior by sitting one layer below it, so how does GVFS go about doing it?
  - As a big user of JGit, Google encountered a similar inefficiency in packfile negotiation and thus created bitmap indexes. This auxiliary data structure still runs on the assumption that the client wants to fully store every object in the repo on disk, which once again is fundamentally different than GVFS's goal. I'm very curious to see how limited refs work!
- We don't want a private fork of git. GVFS is a driver that sits below git and takes advantage of the changes we're making to core git

- Multiple repositories creates all manner of other problems. Note that google has one repo for the entire company.
  - To clarify, while their super repo is a thing, but they also have hundreds of smaller, single-project repos as well.
- There are a lot of reasons to go with a mono-repo, google does the same.

- Wouldn't it have been easier to change git than to write a filesystem filter driver?
  - It's certainly something we considered and to be honest, we're actually doing both. There are two parts to GVFS, the virtualization of the objects directory and the virtualization of the working directory to manage your sparse checkout. We believe the first part belongs in git and we just recently suggested that on the git mailing list. We'll be working to build it into git as long as the maintainers agree with that direction.
  - The second part of the virtualization is less clear. I don't think it belongs in git, at least right now. We needed the filter driver to pull off that piece. Once we had it, it was trivial to slide it under the objects folder as well.
- Our goal with all git/git changes isn't to change Git into something different. We want to enable better performance with large repos, even if those repos don't use GFVS.

- ## 🚀 [Announcing GVFS: Git Virtual File System | Hacker News _201702](https://news.ycombinator.com/item?id=13559662)
  - https://github.com/microsoft/VFSForGit /MIT/202412/csharp/maintenance
  - [Announcing GVFS (Git Virtual File System) - Azure DevOps Blog _201702](https://devblogs.microsoft.com/devops/announcing-gvfs-git-virtual-file-system/)
  - VFS for Git virtualizes the file system beneath your Git repository so that Git and all tools see what appears to be a regular working directory, but VFS for Git only downloads objects as they are needed. 
  - > Notice: With the release of VFS for Git 2.32, VFS for Git is in maintenance mode. 
  - > Note: for new deployments, we strongly recommend you consider Scalar instead of VFS for Git. 
- A lot of questions like why not use multiple repos, why not git-lfs, why not git subtree, etc. are answered

- > One of the core differences between Windows and Linux is process creation. It's slower - relatively - on Windows. Since Git is largely implemented as many Bash scripts that run as separate processes, the performance is slower on Windows. We’re working with the git community to move more of these scripts to native cross-platform components written in C, like we did with interactive rebase. This will make Git faster for all systems, including a big boost to performance on Windows.

- For the problem of large files I think Git LFS has largely won out over git annex, mostly because it's natively supported by GitHub and GitLab and requires no workflow changes to use.
  - Atlassian's Bitbucket and Microsoft's Visual Studio Team Services both also support Git LFS.

- Pros of git-annex:
  - it is conceptually very simple: use symlinks instead of ad-hoc pointer files, virtual files system, etc. to represent symbolic pointer that point to the actual blob file; 
  - you can add support for any backend storage you want. As long as it support basic CRUD operations, git-annex can have it as a remote; 
  - you can quickly clone a huge repo by just cloning the metadata of the repo (--no-content in git-annex) and just download the necessary files on-demand; 
  - And many other things that no other attempt even consider having, like client-side encryption, location tracking, etc.
- Git Annex is only a partial solution, since it only solves issues with binary blobs. It doesn't solve problems with large repos.

- That still only solves half the problem with large binary blobs. The other half is that almost all of the binary formats can't be merged and so you need a mechanism to lock them to prevent people from wiping out other people's changes. Unfortunately that runs pretty much counter the idea of DCVS.

- When git-annex finds a conflict it can't solve, it gives back to you the two versions of the same file with the SHA of the original versions suffixed. This way you can look at both and resolve the conflict.

- 
- 
- 
