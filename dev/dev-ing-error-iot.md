---
title: dev-ing-error-iot
tags: [dev, error, iot]
created: 2020-09-18T09:26:23.131Z
modified: 2021-03-29T19:29:42.140Z
---

# dev-ing-error-iot

# ubuntu

- zip分卷压缩
  - 使用zip -s可创建a.z01等分卷文件
  - 如何合并这些分卷文件更好，cat命令创建的大压缩包无法解压，只能通过zip -F创建
  - 小分卷文件合并得到的大压缩文件，无法通过unzip命令解压，却可以通过文件管理器gui解压

```

Archive:  b.zip
   creating: pet/
  inflating: pet/猫咪版.mp4  
  error:  invalid compressed data to inflate
error: invalid zip file with overlapped components (possible zip bomb)

```

- [tracker-store and tracker-miner-fs eating up my CPU on every startup](https://askubuntu.com/questions/346211/tracker-store-and-tracker-miner-fs-eating-up-my-cpu-on-every-startup)
# hp-omen8plus
- [Keep getting Performance mode temporarily disabled due to high operation temperature alert in power settings - Ask Ubuntu](https://askubuntu.com/questions/1530597/keep-getting-performance-mode-temporarily-disabled-due-to-high-operation-tempera)
  - I had a similar issue a while ago, it turned out to be the CPU PROCHOT flag. Still not sure what caused it, but in the end I had to use a script to disable it

- [Ubuntu 20.04 not booting after choosing different NVidia Proprietary driver. Failed to start NVidia Persistence Daemon - Ask Ubuntu](https://askubuntu.com/questions/1263419/ubuntu-20-04-not-booting-after-choosing-different-nvidia-proprietary-driver-fai)
  - [Unable to boot Ubuntu 24.04 - Failed to start nvidia-persistenced.service - Ask Ubuntu](https://askubuntu.com/questions/1520799/unable-to-boot-ubuntu-24-04-failed-to-start-nvidia-persistenced-service)

```sh
# Recovery Menu box: Choose the option
# root  - Drop to root shell prompt. 
ubuntu-drivers list
apt-get remove --purge '^nvidia-.*'
apt-get install ubuntu-desktop
reboot
```

# hp-envy-15
- tracker-miner-fs cpu high
  - 导致触摸板的鼠标指针失效，或者不流畅
  - [tracker-miner-fs is taking 90% of CPU](https://askubuntu.com/questions/1258757)
    - Tracker is an indexing system. It searches all files for words, which are included in a database so you can quickly find files containing specific words.
    - tracker reconstruct: `tracker reset --hard ; tracker daemon --start`

- 无法开机
  - 变通方案：使用win 10的wsl子系统
  - 魔法方案：可能是硬盘松动了，尝试拍几下笔记本底座面，拍几下键盘面

```

boot device not found 找不到启动设备

hard disk 3F0

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

- [三星M2 NVME每天只能在Linux上输入只读信息，而不能在Windows上输入](https://mlog.club/article/2802971)
  - 记住发生故障的具体时间，然后查看系统日志
    - cat /var/log/syslog
    - 执行命令 dmesg -T，用于打印Linux系统开机启动信息，kernel会将开机信息存储在ring buffer中
