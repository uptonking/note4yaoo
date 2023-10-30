---
title: thread-web-mobile
tags: [job, mobile, thread, web]
created: 2021-09-29T06:38:20.588Z
modified: 2021-09-29T06:38:35.002Z
---

# thread-web-mobile

# guide

# discuss-stars

## 

## [Web App vs Site vs Hybrid_202310](https://icing.space/2023/web-app-vs-site-vs-hybrid)

- Rather than worry about framework features, I think in terms of URLs, HTTP status, HTML `<head> & <body>`.
# discuss

## 

## 

## [Mattermost Mobile Search Optimization Challenge](https://www.youtube.com/watch?v=_qYFonJoyZI)

- This PR speeds up the response time when a user switches between the Messages and Files tabs in the search results screen.
  - https://github.com/mattermost/mattermost-mobile/pull/6579
  - 👉🏻 This was accomplished by mounting the Files and Messages in a view that is twice the device width and transitioning the View left and Right when clicking the Messages or Files tabs. This greatly increases the speed because the posts and files are only rendered once.
  - Another change was to let the two results views scroll independently so the user can scroll in one view, view the other, and upon returning to the original view, their scroll position will have been persisted.

## [design crew, which would you pick for a mobile layout?](https://twitter.com/steveruizok/status/1564893253274673152)

- Wow, Miro’s mobile team has some great solutions here.
- Maybe go back to what we're doing currently, which is to put all styles into a menu that's either open or closed? Basically the same layout as in desktop, but hidden behind a button.

- I think in a case of mobile, less is more.  Kinda like you show with Miro below, hide what's not needed.
  - Also, buttons have to be notably larger to avoid fat-fingering, so delicate, loaded toolbars probably need to avoided entirely in favor of a few larger ones (when applicable)

- Not a designer, but most mobile apps for editing photos and the like (that I’ve used on iOS) have the tool selection at the bottom like C.

## [hacker news: I Replaced My Native iOS App with a Cross-Platform Web App and No One Noticed](https://news.ycombinator.com/item?id=31243501)

- This post makes very big claims based on a very basic application that doesn't seem to be much more than a few toggle buttons and a couple of animations thrown in, and some 'statistics' that don't appear to be based on any actual facts.
  - I work in a team developing an app that has around 5million users, and we abandoned an Ionic first version 5 years ago, after a couple of years of nightmarish development, where (after the first implementation, which went reasonably well) 
  - **we spent most of our development time fixing** inexplicable bugs, chasing native features, getting inconsistent UI problems, broken builds from package updates and a myriad other problems that just drained our energy and were generally dispiriting.
  - I personally felt the entire experience was a horrible professional dead-end. Luckily our management decided to switch to a native application, and learning Swift has been the most fulfilling part of my entire career. The application is faster, more reliable, the bugs are locatable and fixable; the entire framework feels solid and professional.

- I like react-native and nativescript's approach a lot more.. They use native UI elements.

- I can second this. My Ionic app runs incredible stable, no issues, users are happy. It is not super complex and doesn't make use of native APIs beyond in app purchases, but it isn't super trivial either.
- The performance is good on modern devices to the point where you don't notice a difference.
- The main downside are these things:
  1. No fine-grained control over input types / the keyboard that is displayed. You basically have to use whatever Safari gives you. The options got better in recent years, but a native app has better control over the type of keyboard it shows (maybe you can achieve similar effects with a plugin).
  2. The UI obviously does not respect accessibility settings. For example, if you enable the O/I markers on toggle buttons on the OS level, your app won't show them. But I think React Native wouldn't show them either, so there's that.
  3. Can be a pro and a con: Your app shows the same UI for every OS version. Let's say a user is still on iOS 11 and Ionic tries to adhere to the design language of iOS 15, an app update will also affect iOS 11 users. Whereas with native apps, you can basically say "take this headline element and show it in the way the OS renders this by default". Imho, this doesn't matter for normal users that much, but if you obsess over design, it can be a downside or at least somewhat unexpected.
- And you get a lot of upsides:
  1. Truly one code base with close to zero custom code for each platform. Hence, a solo developer can easily develop an app for iOS, Android, and the web.
  2. Assuming you use Ionic's Capacitor as a runtime environment on devices: It is basically a thin wrapper for Chrome. Since Chrome is evergreen even on older devices, I usually never run into browser issues if users are on Android 6 for example. They simply have the most recent Chrome version and your app benefits from that.Compare this with iOS: Users with an older iOS version run an old version of Safari and hence, you need to make sure that your JS code doesn't break on older Safari versions. Although the compatibility with modern JS got a lot better since iOS 11.
  3. You can easily force the same design on all platforms if you want. I wouldn't recommend it, but for some enterprise-internal tooling, it might make sense.
