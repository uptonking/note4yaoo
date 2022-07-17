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

- ## 

- ## 

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
