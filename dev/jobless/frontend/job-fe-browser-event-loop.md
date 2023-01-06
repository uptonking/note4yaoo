---
title: job-fe-browser-event-loop
tags: [browser, dom, frontend, job]
created: 2021-09-23T08:23:18.415Z
modified: 2021-10-10T09:18:01.462Z
---

# job-fe-browser-event-loop

# guide

# event loop

# [JavaScript中的Event Loop（事件循环）机制](https://segmentfault.com/a/1190000022805523)
- JavaScript是单线程，非阻塞的
  - JavaScript的主要用途是与用户互动，以及操作DOM
  - 即使H5提出了web worker标准，它有很多限制，受主线程控制，是主线程的子线程。

- 非阻塞：通过 event loop 实现。

- 任务队列: 
  - 异步代码的执行，遇到异步事件不会等待它返回结果，而是将这个事件挂起，继续执行执行栈中的其他任务。
  - 当异步事件返回结果，将它放到事件队列中，被放入事件队列不会立刻执行起回调，
  - 而是等待当前执行栈中所有任务都执行完毕，主线程空闲状态，主线程会去查找事件队列中是否有任务，如果有，则取出排在第一位的事件，并把这个事件对应的回调放到执行栈中，然后执行其中的同步代码。

## 浏览器的事件循环

- 为什么要引入微任务
  - 页面渲染事件，各种IO的完成事件等随时被添加到任务队列中，一直会保持先进先出的原则执行，我们不能准确地控制这些事件被添加到任务队列中的位置
  - 有高优先级的任务需要尽快执行，那么一种类型的任务就不合适了，所以引入了微任务队列

- 宏任务
  - script(整体代码)
  - setTimeout()/setInterval()
  - postMessage
  - I/O
  - UI交互事件

- 微任务
  - new Promise().then(回调)
  - MutationObserver(html5 新特性)

- 在当前执行栈为空时，主线程会查看微任务队列是否有事件存在
  - 存在，依次执行队列中的事件对应的回调，直到微任务队列为空，然后去宏任务队列中取出最前面的事件，把当前的回调加到当前指向栈。
  - 当前执行栈执行完毕后时会立刻处理所有微任务队列中的事件，然后再去宏任务队列中取出一个事件。
- 同一次事件循环中，微任务永远在宏任务之前执行。

- 在事件循环中，每进行一次循环操作称为 tick，每一次 tick 的任务处理模型是比较复杂
  - 执行一个宏任务（栈中没有就从事件队列中获取）
  - 执行过程中如果遇到微任务，就将它添加到微任务的任务队列中
  - 宏任务执行完毕后，立即执行当前微任务队列中的所有微任务（依次执行）
  - 当前宏任务执行完毕，开始检查渲染，然后GUI线程接管渲染
  - 渲染完毕后，JS线程继续接管，开始下一个宏任务（从事件队列中获取）
- 总结一下执行的顺序：
  - 执行宏任务，然后执行该宏任务产生的微任务，若微任务在执行过程中产生了新的微任务，则继续执行微任务，微任务执行完毕后，再回到宏任务中进行下一轮循环

## Node下的事件循环

- 表现出的状态与浏览器大致相同。
- node 中事件循环的实现依赖 libuv 引擎。

- node版本更新到11之后，Event Loop运行原理发生了变化，一旦执行一个阶段里的一个宏任务(setTimeout, setInterval和setImmediate)就立刻执行微任务队列，跟浏览器趋于一致

- node中事件循环的顺序
  - 外部输入数据 --> 轮询阶段（poll） --> 检查阶段(check) --> 关闭事件回调阶段(close callback) --> 定时器检查阶段(timer) --> I/O 事件回调阶段(I/O callbacks) --> 闲置阶段(idle, prepare) --> 轮询阶段

