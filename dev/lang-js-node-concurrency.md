---
title: lang-js-node-concurrency
tags: [concurrent, js, lang, node]
created: '2021-08-30T06:41:24.479Z'
modified: '2021-08-30T06:41:48.713Z'
---

# lang-js-node-concurrency

# discuss

- ## 

- ## 

- ## 

- ## child_process 是用于创建子进程和父子进程通信的，有4个 api： spawn、exec、execFile、fork
- https://www.zhihu.com/pin/1413231233476685824
- spawn 是用 shell 来跑一段命令，返回一个 stream
- exec 基于 spawn，只是对返回的 stream 做了封装，直接可以拿到 buffer，只不过有上限，可以用  maxBuffer 设置
- execFile 没有跑 shell 环境，可以执行可执行文件，当然也可以跑 shell
- fork 则是用于执行 js 文件的
  - cluster 的 fork 是创建多个子进程以及通信的，会执行到分叉的地方
- 而关于通信：cp 的 api 都支持管道的 pipe，而所有的进程创建方式都支持事件的方式，底层是消息队列
