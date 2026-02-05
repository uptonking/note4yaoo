---
title: lib-utils-storage-filesystem-community
tags: [comunity, filesystem, storage]
created: 2024-05-22T11:23:32.926Z
modified: 2024-05-22T11:24:07.511Z
---

# lib-utils-storage-filesystem-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-fs-comparison 🆚️
- ## 

- ## 

- ## 

- ## 

- ## [SSD Filesystem: XFS vs F2FS vs Btrfs vs Bcachefs vs ext4 : r/linuxquestions _202305](https://www.reddit.com/r/linuxquestions/comments/13usxg9/ssd_filesystem_xfs_vs_f2fs_vs_btrfs_vs_bcachefs/)
- AFAIK the dedicated flash FSs like F2FS are meant for devices where the FS has direct control over the physical sectors. On drives that present virtual sectors to the OS and control the physical sectors themselves in firmware (wear leveling) flash filesystems have no effect. That should probably be every SATA or NVME SSD.
- Btrfs only if you actually want to use the features like snapshots / subvolumes, copying files with reflinks (CoW), deduplication, transparent compression, data checksums and so on.
- Bcachefs isn't in the mainline kernel and if you have to ask this question I would strongly advise against using FSs that are not mainline.
- XFS and ext4 aren't that different. XFS has a few features that ext4 has not like CoW but it can't be shrinked while ext4 can. They perform differently for some specific workloads like creating or deleting tenthousands of files/folders. But none of these will be relevant to a bog standard use case like "browsing the internet and sometimes playing games like Minecraft".

- TL; DR: Just use the default of your chosen distro.

- ## 🆚️ [EXT4, BTRFS or XFS? : r/linuxquestions _202310](https://www.reddit.com/r/linuxquestions/comments/178fxcl/ext4_btrfs_or_xfs/)
  - Which filesystem is more appropriate for a NVME SSD?

- I've used ext4, XFS, Btrfs, and ZFS for gaming at different points. 
  - While the "next-gen" features of `Btrfs` are awesome, it tends to be slower. 
  - Of the other two, I tend to prefer `ext4`, as 🌹 XFS tends to perform better with large sets of data, but it's a smaller difference than with Btrfs.
- Another point for `ext4` is you can resize partitions both ways, whereas `XFS` can only be grown. For 99% of people, this doesn't really matter. 
  - I run some servers and like to be able to shrink partitions if needed, so I tend toward ext4, just in case. 
  - ⤴️ ext4 can also be "upgraded" to Btrfs, so if you wanted to, you could change to it.
- I actually prefer ZFS for performance, though. Basically Btrfs but better in every way (mostly because everything works, Btrfs is still a work in progress). ZFS typically benchmarks very well, so long as you have enough system resources. It isn't straightforward to setup under Linux, either. So, it's conditional.

- One downside of ext4 is fixed number of inodes, not sure if Fedora creates by default with inode64 flag, but lots of newcomers get caught on that and get completely lost when the system refuses to do some io operations while it still has available disk space.

- the only thing about zfs that inferior to btrfs is adding disks to a pool
  - I feel that this is more of feature than downside. I heard that they are working on it, but, it is extremely difficult to do preserving all safety and robustness. Personally I do not think that this is even worth the effort. Also, you can add disks to pool. Just not in a random way.

- I don't like that you cannot easily shrink `xfs` but it's still my goto.

- I like BTRFS for the snapshots feature which allows you to rollback if you have an upgrade that causes problems. I typically use that on my root partition. But I'm a huge fan of XFS for my drives that contain my media (music, videos and pictures) because it's fast, is super stable, has great performance and can handle large files with ease.
  - Yep, same here. My root is BTRFS for the snapshot feature, and everything else is XFS.

- Btrfs has copy-on-write (if you copy a 1GB file from Downloads to Documents, total storage used is 1GB not 2GB; it re-uses the old file).
  - So does XFS.

- If you're just a regular user then go for ext4. It's the most common for desktop users and it's reliable as hell. 
  - BTRFS has some nice features but it MAY be slightly more unreliable than ext4 and you have to set things up which can be annoying, even for an intermediate user. 
  - I don't have experience with XFS but I believe Red Hat and other enterprise distros use it due to it's scaling capabilities... so probably not that relevant to you.

