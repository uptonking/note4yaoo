---
title: job-coding-repeat
tags: [coding, job, repeat]
created: 2021-10-04T14:47:10.364Z
modified: 2021-10-04T14:47:29.358Z
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
 * * 思路：先提取整数字符串，然后遍历每位模拟加法计算
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

  // console.log(intStr);

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

# 实现 instanceof

```JS
/**
 * * 判断A的原型链上是否有B的原型
 * 思路是 在a的原型链a.__proto__上查找 b.prototype
 */
function _instanceof(obj, Cls) {
  const bPrototype = Cls.prototype;

  let aProto = Object.getPrototypeOf(obj);

  while (aProto) {
    if (aProto === bPrototype) {
      return true;
    }

    aProto = Object.getPrototypeOf(aProto);
  }

  return false;
}
```

# 实现一个 iterator
- next()方法的参数表示上一条 yield 语句的返回值 ， 所以第一次使用 next 方法时 传递参数是无效的 。
  - 通过 next 方法的参数就有办法在 Generator 函数开始运行后继续向函数 体内部注入值 。

```JS
function makeIterator(array) {
  const nextIndex = 0;
  return {
    next: function(value) {
      return nextIndex < array.length ? {
        value: array[nextIndex++],
        done: false
      } : {
        value: undefined,
        done: true
      };
    }
  };
}

const it = makeIterator(['a', 'b']);

it.next()
// { value: "a", done: false }
it.next()
// { value: "b", done: false }
it.next()
// { value: undefined, done: true }
```

# 手写 jsonp

```JS
/**
 * * 手写jsonp
 * * 思路：拼接querystring(以?或&开头)，动态创建script标签，将回调函数名挂载到window，然后appendChild(script)
 https://juejin.cn/post/6947694608247685127
 * - JSONP只支持GET请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。
 */
function jsonp(url, params, callback) {
  // 判断是否已有参数
  let queryString = url.indexOf('?') ? '?' : '&';
  // 拼接参数
  for (const item in params) {
    if (params.hasOwnProperty(item)) {
      queryString += `${item}=${params[item]}&`;
    }
  }

  // 为cb拼接随机token（可省略）
  const token = Math.random().toString().replace('.', '');
  const cbName = 'jsonpCb' + token;
  queryString += `callback=${cbName}`;

  // 添加标签
  const script = document.createElement('script');
  script.src = url + queryString;

  // 包装回调执行逻辑
  window[cbName] = function(response) {
    callback.apply(this, response);
    document.removeChild(script);
  };

  document.appendChild(script);
}
```
