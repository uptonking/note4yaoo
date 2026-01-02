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
# discuss-windows
- ## 

- ## 

- ## 

- ## sudo, for Windows
- https://github.com/microsoft/sudo
  - Sudo for Windows allows users to run elevated commands directly from unelevated terminal windows.
  - The "Inbox" version of sudo is available for Windows 11 builds 26045 and later.
  - This project is not a fork of the Unix/Linux sudo project, nor is it a port of that sudo project. Instead, Sudo for Windows is a Windows-specific implementation of the sudo concept.

# discuss
- ## 

- ## 

- ## witr: Stop guessing why a process is running on your system.
- https://x.com/GithubProjects/status/2006747292510925092
- https://github.com/behnamazimi/icport
  - Kill ports like a boss

- ## 搞了个无用的小工具，随便取名叫 slug2text
- https://x.com/nake13/status/2004252226395726286
  - 功能很简单：它能帮你把大段文字，无损压缩成一个 Link。
  - 只要保存这个 Link，再次打开，原文就能自动解压还原。
  - 压缩率取决于文字规模和重复度，但我实测下来，塞进一篇论文的长度也没问题。但受限于 url 的长度，所以无法塞入太多内容。
  - 结论：我也没法评估压缩率，但根据它自己的评估，好像已经很不错了。工程实现上没遇到问题， Codex 都是一次编译即通过。
  - 这个服务完全无状态，所以不需要存储和数据库。打开即用，存 link 即可。 密码完全可以加的，应该也不难。
  - 没想到我 10 天前的产品想法，竟然上了 Hacker News 今日热门，还有 140 个讨论。
  - 结果发现，竟然有开发者实现了完全相同的概念，而且做得更简洁。核心逻辑都是利用 URL 实现一个无状态的文本无损压缩服务。
  - [Slug2Text](https://slug2text.pages.dev/)

- 🤔 其实商业化的能力不强，付费特性一般是后台、并发、自动化、回放

- pied piper for text

- 保存Link通过访问云端解压 和保存压缩后的二进制本地解压 我能想到的差异点是多了云端 来控制授权，没太能get到点。
  - 这个并不是严格意义上的云端，因为网页完全开源可随便部署，相当于点开一个页面就能压缩，流程很快。同时还具备了分享能力，丢一个link给别人，别人打开就能看到原文。而且数据并不存储在服务器上，而是存储在link里。

- 有人做了个 URL 版本的 linktree。

- 🐛 The problem with a URL every edit is a new URL. So you send the URL to a friend, then fix a typo, they need a new URL.

- 🐛 Very nice exploration of URL-as-state. The approach is elegant, but the mobile crashes highlight how hostile real-world URL handling still is once links leave the browser.
  - 复制到移动端app或其他app时， url会显示得特别长

- I like these kinds of projects, but adding a file export/import is inevitable. It's less about the limits of a URL and more about practicality.
  - I also have no way to confirm that URLs aren't logged server side, so I'd never trust the claim about "no tracking". That's why these projects also end up self-hosted.

- ### [Show HN: Minimalist editor that lives in browser, stores everything in the URL | Hacker News](https://news.ycombinator.com/item?id=46378554)

- https://github.com/antonmedv/textarea /202512/html
  - https://textarea.my/
  - A minimalist text editor that lives entirely in your browser and stores everything in the URL hash.
  - Your text gets compressed with deflate because we're fancy like that
  - No backend - Zero servers were harmed in the making of this app
- In case you missed it: it is possible to style textarea via CSS and share it.

- [Itty Bitty: Sites contained within their own links | Hacker News _201807](https://news.ycombinator.com/item?id=17459204)

- Funny how I made almost exactly the same but for maps. I needed a way to share a link to a map, with drawings and the ability for the receiver to see their own location on the map. Annotated screenshots solves the first but not the second.
  - https://github.com/gnyman/mapdraw
  - https://nyman.re/mapdraw/#l=60.172108%2C24.941458&z=16

- Per the spec, a URL can hold at least 8, 000 characters.
  - Mainstream browsers support at least 64, 000 characters, and Chrome supports up to 2MB
- Chrome limit is 2MB, Firefox is 1MB, WebKit is no limit.
- It is always worth remembering that, unless you have already ensured that the content has been rendered into a URI-safe subset of ASCII, a character and an octet are not the same thing.

- Was just working on something similar this morning. As an fyi you can avoid the string replacing in the base64 string by using `.toBase64({ alphabet: "base64url" })` and `fromBase64({ alphabet: "base64url"})`.
  - It warned about fromBase64() and toBase64() not existing in main browsers. It is supported but is indeed a new "baseline 2025"feature. It suggested more compatible code using two small functions to convert characters manually.

- I am thinking from a piracy perspective. If I share a link that contains a book, what can be done from DCMA or legal regulators? They can't ask the server (textarea.my) to remove the link because it doesn't exist.
  - From a regulatory perspective, it seems unlikely that most courts would appreciate the difference. In their mind - you run a website, and that website contains copyrighted content. Take it down.
  - 传递违法信息的风险

- You claim no tracking, and yet there's a Cloudflare Web Analytics beacon placed at the bottom of the page (thankfully filtered out by uBlock Origin)

- I made a similar thing but the html for the text editor fits in a data uri, so it can be a bookmark or new tab page for taking quick notes

- TypeScript playground does effectively the same thing for shared links, though it doesn't live-update as you type.
- 
- 
- 
- 
- 

- ## 前有一堆 AI 厂商仿效 Plaud 做 AI 录音笔，今天钉钉却反其道行之，发布了一款让录音设备失效的干扰器
- https://x.com/Ibrahim92796668/status/2003375071575048302
- 什么原理？
  - 应该是用的超声波干扰器。人耳听不到，但是麦克风听得巨大。
  - 超声波干扰器利用的是麦克风硬件的“非线性特性”。当强大的超声波冲击麦克风振膜时，录音设备的电路无法处理这么高的频率，会在内部产生混频。

- ## [How do you secure a linux desktop? : r/linux](https://www.reddit.com/r/linux/comments/1oy3vkg/how_do_you_secure_a_linux_desktop/)
  - we hear a lot about linux such as "linux is safe and most servers run on linux". but i came to realize that its only true for server installation or headless system. out of the box it maybe super secure.
  - i use ufw and fail2ban but are these enough. what precautions do you take
  - edit: what i learned from the comments is i have to learn SElinux or apparmor like things as a guard to actions done by even if i have su.

- Why do you have fail2ban on a desktop? Anyway, the easiest thing you can do to secure your Linux desktop is to only install packages from your distribution's repo. The main threat targeting desktops is an infostealer. Stick to trusted package sources and don't save credentials in your browser.

- `fail2ban` is for public servers where those servers are getting hammer by bruteforcing ssh ports. You don't need it for a client desktop. You're not even serving anything to get bruteforce. 
  - Firewall, no sketchy package installations, keep up to date with security updates and package updates should be it imo. Don't have port open that aren't needed to be open.

- ## etcd这个傻逼2G的设计可以坑多少公司
- https://x.com/ayanamist/status/1918483674334687505
  - 根因：未开启 etcd 自动压实功能，且默认仅为 2GB 容量。
  - 没有谁会想到，一个存储系统，会给自己的用户，设这样奇怪的一个限制。
  - 搞k8s一定会遇到的问题，除非全用的托管版

- etcd是B tree
  - btree 是 mvcc kv 存储，还有一层 raft log 的，很多年前也写过这个坑 

- 其实etcd的存储上限也就十GB左右了，选型etcd是最大的败笔
  - 我们有60G的实例，不过你说得对，10G以上性能就非常差了。k8s选型etcd就注定是个toy project
- k8s之前各种内部自研的容器平台元数据基本都是scale out的关系型数据库。结果k8s愣是搞个etcd，我都怀疑Google故意的。 之前搞过从老古董sigma迁移到k8s，单集群可扩展性下降的非常明显。

- 我之前负责的一个业务，用etcd+sentinel给PG做高可用方案，就没开自动压缩，早早就写满是个假高可用，一次业务虚拟机打补丁重启就异常了，api用的是v2还是v3研发转手了好几个人没人清楚，另一次做改造，还好做了部署路径文件备份，不然就GG了

- 个人感觉如果频繁触碰这个默认限制的话，其实可以考虑还适不适合用 etcd … etcd 的最舒适区可能是数据规模几百 MiB 的样子 

- etcd 也要配监控告警的

- ## 昨天往一个已有镜像中加入了安装ffmpeg，整个镜像size直接翻倍，build镜像速度放了好几倍
- https://x.com/andrew_rong/status/1898532578212413792
- 而且大概率跨平台编译会挂
  - apple M系更容易出问题

- ## netdata 也太强了，不仅能监控电脑硬件情况，还有软件的使用概括：比如 Docker，哪些 image 在运行，哪些退出了。
- https://x.com/tualatrix/status/1882412419005530122
- netdata有点重，目前在用 Beszel + iStatistica开启Web access
- netdata 在服务器上安装之后总是有内存泄漏 现在都不用了
- netdata资源消耗太重了，生产上不会用。不过个人服务器没啥毛病怎么方便怎么来

- ## found this super cool project called `osquery` which lets you run SQL on your OS as if it's a database!
- https://x.com/iavins/status/1866857917129142493
- it’s brilliant. found it when researching self hosted man solutions a while back. https://fleetdm.com is pretty heavily dependent on it from what I gathered.

- ## 如果你想要快速找出一个网站的所有子域，那么可以使用 Sublist3r 这个工具。
- https://x.com/linuxtoy/status/1864604214217069031
  - Sublist3r 通过 OSINT 找出一个网站的子域。
  - OSINT 的来源包括谷歌、百度等搜索引擎，以及 Netcraft、DNSdumpster、ReverseDNS 等等

- ## The amount of times I've scrolled up in my terminal and wanted the result of that to be ^[[A^[[A^[[A^[[A is zero
- https://x.com/_smcf/status/1855171377583849657
- Screen users will know
- the classic terminal moment when you scroll up and instead of finding the result, you get an endless loop of ^[[A. the true art of debugging frustration.
- 

- ## 1Panel 竟然还提供一键安装 AI 大模型
- https://x.com/kuizuo/status/1793608153734746186
- 对我这个4核8g的轻量应用服务器来说，跑大模型还是太吃力了，十几秒出一个字
- MaxKB  就是  1Panel 官方出品的，再加一些其他常用的
- 这是docker镜像。
  - 对，提供了一键安装，但是对于绝大部分机器根本用不起来

- ## Interesting, @intellijidea built block based terminal in 2024.1 like @warpdotdev
- https://twitter.com/OnlyXuanwo/status/1776791869848231993

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
