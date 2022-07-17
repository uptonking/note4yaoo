---
title: note-fwk-js-import-dynamic
tags: [framework, js]
created: 2021-05-24T19:53:52.503Z
modified: 2021-05-24T19:55:05.575Z
---

# note-fwk-js-import-dynamic

# guide

- 对于import cdn-url，社区里面有各种实现方案
  - 能够正常使用，要分析url来源的具体格式
  - import-http
    - https://github.com/egoist/import-http
    - 只支持esm，不支持cjs，不支持await import
  - d3.require
    - This implementation is small and supports a strict subset of AMD.
    - By default, d3.require loads modules from jsDelivr
  - runtime-import
    - https://github.com/yusangeng/runtime-import
  - ref
    - https://github.com/ded/script.js

# faq-not-yet

- 从远程加载js的问题
  - 运行时从远程动态加载自己的插件
  - 运行时从远程动态加载第三方库如lodash

- 如何从远程加载当前js库所依赖的第三方js库
  - 可以先忽略此问题，来简化解决加载的问题

# discuss

- ## [如何在Web前端运行时加载远程插件？](https://zhuanlan.zhihu.com/p/47272705)
- es6提供的dynamic import机制

```JS
import('http://www.baidu.com/app.js').then(mod => {
  const App = mod.default
  const app = new App('#app')
  app.run()
})
```

- 使用webpack打包时, 会报这样的错误.
  - 注意, 这个错误是webpack报的, babel本身不会报错. 事实上babel不会对import()调用做任何转译
- 仍然有两个障碍
  - 第一个是跨域问题, 浏览器对于dynamic import是有跨域限制的, 如果CDN不支持跨域请求, 就会报错
  - 而第二个障碍, 就是css的加载了, 如果我们不希望把css打包进js, 就需要单独的加载方式。而css提供的@import语法, 是用来在css中加载css的, 我们的场景显然不是这样.
- 解决方法
  - 除了浏览器原生实现的dynamic import之外, 现有的运行时加载都是利用动态插入script和link标签实现的. 这一点没什么花头可玩. 别考虑eval, 不靠谱
- 那怎么才能知道插件export了什么呢? 我们只需要做两个约束:
  - 插件编译为umd格式.
  - 运行环境中不能存在require.js等任何amd加载器.

# dynamic-import

- [An ESM bundle for any NPM package](https://medium.com/@joeldenning/an-esm-bundle-for-any-npm-package-5f850db0e04d)
  - https://github.com/esm-bundle/react

- [Using a full URL in a dynamic import()](https://stackoverflow.com/questions/50097327/)
- This is not safe at all, you should not do it IMO. This is as evil as `eval`.
- ES modules aren't guaranteed to support URLs neither in static import nor in dynamic import()
  - Current browser versions (Chrome-based, Firefox, Safari) support URLs for both static and dynamic import, the implementation relies on CORS mechanism and may vary
  - Node.js supports this only with custom ESM loader, it's unlikely that it will allow this by default in future because of security concerns.

- [Can I run a JS script from another using `fetch`?](https://stackoverflow.com/questions/44803944)
- Fetch API is supposed to provide promise-based API to fetch remote data. 
  - Loading random remote script is not AJAX - even if `jQuery.ajax` is capable of that. 
  - It won't be handled by Fetch API.
  - SystemJS is supposed to provide promise-based API for script loading

```JS
const scriptPromise = new Promise((resolve, reject) => {
  const script = document.createElement('script');
  document.body.appendChild(script);
  script.onload = resolve;
  script.onerror = reject;
  script.async = true;
  script.src = 'foo.js';
});

scriptPromise.then(() => { ... });
```

## webpack

- ref
  - webpack await import jsdelivr

- [Error: Cannot find module with dynamic import](https://github.com/webpack/webpack/issues/6680)
- webpack处理dynamic import要求路径前缀即文件所在父目录或祖先目录必须是确定的，不能整个路径是一个变量
  - https://webpack.js.org/api/module-methods/
  - webpack uses a simple logic for building its package bundles. 
  - It can't predict what will happen when the code executes.
  - It pre-packs everything it sees within the `import()` call. 
  - If you call `import('src/'+path)` it will literally package everything in the "src" directory even if "path" is only ever 3 of those files, 
  - because the heuristic that webpack uses is so simple. 
  - It's best to just do them individually.
  - 但是可以使用node的require

- [Using dynamic require on node targets WITHOUT resolve or bundle the target module](https://github.com/webpack/webpack/issues/4175)
