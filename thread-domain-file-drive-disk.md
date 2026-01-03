---
title: thread-domain-file-drive-disk
tags: [cloud-drive, file-manager, thread]
created: 2024-08-03T20:00:08.670Z
modified: 2024-08-03T20:00:33.414Z
---

# thread-domain-file-drive-disk

# guide

- tips

- 🤔 普通网盘和github有什么区别
  - github支持文件的版本历史
  - github的上传与下载对普通用户不友好

- 存储与同步的参考方案
  - 通用: s3, minio
  - 大文件： git-lfs, xet
  - 小文件: git
  - 难点: symlink
  - more
    - Gitlab btw also simply offloads git lfs to S3. 
# discuss-stars
- ## 

- ## 

- ## [Send: Open-source fork of Firefox Send | Hacker News _202410](https://news.ycombinator.com/item?id=41887378)
- I like localsend too. But for some reasons I need to disconnect from tailscale in order for it to work properly.

- I use a combination of LocalSend on all my devices (Win64, Linux, iOS…) and a Syncthing folder that I call QuickSync and added as a shortcut to all of my file managers a few years ago. Syncthing, in particular, works so well that you don’t even notice it, until you have a file conflict. It’s a great solution to have files synced easily.

- ## [Syncthing Android App Discontinued | Hacker News _202410](https://news.ycombinator.com/item?id=41895718)
- Localsend is a great program - but no alternative to syncthing. Syntcthing is running in the background and syncing automatically. Localsend needs active user interaction. Is there a way how to use localsend similarily to Syncthing?
  - That's not a dealbreaker for me, as I don't run syncthing continuously on either end, just when I'm trying to sync my music.

# discuss-pm
- ## 

- ## 

- ## [File storage server alternative to Nextcloud : r/selfhosted _202403](https://www.reddit.com/r/selfhosted/comments/1bpqfkk/file_storage_server_alternative_to_nextcloud/)
- I ended up with Tailscale to VPN back to my home, Samba to expose my storage on my network and Restic as my backup solution. The Finder app on MAC and Files app on iPhone are decent UI. This may not be fancy enough but get the job done for me.

