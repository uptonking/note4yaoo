---
title: pick-discuss-cs
tags: [cs, discuss, pick]
created: '2021-01-25T15:38:45.583Z'
modified: '2021-04-12T16:30:53.967Z'
---

# pick-discuss-cs

# faq

## 

## 

## 

## 

## 

## [为什么很多程序员不用switch，而是大量的if……else if？](https://www.zhihu.com/question/475877331)

- 条件判断语句的四种写法，茴字的四种写法大家不会不知道吧
  - 多个if，卫语句
  - lambda 策略模式
  - DDD领域驱动设计思想+策略模式
  - Actor模型+领域驱动设计+策略模式+事件响应式架构

- 当比较项比较少时（比如 30个？），编译器应该会把switch结构改成if-else结构，因此两者没有区别。
  - 当比较项超出那个数时，switch会按照事先排好序的表进行快速定位，比较项的数目越大，switch的定位效果越明显，哪怕是几千万的比较项，比较次数不会超过20次、就可以定位

## [Windows有了Bash，是不是意味着Powershell过时了？](https://www.zhihu.com/question/41972152/answers/updated)

- 窃以为 PowerShell 和 cmd 最大的不同，并且也是和其它 *nix Shell 最大的不同在于 **PowerShell 的 pipe 传递的是 .net object，而不是 raw 字符串**，
  - 于是这就打开了一扇神奇的大门，因为 PowerShell 的一切组件都可以和谐地共存，彼此不用互相猜忌，不用猜你喂给我的数据合不合法，也不用担心我喂给你的参数格式对不对。
  - 大家共享一个 CLR，拥有丰富的 metadata，自由自在地在 .net 的世界里徜徉和探索。

- powershell不只是shell， powershell是一个完整的，动态的，面向对象的编程语言。
  - cmdlet是powershell作为shell的功能。.net是其类库。
  - powershell的变量系统也更强大
  - 这么看，powershell就是 bash+python啊 

- 不需 Bash，PowerShell 从一发布，就已过时。其实 PowerShell 也没啥生态圈，PowerShell 这东西就没入过流，也不存在过时一说。
  - 不懂就别乱说吧。Windows Server，Exchange Server，SQL Server，Azure这些用户极其庞大的企业级软件和平台，现在哪一个不是要用PS来做自动化运维和管理呢?

- 公司报表系统用powerbi, PowerShell有现成cmdlet支持，可以做很多事

## [Windows 的 PowerShell 和 Linux 的 terminal 有啥区别？](https://www.zhihu.com/question/26860370)

- powershell由微软开源，并长期维护；基于c#实现

- Shell「壳」，即人与电脑的接口，实际上是个命令解释程序，
  - 从标准输入读取你的命令，把命令结果输出到标准输出和标准错误等设备。
  - Linux下的 Bash、Zsh，Windows 下的 cmd、PowerShell，这些都是 shell，这个应该很容易理解。
- Console「控制台」，即在 Linux 下按 Ctrl-Alt-F? 看到的那个命令界面。
  - 事实上，在远古的 Unix 大型机时代，console 应该是指物理连接在主机上的输入输出设备，
  - 而 terminal 是指与 console 进行远程通信的串行设备。
  - 而如今的 Linux 控制台实际上是内核模拟的 /dev/ttyn 终端，/dev/console 一般就是 /dev/tty0，只有 root 用户才能写入。
- TTY 远程连接到控制台的串行设备，现在来说通常也就是 /dev/ttyn 这些设备啦。
- PTY
  - Psuedo Terminal 「伪终端」，是成对的逻辑设备，/dev/ptmx 和 `/dev/pts/<number>`。
  - 实际上 X 的终端以及 telnet 和 ssh 等服务都是通过伪终端来进行的。
  - 远程终端绑定到` /dev/pts/<number>` 端口上，服务器实际对 /dev/ptmx 进行读写，但结果都会反映在 `/dev/pts/<number>`，远程终端会认为自己在读写一个串行终端，服务器也会认为自己在从一个串行终端进行读写，中间则由 telnet ssh X11 等协议进行连接。