- 各阶段
  - 轮询阶段(poll)
    - 等待新的I/O事件，node在一些特殊情况下会阻塞在这里。
    - 用于等待还未返回的 I/O 事件，比如服务器的回应、用户移动鼠标等等。
    - 这个阶段的时间会比较长。如果没有其他异步任务要处理（比如到期的定时器），会一直停留在这个阶段，等待 I/O 请求返回结果。
  - 检查阶段(check)
    - setImmediate()的回调会在这个阶段执行。
  - 关闭事件回调阶段(close callbacks)
    - 例如socket.on('close', ...)这种close事件的回调
  - 定时器检测阶段(timers)
    - 这个阶段执行定时器队列中的回调如 setTimeout() 和 setInterval()。
    - 进入这个阶段后，主线程会检查一下当前时间，是否满足定时器的条件。如果满足就执行回调函数，否则就离开这个阶段。
  - I/O事件回调阶段(I/O callbacks)
    - 这个阶段执行几乎所有的回调。但是不包括close事件，定时器和setImmediate()的回调。
  - 闲置阶段(idle, prepare)
    - 这个阶段仅在内部使用，可以不必理会

- 宏任务：
  - setImmediate、setTimeout、setInterval
  - script（整体代码)
  - I/O 操作等。

- 微任务
  - new Promise().then(回调)
  - process.nextTick

- process.nextTick 是一个独立于 eventLoop 的任务队列。
  - 在每一个 eventLoop 阶段完成后会去检查 nextTick 队列，如果里面有任务，会让这部分任务优先于微任务执行。
  - 是所有异步任务中最快执行的。

- setImmediate
  - 从意义上将是立刻执行的意思，但是实际上它却是在一个固定的阶段才会执行回调，即poll阶段之后。

- setTimeout
  - 指定的时间间隔后执行

## 事件循环 浏览器端

- JS作为单线程执行的语言，程序的执行流依靠执行栈控制，
  - 当主线程遇到异步任务时，会将异步任务放入任务队列，而非执行栈；
  - 在执行栈中的同步任务全部执行结束后，主线程会去任务队列中取出就绪的异步任务（计时器回调不会在计时未结束时执行），执行它们的回调函数，而异步任务又分为宏任务和微任务：
- 宏任务：script( 整体代码)、setTimeout、setInterval、I/O、UI交互事件、setImmediate(Node.js 环境)
- 微任务：Promise、MutationObserver、process.nextTick(Node.js 环境)
- 整体的执行流程：
  - 执行同步代码，这是宏任务
  - 执行栈为空，执行所有微任务
  - 必要时渲染 UI
  - 进行下一轮的 EventLoop ，执行宏任务队列中队首任务的异步代码
- 在浏览器中，setTimeout()/setInterval() 的每调用一次定时器的最小间隔是4ms，这通常是由于函数嵌套导致，或者是由于已经执行的 setInterval 的回调函数阻塞导致的。
  - 例如：setTimeout(fn, 0)只能指定某个任务在主线程最早有空闲时尽快执行
# 浏览器的event-loop
- JS作为单线程语言，引擎只能按顺序往下执行代码，不能并行执行任务，遇到耗时任务时，用户必须长时间等待（阻塞），此时异步就很有必要

- JS引擎执行任务时会先分类后调度：
  - 同步任务会在调用栈中按照顺序等待主线程依次执行
  - 异步任务会先挂起，在异步任务有了结果后，将注册的回调函数放入任务队列中等待主线程空闲时（调用栈被清空），被读取到栈内等待主线程的执行

- 栈中任务 > 微任务队列(依次执行所有就绪任务) > 宏任务(每次执行一项就绪任务)

- async函数类似promise的执行函数，其中代码如果没有await则就是同步执行的
- await能实现类似then()中的回调/处理程序，await会暂停执行异步函数后面的代码，让出JS主线程，直到其后promise被解决，才将异步函数剩余任务放回任务队列

- 最后总结容易出错的几点：
  - 异步的回调只会在异步执行有结果后（就绪）被加入任务队列，之前都放在Event table中
  - setTimeout开始计时是同步的行为，回调会在异步就绪后进入队列
  - Promise.resolve()是同步行为，当落定为解决态后，then回调才会加入任务队列
  - 当await后的promise落定，此时给await提供值并恢复async函数执行的回调作为一个微任务被添加到队列
  - promise链式调用时，前一个回调落定后，后一个回调进入微任务队列
# microtask vs macrotask
- macrotasks
  - setTimeout, setInterval, setImmediate, 
  - requestAnimationFrame, 
  - I/O, UI rendering
