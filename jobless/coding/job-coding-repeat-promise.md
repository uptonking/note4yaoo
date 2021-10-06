---
title: job-coding-repeat-promise
tags: [async, coding, promise, repeat, 手撕代码]
created: '2021-09-23T08:20:13.005Z'
modified: '2021-10-06T17:17:34.809Z'
---

# job-coding-repeat-promise

# promise方法
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
/**
 * * 在每个promise任务的then方法中，都判断resolvedCount
 */
Promise.all2 = (promises) => {
  return new Promise((resolve, reject) => {
    // promise成功结果数组
    const result = [];
    let resolvedCount = 0;

    for (let i = 0; i < promises.length; i++) {

      const promise = promises[i];
      promise.then(
        (response) => {
          result[i] = response;
          resolvedCount++;

          // 当返回结果为最后一个时
          if (resolvedCount === promises.length) {
            resolve(result);
          }
        },
        (error) => {
          reject(error);
        },
      );

    }
  });
};

const p1 = Promise.resolve(1)
const p2 = Promise.resolve(2)
const p3 = new Promise((resolve, reject) => {
  setTimeout(reject, 1000, 'three');
});

Promise.all2([p1, p2, p3])
  .then(values => {
    console.log('resolve: ', values)
  }).catch(err => {
    console.log('reject: ', err)
  })

// reject:  three // 丢失了成功的结果
```

```JS
/**
 * * 在每个promise任务的finally方法中，都判断taskCount
 */
Promise.allSettled2 = function(promises) {
  return new Promise((resolve, reject) => {
    const len = promises.length;

    const result = [];
    let count = 0;

    for (let i = 0; i < len; i += 1) {
      const promise = promises[i];

      promise
        .then(
          (res) => {
            result[i] = { status: 'fulfilled', value: res };
          },
          (error) => {
            result[i] = { status: 'rejected', reason: error };
          },
        )
        .finally(() => {
          count++;

          // 全部执行完了，才会执行resolve
          if (count === len) {
            resolve(result);
          }
        });
    }
  });
};

const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) =>
  setTimeout(reject, 1500, 'foo'),
);
const promises = [promise2, promise1];

Promise.allSettled2(promises).then((results) =>
  results.forEach((result) => console.log(result)),
);
```

```JS
// 有一个promise状态变为fulfilled或rejected，就立即返回promise
Promise.race = (promises) => {
  return new Promise((resolve, reject) => {
    for (let i = 0; i < promises.length; i++) {
      Promise.resolve(promises[i]).then(resolve, reject);
    }
  });
};
```

# promise的实现 / 手写promise

```JS
/**
 * * promise本质上就是一个绑定了回调的对象
 * * 在promise对象内部定义成功失败的回调函数 execResolve/execReject ；
 * * executor的返回值会被忽略，本函数内部一般包含异步操作，不包含也可以
 * * 当异步操作结束时，由开发者将结果传给 execResolve(value)/execReject(reason)，然后保存到this.value/reason，并执行then注册的回调函数
 * - state: pending, fulfilled, rejected, settled
 */
function Promise2(executor) {
  const _this = this;

  this.state = 'PENDING';
  this.value = undefined;
  this.reason = undefined;

  this.onFulfilled = [];
  this.onRejected = [];

  function execResolve(value) {
    if (_this.state === 'PENDING') {
      _this.state = 'FULFILLED';
      _this.value = value;
      _this.onFulfilled.forEach((fn) => fn(value));
    }
  }

  function execReject(reason) {
    if (_this.state === 'PENDING') {
      _this.state = 'REJECTED';
      _this.reason = reason;
      _this.onRejected.forEach((fn) => fn(reason));
    }
  }

  try {
    executor(execResolve, execReject);
  } catch (err) {
    reject(err);
  }
}

/**
 * * 简单实现的支持异步的then，主要是注册回调函数到到promise对象。
 * - 👀️ 未返回promise对象，不支持链式调用。
 */
Promise2.prototype.then2 = function(onResolved, onRejected) {
  if (this.state === 'FULFILLED') {
    typeof onResolved === 'function' && onResolved(this.value);
  }
  if (this.state === 'REJECTED') {
    typeof onRejected === 'function' && onRejected(this.reason);
  }

  if (this.state === 'PENDING') {
    typeof onResolved === 'function' && this.onFulfilled.push(onResolved);
    typeof onRejected === 'function' && this.onRejected.push(onRejected);
  }
};

const testPromise1 = new Promise2((resolve, reject) => {
  console.log(';;--start testPromise1');

  setTimeout(() => {
    // reject('reject-reason');
    resolve('success-value');
  }, 1500);
});

testPromise1.then2(
  (data) => {
    console.log('testPromise1- success', data);
  },
  (err) => {
    console.log('testPromise1- err', err);
  },
);
```

```JS
// promise测试
var original = Promise.resolve(33);
var cast = Promise.resolve(original);
original === cast // true
```