# discuss-dropbox/google-drive/onedrive-like
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Nextcloud alternative experience : r/selfhosted _202407](https://www.reddit.com/r/selfhosted/comments/1ebc5ii/nextcloud_alternative_experience/)
- I've also used just plain Filebrowser and have been playing around with Spacedrive. Might be worth a look

- ## [Has a better Google Drive alternative come out recently besides Nextcloud? : r/unRAID _202506](https://www.reddit.com/r/unRAID/comments/1li334b/has_a_better_google_drive_alternative_come_out/)
- If you want a feature full web browser based file explorer.
  - The SFTPGO is very good for what it does:
  - I use it for:
  - Web File browser
  - SFTP and WEBDAV server
  - User Management with 2FA
  - Encryption
- FOSS and no limits. I don't think that it does Syncing though. But you can just use Syncthing in combination with it and now you've got it all.

- Is this for accessing files remotely or actually syncing? For remotely accessing files I love webDAV. You can map a share on windows, macOS, Linux, iOS, Android etc and it’s accessible like a local folder.
  - I just use SMB over a VPN.
- SFTP works great.

- ## [Why is Seafile not common? : r/selfhosted  _202506](https://www.reddit.com/r/selfhosted/comments/1lm2f1d/why_is_seafile_not_common/)
- Because people are apprehensive(忧虑的, 担心的) of how Seafile stores data. 
  - Seafile stores data is a proprietary FUSE FS which is not directly accessible outside of Seafile. 
  - They do it for performance reasons and a whole list of other pros that massively outweigh the cons of this approach. It's also the reason Seafile outperforms every other Open Source Cloud Provider out there.
  - That said, in a community like this(selfhosted) where people are highly cautious of their data, a proprietary inaccessible FS is a taboo.
  - Seafile stores data as blobs in their proprietary database in a Git like fashion which can be exposed using a Fuse FS. This architecture allows them to outperform every other File Storage app out there.
- FUSE is not used in the Seafile server, its just hash-identified blobs on the file system, kinda like Git. There's a separate tool for exploring a Seafile library without a server using FUSE, but its not part of Seafile proper.
  - Arguably the Seafile disk layout is ideal for using object storage as the storage backing, like S3 or MinIO, but for personal use most people won't be doing that.
- It's also paywalled.
  - Valid complaint. I wish S3 support was in the community edition. Seems silly that it isn't.
- The FUSE wrapper is read-only though which is a bit of a bummer.

- OpenCloud (recent fork of OCIS) now stores files in a posix (normal file system) format and is lighter and possibly faster than SeaFile. 
  - The setup is a big bowl of spaghetti. Very clever I am sure, but not easy to untangle. I am slowly working on a setup which doesn't have traefik but will integrate collabora, but it's taking more time than I have patience 

- ## [Thinking About a Better File-Sharing Platform—Need Your Input! : r/selfhosted _202408](https://www.reddit.com/r/selfhosted/comments/1euwqrb/thinking_about_a_better_filesharing_platformneed/)
- Is this something you will be actively maintaining in 15 years? 20 years? Many open source projects fail because there is no money being directly involved and that means the dev process isn’t going to be maintainable. Personally I would love a stable program at a cost even.
- i am personally not looking to contribute to nextcloud since I find it to be bloating day by day when the basic functionality does not work and maintenance is a nightmare (for some). The number of issues on github is reflective on how bad the state is currently.
  - I think we can do better and offload file management to any S3 compliant storage (minio, garage, seaweedfs, or any cloud provider) and focus on the indexing and sharing of files.

- You can check Owncloud OCIS, it is rewritten to go but right now it focusing only on files but I had problems with mobile client

- I love everything about OCIS except that it's complicated (there is a lot of documentation but it's not always easy to figure out how to actually put the pieces together) and that it stores files in a proprietary format on the server. As u/henry_tennenbaum says, there is a new POSIX driver which I haven't tried yet
  - However OCIS is still a complicated beast aimed primarily at large installations. I think there is probably space for a smaller, simpler solution aimed at selfhosters that can make different tradeoffs because it's not expected to scale in the way NextCloud and OCIS are.

- ## [Better file manager than FileBrowser? : r/selfhosted _202402](https://www.reddit.com/r/selfhosted/comments/1axbsni/better_file_manager_than_filebrowser/)
- I would say the next step up would be either nextcloud or seafile, only reason I have stayed with file browser is it's just simple and does not break.

- I use and enjoy FileBrowser, but when I'm moving a lot of files around I normally do it in Windows using a mounted drive. I have also used Webtop and use KDE Plasma's Dolphin file browser and that is good if you're on a machine that you don't want to mount network drives to.
  - Yeh so this is me. Every now and again I need to move a lot of files around.
  - The “move” feature in FileBrowser is just painful to use. Especially when I have click 20 times just to find the folder I want to move the file to

- I am currently facing a problem: I want to use nginx proxy to access it, but when my proxy path is not location /, for example, when my proxy path is location /fb, it will cause Filebrowser to be inaccessible. How can it customize the project path to fit my needs?

- ## [NextCloud vs OwnCloud vs FileCloud (2024) : r/selfhosted _202408](https://www.reddit.com/r/selfhosted/comments/1euvkxr/nextcloud_vs_owncloud_vs_filecloud_2024/)
- I use Immich for photos and Seafile for general purpose shared storage.  Immich is great, Seafile is okay, much better than Nextcloud though. 
  - i use Immich for image and Videos... It is closest to Google Photos in terms of UI. For rest of the thing, Nextcloud

- I've been on nextcloud for years. It works well enough for how sporadically I do anything with it, but really considering switching to OCIS instead. I don't need all of nextcloud's collaborative features and its in dire need of a re-write.

- I don't understand why FileCloud is in this list? Not open source and not selfhostable as far as I can see?
  - Tried it but there are too many limitations. Biggest is you cannot select any folder on your PC for sync. That is only available in the paid version. 

