---
title: job-coding-repeat-promise
tags: [async, coding, promise, repeat, 手撕代码]
created: 2021-09-23T08:20:13.005Z
modified: 2021-10-06T17:17:34.809Z
---

# job-coding-repeat-promise

# 实现promise的一个示例

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
 * * 💡️ 实现promise的一个示例
 * https://wangyaxing.cn/blog/jsCode/%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AAPromise.html
 * * 3个实例属性：this.status, this.resolveList, this.rejectList
 * * then()方法的作用是将回调函数注册到 this.resolveList/rejectList
 * * execResolve()/execReject()的任务是改变状态，以及执行resolveList的函数，将value/reason传递给注册过的cb
 *
 */
class Promise {
  constructor(executor) {
    /**
     *  三种状态：pending进行中; fulfilled已成功; rejected 已失败
     */
    this.status = 'pending';

    this.resolveList = []; // 成功后回调函数
    this.rejectList = []; // 失败后的回调函数
    this.finalList = [];

    executor(this.execResolve.bind(this), this.execReject.bind(this));
  }

  execResolve(value) {
    if (this.status !== 'pending') return;
    this.status = 'fulfilled';

    // 延迟执行，提供机会让then()方法执行注册事件处理函数
    setTimeout(() => {
      this.resolveList.forEach((fn) => {
        value = fn(value);
      });
    });
  }

  execReject(reason) {
    if (this.status !== 'pending') return;
    this.status = 'rejected';

    setTimeout(() => {
      this.rejectList.forEach((fn) => {
        reason = fn(reason);
      });
    });
  }

  /** 💡️ 任务是注册成功或失败回调函数 */
  then(onResolve, onReject) {
    if (onResolve) {
      this.resolveList.push(onResolve);
    }
    if (onReject) {
      this.rejectList.push(onReject);
    }
    return this;
  }

  finally(onFinally) {
    // if (this.status === 'pending') return;

    if (onFinally && typeof onFinally === 'function') {
      this.finalList.push(onFinally);
    }

    return this;
  }

  /** 注册异常处理 */
  catch (cb) {
    if (cb) {
      this.rejectList.push(cb);
    }
    return this;
  }

  /**
   * 实现Promise.resolve
   * 1.参数是一个 Promise 实例, 那么Promise.resolve将不做任何修改、原封不动地返回这个实例。
   * 2.如果参数是一个原始值，或者是一个不具有then方法的对象，则Promise.resolve方法返回一个新的 Promise 对象，状态为resolved。
   */
  static resolve(data) {
    if (data instanceof Promise) {
      return data;
    }
    return new Promise((resolve, reject) => {
      resolve(data);
    });
  }

  // 实现Promise.reject
  static reject(err) {
    if (err instanceof Promise) {
      return err;
    }
    return new Promise((resolve, reject) => {
      reject(err);
    });
  }

  /**
   * 实现Promise.all
   * 1. Promise.all方法接受一个数组作为参数，p1、p2、p3都是 Promise 实例，如果不是，就会先调用下面讲到的Promise.resolve方法，将参数转为 Promise 实例，再进一步处理。
   * 2. 返回值组成一个数组
   */
  static all(promises) {
    return new Promise((resolve, reject) => {
      let promiseCount = 0;
      const promisesLength = promises.length;
      const result = [];
      for (let i = 0; i < promises.length; i++) {
        // promises[i]可能不是Promise类型，可能不存在then方法，中间如果出错,直接返回错误
        Promise.resolve(promises[i]).then(
          (res) => {
            promiseCount++;
            // 注意这是赋值应该用下标去赋值而不是用push，因为毕竟是异步的，哪个promise先完成还不一定
            result[i] = res;
            if (promiseCount === promisesLength) {
              return resolve(result);
            }
          },
          (err) => {
            return reject(err);
          },
        );
      }
    });
  }

  static allSettled(promises) {
    return new Promise1((resolve, reject) => {
      const result = [];

      let count = 0;
      const len = promises.length;

      for (let i = 0; i < len; i++) {
        Promise1.resolve(promises[i])
          .then(
            (val) => {
              result[i] = { status: 'fulfilled', value: val };
            },
            (reason) => {
              result[i] = { status: 'rejected', reason };
            },
          )
          .finally(() => {
            count++;
            if (count === len) {
              resolve(result);
            }
          });
      }
    });
  }

  /**
   * 实现Promise.race
   * 1. Promise.race方法的参数与Promise.all方法一样，如果不是Promise实例，就会先调用下面讲到的Promise.resolve方法，将参数转为 Promise 实例，再进一步处理。
   * 2. 返回那个率先改变的 Promise 实例的返回值
   */
  static race(promises) {
    return new Promise((resolve, reject) => {
      for (let i = 0; i < promises.length; i++) {
        Promise.resolve(promises[i]).then(
          (res) => {
            return resolve(res);
          },
          (err) => {
            return reject(err);
          },
        );
      }
    });
  }
}

// ---- 测试用例 ----

const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('resolve');
    resolve(222);
  }, 1000);
});

p.then((data) => {
    setTimeout(() => {
      console.log('data', data);
    });
    return 3333;
  })
  .then((data2) => {
    console.log('data2', data2);
  })
  .catch((err) => {
    console.error('err', err);
  });

