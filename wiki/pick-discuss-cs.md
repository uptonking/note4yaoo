---
title: pick-discuss-cs
tags: [cs, discuss, pick]
created: 2021-01-25T15:38:45.583Z
modified: 2021-04-12T16:30:53.967Z
---

# pick-discuss-cs

# discuss

## 

## 

## 

## [普通程序能利用GPU运算吗？](https://www.zhihu.com/question/55249247)

- 能是能用。乘加运算，逻辑判断等操作你都可以用gpu完成。
  - 关键是有没有意义，gpu是面向吞吐量设计的硬件。由于内部线程预分配资源，线程切换代价极小。只有喂给gpu够多的数据量，才能充分用好gpu高带宽的优势，从而产生明显加速效果。
  - 单cpu同时并行的线程数量少，而且切换开销更大。内存带宽也低，吞吐量上不去。

## [后端可以直接从cookie里取到token，为什么前端还要token设置到Authorization？ - 知乎](https://www.zhihu.com/question/558219586)

- 两种方案：
- 将 token 放在 cookie 里；
  - 前端可以完全不写代码，设置 cookie 可以依赖后端的 Set-Cookie 响应头，同域名的情况下发送所有请求的时候 cookie 也是自动带上的（也有坏处，这样经常会造成网络流量和带宽的浪费）；
  - 在安全性方面，cookie 可以设置 HttpOnly 来保护 cookie 无法被 JS 代码捕获，避免 XSS 等攻击，还可以设置 Secure 来确保只在 https 环境下传输 token；这些能力由浏览器提供，Authorization 无法实现；
  - 但是，cookie 会存在 CSRF 攻击的问题，虽然浏览器厂商在逐步禁止第三方 cookie（似乎推迟到 2024 年了），但是这个问题还是不得不防（如果想使用第三方 cookie，可以在后端响应中设置 cookie 的 SameSite 属性）；
  - 在一级域名相同的情况下，cookie 可以实现跨子域名互通，比如 a.example.com 和 b.example.com 之间可以实现 cookie 互通（设置 cookie 时提供 Domain=example.com 属性），这个能力也是 Authorization 不具备的；
  - 网页中的图片 `<img />` 请求时也会自动带上 cookie，便于控制网络图片的访问权限，这个是 Authorization 做不到的，必须把 token 放在 url 查询里面才行。
- 将 token 放在请求头里，用 Authorization 字段。
  - 此字段需要由 JS 代码来写入，请求想要带上 Authorization 字段则需要用 JS 代码来给请求方法添加全局拦截器，因此它天生具备防止 CSRF 的功能；
  - 只有浏览器使用 cookie，而小程序、Node.js 等环境，都是没有 cookie 的，只能使用 Authorization；因为此字段完全由 JS 来操作，我们可以自己实现诸如 cookie 的 Secure、Expires 等功能；
  - 前端将 token 持久存储，一般会存储在 LocalStorage 里面，此时存在 XSS 攻击盗取 token 的问题（建议将 LocalStorage 里的 token 加密），而且它是无法跨域互通的，即使两个网站的一级域名相同也无法互通；
  - 部分认证规范要求使用 Authorization 字段，例如 JWT，如果使用了相关的认证（尤其是第三方服务），则必须使用此字段。
- 无论对于前端还是后端而言，这两种方案都是各有利弊的

- 还有一点补充一下，如果用cdn之类，导致前端和后端域名不同的话带cookie实现跨域比较麻烦。反之如果前端和后端是同域名，也不限制path会导致请求静态文件也带上cookie比较吃流量

## [machine learning 在 Java 上的开发是不是已经没落？ - 知乎](https://www.zhihu.com/question/68177121)

- 对于ml engineer，其实最重要的标准是“好写好改”，而不是语言运行效率以及语法有没有真泛型之类的东西。
  - 配合jupyter这样的互动式notebook，python这样的dynamic脚本语言是非常适合ds/ml engineer日常工作的。
  - 而对于infra engineer，我觉得你是不会去想java和c++没落的，因为你天天都在用啊。

- 易用性才是王道，你看pytorch速度牺牲成这个样子还是能一统江湖。
  - 比Java、c++写起来更容易（代码短，写的快，不用考虑各种次要东西）

- 实际工作中，模型调试只占整体工作的很小一部分，大部分时间都在分析数据和pipeline开发上。所以想把算法落地上线，工程能力是必不可少的。毕竟基建完备，无需开发的大厂就那么几家。

- 使用一项编程语言除了语言本身，还要看社区。Python下面这么多ml的包，大势已成，很难动摇。很多想把ml从R&D向production转变的库也开始自己实现一些类型检查，依赖注入的方案。同时ml是一个很复杂的综合性领域，要形成产出，需要涉猎很广，Python作为胶水语言，有它独特的优势所在。

