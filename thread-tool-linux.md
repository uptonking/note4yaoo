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

- ## zsh 在特别大的一个 Git 仓库下会特别卡
- https://twitter.com/alswl/status/1773166682887888927
  - 原因是 zsh 的 prompt 会在每次命令执行之后计算 Git 仓库的 status 和 dirty status。
  - 解法是可以通过图中命令禁用。
- 这是 oh-my-zsh，不是 zsh 本身。这要看你的 oh-my-zsh 都配置了那些插件，配置了 git 插件就会执行这些命令。
  - 是的，我没刻意区分。oh-my-zsh 的主题中 hell prompt 里面会带上 Git 仓库状态。

- 主要是 oh-my-zsh 太慢了吧，可以试试gitstatus 
  - 我尝试了一下，gitstatus 原理是会拉起一个 gitstatusd 后台，用预热方式换时间。

- 完全没必要禁用，换一个异步的主题就行，比如 powerline10k

- ## 使用 nix 管理所有的命令行应用 https://nix.dev
- https://twitter.com/vikingmute/status/1769540841553772726
  - 使用 homebrew bundle 安装所有的 GUI，可以快速配置新的Mac 环境。
  - 使用 dotfiles  管理各种配置。
- 为什么命令行应用要另外用 http://nix.dev ？例如我要安装 git, 直接 brew install git 不好？
  - brew 只能在 mac 上用，无法锁软件版本，也存在依赖冲突问题，对开发环境的搭建不友好。
  - http://nix.dev 是支持多环境的，类似pyenv的概念
- nix是跨平台的系统层包管理工具，所以它能做的远比 pyenv 要多。 
  - 举例来说，我使用了一套配置同时管理 10 多台 NixOS 主机以及 2 台 macOS 的系统环境跟开发环境，而且我的 macOS 跟 NixOS 的开发环境基本相同，配置完全共用，通过 git 仓库实现无缝同步。
- dotfile跟vscode devcontainer关联，开发环境（容器）也可以一键配置

- https://twitter.com/vikingmute/status/1770004206273069091 
  - 可复现能力以及跨平台能力。nix 的配置在 macOS WSL 跟 Linux 三端都能复现出完全一致的环境，而且多端能通过 git 仓库无缝同步。 非常适合机器多的个人用户，或者企业开发环境的搭建。 缺点是门槛高一些。

- ## “因为程序编译问题鲁莽地删掉了 libc.6.so”
- https://twitter.com/IIInoki/status/1767932966259335240
- 谁年轻的时候没有因为libc版本低，然后升级libc导致系统挂掉的。
- 感觉去镜像上下个同发行版的libc包解压复制回去就行了
- linux下所有so都有版本依赖，你从别的地方搞来的so多数情况下不满足依赖条件，也就无法工作

- ## if Linux was a stock, you better buy it sooner than later ... steady growth and it's wonderful these days from daily tasks to gaming and developing (that one has always been the case though).
- https://twitter.com/WebReflection/status/1764653246608539946
  - Linux on the desktop breaks 4% for the first time on Statcounter

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
