---
title: lib-xplat-pwa
tags: [cross-platform, dev, mobile, pwa]
created: 2022-11-11T00:37:46.916Z
modified: 2022-11-11T03:09:56.491Z
---

# lib-xplat-pwa

> is inactive ❓

# guide
- pwa-cons
  - ❓ 本地离线的index.html或其他资源如图标，如何更新内容
    - 轮询/主动推送
    - 参考twitter个人界面，在其他界面retweet后，个人界面也会随着更新，有延时
  - ❓ 更换浏览器时，pwa如何同步
    - 第三方云存储
    - 基于浏览器内置sync
  - ❓ 更换设备时，pwa如何同步
    - 类似手机厂商的桌面云同步
    - 操作系统的同步桌面，或同步标签页

- 考虑用pwa只处理桌面端跨端离线使用的问题，不处理移动端商店
  - 对移动端需要简化逻辑和调整ui
  - 不要在自动打包上折腾过多精力，一个store一个标准
  - react-native封装webview的方式也许更好
  - 移动端使用sqlite嵌入式数据库更通用

- 实现离线时不使用浏览器扩展的形式
  - indexeddb的访问存在same-origin的限制，不应该维护两套数据(在线url和扩展页url不同)
  - pwa支持离线使用，使用webview打包也简单
  - 但pwa一般不支持类似浏览器的刷新页面

- pwa的离线
  - service worker只处理离线资源，不拦截请求而做缓存
  - 用户操作local-first，缓存用indexeddb而不用service worker

- ref
  - [PWA技术理论+实战全解析](https://zhuanlan.zhihu.com/p/144512343)
  - https://github.com/hemanth/awesome-pwa
# usecase
- 国外案例
  - vscode
  - [excalidraw](https://excalidraw.com/)
  - [tldraw](https://www.tldraw.com/)
  - [draw.io](https://app.diagrams.net/)

- 国内案例
  - [微博 移动版](https://m.weibo.cn/)

- PWA应用商店
  - [Appscope](https://appsco.pe/)
    - https://appsco.pe/toplist
  - [zero data app](https://0data.app/glance/)
  - [Store.app - Explore Modern Web Apps & PWAs](https://store.app/)
# pwa-sites
- MConverter - File Converter: AVIF, JXL, WebP
  - https://mconverter.eu/
# pwa-product-examples
- crossnote
  - https://crossnote.app/

- https://github.com/RobinLinus/snapdrop /GPLv3/202303/js
  - https://snapdrop.net/
  - local file sharing in your browser. Inspired by Apple's Airdrop.
  - Vanilla HTML5/ES6/CSS3 frontend
  - WebRTC/WebSockets
  - https://github.com/schlagmichdoch/PairDrop /js
    - PairDrop is a sublime alternative to AirDrop that works on all platforms.
    - File Sharing on your local network

- https://github.com/blenderskool/blaze
  - File sharing progressive web app built using WebTorrent and WebSockets
- https://github.com/The-Robin-Hood/dropit
  - PWA shares your files locally at ease
# discuss
- ## 

- ## 

- ## What Progressive Web Apps Can Do Today is a *great* demo of all the stuff possible right now in a web browser, no native app BS needed
- https://mastodon.social/@migurski/111757339283733242
  - [What PWA Can Do Today](https://whatpwacando.today/)

- ## 有哪些使用 PWA 的 app ？
- https://www.zhihu.com/question/59108831/answers/updated

- ## PWA过了那么久为什么还没有发展起来呢?
- https://www.zhihu.com/question/325432140/answers/updated
- 感觉还是国内厂商的环境比较差，大家都希望通过APP去吸引更多的流量，不愿意去尝试PWA，如果有成功的案例可以尝到PWA的甜头，应该就会有更多的厂商参与进来了。

- ## 有哪些使用 PWA 的 app ？
- https://www.zhihu.com/question/59108831/answers/updated
- 由于中国的特殊性，PWA 的前景在一定程度上比较悲观：
  - 国内较重视 iOS，而 在ios系统中有50M缓存大小的限制
  - 国内的 Android 实为「安卓」，不自带 Chrome 是一，可能还会有其他兼容问题。
  - 国内厂商可能并不会像三星那样对推动自家浏览器支持 PWA 那么感兴趣。
  - 依赖 GCM 推送的通知不可用，Web Push Protocol 还没有国内的推送服务实现。
