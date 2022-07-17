---
title: job-js-concurrent-async
tags: [async, concurrent, job, js]
created: 2021-10-10T09:09:14.586Z
modified: 2021-10-10T09:30:55.386Z
---

# job-js-concurrent-async

# guide

## [async await 和 promise 的关系](https://github.com/sisterAn/JavaScript-Algorithms/issues/149)

- async/await 应该就是个语法糖，是对 Promise + Generator 的更好的封装，async/await 是后面才出现的(ES2017)，在这以前用 Generator 可以实现异步任务，如dva库的 effects 实现。
  - Promise 相当于是 JS 引擎的底层异步 API，其它的异步方案是在它的基础上构建
- 通过 typescript 或 babel 的 playground，编写 async/await 代码转换到 ES2015 的语法就会发现，可以看到输出代码内部用的其实就是迭代器去实现的

## 异步

- promise本身可以抽象一个异步操作，同时具有状态来表示异步操作的完成情况，状态可被resolve()和reject()改变。
  - Promise虽然摆脱了回调地狱，但是then的链式调用也会带来额外的阅读负担
  - Promise传递中间值非常麻烦，而async/await几乎是同步的写法，非常优雅
- ES6之前使用异步返回值的操作都需要放在回调函数中，异步结果作为回调参数，回调成为闭包
- new Promise执行程序是同步任务，会被放到主进程中去立即执行。
  - then()函数是异步任务，当promise状态落定时，回调才会进入异步队列

- ES6中使用异步返回值的操作都需要放在处理程序中，ES8的async/await旨在解决利用异步结构组织代码
  - 错误处理友好，async/await可以用成熟的try/catch，Promise的错误捕获非常冗余
  - 调试友好，Promise的调试很差，由于没有代码块，你不能在一个返回表达式的箭头函数中设置断点，如果你在一个.then代码块中使用调试器的步进(step-over)功能，调试器并不会进入后续的.then代码块，因为调试器只能跟踪同步代码的『每一步』
- 带async关键字的函数会返回一个promise对象，如果里面没有await，执行起来等同于普通函数；
  - await 要在 async 函数的内部，等待其右侧的表达式完成。
  - await会迫使异步函数让出主线程，阻塞async内后续的代码，先去执行async外的代码。
  - 等外面的同步代码执行完毕，才会执行里面的后续代码。就算await的不是promise对象，是一个同步函数，也会等这样操作

## promise

- `Promise.all()` 必须全部resolve，有一个失败就立即reject
  - takes an iterable of promises as an input, and returns a single Promise that resolves to an array of the results of the input promises. 
  - This returned promise will resolve when all of the input's promises have resolved
  - It rejects immediately upon any of the input promises rejecting or non-promises throwing an error
  - 使用 Promise.all() 执行过个 promise 时，只要其中任何一个promise 失败都会执行 reject ，并且 reject 的是第一个抛出的错误信息，只有所有的 promise 都 resolve 时才会调用 .then 中的成功回调
  - 但大多数场景中，我们期望传入的这组 promise 无论执行失败或成功，都能获取每个 promise 的执行结果，为此，ES2020 引入了 Promise.allSettled()
  - 适合promise彼此相互依赖，其中任何一个被 reject ，其它都失去了实际价值

- Promise.allSettled() 
  - returns a promise that resolves after all of the given promises have either fulfilled or rejected, with an array of objects that each describes the outcome of each promise
  - In comparison, the Promise returned by Promise.all() may be more appropriate if the tasks are dependent on each other / if you'd like to immediately reject upon any of them rejecting.
  - 可以获取数组中每个 promise 的结果，无论成功或失败
  - 适合promise彼此不依赖，其中任何一个被 reject ，对其它都没有影响
  - 期望知道每个 promise 的执行结果
