---
title: dev-ing-error-not-yet
tags: [dev, error, not-yet]
created: '2021-03-29T18:54:26.760Z'
modified: '2021-03-29T19:29:15.528Z'
---

# dev-ing-error-not-yet
- 编译latex生成的pdf文档中参考文献的链接为什么有cyan色的边框
# pieces
- ## input设置`border: none; `后，仍然显示边框的问题
  - 排查失败
  - MuiPickersUtilsProvider   DatePicker
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
