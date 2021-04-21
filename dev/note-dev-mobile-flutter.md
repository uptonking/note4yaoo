---
title: note-dev-mobile-flutter
tags: [dev, flutter, mobile]
created: '2021-04-21T16:07:56.389Z'
modified: '2021-04-21T16:08:27.595Z'
---

# note-dev-mobile-flutter

# guide

# discuss

- ref
  - [twitter: JetPack compose flutter ](https://twitter.com/search?q=JetPack%20compose%20flutter%20min_replies%3A1&src=typed_query&f=live)

- ## 

- ## [Kotlin、Java和Flutter在安卓项目中的使用情况?](https://www.zhihu.com/question/377409430/answers/updated)
- 对于Android而言， Java至今还是只支持 Java8 而已
  - 安卓上的java本身是阉割版的java，java11之后的特性，基本上安卓上的java没有继续跟进了
  - 而是转向kotlin，以补充低版本java特性的不足
- flutter的owner是谷歌自己，跟kotlin，java的owner不是谷歌自己就不一样
- 当你学会 Java 之后，学习 Kotlin 语言大概就是一周的上手时间，Kotlin 通过大量的语法糖可以加快你的开发速度
- 自己考虑下未来研发的方向，转行Java的工作机会更多

- ## [flutter凉了吗?](https://www.zhihu.com/question/374113031/answers/updated)
- Flutter2.0出来了，Ubuntu选flutter为应用的默认选择
  - Flutter将成为Canonical创建的未来移动和桌面应用程序的默认选择。

- ## [Jetpack Compose or Flutter... which is the safest bet?](https://www.reddit.com/r/androiddev/comments/judj8o/jetpack_compose_or_flutter_which_is_the_safest_bet/)
- Flutter pros:
  - Easy to learn
  - Used by Google themselves in Google Pay, Google Assistant, Google Ads, etc.
  - Used by Ebay, Alibaba, Baidu, Square, Tencent
  - Used by popular apps like Insight Timer
  - Will work on Fuchsia OS

- Flutter cons:
  - Devs seem to prefer Kotlin over Dart
  - If Google drops Flutter, your investment in learning Dart will be for nothing
  - iOS animation bugs
  - Not many first party plug-ins, and some of the few that exist have issues

- Jetpack Compose pros:
  - Similar to SwiftUI, so easier to get into for new iOS devs and current Android devs
  - Built by Google and Jetbrains, who have a track record of excellent products
  - devs who prefer native android won't have much of a problem with this

- Compose cons:
  - Younger project, currently in Alpha, so who knows if it'll catch up to Flutter by the time it's mature
  - If Flutter continues to grow, it'll be harder to convince Flutter devs to switch
  - With so many companies (including Google) already invested in Flutter, what reason do they have to even consider Compose?
  - If Fuchsia turns out to be a success and not a toy project, Flutter will be ahead in this new OS. Doesn't mean Android will just disappear though

- ## Kotlin multiplatform： A new ReactNative/Flutter/cross-platform contender is here
- https://twitter.com/sebastienlorber/status/1300700261359521794
  - Kotlin multiplatform allows to share logic (business or other) between Android and iOS and access native Apis. 
  - No shared UI yet, but that could come later (Jetpack Compose cross platform?)
  - For Swift cross-platform there's also http://scade.io
- Mobile webview tech is still there, and there's a new Cordova alternative pushed by Ionic team
  - https://capacitorjs.com/
  - Capacitor is an open source native runtime for building Web Native apps. 
  - Create cross-platform iOS, Android, and Progressive Web Apps with JavaScript, HTML, and CSS.
  - 既然是基于webview，那对native框架的依赖就会降低

- ## Is Jetpack Compose hot reload possible like Flutter?
- https://twitter.com/MehmetPekerrr/status/1375231185127944204
  - I know Jetpack Compose uses the Skia engine to draw on the screen. But jetpack compose preview is not fast as needed. Is it possible technically?
- Hot reload is technically possible, but is currently constrained primarily by build times, and Gradle is especially slow.  
  - Improving hot reload would require improving build times or using an interpreter to bypass builds altogether - possible but requires more engineering.
  - Hot reload in flutter is powered directly by Dart’s ability to directly inject updated source code into the Dart VM when the app is already running.
  - The JVM has the ability to inject new class/method/field definitions. This is how debuggers work in Java.

- ## Flutter Developers working with Jetpack Compose
- https://twitter.com/Fbillionare/status/1375113097388638212
- The similarities aren't super surprising, as we had ongoing discussions with the Flutter team when designing Jetpack Compose.  Thankful for all their help and friendship!
