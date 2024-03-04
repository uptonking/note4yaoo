---
title: lang-python-community-async
tags: [async, community, python]
created: 2023-08-28T06:15:02.919Z
modified: 2023-08-28T06:15:13.277Z
---

# lang-python-community-async

# guide

# discuss
- ## 

- ## 

- ## 

- ## js 的 await 语法和 python 几乎就是一样的
- https://twitter.com/LaiskyCai/status/1764462751227777066
  - 我觉得跟 js 完全一模一样啊，应该说当初 ECMA6 设计的时候就是照着 py 抄的。
  - py 会传染 js 也会传染。想要不传染的解耦写法也是类似的。异步编程的基本功就是要掌握 同步/异步 的互相转换。比如同步等异步、异步包同步。

- js传染没那么严重，在同步里写也可以用then，py就没得选择了，主要是js天生异步吧

- 感觉 JS 这块语法更像 C# 的，两者都是 ECMA 的东西。

- ## python http.server 的性能过于差了
- https://twitter.com/yihong0618/status/1763402989996540391
- py 的主要问题是同步吧，其实任意换个异步框架就行了。用 aiohttp 几行写一个应该也行。
- aiohttp不知道能否解决传输耗时慢的问题。静态文件web服务器的逻辑就两步吧，读文件，网络传输。读文件能否也换成某种非阻塞文件系统I/O？
  - 前些年都是用 threadpool 模拟的，不知道近几年有没有 io_uring 的库。

- caddy file sever 还行

- nginx的webdav不好用。我家里的NAS把dufs放在nginx后面作为文件共享使用。

- https://twitter.com/Ehco1996/status/1763386830781812860
  - py 有什么 web 框架可以 serve static 文件了咩？
  - pod 里始终要挂个 NGINX 还是太难受了，不如 golang 一把梭

- python -m http.server
  - python处理这种静态文件性能不行，文件大一点或者F5多按几下就挂了
