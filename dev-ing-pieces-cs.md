---
title: dev-ing-pieces-cs
tags: [cs, dev]
created: 2020-03-28T19:35:12.408Z
modified: 2021-03-29T19:29:56.558Z
---

# dev-ing-pieces-cs

# pieces

- ## 

- ## 

- ## [原子变量、关中断、信号量、自旋锁](https://www.zhihu.com/question/332113890/answer/2071397624)
- Linux上实现数据同步主要有五个工具：原子变量、中断控制、自旋锁、信号量(semaphore)、读写锁

- 原子操作需要底层操作系统支持，X86 CPU支持许多原子指令，C语言正是通过嵌入汇编代码调用这些原子指令来实现原子操作，而Java是在JVM层面对原子操作进行了实现。
- 上述原子操作虽然可以完成同步操作，但是只能对付一些简单的单体变量，对于复杂的数据结构，如果使用原子操作，可想而知代码的复杂程度有多大。
- 在这个时候可以考虑通过关闭中断，从而实现相应的代码控制。
  - x86平台上的CPU关闭中断、开启中断指令是cli、sti，其主要是对CPU的eflags寄存的IF位进行设置，CPU据此来决定是否响应中断信号。
- 简单来说，在关闭中断的时候，把之前的状态存入地址为flag的内存中；在开启中断时，究竟是否开启中断，是由flag地址中存储的值来确定的！（即进行关闭中断操作之前的中断状态）
  - 注：内存中的flag只是用来保存的，CPU是否中断由寄存器中的值而定。
  - 注：这里没有区分中断的优先级，但是实际的操作系统中，低级中断应该被高级中断所打断。
- 中断完美解决了原子操作只能针对单体变量的情况，但是——中断只能控制单核CPU，在多核CPU的情况下，又会遇到并发冲突的问题了，这个时候就需要使用“自旋锁”。
  - x86 提供了一个原子交换指令：xchg——让寄存器的值和内存空间的值进行交换。

- 以上解决同步的方式都不适合长等待，利用自旋锁这种方式去获取需要一定时间准备的资源，并且会造成CPU的时间消耗。
- 试想，能不能有一种机制，当资源准备好了之后，提醒CPU去获取呢？
  - 还真有，那就是在1965年由荷兰学者Edsger Dijkstra（没错，就是提出那个算法的男人）提出的信号量机制。
- 信号量机制由三个环节组成：
  - 等待：程序等待资源准备好
  - 互斥：同时只有一个程序可以访问资源
  - 唤醒：资源准备好之后唤醒固定程序

- ## [互斥锁（mutex）的底层原理是什么](https://www.zhihu.com/question/332113890/answer/1052024052)
- 所谓的锁，在计算机里本质上就是一块内存空间。
  - 当这个空间被赋值为1的时候表示加锁了，被赋值为0的时候表示解锁了，仅此而已。
  - 多个线程抢一个锁，就是抢着要把这块内存赋值为1。
  - 在一个多核环境里，内存空间是共享的。
  - 每个核上各跑一个线程，那如何保证一次只有一个线程成功抢到锁呢？
  - 你或许已经猜到了，这必须要硬件的某种guarantee。
- 硬件层
- CPU如果提供一些用来构建锁的atomic指令，譬如x86的CMPXCHG（加上LOCK prefix），能够完成atomic的compare-and-swap （CAS），用这样的硬件指令就能实现spin lock
  - 本质上LOCK前缀的作用是锁定系统总线（或者锁定某一块cache line）来实现atomicity，可以了解下基础的缓存一致协议譬如MSEI。
  - 简单来说就是，如果指令前加了LOCK前缀，就是告诉其他核，一旦我开始执行这个指令了，在我结束这个指令之前，谁也不许动。
  - 这样便实现了一次只能有一个核对同一个内存地址赋值。

- 操作系统层
  - 一个spin lock就是让没有抢到锁的线程不断在while里面循环进行compare-and-swap，燃烧CPU
  - 如果需要长时间的等待，这样反复CAS轮询就比较浪费资源，这个时候程序可以向操作系统申请被挂起，然后持锁的线程解锁了以后再通知它。
  - 这样CPU就可以用来做别的事情，而不是反复轮询。但是OS切换线程也需要一些开销，所以是否选择被挂起，取决于大概是否需要等很长时间，如果需要，则适合挂起切换为别的线程。