- microtasks
  - promise, queueMicrotask()
  - MutationObserver
  - process.nextTick, 

- event loop algorithm
  1. Dequeue and run the oldest task from the macrotask queue (e.g. “script”).
  2. Execute all microtasks: While the microtask queue is not empty: Dequeue and run the oldest microtask.
  3. Render changes if any.
  4. If the macrotask queue is empty, wait till a macrotask appears.
  5. Go to step 1.
- To schedule a new macrotask:
  - Use zero delayed `setTimeout(f)`: split a big calculation-heavy task into pieces
- To schedule a new microtask
  - Use `queueMicrotask(f)`.
  - Also promise handlers go through the microtask queue.
- There’s no UI or network event handling between microtasks: they run immediately one after another.
- For long heavy calculations that shouldn’t block the event loop, we can use Web Workers.
  - Web Workers can exchange messages with the main process, but they have their own variables, and their own event loop.

- All microtasks are completed before any other event handling or rendering or any other macrotask takes place.
  - it guarantees that the application environment is basically the same (no mouse coordinate changes, no new network data, etc) between microtasks.

## [Difference between microtask and macrotask within an event loop context](https://stackoverflow.com/questions/25915634)

- One go-around of the event loop will have exactly one task being processed from the macrotask queue (this queue is simply called the task queue in the WHATWG specification).
  - After this macrotask has finished, all available microtasks will be processed, namely within the same go-around cycle. 
  - While these microtasks are processed, they can queue even more microtasks
- If a microtask recursively queues other microtasks, it might take a long time until the next macrotask is processed. 
  - This means, you could end up with a blocked UI, or some finished I/O idling in your application.
- requestAnimationFrame (and UI rendering) are not "tasks", they are part of the event loop processing and are just callbacks, 
  - rAF being stored in a map not a queue 
  - and other UI events like scroll or resize being just DOM events. 
  - This means you can have many non-microtask js jobs executed in the same event loop iteration

- when a task (in macrotask queue) is running, new events may be registered. So new tasks may be created.
  - setTimeout(callback, n)'s callback is a task, and will be pushed into macrotask queue, even n is 0; 
  - promiseA.then()'s callback is a task
    - promiseA is resolved/rejected:  the task will be pushed into microtask queue in current round of event loop.
    - promiseA is pending:  the task will be pushed into microtask queue in the future round of event loop(may be next round)
- task in microtask queue will be run in the current round, while task in macrotask queue has to wait for next round of event loop.
- we all know callback of "click", "scroll", "ajax", "setTimeout"... are tasks, however we should also remember js codes as a whole in `script` tag is a task(a macrotask) too.

```JS
console.log(1);
setTimeout(() => {
  console.log(2);
});
new Promise((resolve) => {
    console.log(3);
    resolve("resolve");
    console.log(4);
    reject("error");
  })
  .catch((err) => {
    console.log(err);
  })
  .then((res) => {
    console.log(res);
  });

Promise.resolve().then(() => {
  console.log(5);
});
console.log(6);

// 输出顺序 1 3 4 6 5 resolve 2
```

```js
console.log(1);
setTimeout(() => {
  console.log(2);
  Promise.resolve().then(() => {
    console.log(3)
  });
});
new Promise((resolve, reject) => {
  console.log(4)
  resolve(5)
}).then((data) => {
  console.log(data);
})
setTimeout(() => {
  console.log(6);
})
console.log(7);

// 1475236
```

```JS
async function async1() {
  console.log('async1 start'); //2
  await async2();
  console.log('async1 end'); // 6
}
async function async2() {
  console.log('async2'); //3
}

console.log('script start'); //1
setTimeout(function() {
  console.log('setTimeout'); //8
}, 0)
async1();
new Promise(function(resolve) {
  console.log('promise1'); //4
  resolve();
}).then(function() {
  console.log('promise2'); //7
});
```

