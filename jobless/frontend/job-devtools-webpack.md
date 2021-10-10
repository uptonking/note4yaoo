---
title: job-devtools-webpack
tags: [devtools, job, webpack]
created: '2021-09-24T19:13:02.407Z'
modified: '2021-09-24T19:13:17.894Z'
---

# job-devtools-webpack

# guide

# webpack架构相关

# hmr热更新
- 在entry配置与dev-server相互的逻辑
- webpack-dev-middleware 主要负责监听与修改内容
  - 首先调用 compiler.watch()，对本地文件代码进行编译打包，也就是 webpack 的一系列编译流程
  - 编译结束后，开启对本地文件的监听，当文件发生变化，重新编译，编译完成之后继续监听
toDisk() 和 setFs() 即决定了打包后文件写入磁盘还是内存
- server会在监听到 done 钩子后向浏览器发送 websocket 消息
- hotDownloadManifest 请求 xxx/hash.hot-update.json，响应内容是一个 js 对象，给出了需要更新 chunk 的清单（manifest），其中的 chunk 列表会与当前已加载 chunk 列表比较，找出需要重新下载的 chunk
- 拿到新的代码块后会执行 HMR 的 hotApply() ，这是热更新模块替换的核心，主要分为三个阶段：
  1. 找出过期模块与依赖（check 过程中的需更新 chunk 都会被视为过期）
  2. 从缓存删除过期模块与依赖
  3. 将新模块添加到 modules，之后通过 __webpack_require__ 执行模块的代码，这一步相当于最终完成新模块替换
  4. 最后调用 HMR 的 accept() 方法，接收更新（HMR API）

- ref
  - [从零实现webpack热更新HMR](https://juejin.cn/post/6844904020528594957)
# 如何区分 module、chunk、bundle？
- 对于一份同逻辑的代码，当手写下每一个文件，无论是 ESM 还是 commonJS 或是 AMD，他们都是 module
- 当 module 源文件传到 webpack 进行打包时，webpack 会根据文件引用关系生成 chunk 文件，webpack 会对这个 chunk 文件进行一些操作
- webpack 处理好 chunk 文件后，最后会输出 bundle 文件，这个 bundle 文件包含了经过加载和编译的最终源文件，所以它可以直接在浏览器中运行
- 一般来说一个 chunk 对应一个 bundle，
  - 可以使用 MiniCssExtractPlugin 从 chunks 0 中抽离出了 index.bundle.css 文件

- 总结
  - module，chunk 和 bundle 其实就是同一份逻辑代码在不同转换场景下的取了三个名字
  - 未经打包的源文件是 module，chunk 强调 webpack 模块捆绑过程，最后生成浏览器可以直接运行的 bundle

- chunk就是若干 module 打成的包，一个 chunk 应该包括多个 module，一般来说最终会形成一个 file。
  - 而js以外的资源，webpack 会通过各种 loader 转化成一个 module，这个模块会被打包到某个 chunk 中，并不会形成一个单独的 chunk。

# Loader 和 Plugin 区分
- Webpack 将一切文件视为模块，但是原生只能解析 js 和 json 文件，如果想将其他文件也作为模块处理，就会用到 loader，
  - 所以 Loader的作用是让 webpack 拥有了加载和解析非 JS 文件的能力
  - 如mdx-js/loader

- loader 是文件加载器，能够加载不同类型资源文件，并对这些文件进行特定的处理，简单来说就是将webpack 传入的字符串做出特定的处理修改
  - 遵循 Webpack 制定的设计规则和结构，输入与输出均为字符串，各个 Loader 完全独立，即插即用；

- Plugin 可以扩展 webpack 的功能，让 webpack 具有更多的灵活性，解决 loader 无法实现的事情。
  - 在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。
