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

- [Google proposes way for Fuchsia OS to run Android and Linux programs ‘natively’](https://9to5google.com/2021/02/12/google-fuchsia-os-android-linux-programs-starnix/)
  - [[rfc] Running unmodified Linux programs on Fuchsia](https://fuchsia-review.googlesource.com/c/fuchsia/+/485181)
  - the expectation was that Fuchsia could accomplish this in the same way that Chrome OS is currently able to run Linux apps, by running a full instance of Linux in a virtual machine.
  - Chrome OS is even set to use this same strategy for its ability to run Android apps, thanks to a project called arcvm.
  - a new [proposal](https://fuchsia-review.googlesource.com/c/fuchsia/+/485181/1/docs/contribute/governance/rfcs/NNNN_starnix.md) has been put forward for an alternative solution for Fuchsia to run programs meant for Linux and Android. 
    - Instead of running Linux itself, Fuchsia would gain a system called “Starnix,” which would act as a translator between instructions for the Linux kernel and instructions for Fuchsia’s Zircon kernel.

# pieces

- ## 

- ## 

- ## 

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