# dom操作
- elem.querySelector(css) 会返回给定 CSS 选择器的第一个元素。其结果与 elem.querySelectorAll(css)[0] 相同
- 该搜索器支持伪类，如 :hover 和 :active，但是不支持伪元素，伪元素会使得返回结果始终为空列表
- getElementById(id) 获取的是动态集合，querySelector 获取的是静态集合，即如果在脚本中修改DOM，以 querySelector 获取的元素并不会随之更新
# 事件
- DOM2事件规范规定事件流分为3 个阶段：事件捕获、到达目标和事件冒泡
  - 现代浏览器支持以冒泡的方式处理
- 默认事件处理程序会被添加到事件流的冒泡阶段，主要原因是跨浏览器兼容性好。如果不需要拦截，则不要使用事件捕获。
- DOM0 级事件只有冒泡阶段，DOM2 级事件的第三个参数 false 表示冒泡，true  表示捕获
- DOM0 只能为同时为相同事件绑定一个事件函数，后绑定的会覆盖掉前面的，而DOM2级事件可以绑定多个事件函数

- 页面中事件处理程序的数量与页面整体性能直接相关，因为
  - 每个函数都是对象，都占用内存空间，对象越多，性能越差
  - 指定事件处理程序所需访问 DOM 的次数会先期造成整个页面交互的延迟（脚本与渲染过程抢占主线程）
- 针对过多处理程序的解决方法是事件委托机制：
  - 利用事件冒泡，可以把事件绑定给更高级元素，只使用一个事件处理程序来管理一种类型的事件
  - 对于不可冒泡事件（blur、focus、scroll），在捕获阶段进行委托处理

```JS
// dom操作

document.createElement(node);
ele.appendChild(node)
ele.removeChild(node)
ele.replaceChild(new, old)
ele.insertBefore(new, old)
```

## 页面生命周期事件

- DOMContentLoaded ：DOM 已经就绪，因此处理程序可以查找 DOM 节点，并初始化接口。
  - 只要页面中的 DOM 结构加载完成后就可以触发
  - DOMContentLoaded 必须等待脚本加载执行结束，但是对有 `<async>` 特性的脚本，DOMContentLoaded 不会被阻塞。
- load ： 外部资源已加载完成，样式已被应用，图片大小也已知了。
  - 整个页面（包括图片、CSS）加载完毕后触发

- `<script defer>` 和 `<script async>` 都能开启对文档中脚本资源的异步并行下载，区别是：
  - async属性的脚本会在下载完毕后尽快执行，多个脚本之间的顺序不能保证；
    - 多个defer脚本会保持其相对顺序，就像常规脚本一样
  - defer属性的脚本一定会在完成页面 DOM 结构加载后，触发 DOMContentLoaded 前执行
    - 多个defer脚本会保持其相对顺序，就像常规脚本一样
# 浏览器架构
- 现代浏览器通常由7部分构成：
  - 渲染引擎：负责显示请求的内容。如果请求的内容是 HTML，它就负责解析 HTML 和 CSS 内容，并将解析后的内容显示在屏幕上。
  - JS引擎：用于解析和执行JavaScript代码。
  - 浏览器引擎 ： 在用户界面和渲染引擎之间传送指令。
  - 用户界面： 地址栏、前进/后退按钮、书签菜单等。除浏览器主窗口显示的页面外，其他各个部分都属于UI。
  - 用户界面后端 ：绘制基本的窗口小部件，比如组合框和窗口。提供平台无关的API，在底层使用操作系统的UI方法。
  - 数据存储：持久层。浏览器需要在硬盘上保存各种数据，例如 Cookie。
  - 网络 ：用于网络调用，比如 HTTP 请求。其接口与平台无关，并为所有平台提供底层实现。

- 现代浏览器通常都是多进程的
  - Browser 进程：主控进程，负责协调，只有一个
  - 渲染器进程（内核）：默认每个 tab 页面一个，互不影响，控制页面渲染、脚本执行、事件处理等，但有时会优化合并
  - GPU 进程：最多一个，用于 3D 绘制
  - 插件进程：每个插件对应一个，启用该插件时创建
  - 缓存进程
  - 网络进程

- 每一个tab页面可默认对应一个渲染器进程，这个进程是多线程的：UI线程、JS引擎线程、事件触发线程、网络请求线程等
# 从输入url到页面显示的过程

## URL 解析

