---
title: lib-utils-codesandbox-plugin
tags: [codesandbox, extensions, plugin-system, scripts, utils]
created: 2023-09-02T09:15:34.289Z
modified: 2023-09-02T09:16:30.412Z
---

# lib-utils-codesandbox-plugin

# guide

- sandbox-dev
  - 简单场景考虑基于eval/Function的方案
  - 复杂场景可参考 microsoft-excel-addon script-lab
  - 服务端的设计实现可参考jupyter server
# csb-draft
- 快速预览ai生产的代码
  - codesandbox不够快，npm install的流程本身存在慢的缺点，如何提速

- iframe内的console.log在chrome-devtools可以看到吗
# csb-dev-xp
- SandpackClient抽象类有3种实现， Node/Static/Runtime, 前端项目默认使用Runtime

- 调试codesandbox-client的源码时，注意 packages/codesandbox-api/src/dispatcher/index.ts 的dispatch方法中不要使用 `console.log`，
  - 否则iframe内的console更新事件会向parent window触发on-message的逻辑，顶层window也会通知iframe更新了，导致chrome-devtools不停显示console.log进入死循环

- SandpackPreview组件会渲染预览面板的url和iframe内容
  - 组件中的useSandpackClient会在iframe元素首次渲染时执行sandpack.registerBundler 注册iframe用来 createClient(iframe)
  - SandpackRuntime在执行constructor时，会初始化 new IFrameProtocol(this.iframe, this.bundlerURL); 
  - 然后在顶层window上注册message handler处理iframe发来的事件 window.addEventListener("message", this.eventListener); 

- 💡 点击预览面板内容url发生跳转时，预览面板顶部的url自动更新的实现逻辑
  - 核心逻辑: 预览面板顶部的url渲染在单独的input元素，监听到urlchange事件时会自动更新input元素显示的内容
  - 预览面板顶部的input元素在初始化时会通过 SandpackRuntime.listen方法注册 自动更新input元素的方法 urlChangeFn
  - SandpackRuntime在执行constructor时，会初始化 IFrameProtocol
  - IFrameProtocol在执行constructor时会在顶层window上注册 window.addEventListener("message", this.eventListener); 
  - 顶层window每次收到`message`事件时，this.eventListener会执行所有 this.globalListeners 和 this.channelListeners，其中包含 自动更新input元素的方法urlChangeFn
  - 在 codesandbox-client/packages/sandbox-hooks/url-listeners.js 的setupHistoryListeners方法中定义了iframe的`window.history`变化时，通知parent window的事件，这个增强history的逻辑会在csb-client的入口文件packages/app/src/sandbox/startup.ts执行时立即执行
  - 点击预览面板内容中的超链接url时，会随着`window.history`的变化触发自定义`pushState`的逻辑，立即通过 `window.parent.postMessage(｛type: 'urlchange'｝)`发送消息到顶层window，然后顶层window会触发更新input元素的方法urlChangeFn

- SandpackTranspiledCode组件渲染了一个 display-none 的iframe元素，此组件多用在文档中
  - 这里注册了一个iframe，用来执行 runSandpack -> await createClient(iframe); 

- 
- 
- 

## docker/vm

- 采用容器方案的缺点，不方便单个容器升降级配置
  - 采用vm更方便
- cde容易被利用进行ddos，特别是被NAT后
# webcontainer/nodebox
- pros
  - 让原生程序在浏览器、移动端执行
  - 让浏览器中的文件系统更方便
# iframe
- iframe渲染时注入自定义脚本的实现方案，(针对拦截window.history的场景)
  - 不要采用 `iframe.contentDocument.body.appendChild(script)` 方式来注入包含window.onload的自定义js，直接用iframe.onload
  - onload事件直接注册在iframe元素上，而不是 iframe.contentWindow 上
  - 在iframe.onload事件里面，iframe.contentWindow有值，但iframe.contentDocument为null
  - 🤔: 从top.window访问iframe.contentWindow.history存在跨域限制，解决方案是postMessage
- iframe load事件不触发的另一种思路是，初始iframe不设置src，之后在js中先设置load，再设置src
  - [Iframe onload event when content is set from srcdoc - Stack Overflow](https://stackoverflow.com/questions/62087163/iframe-onload-event-when-content-is-set-from-srcdoc)
    - A workaround that works for me (tested in current versions of Firefox and Chrome) is to set the `srcdoc` after having added the `load` listener
  - [onload event inside iframe only triggers once - Stack Overflow](https://stackoverflow.com/questions/27962471/onload-event-inside-iframe-only-triggers-once)
    - t's due to a race condition - the `load` handler needs to be attached before the iframe loads its `src`.
  - [Dynamically create an iframe and attach onload event to it - Stack Overflow](https://stackoverflow.com/questions/6183737/dynamically-create-an-iframe-and-attach-onload-event-to-it)
    - Some browsers do have the `onload` event for an iframe, first you should try to attach it before setting the iframe's `src` attribute.
    - You could user a timer to check if the frame's contentWindow's readystate is complete

- iframe的跨域问题 🐛
  - 解决访问iframe.contentWindow.document/history出现跨域问题的另一种思路，是在访问地址所在的服务器注入自定义业务逻辑
  - [Blocked a frame with origin "xyz" from accessing a cross-origin frame – Noibu _202501](https://help.noibu.com/hc/en-us/articles/4413414445069-Blocked-a-frame-with-origin-xyz-from-accessing-a-cross-origin-frame)
    - By default, iframes are protected by same-origin policy. This means that any site hosting an iframe is not allowed to access any content within the iframe unless they share the same protocol, domain, and port.
    - The only two actions a site can perform with this iframe are to access its `contentWindow` attribute and modify its `location` attribute
    - Any other interaction with the iframe is considered a violation of the same-origin rule and results in the cross-origin error.

```JS
// This function takes a given url and creates an iframe for it 
let injectIframe = function(url) {

  let iframe = document.createElement('iframe');
  iframe.src = url;

  // This adds a listener to run some code once the iframe initializes
  iframe.addEventListener("load", function() {

    // This is allowed! 
    console.log(iframe.contentWindow);

    // This is not allowed!
    console.log(iframe.contentWindow.document);

  });

  // This adds the iframe onto the target site
  document.body.appendChild(iframe);

};
```

- iframe内最外层元素的 `height: 100%` 经常导致嵌入元素的整体高度异常或滚动异常

- iframe页面没有自己的历史记录，使用的是基座(父页面)的浏览历史
  - 当iframe页在内部进行跳转时，浏览器地址栏无变化，基座中加载的src资源也无变化
  - 当浏览器刷新时，无法停留在iframe内部跳转后的页面上，需要用户重新走一遍操作
# more
- [比 eval 和 iframe 更强的新一代 JavaScript 沙箱 - JavaScript 提案：ShadowRealm](https://zhuanlan.zhihu.com/p/549547458)

- [iframe接班人-微前端框架qiankun在中后台系统实践](https://zhuanlan.zhihu.com/p/259209543)
