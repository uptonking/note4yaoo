---
title: thread-tool-linux
tags: [linux, nix, thread, tool, ubuntu]
created: 2024-01-06T13:48:06.291Z
modified: 2024-01-06T13:48:42.969Z
---

# thread-tool-linux

# guide

# discuss-stars
- ## 

- ## 

- ## 如果让我只分享一个 shell 小技巧，那么就是个我已经用了快十年的“默认连接 tmux session”了
- https://twitter.com/beihuo/status/1758014886679069159
  - 这段代码的主要功能是：如果当前运行的 Terminal 是 Apple Terminal，那么就使用 tmux 并连接到名为 hack 的 session。如果你使用其他软件，可以改成对应的名字。这个判断不会影响 IDE 里面的嵌入式终端。默认的 session 你也可以改成自己喜欢的。
  - 这段代码虽然短，但是从此以后再也无需关心 Terminal 的状态，随用随开，随时关闭。心态超放松。

- 可以开多个窗口吗？
  - 可以开多个 tmux window

- tmux a -t stamhe
  - tmux new -s stamhe
# discuss
- ## 

- ## 

- ## 

- ## 终端退出时，并非所有子进程都会退出。只有那些没有忽略或特别处理SIGHUP信号的子进程会随着终端的关闭而退出。
- https://twitter.com/unixzii/status/1754172044563083481
  - 可以通过编程手段改变进程对SIGHUP信号的默认行为，例如，通过捕获和忽略此信号，使得进程能够在终端关闭后继续运行
- 记得好像是因为终端关闭的时候会向子进程发送sighup信号？然后一般的子进程收到sighup就会终止，除非有nohup
- 操作系统会向该终端上所有的前台进程组发送挂断信号。因为系统认为留下了的子进程干不了什么事业，留着也是浪费资源。所以看出，那时候系统设计者是知道father的重要性的。但还是留了一口气，如果儿子确实牛逼，可以给挂到init上。

- ## 我还记得在本科时候的Linux编程课上，学习了etc和usr的全称——Essential Text Configuration, Unix System Resource。特别是后者很容易望文生义以为是user
- https://twitter.com/liujinmarshall/status/1753478223135142051

- ## SRE Deep Dive into Linux Page Cache
- https://twitter.com/TanelPoder/status/1751882719603126643
  - [Linux Page Cache for SRE | Viacheslav Biriukov](https://biriukov.dev/docs/page-cache/0-linux-page-cache-for-sre/)

- ## Linux file system explained.
- https://twitter.com/alexxubyte/status/1743309278042316933
- The Linux file system used to resemble an unorganized town where individuals constructed their houses wherever they pleased. However, in 1994, the Filesystem Hierarchy Standard (FHS) was introduced to bring order to the Linux file system.
  - By implementing a standard like the FHS, software can ensure a consistent layout across various Linux distributions. Nonetheless, not all Linux distributions strictly adhere to this standard. They often incorporate their own unique elements or cater to specific requirements.
  - To become proficient in this standard, you can begin by exploring. Utilize commands such as "cd" for navigation and "ls" for listing directory contents. Imagine the file system as a tree, starting from the root (/). With time, it will become second nature to you, transforming you into a skilled Linux administrator.
