---
title: note-dev-mobile
tags: [dev, mobile]
created: '2019-06-09T05:37:46.916Z'
modified: '2020-07-14T09:32:18.390Z'
---

# note-dev-mobile

- 跨平台技术选型参考
  - 要不要做app，现在app的需求减少了，连做web的也减少了，小程序正流行
  - 有多少业务计算会放到移动端而不是服务端，对应的框架库是否丰富
  - 考虑同时维护多套移动端代码的成本，后台业务逻辑可通用
  - 考虑跨平台是否需要一致的ui与功能，如ios刘海屏、支付功能
  - 开发ppt应用，webview足矣，也要考虑扩展性

- 跨平台可选技术栈
- 基于webview
  - ionic
- 基于自定义渲染canvas/skia
  - flutter
- 基于平台相关组件/dom
  - react-native
  - kotlin-native
  - Xamarin
  - apicloud
  - uni-app/dcloud
    - 开发一次，编译到10个平台
- 小程序
  - mpvue(deprecated)

# features

- 跨平台一致的ui体验
- 动画支持
- 调用摄像头扫码

# react-native

- 优点
  - 大公司支持
  - 开发迭代快速，更快快速，h5更新有时可绕过审核
- 缺点
  - 引入react-native会增加打包体积，参考electron打包体积的影响
  - 动画在低配设备上效果不佳
  - 进入app的react-native部分时，加载时间较长
  - react-native功能滞后于原生平台提供的新功能
  - 有时不会向后兼容，比如PropType被弃用
  - 定位问题需要时间判断是在react-native还是native
  - 代码容易产生多个分支，增加冲突解决与维护工作
  - 修复问题需要考虑3个技术栈