- 纯Python代码当然是比纯Java代码慢得多。但是，无论Python还是Java代码（特别是考虑到GPU, NPU），跟C/C++相比都是渣。所以关键是谁调用C/C++快。这方面Java完败。
  - 与C的接口，很少有语言能比Python效率高的。
  - 毕竟，Python VM没有任何内置类型。这个语言里连int都要通过Python/C扩展API调用C代码实现。这使得Python的int很慢，但也使得Python里调用C扩展的开销不比使用int大。
  - 没有堆内堆外，没有类型转换。对于C来说每个Python对象就是一个C struct。对于Python来说每个C struct只要有PyObject header就是Python对象。
  - 纯Python代码的慢换来了调用C扩展的快

- 搞数据科学的重点在于数据，而不在于编程，对他们来说，怎么简单怎么来才是最正确的做法。

- 最近机器学习Oracle 开源了Tribuo支持主流机器学习算法，AWS开源了 DJL 专攻深度学习实现。主要是也没有python那么火爆吧，功能性一直都不会很差。
  - aws 为啥不推deepleaning4j？
  - DL4J依赖项比较多，同时架构也很陈旧。再有一点就是只支持TF 1.x而且输出结果和python都有出入

- 实际上大家是用Hive/Spark取数，放到Python里训练，然后再用Spring接Python上线的...

## [用A4纸记录一个G的数据需要多少钱？](https://www.zhihu.com/question/483838337)

- 多少钱看你用什么纸什么打印机
- 记录数据为什么要用10pt等线字体呢？
- 既然电脑的数据是二进制的0和1，那么我们用纸来记录的时候，用一个点是否有颜色来表示就可以了。
  - 所以一张纸能记录多少数据，取决于打印机可以打印出多精细的点。
  - 以京东自营超过30万好评的HP 1136激光打印机为例，分辨率1200dpi，也就是每英寸打印1200个点。
  - A4纸大小是8.3"×11.7"，很容易计算打满的话是139, 838, 400个点。
  - 不过为了避免边缘的数据难以分辨，我们在四周留出100个点的空白（2毫米多一点），那就是135, 078, 400个点，每个点代表1bit，每字节8bit，那就是16, 884, 800字节。
- 然后我们可以双面打印，所以要打印1000进制的1GB数据，需要：
  - 1, 000, 000, 000÷16, 884, 800÷2=30张纸。
- 如果是1024进制的1GiB数据，需要：
  - 1, 073, 741, 824÷16, 884, 800÷2=32张纸。

- 计算机如何储存数据，以及数据如何展现。
  - 计算机是数字化储存，而我打印出来，转变成了模拟性储存。
  - 就像计算机电路里面有模拟电路和数字电路，一般我们把模仿现实世界的部分称作模拟，而经过数字技术，数字算法抽象，转换的叫做数字化，这是很关键的，落实到储存来说，就代表了如何数字化储存，和储存的东西原来在现实世界是什么。
  - 想要在纸张上模拟数据储存，比如题目下面有几个回答都在做，转换成2进制储存，这个思路是对的，但是实际上不这么做，
  - 虽然计算机是01储存，但是实际上在纸张上我们可以采取更短的格式，比如十六进制，十六进制在日常实用当中，常常作为二进制的一种等价转换，因为十六是2的四次方，所以八位二进制可以表达成两位十六进制，这样子，空间上就节约了
  - 根据这个思路，在不做数据压缩的情况下，在A4纸上按字节储存数据的话，应该实用更高进制，比如十六进制，乃至于六十四进制。
- 已经有人想到并实现出来了: ollydbg的作者olly制作了paperback用于在纸张上打印图像以存储数据。

## [我觉得静态类型系统分为三个层次](https://www.zhihu.com/pin/1409598553932746752)

- 一种是纯静态的，就是类型都是定义变量的时候声明的。古老语言是没有泛型的，不够灵活
- 第二种是支持泛型的，也就是类型参数，类型可以通过泛型参数动态确定。java 是这一种，只支持泛型，有了一定的动态性。
- 第三种就是高级类型了，除了传参以外还支持各种逻辑，甚至图灵完备，用来动态生成类型，
  - 比如 ts 的类型，可以做判断、递归、取属性等等。
  - 这种就是动态性特别强的类型系统了。
- 从简单到复杂分为这三种类型系统。

- c++的泛型算第二种还是第三种呢
  - 第二种

## [dsl是领域特定语言的意思](https://www.zhihu.com/pin/1412785287882129408)

- 就是为了方便描述一个领域的逻辑特别设计的语法，
  - 比如 vue 的 template 和 react 的 jsx，包括 html、css 都是为了描述视图设计出的 dsl。
  - vue template parser 由 vue 实现，react 的 jsx parser 由 babel 实现，html、css 的 由浏览器的渲染引擎实现

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