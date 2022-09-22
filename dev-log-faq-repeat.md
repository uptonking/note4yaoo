---
title: dev-log-faq-repeat
tags: [dev, faq, repeat]
created: 2021-02-27T14:40:13.374Z
modified: 2021-03-29T19:17:20.657Z
---

# dev-log-faq-repeat

# is `JSON.parse` faster than declaring an object literal

- [The cost of parsing JSON](https://v8.dev/blog/cost-of-javascript-2019#json)
  - Because the JSON grammar is much simpler than JavaScript’s grammar, JSON can be parsed more efficiently than JavaScript. 
  - This knowledge can be applied to improve start-up performance for web apps that ship large JSON-like configuration object literals (such as inline Redux stores).
  - Instead of inlining the data as a JavaScript object literal, it can be represented in JSON-stringified form, and then JSON-parsed at runtime
  - **As long as the JSON string is only evaluated once, the `JSON.parse` approach is much faster compared to the JavaScript object literal**, especially for cold loads.
  - A good rule of thumb is to apply this technique for objects of 10kB or larger — but as always with performance advice, measure the actual impact before making any changes.
  - At small-scales, JSON.parse is not faster than using object-literals in JavaScript.

- ref
  - [If that's the case, why are my results showing otherwise?](https://stackoverflow.com/questions/59149074)
# web app running in webview vs browser
- [android WebView](https://developer.android.com/reference/android/webkit/WebView)
  - In most cases, we recommend using a standard web browser, like Chrome, to deliver content to the user. 
  - `WebView` objects allow you to display web content as part of your activity layout, but lack some of the features of fully-developed browsers. 
  - A WebView is useful when you need increased control over the UI and advanced configuration options that will allow you to embed web pages in a specially-designed environment for your app.

- [What is the engine of Android native browser?](https://stackoverflow.com/questions/33998074)
- Starting with Android 4.4 KitKat, Google has begun licensing Google Chrome (a proprietary software) separately from Android, but usually bundled with (what most device vendors did). 
- Android 4.4 includes a completely new implementation of WebView that's based on Chromium 30. 
  - The new Chromium WebView is included on all compatible devices running Android 4.4 and higher.
- Starting with Chrome version 51 on Android 7.0 and above, the Chrome APK on your device is used to provide and render Android System WebViews. 
  - You can choose your WebView provider by enabling Developer Options and selecting WebView implementation.
  - multiprocess - Starting with Chrome version 51 in Android 7.0, WebView will run web content in a separate sandboxed process when the developer option `Multiprocess WebView` is enabled.
# 配置项过多时，如何处理更好，特别是针对组件或应用
- tips
  - search: component too many props/options
  - Too many options = bad software.

- 参考
  - vscode的settings页面
  - tsconfig的配置options页面
  - webpack的配置
  - css属性的类别和属性值的指定

- 惯例优先原则/约定优于配置(convention over configuration)
  - 提供合理的默认值
  - opinionated的另外一个同义词是Convention over configuration，或者coding by convention
- 拆分出弱耦合的小组件，然后组合小组件
- 将部分紧密相关的配置项组合成一个大对象作为一个大的配置项，还要考虑方便替换该大配置对象的默认值
  - group by features
  - 类似component的`variant`属性，设计目的就是一次修改多个值
- 利用custom hooks，将配置项参数作为函数的参数，而不是组件自身的参数
  - 也称为 state reducer pattern

- It has too many configuration options and lacks configuration-by-convention dependency injection, one needs to look up all the services

- [A component with 500+ possible variants feels too much imho.](https://twitter.com/apixelpusher/status/1336875440972181510)
  - 本次讨论没有提出解决方案
  - If I’ve learned anything that past two weeks of focusing on standing up a library quickly it’s to not over-complicate variants or have too many of them for a single component. It’s not useful to force people to waste time parsing a ton of options in a bunch of select inputs.
  - I think this might be true for a lot of components, but a button in a reasonably complex design system? That's easily 500+ (1000+ depending on complexity) variations in the code component. How are you all doing this? Split by size (or w/e), even if that's not true in code?
    - `<Button>` props:
      * Size (several)
      * With icon (left or right)
      * Prominence (primary, secondary, tertiary, etc)
      * Visual style (default, success, danger, brand, etc—we had a lot lol) 
      * Automatic width vs sized to container
      * Some others I'm missing heh

- [What do you get when you put too many props on a component instead of breaking it into smaller components? Prop soup](https://twitter.com/NerdCowboy/status/966027592506617856)
  - if you want the most flexibility, compound components are the way to go imo. 
  - It allows you to create a wrapper component where you can pass in an object like you're saying AND you can create custom functionality elsewhere when you need it.

- [Hick’s Law predicts that the time and the effort it takes to make a decision increases with the number of options.](https://twitter.com/InfoKaaswell/status/1261675520271548418)
  - The more choices, the more time users take to make their decisions.
  - Trello's 3rd signup step has a dropdown with 15 options.
  - That makes it hard to pick one:
  - In a travel booking app like Airbnb, having too many options can lead to a paradox(矛盾的人/事) of choice (and a churn!):
  - Duolingo's list of lessons can sometimes be overwhelming
  - Zapier showed too many navigation links during their upgrade flow which distracts you from crucial checkout steps
  - Find an area where you have a lot of options or a lot of repetitions.
  - Try to either reduce the number of options or find ways to hide items.
  - If you can't minimize the options, try to put them in an easily skimmable order and make sure the items are familiar; else, it won't work.

- ref
  - [Avoid soul-crushing components](https://epicreact.dev/soul-crushing-components/)
    - The beauty of patterns like compound components, state reducers, prop getters, controlled props, etc. is that you can have your simple API and a simple implementation at the same time.
  - [7 code smells in your React components_202011](https://dev.to/awnton/7-code-smells-in-react-components-5f66)
  - [Sometimes tools are too flexible.](https://twitter.com/sebmck/status/1142090256096743425)
