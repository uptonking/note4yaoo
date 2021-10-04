---
title: job-coding-repeat
tags: [coding, job, repeat]
created: '2021-10-04T14:47:10.364Z'
modified: '2021-10-04T14:47:29.358Z'
---

# job-coding-repeat

> 高频：至少被问过2次

# promise
- Promise.all
  - 只要其中任何一个promise任务失败了，就会直接返回这个失败的结果。其他的忽略。 
  - 只有任务数组中全部都成功了，才会把所有的任务结果全部返回。调用 .then 中的成功回调
  - Promise.all返回的是promise所以可以继续调用promise原型上的方法，只是没有值而已
- 使用场景
  - 彼此相互依赖，其中任何一个被 reject ，其它都失去了实际价值

- Promise.allSettled
  - 可以获取数组中每个 promise 的结果，无论成功或失败
- 使用场景
  - 期望知道每个 promise 的执行结果
  - 彼此不依赖，其中任何一个被 reject，对其它都没有影响

```JS
Promise.all = (promises) => {
  return new Promise((resolve, reject) => {
    // promise成功结果数组
    const result = [];
    let resolvedCount = 0;

    for (let i = 0; i < promises.length; i++) {
      Promise.resolve(promises[i]).then((value) => {
        resolvedCount++;
        result[i] = value;

        // 全部
        if (resolvedCount === promises.length) {
          resolve(result);
        }
      }, reject);
    }
  });
};

Promise.allSettled = function(promises) {
  return new Promise((resolve, reject) => {
    promises = Array.isArray(promises) ? promises : [];
    let len = promises.length;
    const argslen = len;

    // 如果传入的是一个空数组，那么就直接返回一个resolved的空数组promise对象
    if (len === 0) return resolve([]);

    // 将传入的参数转化为数组，赋给args变量
    const args = Array.prototype.slice.call(promises);

    // 计算当前是否所有的 promise 执行完成，执行完毕则resolve
    const compute = () => {
      if (--len === 0) {
        resolve(args);
      }
    };

    function resolvePromise(index, value) {
      // 判断传入的是否是 promise 类型
      if (value instanceof Promise) {
        const then = value.then;
        then.call(
          value,
          function(val) {
            args[index] = { status: 'fulfilled', value: val };
            compute();
          },
          function(e) {
            args[index] = { status: 'rejected', reason: e };
            compute();
          },
        );
      } else {
        args[index] = { status: 'fulfilled', value: value };
        compute();
      }
    }

    for (let i = 0; i < argslen; i++) {
      resolvePromise(i, args[i]);
    }
  });
};

// 有一个promise状态变为fulfilled或rejected，就立即返回promise
Promise.race = (promises) => {
  return new Promise((resolve, reject) => {
    for (let i = 0; i < promises.length; i++) {
      Promise.resolve(promises[i]).then(resolve, reject);
    }
  });
};
```

- promise的实现

```JS
/**
 * * Promise 本质上就是一个绑定了回调的对象
 */
function Promise2(executor) {
  const _this = this;

  this.state = PENDING;
  this.value = undefined;
  this.reason = undefined;

  this.onFulfilled = [];
  this.onRejected = [];

  function resolve(value) {
    if (_this.state === PENDING) {
      _this.state = FULFILLED;
      _this.value = value;
      _this.onFulfilled.forEach((fn) => fn(value));
    }
  }

  function reject(reason) {
    if (_this.state === PENDING) {
      _this.state = REJECTED;
      _this.reason = reason;
      _this.onRejected.forEach((fn) => fn(reason));
    }
  }

  try {
    executor(resolve, reject);
  } catch (err) {
    reject(err);
  }
}

/**
 * 简单实现的支持异步的then，
 * - 👀️ 未返回promise对象，不支持链式调用。
 */
Promise2.prototype.then2 = function(onResolved, onRejected) {
  if (this.state === FULFILLED) {
    typeof onResolved === 'function' && onResolved(this.value);
  }
  if (this.state === REJECTED) {
    typeof onRejected === 'function' && onRejected(this.reason);
  }

  if (this.state === PENDING) {
    typeof onResolved === 'function' && this.onFulfilled.push(onResolved);
    typeof onRejected === 'function' && this.onRejected.push(onRejected);
  }
};
```