- ## [Nextcloud vs owncloud : r/selfhosted _202210](https://www.reddit.com/r/selfhosted/comments/ye0j9q/nextcloud_vs_owncloud/)
- It's an old story that we've seen a million times in FOSS - OwnCloud decided to go more commercial, so everyone of the developers who didn't like that forked it into Nextcloud and afaik it's development is way ahead of OwnCloud now.

- Nextcloud. On the server side all files, unless you enable encryption, are available as just files. So you can back it up from the server easily. I run an RSync cronjob to sync Nextcloud data to another HDD, and from there it get's synced to the cloud 

- I'm personally waiting for owncloud infinite scale to release. It's rebuilt from scratch and looks like it could be much faster and less of a sprawling mess than what nextcloud/owncloud have become over the years through feature creep and just generally being based on older technologies.

- ## [Nextcloud Alternative : r/selfhosted _202412](https://www.reddit.com/r/selfhosted/comments/1hdixdv/nextcloud_alternative/)
- Spun up Seafile, and using webdav for Obsidian.me

- Why are you guys moving off of nextcloud? 
  - It gets updated frequently but nothing ever changes, its slow and cumbersome

- ownCloud Infinite Scale (OCIS) has been great for me. It's a rewrite of the original ownCloud in Go, and is much more lightweight. Been using it for a year now.

- Have you tried Filebrowser? It's kind of barebones, but it's perfect for me.
  - It's cool for the first sight, but it has some down sight s like: exposing your filesystem, a lot of little bugs, no 2FA, and GitHub auto closing issues.
- There is no security layer between web browser of application user and filesystem.
  - You specify which folders and subfolder it can use, as well as which user rights it operates during the docker setup.
- 2FA is up to you to setup. Use Authelia or anything else as your proxy auth and pass the header of choice (username, email, ...). Filebrowser will match its value to the user in filebrowser

- ## [[Request]: Lightweight cloud storage solution that isn't nextcloud? : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kgti6z/request_lightweight_cloud_storage_solution_that/)
- If you need only basic file storage and sharing, I would recommend OpenCloud (a fork of ownCloud OCIS)
- Why not using OwnCloud directly? What’s the point of forking something that works
  - Because the core maintainer team also moved to opencloud so I would say that this is the new main tree of this product.

- Does opencloud have a good syncing app for desktop?
  - Released literally today

- Take a look at the german fork OpenCloud, that is easy to install and very lightweight
  - German fork sounds funny because Nextcloud is already a german fork of owncloud which itself started as german. 

- Nextcloud is a hog when you add a lot of addons. Disable all addons you don't need, don't enable needless addons, and it becomes lightweight.
  - But if you only need personal storage and access, https://github.com/sigoden/dufs is pretty good. It comes with webdav and a web interface for remote access.

- ## [Please Share/Vote on your favorite self hosted Cloud File Share (Nextcloud, Owncloud, Seafile, etc) : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jab3wt/please_sharevote_on_your_favorite_self_hosted/)
- SMB share + FileBrowser
- What I settled on was simply adding tailscale to my devices, mounting `SMB` shares as a network drive on windows/Linux devices, and pointing `filebrowser` running on docker at the same SMB share to let me access the files through a browser on my android/iOS devices. So far it's been rock solid due to how uncomplicated it is.

- OpenCloud - which has been created and forked by the original owner of OwnCloud who has now left OwnCloud 

- I don't like the proprietary file format of seafile.

- I've been messing with Cryptpad lately, and the standard install has a Cryptdrive

- ## [I am done with Nextcloud & Owncloud hello FileBrowser. : r/selfhosted _202312](https://www.reddit.com/r/selfhosted/comments/18ema7z/i_am_done_with_nextcloud_owncloud_hello/)
- Filebrowser is great. I'm sure Nextcloud is right for some people, but to me it always felt incredibly slow and bloated. My only gripe with Filebrowser is the mobile interface. 

- it's a file browser so you can share the same folder to Windows or MacOS with SMB.

- I love that it doesn't encrypt your files - I just want the ability to throw files onto my home server at any time and in any place.

- Seafile here.
  - The biggest limitation is the non-standard file storage format, that makes backup (e.g. via BorgBackup / Kopia) and interplay with other apps (e.g. PhotoPrism / Paperless / Immich) a real pain.

