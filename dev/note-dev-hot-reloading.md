---
title: note-dev-hot-reloading
tags: [dev, hot-reloading, webpack]
created: 2020-07-09T13:24:45.379Z
modified: 2020-12-08T13:37:10.163Z
---

# note-dev-hot-reloading

# guide

- hot-reload相关的功能大多只用于开发测试
  - production环境下通常不需要webpack-dev-server、nodemon、ts-node、ts-node-dev
# discuss
- ## 
# webpack
- `module.hot.accept('./App',callback)` vs `module.hot.accept()`
  - The former: only accepted callback will be executed on each hot loading.
  - The latter: whole js file will be executed each time, not just accept callback.
  - https://github.com/gaearon/react-hot-loader/issues/413
  - 若入口文件或其他文件都不用 `module.hot.accept` 会怎样
    - 实践表明不影响，仍然会hmr
- webpack的hmr热替换通常替换顶层App组件，子组件替换较难，因为会有状态共享、使用context等情况，并且hmr不保存状态
  - 适合react组件的热替换要用单独的工具库如react-hot-loader
  - 可以使用**Paint Flashing**工具高亮浏览器repaint的部分
  - Hot Module Replacement (HMR) exchanges, adds, or removes modules while an application is running, without a page reload. 
  - HMR is particularly useful in applications using a single state tree since components are "dumb" and will reflect the latest application state, even after their source is changed and they are replaced.
  - ref
    - https://apimirror.com/webpack~2/guides/hmr-react/index
    - https://developer.mozilla.org/en-US/docs/Tools/Paint_Flashing_Tool
- With paint flashing enabled, when you load a page, the entire screen flashes green because the browser has to paint everything. 
  - After the page has been rendered, the work is not done because things on the page can change. 
  - Each of these blinking animations requires the browser to paint a part of the screen, represented with a green rectangle.
- webpack编译react代码时，首页只显示html内容，js修改毫无作用
  - 可以通过 `webpack --config ./webpack.config.js` 的方式查看本次编译了哪些文件
  - 发现只编译了 `src/index.js` 的内容，没有编译config文件中 `entry` 指定的文件
  - 暂时的解决方法是根目录及src目录不要存放 `index.js` 文件，这样webpack才会编译entry配置的入口文件

-  live reloading vs and hot module replacement/hot reloading vs React Fast Refresh
  - Live Reload - Triggers an app wide reload that listens to file changes
  - Hot Module Replacement - Is the same as Live Reload with the difference that it only replaces the modules that have been modified, hence the word Replacement. 
  - The advantage of hmr is that it doesn't lose your app state e.g. your inputs on your form fields, your currently selected tab etc.
  - Hot Reloading is just short for Hot Module Replacement.
- webpack-hmr的原理
  - Hot Module Replacement is a core capability offered by Webpack. Webpack's compiler offers a `module.hot.accept()` API. Your application code can register callbacks to run when certain files have been recompiled. Here's how the process works:
    - Your Webpack config needs to include the HMR client code as an `entry` point in addition to your actual application entry file. This adds a small piece to the client bundle, which will open a websocket connection back to the Webpack dev server.
    - Your client application code calls `module.hot.accept("./someFileName", callbackToRunWhenThatFileIsRecompiled)` .
    - Webpack's dev server watches your files for changes, and recompiles source files when you hit save
    - The dev server sends a message to the client, announcing that those files have been recompiled, and including the new versions of the code
    - The client runs any `module.hot.accept` callbacks that match that file's path
  - What happens in that callback is up to you, but normal usage is to re-import the changed file and swap out the affected code, such as a React component or a Redux reducer. If you use this "plain HMR" approach in your own application, you would generally only have one or two calls to module.hot.accept(), such as one for your root component file and one for your root Reducer file. 
- React-Hot-Loader uses the Webpack HMR API in a very powerful, but complex way. 
  - RHL transforms your code as it is compiled to add "proxy" components that wrap around anything that looks like a React component. 
  - Those "proxy" components insert their own `module.hot.accept()` calls at a much finer-grained level, to try to catch updates to each specific React component file instead of letting the updates "bubble up" to the root component file. 
  - The "proxy" components also try to manage the component state for the "real" components, so that when the "real" components get swapped out, the component state is carried over.
  - Unfortunately, there's a lot of edge cases involved, and that causes a lot of problems. Variations in build config can cause RHL to not work right. This is one of the reasons why Dan Abramov originally stopped working on RHL and started Create-React-App - to provide a stable, consistent, and known build environment as a potential baseline for later revisiting the idea of making advanced hot reloading widely available
  - I personally advise that people not use React-Hot-Loader, and instead stick with "plain HMR". 
    - With "plain HMR", updates to your component tree will not keep component state between reloads, 
    - but the implementation is much simpler and more reliable. 
    - Also, Redux goes great with plain HMR, as any data that's kept in Redux is still there when you reload the component tree from edits, and so the app will re-render based on that Redux state.
- ref
  - https://blog.isquaredsoftware.com/2017/08/blogged-answers-webpack-hmr-vs-rhl/
