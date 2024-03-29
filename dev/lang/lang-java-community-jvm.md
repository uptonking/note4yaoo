---
title: lang-java-community-jvm
tags: [community, java, jvm]
created: 2023-08-28T04:37:19.226Z
modified: 2023-08-28T04:37:45.327Z
---

# lang-java-community-jvm

# guide

# discuss-llvm-jvm
- ## 

- ## 

- ## [详解三大编译器：gcc、llvm 和 clang - 知乎](https://zhuanlan.zhihu.com/p/357803433)
- 传统的编译器通常分为三个部分，前端（frontEnd），优化器（Optimizer）和后端（backEnd）. 
  - 在编译过程中，前端主要负责词法和语法分析，将源代码转化为抽象语法树AST；
  - 优化器则是在前端的基础上，对得到的中间代码进行优化，使代码更加高效；
  - 后端则是将已经优化的中间代码转化为针对各自平台的机器代码。

- GCC（GNU Compiler Collection，GNU 编译器套装），是一套由 GNU 开发的编程语言编译器。GCC 原名为 GNU C 语言编译器，因为它原本只能处理 C语言。
  - GCC 快速演进，变得可处理 C++、Fortran、Pascal、Objective-C、Java 以及 Ada 等他语言。

- LLVM （Low Level Virtual Machine，底层虚拟机)）提供了与编译器相关的支持，能够进行程序语言的编译期优化、链接优化、在线编译优化、代码生成。简而言之，可以作为多种编译器的后台来使用。
  - 苹果公司一直使用 GCC 作为官方的编译器。GCC 作为一款开源的编译器，一直做得不错，但 Apple 对编译工具会提出更高的要求。
  - 其一，是 Apple 对 Objective-C 语言（包括后来对 C 语言）新增很多特性，但 GCC 开发者并不买 Apple 的账——不给实现
  - 其二，GCC 的代码耦合度太高，很难独立，而且越是后期的版本，代码质量越差

- Apple 打算从零开始写 C、C++、Objective-C 语言的前端 Clang，完全替代掉 GCC。
  - Clang 是 LLVM 的前端，可以用来编译 C，C++，ObjectiveC 等语言。
  - Clang 则是以 LLVM 为后端的一款高效易用，并且与IDE 结合很好的编译前端。
  - Clang 只支持C，C++ 和 Objective-C 三种语言。

- 传统编译器工作的时候前端负责解析源代码，检查语法错误，并将其翻译为抽象的语法树（Abstract Syntax Tree）。
  - 优化器对这一中间代码进行优化，试图使代码更高效。
  - 后端则负责将优化器优化后的中间代码转换为目标机器的代码，这一过程后端会最大化的利用目标机器的特殊指令，以提高代码的性能。
- 事实上，不光静态语言如此，动态语言也符合上面这个模型，例如 Java。
  - JVM 也利用上面这个模型，将 Java 代码翻译为Java bytecode。
- 这一模型的好处是，当我们要支持多种语言时，只需要添加多个前端就可以了。
  - 当需要支持多种目标机器时，只需要添加多个后端就可以了。
  - 对于中间的优化器，我们可以使用通用的中间代码。
- 这种三段式的结构还有一个好处，开发前端的人只需要知道如何将源代码转换为优化器能够理解的中间代码就可以了，他不需要知道优化器的工作原理，也不需要了解目标机器的知识。
  - 虽然这种三段式的编译器有很多优点，并且被写到了教科书上，但是在实际中这一结构却从来没有被完美实现过。做的比较好的应该属 Java 和 . NET 虚拟机。
- GCC也将三段式做的比较好，并且实现了很多前端，支持了很多语言。但是上述这些编译器的致命缺陷是，他们是一个完整的可执行文件，没有给其它语言的开发者提供代码重用的接口。即使 GCC 是开源的，但是源代码重用的难度也比较大。

- ## 💡 [有没有可能将Java源代码编译成LLVM能接受的中间形式，以执行Java程序？ - 知乎](https://www.zhihu.com/question/33905984/answers/updated)
- 当然可以，现在 GraalVM 的 native-image 就提供一个以 LLVM 作为后端的模式。
  - 相比 GraalVM 自己的后端，使用 LLVM 为后端会损失一些性能，体积也会大一些，但 LLVM 后端也不只是花瓶，GraalVM 引入它的目的是为了更快地支持一些 GraalVM 自己还没完全支持的平台，比如 Linux RISC-V 64
  - GraalVM 上有一个基于 Truffle 的 LLVM 实现，能运行 .bc 格式的 LLVM IR，文本格式要转成 Bitcode 才行。

