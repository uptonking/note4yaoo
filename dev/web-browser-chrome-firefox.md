---
title: web-browser-chrome-firefox
tags: [browser]
created: '2020-06-28T12:46:23.814Z'
modified: '2020-12-21T07:44:48.911Z'
---

# web-browser-chrome-firefox

# browser-versions

- ref
  - [Chrome version history](https://en.wikipedia.org/wiki/Google_Chrome_version_history)
  - [Firefox version history](https://en.wikipedia.org/wiki/Firefox_version_history)
  - [Safari version history](https://en.wikipedia.org/wiki/Safari_version_history)

- [browser-market-share](https://gs.statcounter.com/)
  - desktop: chrome-0.675, firefox-0.779, safari-0.986, edge-0.796, ie-0.168, opera-0.265
  - mobile: chrome-0.622, firefox-0.0045, safari-0.252, samsung-0.0575, uc-0.0217, opera-0.0191, android-0.0103

- 202101
  - chrome
    - stable(20201112) 87.0.4280, blink 87, v8 8.7
    - canary(20201114) 89.0, blink 89, v8 8.9
  - firefox
    - stable(20201222) 84.0.1
    - future(20210126) 85.0
  - safari
    - stable(20201214) 14.0.2，webkit 610.3.7.1.9, macOS 10.14-11
# browser份额
- [Browser usage table](https://caniuse.com/usage-table)
# chrome
- https://developers.google.com/web/tools/chrome-devtools

- [What's New In DevTools (Chrome 89)](https://developers.google.com/web/updates/2021/01/devtools)
  - Capture node screenshot beyond viewport
    - You can now capture node screenshots for a full node, including content below the fold. 
    - Previously, the screenshot was cut off for content not visible in the viewport. 
    - The full-page screenshots are precise now as well.
    - In the Elements panel, right click on an element and select Capture node screenshot.
  - Lighthouse 7 in the Lighthouse panel
  - Support forcing the CSS :target state
  - Emulate foldable and dual-screen in Device Mode

- chrome各版本特性
  - https://www.chromestatus.com/features
# browser-impl
- https://github.com/lobobrowser/LoboBrowser
  - /44Star/MIT/202004
  - Lobo is an extensible all-Java web browser and RIA platform. 
  - It supports HTML 5, Javascript (AJAX) and CSS 3 plus direct JavaFX and Java (Swing/AWT) rendering. 
  - Cobra is the web browser's renderer API; also a Javascript-aware HTML parser.
- https://github.com/lobobrowser/Cobra
  - Cobra is a rendering engine, origionally designed for LoboBrowser, the gui of LoboBrowser has been separated from it so Cobra can easily be improved by forks of LoboBrowser.
# discuss
- ## [手机端qq浏览器怎么样？](https://www.zhihu.com/question/312923150/answers/updated)
- 挺好用的（不是水军）
  - 第一个是打开文档不错，还可以创建压缩包
  - 第二个是打开一些网页速度还是很快的
  - 第三个是和QQ挂钩，QQ资料卡上有QQ浏览器的等级
    - 因为电脑用的Chrome，手机Chrome没法登录 
- 因为我是大王卡，以前觉得用qq浏览器还能免流，但后来觉得广告太多
# browser-download
- chrome
  - https://www.chromium.org/getting-involved/dev-channel

- chrominum
  - https://www.chromium.org/getting-involved/download-chromium
