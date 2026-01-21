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

# discuss-cn-os
- ## 

- ## 

- ## 

- ## 
# discuss-cn-harmony-huawei
- ## 

- ## 

- ## 

- ## 

- ## [目前鸿蒙系统是Linux还是类unix，以及跨平台方面是使用electron还是flutter？ _202601](https://linux.do/t/topic/1487098)
- 如果你说的纯血鸿蒙，那都不是，next5之后的版本用的鸿蒙微内核，但是怕我们这群开发者掀桌子不跟他玩，预留了类unix的posix接口，你看成类unix也可以（但核心还是他自己的微内核，只是怕你觉得开发麻烦所以强兼了类unix），但也不保证他后面做大了不会一脚把类unix接口踹了换自己的接口玩了，所以前期可以按类unix开发，后期你就要替换成鸿蒙自有接口了，不然效率和新特性你一个都别想吃上
  - 至于4之前的非纯血，带了aosp，那算linux吧（也停更好久了，没啥好适配的，当成安卓就行）
  - 不过跨平台这俩方案好像是都能用，但主流flutter和ArkUI，fl官方适配了oh，所以一般推荐fl，至于el没怎么见过说是，你想强行适配也不是不行，就是费很大劲罢了（还不如放弃）
- arkui/arkts是他自己的，用起来还行，一端开发，多端使用，但属于是拿鸿蒙的代码跑安卓，反向适配其他平台
  - 拿来开发纯鸿蒙端不错，但是多端的话我们是分开的，安卓是安卓，鸿蒙是鸿蒙，不跨平台适配，做的独立包，大部分企业也这么干，个人用fl够了
- 他自己的ide就带ai，深度适配ark语法，我现在就是纯让ai自己改，就是偶尔抽风可能答非所问，反正注意备份别手滑直接点发布或者保存就行
  - 用过chatgpt team的5.2pro做过ark项目，感觉也还行，论界面设计那gpt确实没得说，其他的不敢试，gpt一开始也不知道ark语言，硬是靠他自搜做的项目

- 不知道这个鸿蒙，他们的开发者账号或是签名、上架商店年费具体是多少钱。
  - 现在？免费的，但强实名哦
  - 而且使用量和下载量达标你还有激励奖金拿，我就硬蹭了几千块奖金、十几本证书和开发板，不过我很早就去开发的，算是a测的时候参加的，参加了开源鸿蒙（openharmony简称oh）和闭源鸿蒙（harmonynext也就是现在华为手机上的鸿蒙）
- 应用商店审核严吗？像开发中的软件是怎么侧载的？
  - 说严也不算严，看你开发什么了，我就提交几个小工具蹭奖励而已。不过强实名这点你如果能接受的话都不是啥问题，跟着意见改就是了。
  - 侧载有专门的通道安装，手机上也要打开开关，百度谷歌搜“鸿蒙侧载”有好几个路子，这点也没啥担心的，有些敏感应用只能侧载，算是开了个小口
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