- AOT基本只能解决两个问题：1. 程序启动慢 2. 总之就是想发布一个没有什么依赖的比较小的可执行文件。
  - 注意，AOT极有可能不但不能加速程序运行，反而会减慢程序。
  - 不管是什么形式的AOT，在动态代码方面都要有所妥协。比如反射支持，程序或许可以帮你追踪需要反射支持的类，但是有可能会漏掉一部分，还是需要自己整理。至于动态类加载，这个就别想了，除非你编译出的可执行文件自带一个解释器甚至JIT，否则肯定没办法。

- 还有一个思路，IKVM可以在. Net平台上编译Java文件，然后. Net平台是支持AOT的，所以也许可以这样实现目标。

- 可以的，隔壁的Scala和Kotlin都做到了。而且现在的Graal也支持Java的AOT了。

- 从技术层面，这是可能的。一种不外乎是从Java的AST直接Code Gen到LLVM IR，另外一种则是从Java产生的现有IR转向LLVM IR。
# discuss
- ## 

- ## 

- ## 💡 [为什么 LLVM/Clang 能迅速发展起来？ - 知乎](https://www.zhihu.com/question/31404020/answers/updated)

- LLVM/Clang License是BSD，这条很重要, 背后是有钱的苹果
  - GCC代码搓，历史包袱巨重，而LLVM/Clang 代码组织结构非常漂亮

- 苹果已经决定放弃 clang 这个前端了，确切滴说，他们是要放弃 c，c++ 和 objective c这些 clang 所支持的前端语言，转向苹果公司自己发明的 swiftc 的前端，也就是转向支持 swift 语言
  - 将来苹果产的软件，源代码只会由 swift 编写，上至带有ui的app，下至内核，都将由 swift 编写
  - 目前当然只是在带有ui也就是图形界面的app中，得到了广泛的应用 但是苹果后续会把所有的软件，都用 swift 编写，包括苹果公司的操作系统内核
  - 苹果在短时间内，不会直接废弃 clang 不用，两者会并行和共存一段时间
  - 至于 llvm 的后端，这个苹果也已经开始用 swift 在重构一部分组件了，前端 swiftc 已经在用 swift 重构了，后端的话，苹果社区流出来的说法是，将来可能会在 c++ 的基础上，并行一个 swift 的版本
  - 这个后端的发展，就有点像是 java 后端，c++ 写的 c2 编译器和 graal jit 关系一样，目前两者还是并行，而且可能会并行很长一段时间，将来会不会最终淘汰 c2，不知道，但不排除这个可能性

- llvm虽然优点多多，模块化也做得很好，但还是不得不吐槽一点，不大好裁剪。比如c语言的支持居然和c++，objc混在一起
  - 如果你只是想要一个c编译器，结果你得到的实际是一个支持c语言，objc的c++编译器。gcc这点就很好，一个编译选项就搞定了，你可以只编译cc1而不要cc1plus。

- 主要还是企业的推动，基中最大的是苹果和谷歌。苹果发起了建立在llvm后端之上的clang前端项目。同时也给llvm社区大量的捐款和贡献代码，让llvm项目从此起飞。
  - 目前从架构上看llvm体系远比GCC现代得多，整个Linux和BSD的内核和工具编译都在逐渐切换到llvm上。

- ## 这个 execute jvm bytecode in hardware 的效果不是很好，我在想原因是不是在于 C1 Compiler 没做啥优化
- https://twitter.com/roifex/status/1750471145302941900
- 我觉得应该是有这部分原因但是大头应该还是无法获取足够多的元数据，JVM是典型的堆栈虚拟机，JIT非常依赖运行时的元数据，如果直接让硬件来执行的话很多元数据没办法获得所以效率就下去了

- ## [为什么Kafka或者是pulsar等消息队列可以在JVM上有很好的性能，但数据库却不行？ - 知乎](https://www.zhihu.com/question/628014827)
- 这完全是一个时代的问题。
  - 因为那些传统的数据库Oracle，DB2，SQL Server，MySQL，Postgres……都诞生于1980x～1990x。Java在1995年才诞生，历经各个重大迭代后在200x中期才趋于成熟。
  - 对于数据库而言，最重要的就是内存mapping，directIO，NIO，Sendfile，Off Heap手工管理内存的能力。这些API和库也是2005年以后才才慢慢成熟。
- 如果你接触过数据库的编写，就会明白数据库的核心代码主要就是
  - 查询语句解析和查询执行与优化（纯逻辑）
  - 设计磁盘的Page组成B树这种数据结构供查询
  - 读写readlog/undolog
  - 网络IO管理
  - 内存管理