- TLDR: For desktop ext4 or xfs - both are amazing file systems. Keep away from btrfs and zfs, unless you are building storage solutions. 
  - I, personally, and very subjectively, prefer xfs. All my servers and VMs, except the NAS are on xfs.
- BTRFS: Used to be a huge fun of this FS. But I ate too much shit with it . Maybe it has improved since 4 years ago, but I really doubt.
  - I did not find it stable enough even just as an fs for a developers desktop/laptop. As soon as you start use the fancy-pants features, expect weirdness. E.g. suddenly linux kernel build freezes on a too long write god knows why. The more snapshot's you have the more wired it behaves. And if you add compression to that - it just a matter of time before the whole FS goes bad. And the performance is abysmal.
- ZFS: great for industrial storage systems, iff you tune it right. Also you need to be absolutely sure that you always have at least 10% (better 20% really) free.

- You should use btrfs to hugely save space and have amazing backup features. It can even roll back up to whatever time if you have the snapshot

- XFS have lowest write amplification, so it is pretty good for SSD and in general. 
  - EXT4 is good because it is default choice. And low write amplification as well. 
  - BTRFS - no good, use only if you need it features. Outside some RAID configuration I will not use it personally.
- 🧐 No way am I using BTRFS for production RAID setup when even the project itself tells you not to use the RAID function for production.
  - For production RAID, ZFS is 1000 times more battle-tested for reliability. The problem is presumably bad enough that RedHat decided to abandon BTRFS
- I always thought that this only applies to "RAID5" configuration.

- If you have 32 but apps, don’t use XFS, or add the inode32 option. I learned about that feature when on our build server builds were failing due to missing directories….

- I would recommend btrfs if you use its features such as snapshots, subvolumes, compression etc. Otherwise, I would recommend ext4.

- The distro default. Right now for Fedora it is Btrfs, for Ubuntu and most other popular distros, it is ext4.

- 💡 I should have said BTRFS was developed to work with SSDs from the start. Whereas EXT4 was updated to work with SSDs

- EXT4:
  + Works well for most use cases
  + No maintenance required
  + support grow and shrink
  + can be "upgraded" to Btrfs
  - No extra feature (COW, checksum, ...)

- XFS:
  + Works well for most use cases
  + No maintenance required
  + perform better with large data
  + Supports COW and checksum (but only on metadata)
  + good for SSD
  - support grow, not shrink
  ~ Supports kind of snapshots using reflinks

- BTRFS:
  + Basic use works well for most use cases
  + Supports tons of features (COW, snapshots, checksum, raid options, ...)
  + good for SSD
  + not good for raid
  - Maintenance required (srub, defrag, balance)
  - unstable: Basic use is battle-tested, but specific options can lead to troubles