- Im now switching to it, but only missing feature for me would be user stroage quotas

- ## [Selfhosted alternatives for Dropbox : r/selfhosted _202307](https://www.reddit.com/r/selfhosted/comments/151clya/selfhosted_alternatives_for_dropbox/)
- I've been using Seafile on docker for years, ~75gb in sync across 7 libraries. Only issue I've ever had was a "too many files to sync" error that was fixed with a config line to increase the default and it synced right back up. Still stupid fast compared to NC/OC's sync over WebDAV.

- I'll just give my two cents on filebrowser: 
  - I've been using it for the past few months as a solution to my gf's and I's holiday pictures. 
  - It's incredibly lightweight and simple, however, I find the UI difficult to manage. 
  - Browsing long lists of files, it won't remember where you were and it doesn't keep sort and view preferences per folder. 
  - Uploading multiple files and large files is really buggy over WiFi: as in, they will upload, but the UI won't actually respond so you don't know where you are in your upload progress, then you get back to the folder and your view preferences have reset. It's incredibly frustrating.

- ## [Looking for a self-hosted alternative to OneDrive/Google Drive/Dropbox : r/selfhosted _202408](https://www.reddit.com/r/selfhosted/comments/1ezuu39/looking_for_a_selfhosted_alternative_to/)
- Google drive alternative is Seafile. Install docker instance on home server. Just like Google drive, it has clients for Android, iPhone and PC. All sync & files are available anywhere you go.
  - Another option is Next cloud but it's slow.
  - Third option is OIDC, own cloud based file storage/sync.
  - For photos, look at immich (similar to google photos but self hosted)
- Been using Seafile for so many years. Phone (auto-sync photos), Linux, Windows, Mac. Great piece of self-hosted software

- 🐛 Seafile has (had?) a proprietary file organization, if it breaks you wont able to repair it or export your data, as said in othet comments. Try filebrowser or filerun or nextcloud. I wrote proprietary filesystem, is has a proprietary file organization in a db or something like it. By the way it could be problem I dont want to face.
  - Yeah, this is why I usually recommend OwnCloud or NextCloud. I am not comfortable with an abstracted file system that relies on a database to make sense. If something goes wrong with my OwnCloud install, I can just copy files out of the individual user folders, and recreate it. I can also back it up and get files out of the backup without restoring the entire SeaFile instance.

- Worth noting that "Nextcloud being slow" is solved by used Nextcloud AIO (a setup that uses docker containers). This is my current setup and I've been loving it.
# discuss-filesync
- ## 

- ## 

- ## [The future of large files in Git is Git | Hacker News _202508](https://news.ycombinator.com/item?id=44916783)
- I wrote git-bigstore almost 10 (!) years ago to solve this problem—even before Git LFS—and as far as I know, bigstore still works perfectly.
  - You specify the files you want to store in your storage backend via .gitattributes, and use two separate commands to sync files. I have not touched this code in years but the general implementation should still work.
  - GitHub launched LFS not too long after I wrote this, so I kind of gave up on the idea thinking that no one would want to use it in lieu of GitHub's solution, but based on the comments I think there's a place for it.
  - It needs some love but the idea is solid. I wrote a little description on the wiki about the low-level implementation if you want to check it out.
  - Also, all of the metadata is stored using git notes, so is completely portable and is frontend agnostic—doesn't lock you into anything (except, of course, the storage backend you use).

- > Large object promisors are special Git remotes that only house large files.
  - I like this approach. If I could configure my repos to use something like S3, I would switch away from using LFS. 
  - S3 seems like a really good synergy for large blobs in a VCS. The intelligent tiering feature can move data into colder tiers of storage as history naturally accumulates and old things are forgotten. I wouldn't mind a historical checkout taking half a day (i.e., restored from a robotic tape library) if I am pulling in stuff from a decade ago.
- The article mentions alternatives to git lfs like git annex that support S3 already (which IMHO is however still a bit of a pain in the ass on windows due to the symlink workflow). Also dvc plays nicely with git and S3. Gitlab btw also simply offloads git lfs to S3. All have their quirks. I typically opt for LFS as a no-brainer but use the others when it fits the workflow and the infrastructure requirements.

