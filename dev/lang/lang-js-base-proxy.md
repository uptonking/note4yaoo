---
title: lang-js-base-proxy
tags: [ECMAScript, js, lang, proxy]
created: 2022-11-23T17:49:32.485Z
modified: 2022-11-23T17:49:54.052Z
---

# lang-js-base-proxy

# guide

- cons
  - [Vue3 解构赋值失去响应式引发的思考](https://zhuanlan.zhihu.com/p/543010554)

- [Proxy和Reflect的要注意的问题与局限性 - 掘金](https://juejin.cn/post/7004452888638554125)
  - 在开发时假如对一个对象做代理时，对代理的所有管理也需要再进行一层代理，原对象对原对象，代理对代理
# examples

# more

- [Vue3.0里为什么要用 Proxy API 替代 defineProperty API ？](https://vue3js.cn/interview/vue3/proxy.html)
  - Object.defineProperty只能遍历对象属性进行劫持
    - Proxy直接可以劫持整个对象，并返回一个新对象
    - Proxy有多达13种拦截方法,不限于apply、ownKeys、deleteProperty、has等等，这是Object.defineProperty不具备的
  - 数组API方法无法监听到
    - Proxy可以直接监听数组的变化（push、shift、splice）
  - 检测不到对象属性的添加和删除
  - 需要对每个属性进行遍历监听，如果嵌套对象，需要深层监听，造成性能问题
