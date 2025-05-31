---
title: lib-xplat-community
tags: [cross-platform]
created: 2021-05-13T07:45:52.261Z
modified: 2021-05-13T07:47:11.964Z
---

# lib-xplat-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-ios
- ## 

- ## 

- ## 

- ## Arc/Dia 浏览器的团队也解决不了 SwiftUI 的性能问题，退回到了 AppKit。
- https://x.com/waylybaye/status/1927615528102965478
  - OpenCat macOS 早期版本也总是卡，优化无果后我直接重写了，几乎所有的 SwiftUI 基础组件：文本、图片、输入框、列表都用 AppKit 重写。然后就一点不卡了…… 
  - 现在 OpenCat 是三套原生代码。

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Wait, just remembered native apps don't have CSS. I might be in trouble.
- https://twitter.com/markdalgleish/status/1435055048967409668
- React Native has a kinda fake CSS thing, it's pretty OK.
- In react native we exclusively use inline styles…you’re gonna love it!
- React native is fantastic. There’s a great library called @shopify/restyle which makes it so nice
- Android does have styles. They don't cascade though, just inherit

- ## #RN4Desktop "delivers huge performance wins" over Electron and combines high quality, delightful, _native_ UX and dev experience. 
- https://twitter.com/ReactNativeMSFT/status/1428463475668389891
- This is what happens when components are allowed to be independent, not vendor controlled & web bound. 
  - Electrons days are practically numbered once desktop platform renderers are stable. 
  - A future in which you can drive any platform and participate in a truly x-platform eco-system
- Do you think we will see a wegl render for desktop like expo made for mobile any time soon? If we could run reac three fiber native on desktop within react native desktop that would be huge

- ## 分享下跨端引擎的一般实现思路
- https://www.zhihu.com/pin/1375839930619396097
- 首先，跨端要有一套统一的api，一般都是实现前端的那些 dom api，
  - 这样在这个容器之上可以跑前端框架，再上层就是前端写的业务代码了。
  - 容器之下的api实现由native来实现，比如dom、style的 api 由安卓、ios各自的布局方式来实现，设备的 api 也是一样。
  - 原生实现的api通过 jni 等方式提供给 c++ 调用，注入到js引擎（c++）中。 
  - 这样前端写的业务代码就可以用这些api来完成各种布局、交互、逻辑的开发了。
- 当然这套统一的api也不一定非得实现前端那一套，
  - 比如flutter就是使用自己的标准，使用 dart 来写逻辑，渲染也是自己的一套，优点是针对性更强，缺点就是不能对接前端生态。
  - 也有使用flutter的渲染能力对接前端的dom、style 的api的方案，比如kraken，这样容器之上依然是前端框架，只不过渲染相关api的实现换成了 flutter。
  - 不管是 flutter、还是安卓、ios 实现，都要对接 chrome devtools 来做调试，提供和前端开发一样的调试体验。
- 容器的思路是运行时的思路，另一种思路就是编译的思路，比如小程序的转译工具 taro、uniapp 等，不过这种思路边缘 case 太多，它们也越来越多功能靠 runtime 来做了。
  - 不管是运行时容器的思路还是编译的思路都需要一个比较大的团队来长期维护，这个不是小公司能够做的，只有大公司才会搞这些。
  - 这也是vue不考虑做跨端的原因（weex和尤大关系不大），投入太大了。