- At my current job I've started caching all of our LFS objects in a bucket, for cost reasons. Every time a PR is run, I get the list of objects via `git lfs ls-files`, sync them from gcp, run `git lfs checkout` to actually populate the repo from the object store, and then `git lfs pull` to pick up anything not cached. If there were uncached objects, I push them back up via `gcloud storage rsync`. Simple, doesn't require any configuration for developers (who only ever have to pull new objects), keeps the Github UI unconfused about the state of the repo.
  - I'd initially at spinning up an LFS backends, but this solves the main pain point, for now. Github was charging us an arm and a leg for pulling LFS files for CI, because each checkout is fresh, the caching model is non-ideal (max 10GB cache, impossible to share between branches), so we end up pulling a bunch of data that is unfortunately in LFS, every commit, possibly multiple times. Because of this they happily charge us for all that bandwidth, because they don't provide tools to make it easy to reduce bandwidth (let me pay for more cache size, or warm workers with an entire cache disc, or better cache control, or...).
  - and if I want to enable this for developers it's relatively easy, just add a new git hook to do the same set of operations locally.

- We use a somewhat similar approach in RWX when pulling LFS files
  - We run `git lfs ls-files` to get a list of the lfs files, then pass that list into a task which pulls each file from the LFS endpoint using curl. Since in RWX the output of tasks are cached as long as their inputs don't change, the LFS files just stay in the RWX cache and are pulled from there on future clones in CI. 
  - In addition to saving on GitHub's LFS bandwidth costs, the RWX cache is also _much_ faster to restore from than `git lfs pull`.

- You can install your own S3 compatible storage system on premises. 
  - It can be anything from a simple daemon (Scality, JuiceFS) to a small appliance (TrueNAS) to a full-blown storage cluster (Ceph). OpenStack has it own object storage service (Swift).
  - If you fancy it for your datacenter, big players (Fujitsu, Lenovo, Huawei, HPE) will happily sell you "object storage" systems which also support S3 at very high speeds.

- TFA asserts that Git LFS is bad for several reasons including because proprietary with vendor lock-in which I don't think is fair to claim. GitHub provided an open client and server which negates that.
  - LFS does break disconnected/offline/sneakernet operations which wasn't mentioned and is not awesome, but those are niche workflows. It sounds like that would also be broken with promisors.

- Another way that LFS is bad, as I recently discovered, is that the migration will pollute the `.gitattributes` of ancestor commits that do not contain the LFS objects.
  - In other words, if you migrate a repo that has commits A->B->C, and C adds the large files, then commits A & B will gain a `.gitattributes` referring to the large files that do not exist in A & B.
  - This is because the migration function will carry its ~gitattributes structure backwards as it walks the history, for caching purposes, and not cross-reference it against the current commit.
- That doesn't sound right. There's no way it's adding a file to previous commits, that would change the hash and thereby break a lot of things.
- `git lfs migrate ` rewrites the commits to convert large files in the repo to/from LFS pointers, so yes it does change the hashes. That's a well-documented effect.

- Git annex is somewhat more decentralized as it can track the presence of large files across different remotes. And it can pull large files from filesystem repos such as USB drives. 
  - The downside is that it's much more complicated and difficult to use. Some code forges used to support it, but support has since been dropped.

- Git LFS didn't work with SSH, you had to get an SSL cert which github knew was a barrier for people self hosting at home. I think gitlab got it patched for SSH finally though.
  - I think it is a much bigger barrier than ssh and have seen it be one on short timeline projects where it's getting set up for the first time and they just end up paying github crazy per GB costs, or rat nests of tunnels vpn configurations for different repos to keep remote access with encryption with a whole lot more trouble than just an ssh path.

