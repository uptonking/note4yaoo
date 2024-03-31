---
title: thread-fwk-mobile-cross-platform
tags: [framework, mobile, thread]
created: 2021-04-30T14:17:46.235Z
modified: 2021-04-30T15:26:55.024Z
---

# thread-fwk-mobile-cross-platform

# guide

- 新操作系统是否支持主流娱乐app
  - macOS支持的不够多
  - ChromeOS支持的太少
  - 普通的办公软件支持的多不多
  - 专业软件如ps设计、机械、地图几乎都不可能支持
# discuss
- ## 

- ## 

- ## 

- ## 🆚️ 请问大家，2024 年了，跨平台移动端开发，Capacitor vs. React Native vs. Flutter，你们会怎么选？好奇一些真实的使用体验
- https://twitter.com/noworkforsixian/status/1774332953683964369
- 在我眼里 Web > React Native >> Swift UI >>>>> Flutter
- RN. 最少我Flutter写得很糟心…
  - Dart的语法也不太喜欢
  - 比较影响的还有Linux上直接跑好像还不能热重载（浏览器可以，桌面我没重载成功过）
- 如果有跨平台移动端社交类开发，我应该选RN，毕竟dart要从头学
- 不来试试Compose吗，kt写起来真的挺舒服的，这框架再完善完善应该能很不错
  - iOS 还在 Alpha
- 公司大，用flutter，体验比较好。小公司，直接H5离线一把梭
- 如果考虑最优体验、最优性能、最好生态的话，三个中 flutter 会更好（基于原生渲染），背靠  Google 也在持续投入，未来很多体验问题也会继续解决。（包括鸿蒙适配）
- 感觉最快最简单，最省时间的就是capacitor了，他们家ionic感觉都挺活跃的。只要不涉及小程序，单兵作战那就capacitor
- Kotlin multiplatform, 业务逻辑早就可以共享，现在还有compose 可以共享UI层代码。
- 我2018年开始用react native开发，之前做原生android开发。react native的热更新太好了，后期维护要比其他好太多了。flutter听说运行效果会比react native好一些。但是这个我觉得见仁见智。最后要说运行体验，那肯定原生比这些都强，但是一般普通的应用，区别不大。
- 主动权在甲方，独立开发者的话，不会选跨端少的
- 看看第三方的对跨平台支持。
- 这年头学语言的成本极低不会浪费你多少时间

- 有人提到开发成本，其实目前很多 UI 框架都是基于声明式的（SwiftUI、Jetpack Compose、flutter 等），学习成本都比较低，理解一次基本各个框架核心都理解了，只剩 api 的理解成本了，相反 js 的学习成本可能更高（capacitor 基于 vue、rn 基于 react）。

- NativeScript有话要说
  - 现在可以直接用DOM了，整个web生态都能用

- ## 🚀 I'm please to announce that Node.js Mobile is rebooted! New docs, new version, new CLI tool _202310
- https://twitter.com/andrestaltz/status/1718591964235362642
  - Node.js can run inside a mobile app
  - Its core component is a library – available for Android and iOS – that lets you add a Node.js background worker to any mobile app.
- If its what am thinking that means with this package we can achieve ssr on react-native? Since the package brings node runtime to our app
  - In theory yes. I don't know if it's actually easy, or if it makes sense.
- What do people build with nodejs on mobile?
  - @manyver_se , has a TCP server, a UDP server on LANs, and an HTTP server, all running from a mobile app
- That means my app can run a self hosted server function like NextJs which fullstack?
  - Yes

- ## if I were working on React Native stuff, I would seriously consider statically linking JavaScriptCore on iOS. 
- https://twitter.com/jarredsumner/status/1416842049823772673
  - Since the JIT is disabled anyway
  - you can do bytecode caching!
- turns out JSC does have a builtin console.log, it's just disabled in their API
- https://github.com/mceSystems/node-jsc
  - A node.js port to the JavaScriptCore engine and iOS

- ## Jetpack Compose advances to the browser! 
- https://twitter.com/kotlin/status/1389550923635167232
  - Our newest technology preview brings Google’s toolkit for building reactive user interfaces with Kotlin to the web.
