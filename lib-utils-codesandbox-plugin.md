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
# webcontainer/nodebox
- pros
  - 让原生程序在浏览器、移动端执行
  - 让浏览器中的文件系统更方便
# iframe
- iframe页面没有自己的历史记录，使用的是基座(父页面)的浏览历史
  - 当iframe页在内部进行跳转时，浏览器地址栏无变化，基座中加载的src资源也无变化
  - 当浏览器刷新时，无法停留在iframe内部跳转后的页面上，需要用户重新走一遍操作
# more
- [比 eval 和 iframe 更强的新一代 JavaScript 沙箱 - JavaScript 提案：ShadowRealm](https://zhuanlan.zhihu.com/p/549547458)

- [iframe接班人-微前端框架qiankun在中后台系统实践](https://zhuanlan.zhihu.com/p/259209543)
