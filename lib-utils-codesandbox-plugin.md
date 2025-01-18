---
title: lib-utils-codesandbox-plugin
tags: [codesandbox, extensions, plugin-system, scripts, utils]
created: 2023-09-02T09:15:34.289Z
modified: 2023-09-02T09:16:30.412Z
---

# lib-utils-codesandbox-plugin

# guide

- tips
  - 简单场景考虑基于eval/Function的方案
  - 复杂场景可参考 microsoft-excel-addon script-lab
# csb-draft
- iframe内的console.log在chrome-devtools可以看到吗
# csb-dev-xp
- 调试codesandbox-client的源码时，注意 packages/codesandbox-api/src/dispatcher/index.ts 的dispatch方法中不要使用 `console.log`，
  - 否则iframe内的console更新事件会向parent window触发on-message的逻辑，顶层window也会通知iframe更新了，导致chrome-devtools不停显示console.log进入死循环

- SandpackClient抽象类有3种实现， Node/Static/Runtime, 前端项目默认使用Runtime

- 💡 点击预览面板内容url发生跳转时，预览面板顶部的url自动更新的实现逻辑
  - 核心逻辑: 预览面板顶部的url渲染在单独的input元素，监听到urlchange事件时会自动更新input元素显示的内容
  - 预览面板顶部的input元素在初始化时会通过 SandpackRuntime.listen方法注册 自动更新input元素的方法 urlChangeFn
  - SandpackRuntime在执行constructor时，会初始化 IFrameProtocol
  - IFrameProtocol在执行constructor时会在顶层window上注册 window.addEventListener("message", this.eventListener); 
  - 顶层window每次收到`message`事件时，this.eventListener会执行所有 this.globalListeners 和 this.channelListeners，其中包含 自动更新input元素的方法urlChangeFn
  - 在 codesandbox-client/packages/sandbox-hooks/url-listeners.js 的setupHistoryListeners方法中定义了iframe的`window.history`变化时，通知parent window的事件，这个增强history的逻辑会在csb-client的入口文件packages/app/src/sandbox/startup.ts执行时立即执行
  - 点击预览面板内容中的超链接url时，会随着`window.history`的变化触发自定义`pushState`的逻辑，立即通过 `window.parent.postMessage(｛type: 'urlchange'｝)`发送消息到顶层window，然后顶层window会触发更新input元素的方法urlChangeFn

- 
- 
- 

# webcontainer/nodebox
- pros
  - 让原生程序在浏览器、移动端执行
  - 让浏览器中的文件系统更方便
# iframe
- iframe内最外层元素的 `height: 100%` 经常导致嵌入元素的整体高度异常或滚动异常

- iframe页面没有自己的历史记录，使用的是基座(父页面)的浏览历史
  - 当iframe页在内部进行跳转时，浏览器地址栏无变化，基座中加载的src资源也无变化
  - 当浏览器刷新时，无法停留在iframe内部跳转后的页面上，需要用户重新走一遍操作
# more
- [比 eval 和 iframe 更强的新一代 JavaScript 沙箱 - JavaScript 提案：ShadowRealm](https://zhuanlan.zhihu.com/p/549547458)

- [iframe接班人-微前端框架qiankun在中后台系统实践](https://zhuanlan.zhihu.com/p/259209543)
