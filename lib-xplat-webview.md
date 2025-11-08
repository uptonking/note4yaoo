---
title: lib-xplat-webview
tags: [browser, cross-platform, webview]
created: 2023-01-13T10:24:54.200Z
modified: 2023-01-13T10:25:20.501Z
---

# lib-xplat-webview

# guide

# dev-webview

# limitations

# discuss-compatibility
- ## 

- ## 

- ## 

- ## [微信 x5调试页面打不开，因为没有使用x5内核是什么原因？ - 知乎](https://www.zhihu.com/question/507357682)
- 最新版的微信已经不支持使用x5内核打开vConsole调试了。如果需要调试微信内的网页，可以参考以下方式在网页中嵌入vConsole或通过chrome devtools进行调试

- ## [腾讯QQ、微信自带的X5内核和MIUI系统自带的Chromium内核相比，有哪些优势和劣势？ - 知乎](https://www.zhihu.com/question/53902328/answers/updated)
- 在高版本的安卓系统上新版本的微信，之前看过好像也是基于WebView的（当时是看的安卓10）。x5现在只用在兼容低版本系统这个场景。
- 现在微信是自己捆绑了一个Chromium 86内核，叫xweb，默认是不使用系统webview的。

# discuss-python-webview
- ## 

- ## 

- ## 

- ## python做gui除了qt还有别的方案吗？qt真丑
- https://x.com/liujiayi1111/status/1986670166831218788
- 目前多数GUI框架都有Python集成，Python自带的GUI解决方案是tkinter（TCL/TK）。不过这玩意默认比QT丑多了，并且要做好看也比QT难。QT其实可以做得很好看的。QT一个简单的美化选择是Qt-Fluent-Widgets。雨落自己的话，比较喜欢pygtk，因为喜欢用GTK
- pyqt webview，或者pyqt qml，建议还是上webview容易做出好看的gui，还是回归tauri吧

- 如果不是非要桌面软件，flask托管web前端，启动后直接拉起浏览器，在浏览器http前后端交互。前端生态多完善，简单又实用。使用上和桌面软件没啥区别。当然如果必须要桌面软件，用electron或者webview把网页嵌进去也行。

- qt规则太重，学起来累，而且，规则也阻碍了它持续更新

- UI好看主要看设计师