- Java并不是不能写数据库，实际上Java社区最早很推荐大家用H2做测试相关和小型业务的，本地使用的数据库。但当时的行业布局基本上已经稳定了，Java在这方面已经没有机会了。没人会投入大量的人力物力去开发一个注定没有市场，但成本巨大的存储软件。

- pulsar 不清楚，不过记忆中 kafka 的协议设计上把数据面流量都尽力 offload 给内核跑的印象(通过sendfile之类？)，它的 java 代码按说都是控制面，连个 jvm 的堆外内存都用不着，吞吐量高都是内核立功。
  - 零拷贝+顺序写入，老八股了

- 功能更多的消息队列不知道，kafka这种的话换个语言实现应该也是基于零拷贝，顺序IO这些思路来优化
  - 除此之外消息队列这东西感觉会出现大量的被压缩过的序列化对象，服务端应该会不停地出现大量不需要做过多处理的临时对象，在这种情况下现代化的gc对性能来说应该是优势而不是负担，直觉上用c++实现一版kafka往死里优化性能估计也不会更强
- 通用 gc 肯定不如场景定制的性能好，细粒度控制能力也不足，只是开发成本低。

- mq基本都是顺序读写，数据库存在较多的随机读写。

- 在ap这一块，jvm对向量化支持不佳，现在很多厂都在换成c++写的执行引擎，性能提升还是挺显著的
  - 现在jdk也有vector api了
