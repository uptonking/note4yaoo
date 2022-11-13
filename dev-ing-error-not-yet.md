---
title: dev-ing-error-not-yet
tags: [dev, error, not-yet]
created: 2021-03-29T18:54:26.760Z
modified: 2021-03-29T19:29:15.528Z
---

# dev-ing-error-not-yet

# pieces

- ## event argument has no target.result property on IDBRequest: success event_201903
- https://github.com/microsoft/TypeScript/issues/30669
  - 没人修
  - https://stackoverflow.com/questions/61162942

- ## What does status=canceled for a resource mean in Chrome Developer Tools?
- https://stackoverflow.com/questions/12009423

- [Get cancelled xhr Status in javascript](https://stackoverflow.com/questions/52033901)
  - when making the xhr request & in transferFailed function, you will get this.response is null
  - 请求结果为null时可能出现此问题 ？ 

- ## ubuntu The following packages have been kept back:
- https://askubuntu.com/questions/1399734

- ## Overriding existing handler for signal 10. Set JSC_SIGNAL_FOR_GC if you want WebKit to use a different signal
- [GUI starts with empty black window with webkit2gtk 2.32.0](https://github.com/vertcoin-project/one-click-miner-vnext/issues/271)
  - ubuntu上手动降级依赖特别麻烦，需要手动一个个下载传递依赖；并且当gnome依赖某一个传递依赖如gtk版本时，传递依赖不能乱下
  - 降级ubuntu的源可能不能满足gnome依赖，要注意

- ## react-accessible-menu的LotsOfItemsWithinContainer示例，最外层容器只能用height，而不能用maxHeight
  - 否则内容高度会全部显示，而没有预期的overflow-hidden的效果

- ## 编译latex生成的pdf文档中参考文献的链接为什么有cyan色的边框
  - 因为网页上pdf是canvas显示，下面的文字在canvas上有个默认色，当选中时又有一个dom颜色

- ## input设置`border: none; `后，仍然显示边框的问题
  - 排查失败
  - MuiPickersUtilsProvider DatePicker
  - . MuiInputBase-input{ border: 0; }
  - https://codesandbox.io/s/material-demo-forked-fg5xk?file=/demo.js

- ## 在ckeditor项目执行yarn install的异常信息
  - Error: https://github.com/ckeditor/jsdoc: ETIMEDOUT
  - Error: https://github.com/pemrouz/buble: ETIMEDOUT
  - Error: https://github.com/ckeditor/jsdoc: ESOCKETTIMEDOUT

- ## 浏览器窗口占半屏时，直接跳转到@pgd/css docs文档页的url，若url尾部含有锚点如#button，则右边文档内容会被左边fixed的目录挡住，显得凌乱
  - 点击目录文字跳转时也会出现此问题
  - 出现此问题时，若先最大化窗口再半屏化窗口，则问题消失，正常显示
- 解决方法是css魔法 `min-width: 0`
