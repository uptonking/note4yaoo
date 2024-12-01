---
title: cli-bash-shell
tags: [cli, lang-bash, shell]
created: 2024-01-16T11:58:24.868Z
modified: 2024-02-04T19:53:29.532Z
---

# cli-bash-shell

# guide

# Bash 脚本教程
- https://wangdoc.com/bash/
  - https://wangdoc.com/bash/condition
  - https://github.com/wangdoc/bash-tutorial
  - 本教程介绍 Linux 命令行 Bash 的基本用法和脚本编程

- Bash 变量名区分大小写，HOME和home是两个不同的变量。
- Bash 没有数据类型的概念，所有的变量值都是字符串。

- Bash 允许字符串放在单引号或双引号之中，加以引用。
  - 单引号用于保留字符的字面含义，各种特殊字符在单引号里面，都会变为普通字符，比如星号（*）、美元符号（$）、反斜杠（\）等
  - 双引号比单引号宽松，大部分特殊字符在双引号里面，都会失去特殊含义，变成普通字符。

- echo
  - echo "$a" 可以打印变量值

- `$?`为上一个命令的退出码，用来判断上一个命令是否执行成功。返回值是0，表示上一个命令执行成功；如果不是零，表示上一个命令执行失败

- check file exists in bash, -e vs -f
  - -e: Returns true if the file or directory exists, regardless of its type (regular file, directory, symbolic link, etc.)
  - -f: Returns true only if the file is a regular file (not a directory, symbolic link, etc.).

- Bash提供四个特殊语法，跟变量的默认值有关，目的是保证变量不为空。

```shell
# 变量var1声明, 等号两边不能有空格, 变量可以重复赋值; 读取变量用$var1
variable=value
# 如果变量的值包含空格，则必须将值放在引号中。
var1="hello world"
# 读取变量的时候，变量名也可以使用花括号{}包围，比如$a也可以写成${a}。

# 如果变量varname存在且不为空，则返回它的值，否则将它设为word，并且返回word。
# 它的目的是设置变量的默认值。${count:=0}表示变量count不存在时返回0，且将count设为0。
${varname:=word}

# 如果变量varname存在且不为空，则返回它的值，否则返回word
# 它的目的是返回一个默认值
${varname:-word}

# 如果变量名存在且不为空，则返回word，否则返回空值。
# 它的目的是测试变量是否存在
${varname:+word}

# 如果变量varname存在且不为空，则返回它的值，否则打印出varname: message，并中断脚本的执行
# 它的目的是防止变量未定义，未定义时就中断执行，抛出错误
${varname:?message}

# if
# [ -n string ]：如果字符串string的长度大于零，则判断为真。
# [ -z string ]：如果字符串string的长度为零，则判断为真。
# test命令内部的>和<，必须用引号引起来（或者是用反斜杠转义）。否则，它们会被 shell 解释为重定向操作符。
# [ integer1 -eq integer2 ]：如果integer1等于integer2，则为true。
# [ integer1 -ne inte ger2 ]：如果integer1不等于integer2，则为true。
# [ -e file ]：如果 file 存在，则为true。
# [ -d file ]：如果 file 存在并且是一个目录，则为true。

```

# blogs
- [一篇教会你写90%的shell脚本 - 知乎](https://zhuanlan.zhihu.com/p/264346586)
# tips
- ## [Why does the less-than sign not work as a replacement for cat in bash? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/106039/why-does-the-less-than-sign-not-work-as-a-replacement-for-cat-in-bash)
  - The less than and symbol (<) is opening the file up and attaching it to the standard input device handle of some application/program. But you haven't given the shell any application to attach the input to.
- the `<file` can be on either side of the command
  - `<file grep foo`; 
  - `while read line; do echo "$line"; done < file `; 

- `some-cmd < somefile` or `< somefile some-cmd`

- ## [When are square brackets required in a Bash if statement? - Stack Overflow](https://stackoverflow.com/questions/8934012/when-are-square-brackets-required-in-a-bash-if-statement)
  - The square brackets are a synonym for the `test` command
  - `test` is a command, which takes an expression and evaluates it

- ## [if statement - Are double square brackets [[ ]] preferable over single square brackets [ ] in Bash? - Stack Overflow](https://stackoverflow.com/questions/669452/are-double-square-brackets-preferable-over-single-square-brackets-in-b)
  - [[ has fewer surprises and is generally safer to use. 
  - But it is not portable - POSIX doesn't specify what it does and only some shells support it 
  - If you use [[ ]] you lose portability

- [Bash operators: "!" vs "-z" - Stack Overflow](https://stackoverflow.com/questions/51440450/bash-operators-vs-z)
  - -z STRING: returns true if the length of STRING is zero.
  - ! EXPRESSION: returns true of EXPRESSION is false
# more
