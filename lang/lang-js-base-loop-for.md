---
title: lang-js-base-loop-for
tags: [ECMAScript, for-loop, js, lang]
created: 2022-11-23T17:43:21.330Z
modified: 2022-11-23T17:44:28.971Z
---

# lang-js-base-loop-for

# guide

# `for await...of` vs `for...of`

- `for await...of` can only be used in contexts where `await` can be used, which includes inside an `async` function body and in a module. 
  - Even when the iterable is sync, the loop still awaits the return value for every iteration, leading to slower execution due to repeated promise unwrapping.

- [浅析异步循环for await of的使用及执行机制及for of/forEach本质区别和遇到异步时的处理 - 古兰精 - 博客园](https://www.cnblogs.com/goloving/p/16009741.html)
  - 遍历promise数组的方法比较

```JS
// 💡 普通for of会先执行所有for循环体，然后异步并发执行promise，异步p的fn先执行完的先结束

function getTime(seconds) {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('ppp; ', seconds);
      resolve(seconds)
    }, seconds);
  })
}

function test() {
  let arr = [getTime(2000), getTime(300), getTime(1000)]
  for (let x of arr) { // 👉🏻 打印的是promise对象
    console.log('fff; ', x);
  }
}

test()

// fff;  Promise {<pending>}-2000
// fff;  Promise {<pending>}-300
// fff;  Promise {<pending>}-1000

// ppp;  300
// ppp;  1000
// ppp;  2000
```

```JS
// 💡 for await...of遍历promise时，会先等of后的所有promise并发执行完，然后执行所有循环体

function getTime(seconds) {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('ppp; ' + seconds);
      resolve(seconds)
    }, seconds);
  })
}

async function test() {
  let arr = [getTime(2000), getTime(300), getTime(1000)];
  for await (let x of arr) {
    console.log('fff; ', x);
  }
}

test()

// Promise {<pending>}[[Prototype]]: Promise[[PromiseState]]: "fulfilled"[[PromiseResult]]: undefined
// ppp; 300
// ppp; 1000
// ppp; 2000

// fff;  2000
// fff;  300
// fff;  1000
```

- for...of 内部处理的机制和 forEach 不同，forEach 是直接调用回调函数，for...of 是通过迭代器的方式去遍历。

```JS
// 定义一个fetch函数模拟异步请求，延迟n秒执行； 可调整实参321为642，等待时间更明显
function fetch(n) {
  return new Promise((resolve, reject) => {
    console.log('ppp; ', n);
    setTimeout(() => {
      resolve(n);
    }, 1000 * n);
  })
}

// 👉🏻 完全顺序执行，效率低
async function test() {
  const arr = [3, 2, 1];
  for (const item of arr) {
    const res = await fetch(item); // 💡 会等待方法执行完
    console.log('fff; ', res)
  }
  console.log('end')
}
test();

// ppp;  3
// Promise {<pending>}[[Prototype]]: Promise[[PromiseState]]: "fulfilled"[[PromiseResult]]: undefined
// 等待
// fff;  3
// ppp;  2
// 等待
// fff;  2
// ppp;  1
// 等待
// fff;  1
// end

// 👉🏻 for-await会先执行所有promise
async function test() {
  const arr = [fetch(3), fetch(2), fetch(1)];
  for await (const item of arr) {
    console.log('fff; ', item)
  }
  console.log('end')
}
test();

// 👉🏻 Promise.all会先执行所有promise，和for await-of输出一样
async function test() {
  const arr = [fetch(3), fetch(2), fetch(1)];

  Promise.all(arr).then(values => values.forEach(item => {
    console.log('fff; ', item)
  }));

  console.log('end');
}
test();

// 前面所有promise一次性打印
// ppp;  3
// ppp;  2
// ppp;  1
// Promise {<pending>}[[Prototype]]: Promise[[PromiseState]]: "fulfilled"[[PromiseResult]]: undefined
// 等待最长时间
// fff;  3
// fff;  2
// fff;  1
// end

// 👉🏻 普通for循环，并发执行
function test() {
  const arr = [3, 2, 1]
  arr.forEach(async item => {
    const res = await fetch(item)
    console.log('fff; ', res)
  })
  console.log('end')
}
test();

// ppp;  3
// ppp;  2
// ppp;  1
// end
// 1
// 等待
// 2
// 等待
// 3
```

- [for...in 和 for...of 的区别及 for await of 的用法 - 掘金](https://juejin.cn/post/7094210110578229261)
  - 如果你想顺序执行，只能延迟创建 promise 对象，而不能及早创建。即，你创建了 promise 对象，它就立刻开始执行逻辑。
  - 直接使用 async + for of + await 也可实现顺序迭代调用；
  - for await of 是并发异步得到结果后再迭代类似 promise.all。