- 浏览器进程的UI线程会捕捉输入内容
  - 如果是一个地址，UI线程会启动一个网络线程进行 DNS 查询，接着建立连接获取数据
  - 如果是一串关键词，浏览器会调用默认配置的搜索引擎进行查询

## DNS 查询

- 如果浏览器有缓存，直接从中获取IP地址，否则在系统缓存、路由器缓存查询，
  - 如果都没有命中，则向 DNS 服务器发起解析请求

## 建立TCP连接，进行HTTP传输

## HTML 解析 & DOM 生成

- 主线程解析html，html文档会经过词法分析与树构造过程，生成一棵 DOM 树。
  - 期间遇到CSS文件、多媒体资源等，渲染器进程会创建额外的网络线程进行请求，并不会阻塞主线程对 html 的解析；
  - 但是遇到js文件时，主线程会暂停 html 解析，等待文档中的 js 文件加载、解析、执行完毕，之后才恢复 html 解析过程
- js 文件的加载解析阻塞 html 是因为浏览器并不知道 js 的执行是否会改变当前页面的 html 结构，如果脚本调用 document.write() 修改 html，则之前的 html 解析就没有意义了
- CSS 的下载不会阻塞 html 解析，但 CSS 的解析本身由主线程完成，因此当 DOM 树生成完毕，需要等待 CSS 解析完进入下一步

## CSS 解析 & 样式计算

## layout

- 主线程通过遍历 DOM 树和计算样式，生成一棵 Layout tree，精确计算出每个节点在屏幕上的的 x，y 坐标与尺寸信息。
- Layout tree 和 DOM tree 不一定一致
  - 一些结点会被忽略（比如 script 标签，meta 标签等），因为不会影响渲染的输出
  - 一些结点是通过 CSS 样式隐藏了，这些节点同样被忽略——例如应用 display:none 样式的结点
  - 一些结点被添加进布局树，比如 ::before，::after 添加的伪元素

## paint

- 由于有 z-index 或脱离文档流的元素，layout tree 中结点顺序并非渲染顺序，因此主线程会遍历 layout tree，调用节点对应绘制逻辑（这里的绘制逻辑并不是真正意义上的显示器设备完成绘制，而是生成一条条的绘制记录），最终得到一个绘制记录表（paint record）
- paint 过程结束后，还会得到 layer tree

## composite

- 知道了完整的绘制信息后，需要将它们转换为屏幕上的像素点，这一过程称为栅格化（Rastering）。
- 现代浏览器采用一种“合成”过程进行栅格化
  - 主线程将绘制信息（layer tree 和绘制顺序）传递给合成器线程，后者将每个图层进行栅格化
  - 由于原始图层可能是整个页面长度的大小，合成器线程会将图层分为许多块（tiles），交给不同的栅格线程（Raster Thread），栅格线程光栅化 tiles 并存储在 GPU 缓存中，合成器线程会收集 Draw Quads 图块信息，其中记录了每个 tile 在 GPU 中的位置与在页面中的目标渲染位置
  - 根据图块信息，合成器线程会合成一个“合成器帧”，通过 IPC 传递给浏览器进程，浏览器进程又会传送给 GPU，最终由 GPU 渲染到屏幕上
  - 当页面滚动，合成器线程又会生成下一个“合成器帧”，同样传递给 GPU 渲染

## 页面交互与更新

- reflow
  - 调整浏览器窗口大小
  - 增加、删除、修改DOM节点
  - 修改字体（字号字形会影响盒子布局）
  - display: none：会触发重排和重绘，因为这是不保留物理空间的隐藏

- repaint
  - visibility: hidden：只触发重绘，因为此盒子依旧占位存在，只不过透明了
# 浏览器渲染优化
- 重绘与重排都会占用主线程，而 JS 也运行在主线程上，因此会面临抢占主线程的问题
- requestAnimationFrame
- transform、opacity
- DocumentFragment
  - 在操作 DOM 时，如果需要增加大量的节点，可以先创建一个 DocumentFragment，对该文档片段进行操作，最后调用 append(frag)，这样只会在最后一次插入片段时触发一次重绘重排
- 对参与动画的元素设置为绝对定位
  - 避免对元素的父元素布局产生影响，尽量减小每次重新渲染的开销
- 
- 