- [Technology Preview: Jetpack Compose for Web](https://blog.jetbrains.com/kotlin/2021/05/technology-preview-jetpack-compose-for-web/)
  - Compose for Web is far from being done
  - We still want to provide a first look at this new Kotlin/JS-powered target for Jetpack Compose
  - Jetpack Compose for Web works on top of Kotlin Multiplatform, meaning you can develop an Android, Desktop, and Web application using Jetpack Compose as your UI framework
  - Kotlin Multiplatform allows you to share platform-agnostic code and functionality like your business logic through common code, while still being able to implement and use platform-specific functionality from Android, Desktop JVM, and the JavaScript ecosystem alike.
  - In this preview, you can already freely reuse all core Compose state management concepts across the platforms. 
  - Compose for Web currently does not allow you to directly reuse existing widgets (unlike the Android and Desktop targets for Jetpack Compose, which allow direct code sharing for most widgets out of the box).
  - However, you can use Kotlin Multiplatform’s expect/actual mechanism to build your own common widgets with implementations for all three platforms. 
  - This way, you can apply the same principles to build your app UI on mobile, desktop, and web.
  - This technology preview includes two types of APIs that we are currently exploring and designing for declaring user interfaces in Kotlin code with Compose: a DOM API, and a web implementation of the widgets you already know from Jetpack Compose for Desktop and Android.

- ## Fuchsia is not an Android replacement
- https://twitter.com/alex_tiki/status/1388091353867948032
- Only a question of time 😁 but after the court win against Oracle you could be right
  - Oracle took Google to court about licenses on uses of Java (APIs).
- Google started Fuchsia for 2 totally different reasons: 
  - (1) they consider linux kernel insecure because monolithic, 
  - (2) they want to solve the Moore's law limit on the software, therefore they want to design a different hw, 
  - and they need a different os (Fuchsia) to take full advantage over this new design. 
  - Fuchsia at the core has a lightweight microkernel (zircon) which has one nice peculiarity: can run any other os on top of it. Therefore, it can scale from small devices like IoT and so, to watches, phones, tablets, laptops and so on. As you can see, it's not targeting phones only. 
- One simple use case is to introduce Fuchsia on phones, but headless: it will run Android on top of it, so for the user (and you and me) it will be a normal Android phone, just x200 faster (random number here), with same specs and price, but different hw design. Would you buy it? 
  - Fuchsia will grow, later on, they'll introduce a shell to it, and possibly a laptop running it, with their own silicon SoC alike Apple is already doing with the M1. Interesting times ahead of us.
- I don't doubt that they will coexists for quite a while but if the Fuchsia phones are good Android will vanish as fast as Windows Phone
  - True that, but now you're talking still 5-10 years from now, say 2030 or so. 
  - Because there's the whole ecosystem of Android apps, and they know very well an os without them is nothing. 
  - So, they **could easily prefer an headless Fuchsia** running Android on top of it, to a phone running the Fuchsia shell, which will run Android apps against Android running within Fuchsia. 
  - Because Fuchsia is declarative with nouns and verbs, so it could take some time to adapt it to phones. But maybe you're right and this comes faster than I think

- ## [Google proposes way for Fuchsia OS to run Android and Linux programs ‘natively’](https://9to5google.com/2021/02/12/google-fuchsia-os-android-linux-programs-starnix/)
  - [[rfc] Running unmodified Linux programs on Fuchsia](https://fuchsia-review.googlesource.com/c/fuchsia/+/485181)
  - the expectation was that Fuchsia could accomplish this in the same way that Chrome OS is currently able to run Linux apps, by running a full instance of Linux in a virtual machine.
  - Chrome OS is even set to use this same strategy for its ability to run Android apps, thanks to a project called arcvm.
  - a new [proposal](https://fuchsia-review.googlesource.com/c/fuchsia/+/485181/1/docs/contribute/governance/rfcs/NNNN_starnix.md) has been put forward for an alternative solution for Fuchsia to run programs meant for Linux and Android. 

    - Instead of running Linux itself, Fuchsia would gain a system called “Starnix,” which would act as a translator between instructions for the Linux kernel and instructions for Fuchsia’s Zircon kernel.
