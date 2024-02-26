---
title: lib-utils-storage-filesystem-web-community
tags: [filesystem, indexeddb, storage, web-storage]
created: 2022-11-27T14:19:27.900Z
modified: 2023-09-16T17:43:09.215Z
---

# lib-utils-storage-filesystem-web-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-webdav
- ## 

- ## 

- ## 🆚️ [Wddbfs – Mount a SQLite database as a filesystem | Hacker News _202402](https://news.ycombinator.com/item?id=39417503)
- This seems really nice! If this is posted by the author looking for feedback:
  - 1) WebDAV is a much better choice than FUSE. FUSE is a good concept, but buggy and poorly-implemented. Things like sshfs can break in very bad ways if e.g. there is a network connectivity issue. Not a hack.
  - 2) Writes seem like a very bad idea. Keep those out unless you come up with a clean way to handle them (which seems difficult if not impossible given the differences in FS versus relational abstractions, especially with regards to data validation). Not a limitation.
  - 3) The major use-case I have is if I have a small (<1MB) database, and don't know the structure. Lots of tools use small sqlite databases. There is no way to query all tables for something, whereas tools like find and grep can look through all files. 

- I'm indifferent on the WebDAV vs FUSE thing, actually. But if the author wanted a nicer way to query a bunch of text files, where each line would roughly represent what a db row would, and there's whatever random delimiter character in there, then I think he gave in and went to a database too soon.
  - Besides the ubiquitous GNU textutils, there are tons of tools out there for working with record-oriented CSV and TSV files.

- > WebDAV is a much better choice than FUSE.
  - That's a pretty spicy opinion. WebDAV is slow; FUSE works great. Use interrupt mounts for things like sshfs (or NFS, for that matter).
- I have had problems with particular fuse implementations (sshfs included, s3fs especially), but I've never had trouble writing FUSE implementations that behave correctly. Is there something deficient in the spec that you want to call out, or is the idea just that WebDAV carefully built networking into its core concepts, where you have to do a lot of extra work to squeeze those ideas correctly into a FUSE implementation?
  - I suspect if you've run into problems with a lot of things built on FUSE, the problem is FUSE.
  - Yes, s3fs and sshfs can both leave the system in an unstable state. For example, there can be a dead mount which is impossible to unmount, and in severe cases, blocks a clean reboot.
  - A file system in user space (or in network space) should NEVER break the system, no matter what happens in user space (or in network space). Most network file systems try to respect this (albeit with mixed success). FUSE does not.
  - I'm not claiming FUSE cannot be made to work. Just that it's very bad since (1) plenty of smart people clearly failed to do so (2) the badness it leaves behind should be more than it's permitted to.

- I build a couchDB webdav server back in the day, you could also edit json documents or file blobs directly. 
  - the problem i discovered was that all OSes totally staled their webdav support and there are also enough differences between oses to be annoying. 
  - In the end to build somthing with great performance you would also need to control the webdav client side and probably build a fuse webdav client. 
  - I would have loved to see webdav maturing and becoming what the 9P vision was just for the web, but this obviously never happened as all the applications just went into to the web and used rest instead of webdav and everything else moved to sync protocols that sync to local folders.
- I'm with you on wishing WebDAV continued its rollout. These days there are great low-drama server-side deployments like https://github.com/sigoden/dufs. It's run relative too - you could habe multiple dufs processes serving up different directories in different ways. 
  - But for WebDAV, you can't simply mount that on the client side for every OS that's equally low configuration.
  - For that reason, I really like sshfs as it can be initiated from the client-side without a lot of config (just a mkdir of the mapped dir), and it's OK most time despite it's lack of speed and multi-day uptime. 
  - I'm on a chromebook now and it turns out that Samba is the easiest client-side tech to use for remote file systems. DAv should've been ubiquitous.

- I was expecting this to be a way to mount so-called SQL Archives (https://sqlite.org/sqlar.html) but this is just as cool.

- I'm also working on something like this: https://github.com/Airsequel/SQLiteDAV My mapping is: table -> dir, row -> dir, cell -> file
# discuss
- ## 

- ## 

- ## 

- ## It seems that file system use cases could be boil down into:
- https://twitter.com/Horusiath/status/1761345182924968138
  1. append-only log
  2. (block-based) key-value store
  3. insert or full-replace BLOB file
  4. give me a disk segment and GTFO
- My tweet is about OS API and file system write patterns. In practice database can be implemented using any of the 4 above (+ their combination).

- File system is often used as shared memory

- Why is 2 “block-based”?
  - Maybe I went too deep into implementation part on this one, but pretty much every persistent KV store nowadays uses uniform-sized blocks, and this assumption goes from OS (prefetching fixed size buffers) down to hardware (having fixed size alloc units).
- I was confused because I thought you were looking for "block storage". BTW, not every KV uses uniform-sized blocks. If your KV supports compression and writes fixed-size blocks/pages to disk then it will almost always waste space.
  - The ones that don't use uniform sized blocks usually work like append-only logs, which are then occasionally reorganised (also using either uniform blocks or another append-only log). And yes pretty much every KV does waste the space all the time, one way or another.
- 🆚️ RocksDB supports variable-sized pages and as a result is much more space efficient than other engines. For example, in MySQL world more space efficient than InnoDB.
  - Except that RocksDB (and LSM) in this context is a series of append-only log files.

- ## This is one downside of having no hard links in an FS: renaming a directory means copying all the contained data to the new location.
- https://twitter.com/msimoni/status/1729921989408661877
  - If you have hard links, and you're moving a directory, you can just remove the old hard link and insert the new hard link. But if you don't have hard links ...
- I am surprised seasoned os designer made the decision to not have hard link!
  - I think the reasoning here is to keep the 9P protocol as simple and general as possible. If 9P supported hard links, then every file server has to support hard links, and in Plan 9's everything's a file server.
- Yes, it makes sense. Hard links break FS abstraction a bit since they don't work across file systems
- And soft links break FS abstraction a bit because they introduce cycles, turning tree into a graph (and for other reasons)
- I don't think cycles would _very_ problematic, actually. Tools like cp and rm would have to remember all objects they had already seen (and simply stop there), but that's no longer a real problem, with today's large RAMs.
  - Sure. Still complicates things a bit imo
- That's true also when moving across file systems, since hard links don't go across. Btw, interesting if Git uses some tricks to construct working copy of a commit quickly.

- If the OS provides a syscall for directory rename, the filesystem could internally do it in a hard link like way, without exposing the concept to userspace
