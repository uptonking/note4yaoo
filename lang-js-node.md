---
title: lang-js-node
tags: [js, lang, node]
created: '2019-09-12T02:32:06.774Z'
modified: '2020-07-14T09:26:55.226Z'
---

# lang-js-node

## pieces

- **node-path**
- `path.join(path1，path2，path3.......)`
  - 先解析相对路径..，再拼接返回，path片段/docs, ./docs, docs三种方式处理无差别
  - 用平台特定的分隔符把全部给定的path片段连接到一起，并规范化生成的路径
  - path片段前的 `./` 可有可无，只进行路径拼接
  - `path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');`
    - 返回: `/foo/bar/baz/asdf`
- `path.resolve([from...],to)`
  - 先解析路径，再生成绝对路径返回，./docs, docs相同，/docs会作为绝对路径起点
  - 按参数从左向右，把路径片段的序列解析为一个**绝对路径**，一定生成绝对路径
  - `path.resolve('/foo', '/bar', 'baz')` 会返回 `/bar/baz`
- `__dirname`
  - Node.js中的文件路径大概有 __dirname, __filename, process.cwd(), ./ 或者 ../
    - 前3者都是绝对路径
  - `__dirname` ：    当前执行文件所在目录的绝对路径
  - `__filename` ：   当前执行文件的带有完整绝对路径文件名的绝对路径
  - `process.cwd()` ：当前执行node命令时候的文件夹目录名，绝对路径 
  - `./` ：跟process.cwd()一样，返回node命令时所在的文件夹的绝对路径
  - `require(./a.js)` ：当node遇到require时，会相对当前执行文件查找
  - 建议：只在require()中才使用相对路径(./, ../)的写法，其他地方一律绝对路径

## 多线程

- Node.js保持了JavaScript在浏览器中单线程的特点
  - 它的优势是没有线程间数据同步的性能消耗也不会出现死锁的情况
  - 所以它是线程安全并且性能高效的
- 单线程有它的弱点，无法充分利用多核CPU资源，CPU密集型计算可能会导致I/O阻塞，以及出现错误可能会导致应用崩溃。
- 为了解决单线程的缺点，现在提出了很多解决方案
- 浏览器端： HTML5制定了Web Worker标准
  - Web Worker的作用就是为JavaScript创造多线程环境，允许主线程创建Worker线程，将一些任务分配给后者运行 
- Node端：采用了和Web Worker相同的思路来解决单线程中大量计算问题 ，官方提供了child_process模块和cluster模块
  - cluster底层是基于child_process实现
  - child_process、cluster都是用于创建子进程，然后子进程间通过事件消息来传递结果
  - 这个可以很好地保持应用模型的简单和低依赖，从而解决无法利用多核CPU和程序健壮性的问题
  - cluster底层就是child_process，master进程做总控，启动1个agent和n个worker，agent来做任务调度，获取任务，并分配给某个空闲的worker来做。
    - 每个worker进程通过使用 `child_process.fork()` 函数，基于 IPC 实现与master进程间通信
    - fork出的子进程拥有和父进程一致的数据空间、堆、栈等资源，但是是独立的，也就是说二者不能共享这些存储空间。那我们直接用fork自己实现不就行了。
    - 这样的方式仅仅实现了多进程。多进程运行还涉及父子进程通信，子进程管理，以及负载均衡等问题，这些特性cluster帮你实现了
- child_process模块通过它可以开启多个子进程，在多个子进程之间可以共享内存空间，可以通过子进程的互相通信来实现信息的交换
- Node10提供了实验性质的 worker_threads 模块，才让Node拥有了多工作线程，从Node12开始成为正式标准
  - Workers (threads) are useful for performing CPU-intensive JavaScript operations. 
  - They will not help much with I/O-intensive work. 
  - Node.js’s built-in asynchronous I/O operations are more efficient than Workers can be.
- Node.js 通过提供 cluster、child_process API 创建子进程的方式来赋予Node.js “多线程”能力
  - 但是这种创建进程的方式会牺牲共享内存，并且数据通信必须通过json进行传输，有一定的局限性和性能问题
- 基于此，Node.js提供了worker_threads，它比child_process或cluster更轻量
  - 与child_process或cluster不同，worker_threads可以有效地共享内存，通过传输ArrayBuffer实例或共享SharedArrayBuffer实例来实现
  - JavaScript和Node.js没有线程，只有基于Node.js架构的多工作线程
