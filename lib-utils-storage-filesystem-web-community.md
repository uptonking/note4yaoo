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
# discuss-sshfs
- ## 

- ## 

- ## [A currently maintained fork of SSHFS | Hacker News _202309](https://news.ycombinator.com/item?id=37390184)
- If you want something in user land and you don't mind emacs there is TRAMP “Transparent Remote (file) Access, Multiple Protocol”.
  - My favorite thing about using TRAMP is being able to cd to a directory on a remote system, and then cp a file either from my working directory to my local machine (or another remote!), or from my local machine to the current working directory.
  - Before I started using TRAMP, my flow for this was: SSH to a remote system, locate where I want to copy a file to with cd + ls, kill my SSH session, and then scp or rsync the file over, and then usually SSH back into the system.

- Couldn't you just use sftp?
  - Idk when you stopped using scp, but scp has been deprecated, and at least w/openssh, using sftp under the hood for years now. You probably have used it if you've scp'd since 2020.
- My point above was that I was making and killing multiple SSH connections to find where I want to copy a file, and then do the copy. Using SCP with an SFTP backend would still do that.

- I think SFTP is a good but underrated protocol, when mirroring a file tree bidirectionally makes more sense than cloning one to another.
  - SFTP is a major step up from FTP, but there's a lot of unrealized potential on the server side, so you can't just work on better clients. Both OpenSSH and the GNU lsh server only offer an old version of the protocol -- v2

- rclone mount is my go-to now for sshfs functionality - better performance, stability and caching options
  - rclone cannot write to the middle of a file though, without transferring the whole file. That is my main issue with it. Maybe sshfs has the same limitation though.
- rclone mount uses sftp in the background which compresses the entire stream (you can control that by passing args to the ssh command spawned by rclone) but it doesn't do it per-file. In practice I don't know if there is a difference.

- Nautilus (Ubuntu's file explorer) allows to mount SFTP folders. Supposedly it uses `gvfs` under the hood.
  - Note that SFTP uses an SSH connection for its file transfers, so I have not seen an UI difference from SSHFS

- gvfs has a bridge to fuse, cf. https://manpages.ubuntu.com/manpages/trusty/man1/gvfsd-fuse.... -- that means: Yes, you can use gvfs mounts natively in all other non-GNOME/GTK-applications running on your computer.

- Is there a more security-oriented alternative to SSHFS, where the connecting client won't be given shell access on the server?
  - If the user account is only supposed to have file transfer capabilities/no shell access, add it a to a specific group e.g. `sftponly`, and only allow this group to use the `internal-sftp` command in `/etc/ssh/sshd_config`
# discuss-file-upload
- ## 

- ## 🤔 做一个文件导出的功能，数据量可能会很大，所以采用了异步导出
- https://x.com/TinsFox/status/1955267842519028014
  - 我建议是服务端推送结果，完事了前端弹窗通知, 用 MQTT/websocket/SSE 都行
  - 结果他们要用轮询, 今天上线了之后一看 network ，满屏轮询请求, 我都没有进到那个模块的页面

- MQTT的话虽然可以用但是不太符合它的设计目的，websocket和SSE我感觉要看系统中是否已经引入了这样的东西，如果已经有了优先考虑这两个，如果没有的话轮询确实还是比较合适的，为了实现这一个小功能为系统引入新的组件有点牛刀杀鸡了

- 感觉没啥，很多大厂的网页都是轮询，最经典的扫码登录也是轮询，当然这个看服务器资源，还有其他条件。

- ## Uploading files on the internet could be so much more efficient if whoever designed the `multipart/form-data` spec just included one small detail: a header telling you how long the content is.
- https://x.com/JoshCaughtFire/status/1927221147860427076
- It’s was designed for streaming where you didn't know the final size. The other problem is you can’t trust the header, the client could be lying. 
  - Historically, that’s led to desync issues and vectors like request smuggling, http/2 still sometimes terms and moves to http/1.1 on backends and can cause still cause issues

- 
- 

- ## 上传文件到对象存储，我觉得的最佳实践: 服务端拿签名给前端，前端通过签名调用对象存储的 sdk 上传
- https://x.com/TinsFox/status/1891334067011854529
- 看业务，各有利弊，上传服务端可以直接拿分析结果，做更好的校验。

- 分片上传没法这么做的， 因为分片上传每个分片都要重新计算签名，这样搞相当于每个分片都要先请求服务端在进行上传。从性能和成本考虑本地sts签名的方式最好

- 延迟能降低，但是校验还有 db 同步不好做。

- 不占用服务端带宽的感觉真棒

- 难道有把密钥写到前端去签名上传的吗
  - 有的，前端的 SDK 支持用秘钥使用，虽然文档说不推荐，但是方便好用

- sdk都可以不需要的，返回签名好的上传url直接上传就可以了
  - 是的，可以用预签名 URL
# discuss-localStorage/sessionStorage
- ## 

- ## 

- ## [On a browser, sessionStorage in Safari's Private Browsing does not work the same as Chrome's Incognito Mode and Firefox's Private Window? - Stack Overflow](https://stackoverflow.com/questions/18860098/on-a-browser-sessionstorage-in-safaris-private-browsing-does-not-work-the-same)
- Safari will just use a quota of 0 in private mode, so all attempts to set a value will fail. This is kinda OK according to the spec, as the spec does not mandate a minimum space requirement.
  - Chrome and Firefox still allow you to use storage, however private storage is independent from non-private, i.e. setting an item in private mode will not reflect back into non-private mode (important for localStorage only).

- Safari latest version (Version 12.0) already have access to sessionStorage without any issue in incognito mode.

- ## [Web Storage (sessionStorage and localStorage) in private browsing mode (incognito) - Stack Overflow](https://stackoverflow.com/questions/26042423/web-storage-sessionstorage-and-localstorage-in-private-browsing-mode-incognit)
- Android and chrome I believe allow you to access old keys in session storage, but not write to it. I know that Safari will not allow any use of session or local storage.

- ## [Local Storage is not supported with Safari in private mode : r/javascript _201503](https://www.reddit.com/r/javascript/comments/2z06aq/local_storage_is_not_supported_with_safari_in/)
- This happens because a private window only has session-based storage. The browser should forget anything that happened during that session, including localStorage requests, so Safari simply says that localStorage isn't available. The error message is still confusing, and other browsers provide localStorage but it really acts like sessionStorage.
  - In Chrome you can't read localStorage items that were set in standard browsing mode while you're accessing a private mode window. Any localStorage items set in private mode will only be available for that session. Apparently instead of giving the user a false sense of storage capability, Safari just says that it's not available in private mode.

- Safari sets the storage limit to 0 bytes in private browsing
# discuss
- ## 

- ## 

- ## 

- ## 

- ## you can ZIP files in the browser using zip.js???
- https://x.com/aidenybai/status/1886128705002496207
- You can even do it natively now with Compression Streams API and DecompressionStream
  - Baseline 2023.  Such new features are buggy a lot of times in different browsers and not quite consistently implemented.
- The compression stream api is really nice but mostly just for gzip. Might not be suitable for all use case.
- Not. Gzip is not zip, so you cannot "do zip files natively now" like zip.js does
- I tried using this recently, it's was a total pain to work with, so I gave up and used zip.js instead
  - very little documentation, awkward API and gzip isn't a particularly nice format if you're building anything for the avg (non technical) user

- Can even encode videos
- you can run full ML models in browser offline at scale. 

- js always can, sometimes it just doesn't think if it should

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