- 严格来说 Windows（具体来说是 Win32 子系统）上并不存在 Linux 上所谓的「控制台」、「终端」和「伪终端」。
  - Windows程序可以被编译到 GUI 子系统和控制台子系统，系统通过程序的入口函数可以判断程序是个 GUI 程序还是控制台程序。
  - 对于 GUI 程序来说，stdin stdout stderr 这些设备都是不存在的。
  - 而 Windows 那个黑黑的命令行窗口被称为「Windows 控制台」，实际上它里面模拟了标准输入、标准输出等设备。
  - 默认情况下从 explorer 中双击打开命令行程序时，系统会动态创建一个新的 console，用 start /b 命令可以让程序在当前 console 中运行，不加 /b 则在新的 console 中运行，而这两个 console 的 stdin stdout 等设备又都完全不相干了。
- tty 实际上是一种字符串流协议。而 Win32 以 API 形式的「终端」协议，一般就很难进行远程通信了。

## [2021年了，Rust在偏底层的某些领域是替代C++的一个好的选择吗？](https://www.zhihu.com/question/451687128)

- 嵌入式，操作系统，硬件驱动这些底层领域大多数用的是C，而不是C++，，所以就更谈不上Rust替代C++了，，
  - C++在嵌入式领域主要的应用是GUI，，比如Qt 
  - C++和Rust最大的特点是"zero cost abstraction"，底层领域只需要“zero cost”，不太需要“abstraction”，，所以语法简单的C更合适

- 当前有两个标志性事件，linux kernel，已经同意使用rust来编写内核模块，这个绝对够底层了。
  - android，Google也决定引入rust来开发底层服务。
- rust自身是MIT/BSD/Apache, linux内核偏向于GPL

- 底层这个领域的特性对 Rust 并不友好。
  - 第一是 Rust 并不是变魔术消除 complexity，它是把 complexity 圈禁在 unsafe code 里。如果你的项目大部分都是 safe code，这个是否还叫「底层开发」就值得商榷。你把好多 safe code 归到底层，这就是说你的架构可能就不清晰。
  - 第二是底层开发强调一个项目尽可能通用，可重用，功能稳定。这种项目的管理本身消除了 C++ 在快速迭代上的弱势，凸显了 C++ 语言本身稳定，工具链成熟的优势。

## [公司项目并发量都特小，自己如何实际接触高并发项目？](https://www.zhihu.com/question/267113602)

- 高并发与大数据的技术问题，终极方案几乎都会转成分布式存储+实时流处理的解决方案，
  - 也就是将高并发的请求负载转换成大吞吐、有序队列的方式，降低高并发的同时性请求导致的CPU、内存、I/O这些资源争用的根本性问题，
  - 然后通过数据分片，落地在数据库的不同分布式节点中，实现数据upsert的水平伸缩性。

- 如果你的公司项目没有特别高的并发，那么你可以把目光转移到低延时和高吞吐上。
- 先说低延时。即使你的服务只有1 qps。如果客户端一次请求响应耗时500ms，你能不能想办法优化到250ms，甚至100ms呢？也是技术挑战。
- 在线和离线系统其实都有高吞吐的概念。
  - 说说在线，比如推荐系统中一次请求召回一万个item（item表示一篇文章或者一个短视频），需要做排序，所谓排序其实就是给item打分。
  - 那么请求一次排序服务（ranking）未必能在规定时间内计算完一万个item的打分。
  - 上游简单的处理是拆包，1000个item一包，发10次请求给排序服务。
  - 虽然对于排序服务而言，qps放大了10倍，但是能够让一万个item在规定时间内返回。
  - 如果排序服务能够一次处理10000，或者5000个item，而耗时也不会超，那么这就是在提高排序服务的高吞吐的能力。

## [深度学习领域，你心目中idea最惊艳的论文是哪篇？](https://www.zhihu.com/question/440729199)

- 有两个: ResNet和Transformer。
  - 许多大领域都离不开这两种结构。
  - Transformer更是从NLP领域走入了CV领域，大有一统天下之势。
  - ResNet大道至简，更倾向于从原来的CNN结构设计出发，通过大量的实验和分析，添加了skip connection，一招封神。
  - Transformer则另起炉灶，干脆完全抛弃了RNN的结构，从根本上尝试self-attn加全连接层对于序列建模的能力。