- 线程向操作系统请求被挂起是通过一个系统调用，在linux上的实现就是futex，
  - 宏观来讲，OS需要一些全局的数据结构来记录一个被挂起线程和对应的锁的映射关系，这样一个数据结构天然是全局的，因为多个OS线程可能同时操作它。
  - 所以，实现高效的锁本身也需要锁。有没有一环套一环的感觉？
  - futex的巧妙之处就在于，它知道访问这个全局数据结构不会太耗时，于是futex里面的锁就是spin lock。
  - linux上pthread mutex的实现就是用的futex。

- 用户态的锁
  - 像Goroutine线程就是go runtime来调度的，而不是OS，所以go routine线程切换的开销要远小于OS线程切换的开销。
  - Goroutine的本质就是一个coroutine，这种轻量的线程在很多语言的runtime里面都有实现。
  - 最近Java也有了（project loom）。

- 前面都是最底层的锁，用这些底层锁还可以构建更上层的锁。
  - Condition variable，semaphore(信号量)，RW lock之类的以后再写。

- ## [DSL是什么](https://www.shuzhiduo.com/A/VGzl44v1zb/)
- DSL 是 Domain Specific Language 的缩写，它不是一种通用的语言，而是为了解决某一类特殊领域的问题而发明的专用语言。
- SQL 和 AWK 这种语言都是 DSL，不能解决通用的问题，但是在自己的领域能够大大提升工作效率。
- 正则表达式 (regular expression) 就可以看作是一个 DSL, 有着自己的语法，目的清晰明确，着力解决字符匹配问题。
- 注意：正则表达式本身并不能解决字符匹配问题，只是一种描述匹配目标的语言，执行环境会对正则表达式进行解析，并使用相关的算法进行实际的字符匹配。

- DSL与传统意义上的通用编程语言 C、Java 以及 Python 完全不同。
  - 通用的计算机编程语言是可以用来编写任意计算机程序的，并且能表达任何的可被计算的逻辑，同时也是图灵完备的。
  - 而DSL并不是图灵完备的，它们的表达能力有限，只是在特定领域解决特定任务的。
  - 最常见的 DSL 包括 Regex正则表达式以及 HTML & CSS：
- Regex正则表达式仅仅指定了字符串的 Pattern，其引擎就会根据 Pattern 判断当前字符串跟正则表达式是否匹配。
  - 正则表达式有自己的语法规范（元字符，运算符的优先级等），犹如一门微型语言，嵌入到通用编程语言 C、Java 以及 Python等里面。
- SQL也属于DSL，虽然可以定义变量和函数，但是不能编写任意的计算机程序，它就无法实现界面编程，而C、Java 以及 Python都可以。这就是DSL的特点，只面向特定领域。

- ## [There is no such thing as the Spread Operator in JavaScript!](https://levelup.gitconnected.com/there-is-no-such-thing-as-the-spread-operator-in-javascript-9c4e4dbd8a02)
- What is the precedence of the Spread Operator? 
  - The correct answers is: It does not matter, because there is no such thing as Spread Operator in JavaScript!
- Another worth-mentioning point is that “An operator is a builtin function [..] that evaluates to exactly one value.”. If we try to run a statement like const `a = …b` in our Web Console, where b is an array, then we’ll `SyntaxError` .
- The way that the Spread Syntax works, is by **evaluating its arguments first, and then spreading the result**. 
  - Thus, `[…a || b]` behaves exactly the same way as `[…(a || b)]` . 
  - Putting a set of parentheses around `a || b` expression helps to remove the ambiguity.

> As a practical reference, Spread Syntax’s arguments are evaluated first and then spread.

- ## [Thunk 是什么？](https://zhuanlan.zhihu.com/p/103908179)
- 我们在很多文章或者第三方库中均见到过 Thunk 这个词出现。但其含义着实难以理解
- 在编程语言刚起步的时候，有不同的求值策略，即函数的参数该在什么时候求值。
  - 其中一种叫 传值调用（call by value）， 顾名思义就是在函数被调用前其参数的值就已经被编译器给算好了，每次调用函数都会用同样的参数值。
  - 另一种策略叫 传名调用（call by name），也就是只有当函数真正被调用的时候才去计算参数的值（惰性求值），在此过程中编译器其实已经把惰性求值的过程包装成了一个名叫 Thunk 辅助函数，函数被调用时，先调这个辅助函数求出参数值，再进入函数主体。这也许是最早 Thunk 这个概念被使用的时候了。
- Thunk 是一类函数的别名，主要特征是对另外一个函数添加了一些额外的操作，类似装饰器。
  - 其主要用途为延迟函数执行（惰性求值）或者给一个函数执行前后添加一些额外的操作。