- ZFS:
  + Supports tons of features (COW, snapshots, checksum, raid options, ...)
  + Can be most performant (though margin is bigger on spinning drives than SSDs)
  - (GPL licensing issues)
  - Usually requires tons of resources (CPU/RAM)
  - Not well integrated in Linux (e.g. reflink does not work, you'll need auto dedup to be enabled to achieve something similar, which comes with a cost of resources/performance)
  - Complex to setup properly, complex to "upgrade" (add disk to a pool)

- This is not exhaustive, but should give a good overview. So my advice:
  - XFS: in general, go for it. It will work out of the box and has some advanced feature such as COW, checksum
  - BTRFS: go for it on Linux you want the extra features but are ok with the added complexity and maintenance
  - ZFS: don't, except for very specific use cases. (On *BSD, Solaris its another story)

- ## [xfs vs ext4 vs btrfs (I am a newbie) : r/archlinux _202201](https://www.reddit.com/r/archlinux/comments/rtugps/xfs_vs_ext4_vs_btrfs_i_am_a_newbie/)
- XFS/EXT4 have been around a long time and considered "stable" and are good to start out as there is much documentation. 
- xfs is solid and faster than ext4 IME. It also has much nicer code.
- Ext4. I tried f2fs recently and grub has some nasty bugs with it. Braking the efi quite often.
- I’m using xubuntu and zfs is shipped with grub snapshot support you don’t need to do anything. I think its better than btrfs and easier.

# discuss-vfs
- ## 

- ## 

- ## 

- ## deepagents-cli 0.0.16 is out: virtual filesystem allows you to expose fs ops to the agent like a filesystem even if they’re backed by a database or object store like Postgres or S3
- https://x.com/Vtrivedy10/status/2018841161637806521
  - built-ins for bash, planning, context management for large tool calls, compaction, skills, memory and more
  - our stack for “hooks” called “middleware” for us is fully open so anyone can inject custom logic into the harness
  - Our prompts, context injection, tool design is open too, spending a lot of time iterating on this
  - The goal is make harness building hackable, and watch the community cook with their creativity

- Are you using a virtual filesystem to sandbox the agent, or are you using it to save the "files" to a database/s3 store? Is there a way to map the FS ops into S3 for example?
  - we support sandboxing as well (more coming soon on this!)
  - but the concept of virtual filesystem is better captured by our “backends” documentation, we’re using it to save files but abstract the underlying storage as fs ops
  - a community member did great work with deepagents-backends showing an example with S3 here

- ## I got the boot time for our little Linux sandbox down to <0.5s with QEMU and it now has TLS MITM. 
- https://x.com/mitsuhiko/status/2018805803239800874
  - Kinda shocked how easy this is to do armed with Opus and Codex. Userland sandbox plumbing is Zig, host is just node. (And I built the FS abstraction on @matteocollina 's new node VFS)
  - The sandbox is unaware of the funky business. It just talks ethernet. There is a JS implementation of Ethernet that handles DNS and TCP and re-encrypts TLS so you can do full interception of all HTTP requests which is super cool because you can just replace fetch.
- Tiago Freitas in founder mode @tiagoefreitas · 14h I wish it had native virtiofs on macos, only old QEMU patch series enable vhost-user backends that could enable VirtioFS. Use case is using macos apps on the same folders available inside the sandbox with native performance. Maybe the clankers can finish that
  - Oh my shit is way worse : D The entire file system is JavaScript 

- So now you can do something like after having mounted the VFS with the eventual thing to run ? For the network part did you attached to a socket ?
  - Sort of, but you register a fetch function instead, and the file system is a full posix like VFS.
# discuss-fs-on-db
- ## 

- ## 

- ## 最近搞了个有趣的玩法，用JuiceFS把PG当成文件系统用，可以实现FS/DB一致的时间点恢复。
- https://x.com/RonVonng/status/1902943946051104890
  - 像Odoo这样的应用就能把所有状态都放在数据库里，而不是在外面还留个文件系统的“小尾巴” 了。
- PG 撑得住？不会越来越臃肿吗？而且所有的文件都走PG的话，文件系统撑得住？

# discuss-file-sync/transfer
- ## 

- ## ⚖️ [Why is ssh not used for file storaging and transfer and instead switch to another things like samba? or can it be actually decent? : r/selfhosted _202511](https://www.reddit.com/r/selfhosted/comments/1oq3zoc/why_is_ssh_not_used_for_file_storaging_and/)
- SFTP exists

- Really depends on what clients are connecting, for Windows, Samba is often recommended because Windows File Sharing is already baked into the OS.
  - However, if your environment mainly have Linux or Mac clients, you can use SSH to do the file transfer or even NFS. 
  - Personally I don't run Samba as I use SSH and NFS for network shares as most of my connecting clients are Linux machines. For Windows machines, I have SSHFS-Win installed on them. There is a native NFS client for Windows but haven't tried it yet.
  - Each protocol has their pros/cons, really depends on your use case.

- SMB is known to have more overhead VS NFS
  - SSHFS less performant than NFS, especially under heavy load or for large file operations

- Ssh is not a file sharing protocol. It is Secure SHell. Using sshfs is clunky and inefficient.
  - NFS and SMB are file sharing protocols and I never had issues with both of them

- ## 需要记笔记做沉淀，也没法远程连自己的电脑（有监控软件），有没有好的解决方法？只能自带电脑了吗
- https://x.com/using_YueCheng/status/1902534987758628995
- 将本地文档转为二维码，然后扫码传输
  - https://github.com/qifi-dev/qrs
  - https://github.com/ganlvtech/qrcode-file-transfer

- 微信输入法，剪切板功能跨设备同步。多找找能跨设备同步的，挺多的。问就是下次注意
  - 走云端都危险啊。还是线下物理同步比较好，之前有位大佬还通过主机的音频接口传输的数据

- 在上一个工作经历里我是用手写来解决问题的。。。买个pad或者大号电子纸之类的东西

- 用localsend直接发到自己的电脑上，最好回家这么干，避免用公司的网

- 写完拍照回去ocr
# discuss
- ## 

- ## 

- ## 