- 🧩 xet on hugging face does seem to not have such bandwidth issues imo. I wish that something like xet but open source could exist.
  - xet is open source, check out https://github.com/huggingface/xet-core.
  - We (I'm on the xet team at HF) are open sourcing our spec + protocol in the coming months. So, with the spec and protocol open-sourced, anyone can create xet clients and implement the protocol to build a xet backend.
  - The specific implementation of our xet backend is deeply integrated into HF backend so open-sourcing it directly wouldn't be very helpful. Once we get the spec + protocol released it should be easy to generate a compatible backend.

- Xet uses block level deduplication.

- ## [Migrating Hugging Face repos off Git LFS and onto Xet : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1je6bfq/migrating_hugging_face_repos_off_git_lfs_and_onto/)
- Is the chunk level dedupe on the client side or the server side?
  - On the client side. We're working on an integration Hugging Face's Python library that will be released soon. All the dedupe specific client code is available here https://github.com/huggingface/xet-core

- ## google 的 cdc-file-transfer 是一个文件同步程序，亮点是比 rsync 的速度快几倍。那么它是如何实现的呢？
- https://x.com/hemashushu/status/1973311859072921927
  - rsync 是一个非常悠久且高效的远程文件（夹）同步程序，当它发现某个文件数据改变需要传输新内容时，它并不会整个文件上传，而是把文件按照固定大小（比如100 kb）切分并结算每一块的hash, 在 remote 端，对目标文件作相同大小的切分和计算hash，然后 local 端把hash序列发送给remote作对比，最后只上传新的或者发生更改的块（block）。这种去重算法能避免上传整个文件，但如果文件是在中间插入新的数据，那么就会导致这个节点后面的block hash全都改变了
  - cdc则改进了文件切分的方法： 在 cdc-file-transfer 里，使用了一种叫 gear based 的切分方法，算法：预先生成随机数组 gear_table[256]，然后读取文件的每一个字节值b，计算hash = (hash << 1) + gear_table[b]，当 (hash & mask) == 0 时（mask是预期每个块的大小，每 2^n 字节，n 为 mask 的位数，每位都是1）就分为一个block.
  - 用这种方法切分的 block 因为不是固定大小的，所以即使原文件中间被插入了或者删除了部分数据，都不会导致后续的所有block hash更改，所以除重率比rsync的固定大小切分法高很多。对于app store或者steam之类的大文件同步很有帮助。

- 可惜的是代码已经被归档，后面不维护了。

- xet 可以看看
  - [Options for self-hosting? · Issue · huggingface/xet-core _202506](https://github.com/huggingface/xet-core/issues/398)
    - No, we currently do not have an option to self-host the Xet Storage backend.
    - the underlying Xet tech is all open source and we'll work on packaging it into a reusable bundle at some point in the future but we need to focus on finishing the migration first.
# discuss
- ## 

- ## 

- ## 

- ## 不理解为何一定要套个 https，下载这种东西流量很大，使用 http 可以有效降低服务器负载和碳排放，
- https://x.com/skywind3000/status/1819754568022106389
  - 下载完了通过可信渠道校验下 md5 就完了，比如通过 https 获取更新配置时带上 md5 和对应 http 的下载地址就足够了，根本不怕被截获，为何非要套个娃呢？
- Linux 的软件仓库，一般可以自选 http/https，反正后面会验 hash 以及 pgp 签名。http 或许会被截获以及篡改，进而暴露你在做一个重要的安全更新，然后被阻止接着第一时间被攻击。而 https 则更稳定，且没有暴露更新细节的风险。这里的碳排能省，但人们或许懒得去省
- http可以被改
  - 改了你会校验 md5 的啊，md5 从 https 获取即可
- 安全团队建议甚至强制https是因为很多业务团队压根不会检验数据。。
  - 没毛病，但凡事别教条主义
- https成本已经很低了
  - 不低，有云厂商甚至卖 https 转 http 服务，因为应用提供分的服务器压力大，自己解码 https 撑不住，所以只提供 http 接口，前面套个云厂商的转换加速服务
- 会不会就是考虑https要正确的客户端时间，这会让很多不常开机的电脑，或时间没有自动同步的用户无法更新。比如中国时间同步的服务器可能访问有限制。
- https连缓存都做不了，这种数据最适合缓存了
- 用 HTTP 的意義在於可以被各級輕易的緩存來節省流量