- 对于我们开发者来说我们基本不用关心函数参数是怎么求值的，一般我们使用的编程语言都已经决定好了。
  - 比如JavaScript，就是用的 传值调用 策略。

```JS
// ThunkActionCreator
function fetchUser(id) {
  // 返回的这个函数是一个 Thunk, 或者叫 ThunkAction
  return async ({ dispatch }) => {
    // 额外的异步API调用
    const user = await api.getUser(id);
    // 此时才真正dispatch action
    dispatch({ type: 'UPDATE_USER', payload: user });
  }
}
```

```js
const util = require('util');
const fs = require('fs');​
// stat函数是一个 Thunk
// - 只有执行stat的时候才会执行真正额fs.stat函数
// - stat还把fs.stat包装成了具有promise接口的函数
const stat = util.promisify(fs.stat);
stat('.').then((stats) => {
  // Do something with `stats`
}).catch((error) => {
  // Handle the error.
});
```

- ## linux的硬链接与软链接

- 现代操作系统为解决信息能独立于进程之外被长期存储引入了文件，文件作为进程创建信息的逻辑单元可被多个进程并发使用
- Linux与其他类UNIX系统一样并不区分文件与目录：目录是记录了其他文件名的文件
- 文件有文件名与数据，这在Linux上被分成两个部分：用户数据 (user data) 与元数据 (metadata)
  - 用户数据，即文件数据块 (data block)，数据块是记录文件真实内容的地方
  - 元数据则是文件的附加属性，如文件大小、创建时间、所有者等信息
    - 在Linux中，元数据中的inode号（inode 是文件元数据的一部分但其并不包含文件名，inode 号即索引节点号）才是文件的唯一标识而非文件名
    - 文件名仅是为了方便人们的记忆和使用，系统或程序通过inode号寻找正确的文件数据块
    - 查看inode号可使用命令 stat 或 ls -i
- 为解决文件的共享使用，Linux系统引入了两种链接：硬链接 (hard link) 与软链接（又称符号链接，即 soft link 或 symbolic link）
  - 链接为Linux系统解决了文件的共享使用，还带来了隐藏文件路径、增加权限安全及节省存储等好处
- 若一个inode号对应多个文件名，则称这些文件为 `硬链接` 。换言之，硬链接就是同一个文件使用了多个别名，硬链接的特点：
  - 文件有相同的inode及data block；
  - 只能对已存在的文件进行创建；
  - 不能交叉文件系统进行硬链接的创建；
  - 不能对目录进行创建，只可对文件创建；
  - 删除一个硬链接文件并不影响其他有相同inode号的文件
  - 硬链接不能对目录创建是受限于文件系统的设计。Linux文件系统中的目录均隐藏了两个个特殊的目录：当前目录（.）与父目录（..）。查看这两个特殊目录的 inode 号可知其实这两目录就是两个硬链接。若系统允许对目录创建硬链接，则会产生目录环
- 若文件用户数据块中存放的内容是另一文件的路径名的指向，则该文件就是 `软连接` 。软链接就是一个普通文件，只是数据块内容有点特殊。软链接有自己的inode号以及用户数据块。因此软链接的创建与使用没有类似硬链接的诸多限制：
  - 软链接有自己的文件属性及权限等；
  - 可对不存在的文件或目录创建软链接；
  - 软链接可交叉文件系统；
  - 软链接可对文件或目录创建；
  - 创建软链接时，链接计数 i_nlink 不会增加；
  - 删除软链接并不影响被指向的文件，但若被指向的原文件被删除，则相关软连接被称为死链接（即dangling link，若被指向路径文件被重新创建，死链接可恢复为正常的软链接）。

- ## 动态链接库 dll

