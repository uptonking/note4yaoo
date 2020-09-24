---
title: log-pieces-iot
tags: [iot, log]
created: '2020-09-18T09:26:23.131Z'
modified: '2020-09-18T09:32:05.147Z'
---

# log-pieces-iot

## hp-envy-15

- 无法开机

``` 
boot device not found

```

- 突然系统崩溃，显示异常，原因未知

  - [EXT4-fs error after Ubuntu 17.04 upgrade](https://askubuntu.com/questions/905710/ext4-fs-error-after-ubuntu-17-04-upgrade)
    - sudo gedit /etc/default/grub
    - GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvme_core.default_ps_max_latency_us=5500"

``` 
ext4-fs error (device nvme0n1p6): __ext4_find_entry: inode: reading directory lblock 0
systemd-journald: failed to write entry ( items,  bytes), ignoring: read-only file system 

nvme0 failed to set APST feature blocks
```

  - [解决 SYSTEMD-JOURNALD: FAILED TO WRITE ENTRY 问题](http://smilejay.com/2018/02/systemd-journald-failed-to-write-entry/)
    - 通过 journalctl --verify 命令找到损坏的journal文件，然后删除或者mv移动它，再重启systemd-journald服务即可

``` 
// 执行 journalctl --verify
f9deb8: Invalid entry item (17/23 offset: 000000                                
f9deb8: Invalid object contents: Bad message                                    
File corruption detected at /var/log/journal/8363b5e4cb2b4b959b362494307725dc/system@0005ab8b6999eabb-228e618fc9ae7d10.journal~:f9deb8 (of 16777216 bytes, 97%).

508df8: Data object references invalid entry at 73ac60                          
File corruption detected at /var/log/journal/8363b5e4cb2b4b959b362494307725dc/system.journal:73a9c0 (of 8388608 bytes, 90%).

```
