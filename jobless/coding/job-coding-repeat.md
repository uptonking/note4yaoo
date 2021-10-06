---
title: job-coding-repeat
tags: [coding, job, repeat]
created: '2021-10-04T14:47:10.364Z'
modified: '2021-10-04T14:47:29.358Z'
---

# job-coding-repeat

> 高频：至少被问过2次


# 实现双向绑定 / 响应式数据

```JS
function Observer(data) {
  Object.keys(data).forEach((key) => {
    if (typeof data[key] === 'object') {
      // 这里只处理了第1层属性
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

/**
 * * proxy对象的get/set中receiver默认是proxy自身，
 * - This is usually the proxy itself. But a set() handler can also be called indirectly, via the prototype chain or various other ways.
 * - The receiver can either be the Proxy created or any object that inherits the Proxy.
 */
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

# 手写 parseInt

```JS
/**
 * * 手写parseInt，不处理小数。返回解析后的整数值。
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/89
 * - 如果被解析参数的第一个字符无法被转化成数值类型，则返回 NaN。
 */
export function _parseInt(str, radix) {
  if (!['string', 'number'].includes(typeof str)) {
    return NaN;
  }

  let ret = 0;

  const intStr = String(str).trim().split('.')[0];
  const len = intStr.length;
  if (!len) return NaN;

  console.log(intStr);

  if (!radix) radix = 10;
  if (typeof radix !== 'number' || radix < 2 || radix > 36) {
    return NaN;
  }

  for (let i = 0; i < len; i++) {
    // join要指定空格，否则默认使用逗号
    const arr = intStr.split('').reverse().join('');
    ret += Math.floor(arr[i] * Math.pow(radix, i));
    // console.log(ret, arr[i], radix, arr);
  }

  return ret;
}
```