- ref
  - [咱不知道的动态链接库小细节 - Oldpan的个人博客](https://oldpan.me/archives/something-about-so-we-dont-know)
  - [动态链接库和静态链接库 — Dynamic Library and Static Library » Lu.dev](https://lucky521.github.io/blog/tech/2016/07/14/dylib-staticlib.html#%E5%8A%A8%E6%80%81%E5%BA%93%E7%9A%84%E7%94%9F%E6%88%90-1)

- 大多数操作系统将解析外部引用（比如库）作为加载过程的一部分，可执行文件包含一个叫做import directory的表，该表的每一项包含一个库的名字。根据表中记录的名字，装载程序在硬盘上搜索需要的库，然后将其加载到内存中预先不确定的位置，之后根据加载库后确定的库的地址更新可执行程序。可执行程序根据更新后的库信息调用库中的函数或引用库中的数据。这种类型的动态加载称为装载时加载，被包括Windows和Linux的大多数系统采用，最复杂的工作之一就是 **加载时链接**。
- 有些操作系统可能在运行时解析引用。在这些系统上，可执行程序调用操作系统API，将库的名字，函数在库中的编号和函数参数一同传递。操作系统负责立即解析然后代表应用调用合适的函数。这种动态链接叫做 **运行时链接** 。因为每个调用都会有系统开销，运行时链接要慢得多，对应用的性能有负面影响。
- 可以动态链接的库，在Windows上是dynamic link library (DLL)，在UNIX或Linux上是Shared  Library。库文件是预先编译链接好的可执行文件，存储在计算机的硬盘上。大多数情况下，同一时间多个应用可以使用一个库的同一份拷贝，操作系统不需要加载这个库的多个实例。  
- Windows和Linux的加载时链接是由操作系统来完成的，格式在不同的系统下有不同的区别，但是原理还是一样的。linux下文件的类型是不依赖于其后缀名的，但一般来讲：
  - .o是目标文件, 相当于windows中的.obj文件
  - .so为共享库, 是shared object, 用于动态连接的, 和dll差不多
  - .a为静态库, 是好多个.o合在一起, 用于静态连接
  - .la为libtool自动生成的一些共享库，主要记录了一些配置信息。
- 通常把一些公用函数制作成函数库, 供其它程序使用，函数库分为静态库和共享库
- 程序函数库简单的说就是一个文件包含了一些编译好的代码和数据，这些编译好的代码和数据可以供其他的程序使用。程序函数库可以使整个程序更加模块化，更容易重新编译，而且更方便升级。程序函数库可分为3种类型：静态函数库（static libraries）、共享函数库（shared libraries）和动态加载函数库（dynamically loaded libraries）。
- 静态函数库是在程序执行前就加入到目标程序中去了；而共享函数库则是在程序启动的时候加载到程序中，它可以被不同的程序共享；动态加载函数库则可以在程序运行的任何时候动态的加载
- 静态函数库实际上就是简单的一个普通的目标文件的集合，一般来说习惯用“.a”作为文件的后缀, 静态库函数允许程序员把程序link起来而不用重新编译代码，节省了重新编译代码的时间。
- 共享函数库中的函数是在当一个可执行程序在启动的时候被加载。每个共享函数库都有个特殊的名字，称作“soname”。Soname名字命名必须以“lib”作为前缀，然后是函数库的名字，然后是“.so”，最后是版本号信息。不过有个特例，就是非常底层的C库函数都不是以lib开头这样命名的。当可执行程序需要在自己的程序中列出这些他们需要的共享库函数的时候，它只要用soname就可以了
- 动态加载的函数库Dynamically loaded (DL) libraries是一类函数库，它可以在程序运行过程中的任何时间加载，们特别适合在函数中加载一些模块和plugin扩展模块的场合。Linux系统下，DL函数库与其他函数库在格式上没有特殊的区别，创建的时候是标准的object格式。主要的区别就是 这些函数库不是在程序链接的时候或者启动的时候加载，而是通过一个API来打开一个函数库，寻找符号表，处理错误和关闭函数库。通常C语言环境下，需要包含这个头文件。
- 动态链接库在unix下，习惯以 .so 为文件名结尾（通常还以 lib 开头）。而Windows下是以 . DLL 为文件后缀。如果需要运行时主动加载一个动态链接库，windows下可以使用 LoadLibrary 这个 kernel API (在 kernel32.dll 中)；unix 下是用 dlopen 。Windows 下找到 dll 中导出符号的地址，可以用 GetProcAddress ，而 unix 也有对应的 api。这些相互对应的api，似乎预示着对等的功能，但事实上是有区别的。
- DLL 事实上和 EXE 文件一样，同属 PE 格式的执行文件。对于隐式的引用外部符号，需要把外部符号所在的位置写在 PE 头上。PE 加载器将从 PE 头上找到依赖的符号表，并加载依赖的其它 DLL 文件。
- so 文件大多为 elf 执行文件格式。当它们需要的外部符号，可以不写明这些符号所在的位置。也就是说，通常 so 文件本身并不知道它依赖的那些符号在哪些 so 里面。这些符号是由调用 dlopen 的进程运行时提供的。而 unix 下的执行文件本身会暴露自己静态链接的符号，（可以是自己本身实现的，或者是从静态库 .a 文件里链入的）。dlopen 将把这些符号通报给 dlopen 加载的 .so 文件，最终完成动态链接。
