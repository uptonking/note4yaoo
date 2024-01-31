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