# discuss-ffi
- resources
  - [JEP 412: Foreign Function & Memory API (Incubator)](https://openjdk.org/jeps/412)

- https://github.com/zakgof/java-native-benchmark /202308/java
  - Benchmarking Java's native call APIs: JNI, JNA, JNR, BridJ and Project Panama
  - JMH performance benchmark for Java's native call APIs: JNI (via JavaCpp), JNA, JNR, Bridj and JDK JEP-424 Foreign Function/Memory APIs (Preview).

- ## 

- ## [Foreign function interface in JDK? : java_202201](https://www.reddit.com/r/java/comments/sfiq9k/foreign_function_interface_in_jdk/)
- Take a look at the Project Panama, foreign linker API and particularly this JEP 412

- Try JNI
  - This is not pure Java. It requires special native code.
  - The special native code can be automatically generated using JavaCPP

- Depending on whether you have full control of the JVM you could also look at GraalVM's native interface
# discuss-clojure
- ## 

- ## 

- ## 

- ## [Clojure和Scala的用途一致吗，他们有可比性吗？如果可比，哪个更好呢？ - 知乎](https://www.zhihu.com/question/30948736/answers/updated)
- 语法
  - Clojure采用Lisp语法，语法更简洁。
  - Scala更接近Java习惯。
- 类型系统
  - Clojure是动态类型语言，类型系统弱
  - Scala有强大的静态类型系统，支持类型推断、泛型、既存类型。
- 功能
  - Clojure的标准库小巧，容器不算丰富，能调用Java库，但Java调用clojure函数不方便。
  - Scala与Java的互交互性极好，标准库中有完备的可变容器库以及不可变容器库。社区也有好几种Spark、Play、Akka等杀手级框架。
- 性能
  - Clojure在动态类型语言中是顶尖的性能，Scala和Java性能相当，比Clojure稍快
- 宏
  - Clojure继承了Lisp『代码即数据』的思想，宏稳定易用。用Clojure进行元编程，定义DSL很方便。
  - Scala的宏复杂bug又多，只能说聊胜于无。一部分原因是因为Scala语言本身较为复杂，另一部分原因是Scala宏的设计拙劣
- 综上所述：
  - 如果你的项目大量使用元编程的编程范式，那么用更简洁的Clojure，多用宏，多定义自己的DSL，就不错。
  - 如果你使用主流的面向对象编程和函数式编程范式，那么用Scala更加高效。

- scala是多范式语言，面向对象比java的复杂多了，函数式照搬了haskell风格的，也是较复杂的流派
- clojure是lisp+函数式。为了实用，函数式的特性并不多。
  - 很多人感觉clojure比scala函数式，这个误解很大啊。
  - scala对函数式的支持很多的，加上一些第三方库，比如cats，完全可以把haskell风格的代码写出来。

- Clojure不仅是用fp模拟OOP或支持OOP, 而是解决了java OOP 的很多问题，比如接口封闭，defprotocol提供的不仅是接口，而是胖接口，extend-type宏来扩展已有类型，仅用几个组合子来表达更好的抽象，Clojure社区里面有个说法，Clojure做Java比Java还好
- Scala的OOP 也不是无脑的沿用java，Scala比java更OOP, trait, object, 伴生对象等都是在OOP上比java更远的，问题是复杂性有些没控制好，任你发挥，多继承的同时可能还要考虑线性初始化，绝对让人晕头转向，与Clojure不同的地方就是控制不好代码的熵，而Clojure只用那几个宏做有限的组合

- 评估计算机语言不能离开它的生态系统，这方面我觉得scala完胜
- Scala语言没有唯一的编码范式, 主要有三种:
  1. better Java
  2. 利用typeclass等避免纯OO的boilerplate
  3. 引入cats和shapeless, 然后把Scala的for当成Haskell的do, 然后放飞自我.

- Scala是强类型的静态语言，Clojure是动态语言。所以Scala在开发复杂应用的时候应该更有优势，毕竟很多错误在编译阶段就可以被发现。
# discuss-kotlin/scala
- ## 

- ## 

- ## #scala 和 #java 的互操作完全是 scala 单方面操 java..
- https://twitter.com/tison1096/status/1642808400995319808
- java 里面想要调用 scala 确实挺麻烦的
  - 有些东西是生成符号，带个 dollar 符啥的，看着难看但也能用。上面这个干脆是 scalac 编译时插入信息，这个只用 javac 写都写不出来
- Kotlin和Java基本可以流畅的互操作，但是如果引入第三者，整个编译又是一个灾难。通常这些 JVM 语言自己的 compiler 都兼容 Java 源代码，但是如果是三种语言的混合项目，交叉引用排不出拓扑序，就没办法编译了。

- ## 为啥 Scala 这两年没落成这个样子了，已经和 Logo 还有 AWK 一个水准了，还不如 D 语言？
- https://twitter.com/skywind3000/status/1710869742817308892
- 自己作的，频繁更新+不兼容+社区割裂
- 之前拿了一个对冲基金的 offer，他们后端就 scala 我毫不犹豫就拒了
  - 摩根斯坦利
- 难以相信，毕竟一些大数据项目还在用啊

# discuss-android
- ## 

- ## [为什么安卓不去掉 Java 语言底层？ - 知乎](https://www.zhihu.com/question/310300336)
- 在安卓诞生的时候（2009年~2010年），做手机app大多用C++和功能弱鸡阉割到不行的J2ME，iOS的OC也不是现在这个样子的，很多后面好用的特性都还没出来（ARC、队列、Block、Xib等等）。
- 安卓现在卡不是因为java，而是因为硬件不统一。细节的效果都是需要专门优化的，硬件不统一，没办法一一专门优化，那就难免在细节上出问题
- 早期安卓卡顿是因为谷歌的gc算法写的垃圾，又tm动态生成字节码。前者导致内存碎片多，系统频繁gc。后者影响性能。这就是安卓在5.0以前卡顿的原因。谷歌花了4年时间（2010～2014）解决了这两个问题。
- 从安卓6开始就已经是 ART了，App安装时已经直接生成本地代码

- ## [安卓使用java作为开发语言是不是一个错误？ - 知乎](https://www.zhihu.com/question/514831799)
- 现在影响卡顿的是什么，爱奇艺优酷抖音的app和b站的app去比比，为啥b站还是很流畅地，甚至很老的手机还能用，而爱优腾抖的app多好的机子都觉得卡，这是java的问题？ 这tm就是垃圾塞的太多了，不要再往java上怪了
- 塞班5.0于1999年3月推出，可以运行小型的J2ME程序。塞班最辉煌的时候是2005-2007年左右
  - 2005年8月17日，Google收购Android，2007年11月5日，谷歌发布Android。
  - 感觉谷歌选择安卓选择java 更多的是对标塞班，并且兼容塞班程序在安卓运行 。

- 我觉得不是。Android能成功我觉得很大程度上占了Java的光。使用Java语言（或者说是使用Java语法）使得原先开发J2ME，BlackBerry，包括原本做云测开发的人几乎可以随便翻本从入门到精通，两三天就可以上手。原来的代码可以直接使用。我们以前的J2ME写的核心代码几乎没有修改就直接用在Android上了。这对生态建设有大大的好处。
- 现实情况是你不用Java在那时候也没什么好的技术选型，它起码存量开发者大

- 如今看来java是一门垃圾语音，
  - 应用程序用js，python, php等等比java强太多
  - 系统程序用go，rust应该更好，用虚拟机来跨平台本身就是一个错误的想法，所以rust抛弃虚拟机，返璞归真