- 使用体验总结
  - aribnb
    - [20180620](https://medium.com/airbnb-engineering/react-native-at-airbnb-f95aa460be1c)
    - https://juejin.im/post/5b2a5368f265da595c0cf6d5
  - udacity
    - [20180703](https://engineering.udacity.com/react-native-a-retrospective-from-the-mobile-engineering-team-at-udacity-89975d6a8102)
    - https://juejin.im/post/5b421b606fb9a04fd15ff802

- react-native vs ionic-framework
  - ionic4 玩家告诉你 , ionic坑很多 , 三方依赖远不如RN . 我都在推进公司转RN

- ref
- [为什么说现在 React Native 凉了？](https://www.zhihu.com/question/266630840/answers/updated)

# kotlin-native

- 优点
  - google正大力支持kotlin
- 缺点
  - 正在研发期，不稳定

# flutter

- 优点
  - google支持
- 缺点
  - 生态不丰富

- flutter vs react-native
  - 不谈需求选技术的都是耍流氓，开发前一定要先确定好自己的需求和条件，身为独立开发者时间和变现效率是最重要的
  - React Native的优势在于JavaScript和React的丰富生态，并且支持热更新，劣势是在界面兼容和性能上不及Flutter；
  - Flutter的优势在于高性能的界面开发、控件平台无关性和多平台支持，最明显的劣势是不支持热更新，同时目前生态不及React Native丰富。
  - 如果熟悉原生开发，Flutter可能是不错的选择。
  - React Native 的社区要远超 Flutter。但很多库都有2、3年没人维护了。
  - 2020年我依然选择React Native，主要是因为以下几个点：
    - IOS，Android，WEB三端同时开发的成本最低（开发时间成本，学习成本），
      - 很多库、组件web端和手机端的代码几乎一致，比如网络请求，CSS就用Styled Components
    - 大部分的场合，我是不需要那么高的性能的
    - Dart语言的学习成本，而且我不喜欢Dart的那种嵌套地狱式的写法
  - flutter
    - 不成熟是因为生态非常欠缺，连官方package的坑都还没填完，随处可见的"experimental"，
    - 导致复杂应用的开发完全处在一种“找轮子-试轮子-造轮子”的噩梦般的处境之中，对原生开发能力是相当大的考验，
    - 所以即使版本已经来到1.xx-stable，对于没有超强定制能力的非大厂开发团队，Flutter目前仍然不适合用于生产。
  - 我大胆猜测一下：Flutter在Android上最终不会有大的作为。
    - Flutter是Dart和Fuchsia团队的东西，现在没看到Android团队有什么支持动作；
    - Android官方的态度现在已经全面倾向于Kotlin了，而Kotlin 的官方态度也是声称可以跨平台（虽说不成熟，但是可以看得出Kotlin的努力方向）；
    - 最新的 JetPack 开发工具中，有了Kotlin 实现的 JetPack Compose，
      - 这个东西和Flutter本质上是一样的，是自己通过底层来绘图(现阶段还是基于Android Canvas，不过可以方便换成其他的绘图实现)，而没有走Android 视图那一套，
      - 从技术上来讲JetPack Compose 也可以实现跨平台；
    - Dart实在是弱，尤其是对比起来Kotlin；
    - Flutter在现有项目上扩展很难，也就增加了大家切换到Flutter的阻力；Flutter 不支持热更新；

- ref
  - [在 2020 年，跨端开发时 Flutter 和 React Native 哪个更值得选择？](https://www.zhihu.com/question/384934444/answers/updated)
  - [开发跨平台 App 推荐 React Native 还是 Flutter？](https://www.zhihu.com/question/307298908/answers/updated)
  - [flutter凉了吗?](https://www.zhihu.com/question/374113031/answers/updated)
  - [为何有人会喜欢Flutter？](https://www.zhihu.com/question/427198090/answers/updated)

# android

- 开发因素
  - android设备过于碎片化，不同尺寸不同分辨率的设备ui体验很难一致

- [JetBrains将Skia接入Java的Skija项目_202011](https://www.zhihu.com/question/430884791/answers/updated)
  - 这个东西很明显是为了给Compose铺路啊，看来 Kotlin Compose 全平台UI的日子不远了。
  - JB的思路和flutter很像，都是上层的声明式UI，底层直接图形库渲染，然而Compose做得好的地方是它使用了Kotlin这个谷歌官方支持的语言，而flutter选择的dart则像是一个有人生没人养的孩子，谷歌对它的支持完全不如Kotlin这个干儿子
  - 对于jb要推出的skija很看好，应该是为java成熟老旧的以awt/swing为主的gui交互带来了新的变革与驱动力
    - （swt这种纯原生native gui封装就不提了，越来越没落）
    - 从架构设计理念来讲，swing是相当优秀的，很早就已经采取java 2d绘制widget方式，而非os native widget，
      - 支持可插入式look and feel模式，这就为完全的自定义界面发挥提供了宽阔的空间
      - swing的丑应当主要是自带的默认look and feel的原因
    - 后来windows上的direct ui也是一样的思路。
    - qt实质上底层也是自绘的widget，只是在windows上可以模拟native widget非常逼真
    - jb的全家桶都是基于intellij idea的应用框架，那就是用java swing构建的，只不过jb自己开发了两套高质量的look and feel，一个是亮色的，一个是暗黑的（darcula laf），都已开源
    - 但随着gpu图形加速技术以及交互体验需求的进一步提升，swing及其依赖的传统底层java 2d库已经跟不上形势了，所以出现了javafx基于prism 3d基础，跨平台利用gpu以新的风格样式试图取代swing
    - 但jb另辟蹊径，基于skia，是想从底层代替java 2d开始，构筑类似swing但又充分利用现代图形加速技术的脱胎换骨的新java gui体系。skia已经是广为使用的很成熟的技术栈了，相信以jb的能力，很可能会首先在jb自己的全家桶中见到skija的效果
  - 使用Java语言本身构建的2D绘图API绘制的图像确实是质量堪忧
    - 不支持GPU后端加速不说，原生的GUI 框架Swing简直能够丑上天际，
    - swt、awt则一直保留win98、win2k时代的影子，lookAndFeel提供的几个内置的主题简直无法吐槽
    - 重量、不美观、一直是Java上Desktop GUI的噩梦
    - JavaFX尽管对之前的这些GUI框架有着极大的提高，但实在是太迟，大部分轻量级桌面GUI市场早就被C# API、Qt瓜分了个干净
  - Skia性能毋庸置疑，本身添加了GPU绘制的支持，并且添加了现代GPU后端API支持，包括OpenGL和Metal、Vulkan估计马上就来，它的性能还会差的了么，
    - 至于美不美观，就看GUI框架的设计者的功力了，而不是调用native api 去绘制原生控件
    - 不过java+skia的支持就逆转了这个局面。Java本身可以跨平台运行，并且可以通过这套API形成自绘控件系统。
    - 只要编译好skia对android、Windows、Linux、OS X的动态库，就可以使用一套jar去直接调用动态库去显示GUI了。
  - Flutter底层用的就是Skia+OpenGL的自绘制策略，图形绘制上性能确实是相当流畅。
    - JB推出的Compose Jetpack对于桌面和移动端对Flutter应该是有相当层面上的借鉴。
    - 放弃Native API使用Skia作为图形后端会不会有些大胆？不会的，人家说了：Google Chrome, Android, Flutter, Firefox Canvas, Xamarin, LibreOffice 都有在用，我用怎么了？

# ios
