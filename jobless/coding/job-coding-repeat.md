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
Promise.all1 = (promises) => {
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

Promise.all1([p1, p2, p3])
  .then(values => {
    console.log('resolve: ', values)
  }).catch(err => {
    console.log('reject: ', err)
  })

// reject:  three // 丢失了成功的结果
```

```JS
Promise.allSettled1 = function(promises) {
  return new Promise((resolve, reject) => {
    const result = [];
    const len = promises.length;
    let count = len;

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
          // 全部执行完了，才会执行resolve
          if (!--count) {
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

Promise.allSettled1(promises).then((results) =>
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

# 实现双向绑定 / 响应式数据

```JS
function Observer(data) {
  Object.keys(data).forEach((key) => {
    if (typeof data[key] === 'object') {
      data[key] = new Observer(data[key]);
    }

    // 对每个一级属性都重新定义访问器
    Object.defineProperty(this, key, {
      enumerable: true,
      configurable: true,
      get() {
        console.log(';;get, ' + key);
        return data[key];
      },
      set(val) {
        console.log(';;set, old, new, ', data[key], val);
        if (val === data[key]) return;
        data[key] = val;
      },
    });
  });
}

const obj = {
  name: 'app',
  age: '18',
  a: {
    b: 1,
    c: 2,
  },
};

const app = new Observer(obj);
app.age = 20;
console.log(app.age);

console.log(app.a);
console.log(app.a.c);

// 给对象新增一个属性，内部并没有监听到，新增的属性需要手动再次使用Object.defineProperty()进行监听
app.newPropKey = '新属性';
console.log(app.newPropKey);
```

```JS
const obj = {
  name: 'app',
  age: '18',
  a: {
    b: 1,
    c: 2,
  },
};

const pObj = new Proxy(obj, {
  get(target, key, receiver) {
    console.log(';;get, ' + key);
    return Reflect.get(target, key, receiver);
  },
  set(target, key, val, receiver) {
    console.log(';;set, old, new, ', target[key], val);

    // target[key]=val;
    Reflect.set(target, key, val, receiver);
    // 在浏览器中不需要return，在node中需要return true
    return true;
  },
});

pObj.age = '20';
console.log(pObj.age);

// 新增的属性，并不需要重新添加响应式处理，
// 因为Proxy是拦截对对象的操作，只要你访问对象，就会走到 Proxy 的逻辑中。
pObj.newPropKey = '新属性';
console.log(pObj.newPropKey);
```
