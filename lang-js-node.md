---
title: lang-js-node
tags: [js, lang, node]
created: '2019-09-12T02:32:06.774Z'
modified: '2020-07-14T09:26:55.226Z'
---

# lang-js-node

## pieces

-  ### node-path
- `path.join(path1，path2，path3.......)`
  - 用平台特定的分隔符把全部给定的path片段连接到一起，并规范化生成的路径
  - 先解析相对路径..，再拼接返回，path片段/docs, ./docs, docs三种方式处理无差别
  - path片段前的 `./` 可有可无，只进行路径拼接
  - `path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');`
    - 返回: `/foo/bar/baz/asdf`
- `path.resolve([from...],to)`
  - 按参数从左向右，把路径片段的序列解析为一个**绝对路径**，一定生成绝对路径
  - 先解析路径，再生成绝对路径返回，./docs, docs相同，/docs会作为绝对路径起点
  - `path.resolve('/foo', '/bar', 'baz')` 会返回 `/bar/baz`
  - `path.relative(from,to)`, 可看做resolve的逆运算，返回to目录的相对路径
- `__dirname`
  - Node.js中的文件路径大概有 __dirname, __filename, process.cwd(), ./ 或者 ../
    - 前3者都是绝对路径
  - `__dirname` ：    当前执行文件所在目录的绝对路径
  - `__filename` ：   当前执行文件的带有完整绝对路径文件名的绝对路径
  - `process.cwd()` ：当前执行node命令时候的文件夹目录名，绝对路径 
  - `./` ：跟process.cwd()一样，返回node命令时所在的文件夹的绝对路径
  - `require(./a.js)` ：当node遇到require时，会相对当前执行文件查找
  - 建议：只在require()中才使用相对路径(./, ../)的写法，其他地方一律绝对路径

### events

- Much of the Node.js core API is built around an idiomatic(地道的，符合习惯的，独特的) asynchronous event-driven architecture 
  - in which certain kinds of objects (called "emitters") emit named events that cause Function objects ("listeners") to be called.
  - For instance: 
    - a `net.Server` object emits an event each time a peer connects to it; 
    - a `fs.ReadStream` emits an event when the file is opened; 
    - a `stream` emits an event whenever data is available to be read.
- All objects that emit events are instances of the `EventEmitter` class. 
  - These objects expose an `eventEmitter.on()` function that allows one or more functions to be attached to named events emitted by the object. 
- When the `EventEmitter` object emits an event, all of the functions attached to that specific event are called **synchronously**. 
  - Any values returned by the called listeners are ignored and discarded.
- The `EventEmitter` calls all listeners synchronously in the order in which they were registered. 
  - This ensures the proper sequencing of events and helps avoid race conditions and logic errors. 
  - When appropriate, listener functions can switch to an asynchronous mode of operation using the `setImmediate()` or `process.nextTick()` methods

``` JS
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  setImmediate(() => {
    console.log('this happens asynchronously');
  });
});
myEmitter.emit('event', 'a', 'b');
```

- The `EventEmitter` class is defined and exposed by the `events` module
  - All EventEmitters emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.
  - The `EventEmitter` instance will emit its own '`newListener'` event before a listener is added to its internal array of listeners.

- `emitter.emit(eventName[, ...args])` (v0.1.26)
  - Synchronously calls each of the listeners registered for the event named `eventName`, 
    - in the order they were registered, passing the supplied arguments to each.

- `emitter.addListener(eventName, listener)` (v0.1.26)
  - Alias for `emitter.on(eventName, listener)` (v0.1.101)
  - Adds the `listener` function to the end of the listeners array for the event named `eventName`. 
  - No checks are made to see if the listener has already been added. 
  - Multiple calls passing the same combination of eventName and listener will result in the listener being added, and called, multiple times.
  - By default, event listeners are invoked in the order they are added. 
  - The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

- `emitter.once(eventName, listener)`
  - Adds a one-time `listener` function for the event named `eventName`. 
  - The next time `eventName` is triggered, this listener is removed and then invoked.

- `emitter.off(eventName, listener)` (v10.0.0)
  - Alias for `emitter.removeListener(eventName, listener)` (v0.1.26)
  - Removes the specified `listener` from the listener array for the event named `eventName`.
  - removeListener() will remove, at most, one instance of a listener from the listener array. 
  - If any single listener has been added multiple times to the listener array for the specified eventName, then removeListener() must be called multiple times to remove each instance.
  - Once an event is emitted, all listeners attached to it at the time of emitting are called in order. 
    - This implies that any removeListener() or removeAllListeners() calls after emitting and before the last listener finishes execution will not remove them from emit() in progress. 
    - Subsequent events behave as expected.

``` JS
const myEmitter = new MyEmitter();

const callbackA = () => {
  console.log('A');
  myEmitter.removeListener('event', callbackB);
};
const callbackB = () => {
  console.log('B');
};

myEmitter.on('event', callbackA);
myEmitter.on('event', callbackB);

// callbackA removes listener callbackB but it will still be called.
// Internal listener array at time of emit is[callbackA, callbackB]
myEmitter.emit('event');
// Prints:
//   A
//   B

// callbackB is now removed.
// Internal listener array is [callbackA]
myEmitter.emit('event');
// Prints:
//   A
```

  - Because listeners are managed using an internal array, calling this will change the position indices of any listener registered after the listener being removed. 
  - This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the emitter.listeners() method will need to be recreated.
  - When a single function has been added as a handler multiple times for a single event, removeListener() will remove the most recently added instance. 

- **NodeEventTarget vs. EventEmitter**
- A NodeEventTarget is not an instance of EventEmitter and cannot be used in place of an EventEmitter in most cases.
  - Unlike EventEmitter, any given listener can be registered at most once per event type. Attempts to register a listener multiple times are ignored.
  - The NodeEventTarget does not implement any special default behavior for events with type 'error'.

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