const p1 = Promise.reject('出错了');
p1.then(null, function(s) {
  console.log(s); // 出错了
});

const q1 = new Promise((resolve, reject) => {
  resolve('hello');
});

const q2 = new Promise((resolve, reject) => {
  resolve('world');
});
Promise.all([q1, q2]).then((res) => {
  console.log(res); // [ 'hello', 'world' ]
});
Promise.race([q1, q2]).then((res) => {
  console.log(res); // hello
});
```

# promise的实现示例2

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

# 手写 async/await
- async是generator函数的语法糖
  - 内置执行器
  - 返回值是Promise，而generator返回的是迭代器

- 调用 Generator 函数后，该函数并不执行， 返回的也不是函数运行结果， 而是一个指向内部状态的迭代器对象
- 每次调用 next 方法，内部指针就从函数头部或上一次停下来的地方开始执行 ， 直到遇到下一条 yield 语句（或 return 语句）为止 。
- yield 语句就是暂停标志
  - 遇到 yield 语句就暂停执行后面的操作 ， 并将紧跟在 yield 后的表达式的值作为返回 的对象的 value 属性值 。
  - Generator 函数可以不用 yield 语句，这时就变成了一个单纯的暂缓执行函数 

```JS
/**
 * * 接受一个generator函数，然后自动执行迭代，在迭代完成后，返回...
 * https://segmentfault.com/a/1190000022705474
 */
function asyncToGenerator(genFn) {
  return function() {
    // 调用generator函数 生成迭代器
    const gen = genFn.apply(this, arguments);
    return new Promise((resolve, reject) => {
      /**
       * * 封装了调用generator的next/throw方法的过程
       */
      function runIterator(fnName, args) {
        let genResult;
        try {
          genResult = gen[key](args);
        } catch (err) {
          return reject(err);
        }

        const { value, done } = genResult;

        if (done) {
          // 迭代器迭代完成了，才会resolve
          return resolve(value);
        } else {
          // 若未迭代完成，就继续调用next方法
          return Promise.resolve(value).then(
            (val) => runIterator('next', val),
            (err) => runIterator('throw', err),
          );
        }
      }

      /**
       * * 触发执行generator函数返回值对象的next()方法
       */
      runIterator('next');
    });
  };
}

const getData = () => new Promise(resolve => setTimeout(() => resolve("data"), 1000))

var test = asyncToGenerator(
  function* testG() {
    // await被编译成了yield
    const data = yield getData()
    console.log('data: ', data);
    const data2 = yield getData()
    console.log('data2: ', data2);
    return 'success'
  }
)

test().then(res => console.log(res))
```

# 限制并发请求数量

```JS
class Scheduler {
  constructor() {
    this.queue = [];
    this.running = 0;
  }

  // 执行完一个后，若队列中还有，就继续执行
  run() {

    if (this.queue.length === 0 || this.running === 2) {
      return;
    }
    const p = this.queue.shift();
    this.running++;
    p().then((result) => {
      this.running--;

      // 执行完一个后还会继续执行，直到队列为空
      this.run();
      return result;
    })
  }

  add(promise) {
    this.queue.push(promise);
    this.run();
  }
}
const timout = (time) => new Promise(resolve => {
  setTimeout(resolve, time)
})
const scheduler = new Scheduler();

const addTask = (time, order) => {
  scheduler.add(() => timout(time).then(() => {
    console.log(order);
  }))
}

addTask(1000, '1');
addTask(500, '2');
addTask(300, '3');
addTask(400, '4');

// output: 2 3 1 4
// 一开始，1， 2两个任务进入队列
// 500ms时，2完成，输入2；任务3进队
// 800ms时，3完成，输出 3；任务4进队
// 1000ms时，1完成，输出1
// 1200ms时，4完成，输出4
```

```JS
/**
 * * promise限制并发数示例2
 * * 思路：当count>max时，用队列保存任务函数，否则立即执行
 */
class PromiseScheduler {
  constructor(max) {
    this.max = max;
    this.count = 0;
    this.queue = [];
  }

  add(caller, ...args) {
    return new Promise((resolve, reject) => {
      const task = this.createTask(caller, args, resolve, reject);

      if (this.count >= this.max) {
        this.queue.push(task);
      } else {
        task();
      }
    });
  }

  createTask(caller, args, resolve, reject) {
    return () => {
      caller(...args)
        .then(resolve, reject)
        .finally(() => {
          this.count--;
          if (this.queue.length) {
            const task = this.queue.shift();
            task();
          }
        });
      // 执行任务开始时，count+1，执行完成时，count-1
      this.count++;
    };
  }
}

const timeout = (time) =>
  new Promise((resolve) => {
    setTimeout(resolve, time);
  });

const scheduler = new PromiseScheduler(2);

const addTask = (time, order) => {
  scheduler.add(() => timeout(time)).then(() => console.log(order));
};

// async function addTask(time, order) {
//   await scheduler.add(() => timeout(time));
//   console.log(order);
// }

addTask(1000, '1');
addTask(500, '2');
addTask(300, '3');
addTask(400, '4');
```