- To sum it up, especially indie developers who want to build an app very fast and don't have a team should give Ionic a try.

- React native and flutter are very, very different from a PWA.
  - While a PWA is a web app, react-native renders actual native components, and flutter has its own rendering engine. I wouldn't call them "web-based" tech

- Having a cross platform app (Flutter) with tens of thousands of users for a few years now I can tell you that not a single person has cared to far.
  - I get 20-50 mails daily through a very easy to use feedback and support function, but in none of those thousands of mails has anyone ever cared about how transitions are made or that a button doesn't look like a native iOS button.
  - They care about the value the app provides. About new functions or (in my case) report bad data to fix. That's why they download an app. Not because they want the button to look natural.
  - That's to say. I frequently get feedback about how they love the UX/UI of my app.
  - If there isn't a valid reason to create a native app these days I consider it a waste of time.

## [I Replaced My Native iOS App with a Cross-Platform Web App and No One Noticed](https://javascript.plainenglish.io/i-replaced-my-native-ios-app-with-a-cross-platform-web-app-and-no-one-noticed-1653901ce244)

- So it all started when I came up with the idea for an app that helps parents get their kids ready for school.
  - why not build a todo list for kids? I could make the UX look like a game and even embed gamification design elements to help keep kids focussed and engaged.
- But during my development, I made a huge mistake. I wasted a lot of time building a native iOS app.
- So I decided pretty early on that School Morning Routine couldn’t be a cross-platform web app. My app would involve heavy use of game-style animations and since it’s for kids, it would need to have excellent touch interactions.
  - So… I decided to make native apps. 
- I decided to build the web app next. 
  - I used React with CSS animations, framer motion, and a dash of delightful Lottie animations thrown in. 
- I went to my desk, deleted my native iOS app, and decided to use **Ionic Capacitor**.
- The cost/benefit tradeoff for cross-platform web apps has always been about trading worse performance in exchange for less development time. 
  - In 2014 for most apps, that was a bad tradeoff. But in the past 8 years, a lot has changed. Browser performance has steadily increased

- Cross Platform Web Apps don’t work offline though
- I’ve built over ten iOS and Android apps in the past few years. 
  - Native apps aren’t dead, and they won’t ever be dead. 
  - Cross-platform mobile apps will improve and evolve; 
  - **however, there is a reason why native apps won’t ever be dead**. 
  - Try to build a streaming service or anything that needs to access low-level APIs, test it, and let’s talk. 
  - 60FPS is impossible to get via web apps except for RN and Flutter.
  - Battery or healthy CPU is almost impossible to reach via web cross-platform. 
  - Native UX, animations, and user feel are priceless.

## [JavaScript检测手机浏览器的五种方法](https://www.ruanyifeng.com/blog/2021/09/detecting-mobile-browser.html)

- navigator.userAgent
  - if (/Mobi|Android|iPhone/i.test(navigator.userAgent)) 
  - 最简单的方法就是分析浏览器的 user agent 字符串，它包含了设备信息。
  - 只要里面包含mobi、android、iphone等关键字，就可以认定是移动设备。
  - 优点是简单方便，缺点是不可靠，因为用户可以修改这个字符串，让手机浏览器伪装成桌面浏览器。
- window.screen，window.innerWidth
  - if (window.screen.width < 500) 
  - if (window.innerWidth < 768)
  - window.screen对象返回用户设备的屏幕信息，该对象的width属性是屏幕宽度（单位为像素）。
  - window.innerWidth返回浏览器窗口里面的网页可见部分的宽度，比较适合指定网页在不同宽度下的样式。
- window.orientation
  - if (typeof window.orientation !== 'undefined')
  - 第三种方法是侦测屏幕方向，手机屏幕可以随时改变方向（横屏或竖屏），桌面设备做不到。
- ontouchstart
  - 'ontouchstart' in document.documentElement
  - 手机浏览器的 DOM 元素可以通过ontouchstart属性，为touch事件指定监听函数。桌面设备没有这个属性。
- window.matchMedia()
  - window.matchMedia("only screen and (max-width: 760px)").matches
  - 最后一种方法是结合 CSS 来判断。
  - 如果某个针对手机的 media query 语句生效了，就可以认为当前设备是移动设备。
  - window.matchMedia()方法接受一个 CSS 的 media query 语句作为参数，判断这个语句是否生效。
- 工具包
  - https://github.com/duskload/react-device-detect
