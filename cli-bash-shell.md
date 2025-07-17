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

# blogs-shell
- [一篇教会你写90%的shell脚本 - 知乎](https://zhuanlan.zhihu.com/p/264346586)
# makefile

```makefile
target... : prerequisites ...
          command
          ......
          

# 第一个是make help的注释 documentation comment
create-env-files: ## Copy the dist env files to env files
create-env-files: \
	env.d/development/common \
	env.d/development/postgresql \
	env.d/development/kc_postgresql
.PHONY: create-env-files
```

- 当直接运行make命令，后面不接target参数时，默认会生成Makefile中的第一个目标。如果要生成指定目标，需要在make命令后面接target名称。

- `$(MAKE)` is valid in a Makefile
  - MAKE is a special variable in Make that refers to the make command itself. 

- 
- 
- 

## [Makefile 光速入门](https://siyuanblog.cn/archives/makefile)

- Makefile 就是简化我们敲命令的过程。
- Makefile 实际上就是一个描述命令执行过程的文本文件，就是某种意义上的 shell 脚本，由几个部分构成：
  - target 就是要完成命令的名称
- makefile 中可以定义自己的变量，以实现更方便的编写，变量名通常用全大写来表示
  - 变量定义的 = 和 := 是有一定区别的，:= 的值在赋值时就会确定，而 = 是在使用时才确定。
- 在 makefile 中 % 表示通配符，匹配任意字符串

- 构建一个过程可能有多条命令，如果直接换行，命令是在不同的 shell 上执行的，也就是命令之间不会相互影响
  - 如果要让多条命令在一个 shell 中执行，可以使用 \ 或 ; 

## [makefile快速入门 - 冷豪 - 博客园](https://www.cnblogs.com/learnhow/p/15863951.html)

- 一个makefile文件不能出现重名的目标名，且当你执行make的时候，它会默认执行第一条编译片段，如果第一条编译片段并没有其他依赖，make不会继续向下执行
  - 在检查依赖关系时，同时会检查目标与源文件的时间戳，当源文件时间戳更新时，make会更新依赖它的链路上所有目录。

- makefile还可以通过include的方式包含其它makefile文件，因此我们也可以将公共的部分写到一起。
- 在makefile里，我们也可以编写或调用shell脚本。

- makefile也有预定义的变量。常见的有：
  - RM: 删除程序，默认值为rm -f
  - $@: 目标文件的完整名称
  - $<: 第一个依赖文件的名称
  - $+: 所有的依赖文件，以空格分开，并以出现的先后顺序，可能包含重复的依赖文件
  - $^: 所有不重复的依赖文件，以空格分开
  - CURDIR: makefile的当前路径

- wildcard: 通配符函数，表示通配某路径下的所有文件，通常我们是将所有*.cpp或*.h文件选择出来单独处理
- notdir: 获取到路径的最后一段文件名
- strip: 去掉字符串前后的空格
- shell: 用于在makefile中执行shell脚本
- patsubst 用于进行模式替换，其形式为：$(patsubst pattern, replacement, text)。

- A phony target is one that is not really the name of a file; rather it is just a name for a recipe to be executed when you make an explicit request. 
  - There are two reasons to use a phony target: to avoid a conflict with a file of the same name, and to improve performance.
  - make clean并不是为了生成一个名称为clean的文件，为了防止文件同名，可以用. PHONY来声明伪目标。

- [[教程]从零开始快速编写Makefile - 知乎](https://zhuanlan.zhihu.com/p/430029724)
- Makefile中的等号有4种，"="，":="，"?="，"+="。
  - "?="表示，如果左边的变量没有被赋值，那么将等号右边的值赋给左边的变量；如果VAR_A被赋过值了，VAR_A中的值将保持原来的值不变
  - "+="表示将等号右边的值追加到左边变量中，类似于C语言中的strcat函数
  - ":="理解为"值传递"。
  - = 允许变量的嵌套使用 `var_c = ${var_${var_a}}`

- Makefile的执行是受shell环境变量影响的，shell环境变量会直接传递到Makefile的执行过程中。
  - 可以在执行make命令时为传递环境变量的值，如果执行"make VAR_A=maybe"命令，那么执行过程中VAR_A是maybe

- 在执行make命令时，会打印Makefile里面执行的command，可以通过在command前加上 `@` 来取消打印command。

- 执行过程中也可能出现错误， 一般出现错误后，make命令会立即退出，停止编译。如果想要忽略执行过程中的错误，可以在command前加上 `-` 来忽略这条命令的执行错误。

- sinclude在找不到文件时，并不会报错，会直接跳过。利用这个机制，可以更新目标文件的依赖关系。
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

# discuss-shell

- ## 

- ## 

- ## 

- ## [curl vs wget](https://daniel.haxx.se/docs/curl-vs-wget.html)
- similarities
  - both are command line tools that can download contents from FTP, HTTP(S)
  - both support HTTP cookies

- `curl` is powered by `libcurl` - a cross-platform library with a stable API that can be used by each and everyone. (major difference)
  - curl is MIT licensed. Wget is GPL v3.
  - pipes: curl works more like the traditional Unix cat command, it sends more stuff to stdout, and reads more from stdin in a "everything is a pipe" manner. Wget is more like cp, using the same analogue.
  - More protocols: curl supports FTP(S), GOPHER(S), HTTP(S), SCP, SFTP, TFTP, TELNET, DICT, LDAP(S), MQTT, FILE, POP3(S), IMAP(S), SMB(S), SMTP(S), RTMP, RTSP and WS(S). Wget only supports HTTP(S) and FTP.
  - curl supports HTTP/0.9, HTTP/1.0, HTTP/1.1, HTTP/2 and HTTP/3 to the server and HTTP/1 and HTTP/2 to proxies. wget supports 1.0 and 1.1 and only HTTP/1 to proxies.
  - More SSL libraries and SSL support: curl can be built with one out of twelve (12!) different SSL/TLS libraries, and it offers more control and wider support for protocol details.
  - HTTP auth: curl supports more HTTP authentication methods, especially over HTTP proxies: Basic, Digest, NTLM, Negotiate and AWS v4 signatures.
  - SOCKS: curl supports SOCKS4 and SOCKS5 for proxy access. With local or proxy based name resolving.
  - curl supports HTTPS proxy, that is HTTPS to the proxy. wget does not.
  - Bidirectional: curl offers upload and sending capabilities. Wget only offers plain HTTP POST support.
  - HTTP multipart/form-data sending, which allows users to do HTTP "upload" and in general emulate browsers and do HTTP automation to a wider extent.
  - curl supports gzip, brotli, zstd and deflate Content-Encoding and does automatic decompression.
  - curl can do many transfers in parallel (-Z). wget only does serial.
  - Much more developer activity. 
  - curl comes pre-installed on macOS and Windows 10. Wget does not.

- `wget` is command line only. There's no library.
  - Recursive!: Wget's major strong side compared to curl is its ability to download recursively, or even just download everything that is referred to from a remote resource, be it a HTML page or a FTP directory listing.
  - Wget is GPL v3. curl is MIT licensed.
  - GNU: Wget is part of the GNU project and all copyrights are assigned to FSF. The curl project is entirely stand-alone and independent with no organization parenting at all with almost all copyrights owned by Daniel.
  - Wget requires no extra options to simply download a remote URL to a local file, while curl requires `-o or -O`.
  - Wget supports only GnuTLS or OpenSSL for SSL/TLS support.
  - Wget has no SOCKS support.
  - Wget enables more features by default: cookies, redirect-following, time stamping from the remote resource etc. With curl most of those features need to be explicitly enabled.
